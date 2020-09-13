# Protocols for securing DNS queries
- DNSSEC:
  - between resolver and authoritative name servers
  - provides authentication (dns responses are signed) but not encryption
- dnscrypt and dns-over-http
  - between client and resolver
  - provides authentication and encryption 

# Why DNSSEC adoption lags
Here is a nice [post](https://labs.ripe.net/Members/rene_bakker/bang-for-the-buck-the-adoption-of-dnssec-and-return-on-investment) as to why DNSSEC adoption is still lagging.

Key points:
- It is the registrant that pays a higher price for a signed domain name, but the registrant does not profit from it. The price for a secured domain is much higher, and it is not the registrant, but the end-user who profits from it. Since liability is difficult to address, there is not much incentive to provide a secure domain name.
- In summary this means that the actual damage or relevance of the abuse of the DNS is hard to determine. There are no reliable figures about the damage done by cybercrime related to the DNS. A clear majority of cybercrime starts with e-mail, but there are a lot of other ways to manipulate the end-user other than by abusing the DNS. The actual effect of securing e-mail by using DNSSEC on phishing is therefore hard to establish. It is obvious that DNSSEC enhances the security of e-mail, but the exact impact remains unknown.
- For ISPs that provide access to their customers availability of services are key. Adopting DNSSEC by access providers can infringe this availability. If a signature is not validated (for instance because it is expired) a website cannot be reached by a visitor that uses DNSSEC enabled validation. The website with a bogus domain name cannot be visited by someone who uses DNSSEC enabled validation, but can be reached by regular validation. For the average user, the ‘fault’ is caused by his access provider. 
