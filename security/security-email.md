# SPF, DKIM and DMARC (and ARC)
A fancy link: [Demystifiying DMARC](https://seanthegeek.net/459/demystifying-dmarc/).

## Email primer
An email message is composed of:
- the envelope
  - defined in RFC5321
  - MAIL FROM
  - RCPT TO
- the email proper
  - defined in RFC5322
  - headers added by the source, including From and To
  - headers added by relaying MTAs
  - email body
  - email attachments

Envelope from and to addresses are used to route message to its destination, or route bounce messages in case of failure.  Email From and To headers are used by the Mail User Agent to show the email origin and destination. It is not required that the envelope from and to match the email From and To headers.

Envelope from address can be referred to as MAIL FROM or RFC5321 from.  Email From header can be referred to as the RFC5322 from.

Envelope from and to addresses do not appear when viewing the email source, but sometimes relaying MTAs include the envelope from in a Return-Path header.

## SPF
SPF (Sender Policy Framework, http://www.openspf.org/) allow email recipients to verify inbound emails are being sent from IPs authorized by the sender domain.
- recipient domain MTA extracts the domain from the envelope from address
- MTA queries the SPF record for that domain
- MTA verifies the connecting IP address is authorized by the SPF record

To query an SPF record:
```
host -t TXT gmail.com
```

**Note:** In itself SPF does not prevent email spoofing. It only protects the envelope from address, spammers can still spoof the email From header. Let's say some spammer wants to spoof bob@nice.com they can register the domain bad.com and add a valid SPF record. Then they send emails using:
- spammer@bad.com in the envelope from
- bob@nice.com in the email From header

Emails will pass the SPF check based on the bad.com domain, however the recipient will see bob@nice.com as the email source.

**Note:** In addition to checking the envelope from address, SPF can verify the hostname in the initial HELO message. DMARC only uses the envelope from address validation though.

## DKIM
DKIM (Domain Keys Identified Mail, http://dkim.org) is another anti-spoofing mechanism relying on digital signatures. Administrators for a given domain:
- create a key pair (typically RSA)
- upload the private key to their MTAs
- add the public key in a TXT record

**Note:** whereas SPF applies to the envelope, DKIM applies to the email proper.

When emails are sent out:
- the domain MTAs add a DKIM-signature header with a signature covering the email body and some headers
- the list of signed headers depends on the sender, but it must include the From header
- the recipient domain MTAs fetch the public key from the TXT record and verify the signature

The DKIM-Signature header consists of a list of tag-value pairs. Most importantly:
- a: signing algorithm
- d: domain
- s: selector
- h: list of signed headers
- b: signature 

To query a DKIM record:
```
host -t TXT selector._domainkey.domain
host -t TXT 20161025._domainkey.gmail.com
```

**Note:** In itself DKIM does not prevent email spoofing. The DKIM-Signature domain does not have to match the From header domain. Spammers can send emails with a valid DKIM signature for bad.com, and bob@nice.com in the email From header. It will pass the DKIM check however the recipient will see bob@nice.com as the email source.

## DMARC
DMARC (https://dmarc.org/, https://dmarcian.com/) builds on top of SPF and DKIM. A domain administrator can publish a DMARC policy to indicate SPF and DKIM are set up on that domain, and instruct receivers how to deal with failures. It also specifies a reporting mechanism so that a sender domain gets insights on how recipient email providers handled their traffic.

### DMARC check
DMARC main objective is to protect the email From header address. It relies on the SPF and DKIM checks, but also verifies the domains authenticated by SPF and DKIM match the From header address domain (referred to as alignment in DMARC specifications):
- SPF check must pass, and envelope from address domain must match the email From header domain
- DKIM check must pass, and the DKIM-Signature domain attribute must match the email From header domain

DMARC check will pass if at least one of the conditions above is true. If both fails, the recipient must apply the action in the DMARC policy.

### DMARC policy
The DMARC policy indicates what recipients should do in case when emails fail the DMARC check:
- none: do nothing (DMARC monitoring mode)
- quarantine: typically put the email in the junk folder
- reject: reject the email

The policy can also indicate whether the alignment check should be strict (domain names must match exactly) or relaxed (top-level "organizational" domain names must match). Finally the policy may contain email addresses where recipient domains should send aggregated or failure reports.

To query a DMARC record:
```
host -t TXT _dmarc.gmail.com
```

#### DMARC reports
Aggregated reports are sent typically once per day, with the report in XML format. Emails are grouped by source IP and authentication results, passing just the count of each group.

Failure reports are generated in real-time and consists of redacted copies of individual emails that failed the DMARC check.

There are various tools for analyzing DMARC reports, but most of them are hosted in the cloud and require that a specific email address to be added to the DMARC policy.

To build a self-hosted DMARC analyzer you can use the following:
- https://github.com/techsneeze/dmarcts-report-parser
- https://github.com/techsneeze/dmarcts-report-viewer

To analyze individual DMARC reports:
https://us.dmarcian.com/xml-to-human-converter/

## Email forwarding and anti-spoofing mechanisms
SPF/DKIM/DMARC may impact email forwarding. There are two cases of email forwarding:
- manual (or client-side) forwarding:
  - You receive an email in your inbox and forward it from your email client.
  - This essentially creates a new email which contains the original message (body and some headers).
  - SPF/DKIM/DMARC do not impact those.
- automated (or server-side) forwarding:
  - The email is forwarded by an MTA. This can happen when you set up forwarding rules on your email account, with mailing lists, ... 
  - This will break the SPF check in most (all) cases: either the MTA does not rewrite the MAIL FROM and it doesn't match the SPF record anymore. Or it rewrites it, the SPF check passes but is not aligned with the header from.
  - DKIM check is more resistant to forwarding and should still pass, unless the MTA rewrites some headers or the body. This can occur if the forwarding MTA rewrites MIME boundaries, an antivirus or antispam modifies the message, ...

To remedy the situation, email providers are starting to implement [ARC](http://arc-spec.org/). It allows intermediate MTAs to record email authentication results across hops. Instead of discarding the message based on DMARC, a recipient domain can evaluate the ARC chain.

The forwarding domain may add its own DKIM-Signature header, resulting in a email with two DKIM signatures. This is ok as DMARC will check both signatures.

**Note:** as forwarding emails from DMARC-protected domains is a known issue, some recipient domains may override the DMARC policy if they think the email is legitimate (and forwarded).

A couple of links:
- https://www.dmarcanalyzer.com/forwarding-within-dmarc/
- https://help.returnpath.com/hc/en-us/articles/223242468-How-does-email-forwarding-affect-authentication-results-
