**Last updated April 08 2021**

# Security Keys
## Standards
The FIDO Alliance is an open industry association developing authentication standards related to multi-factor or password-less authentication.

One of these standards is FIDO U2F; U2F was originally developped by Google and Yubico before being transferred to the FIDO Alliance. U2F allows service providers (the relying party) to improve security via a 2nd authentication factor (the authenticator) verified through the user browser (the client). More specifically it describes the U2F protocol and messages exchanged between the client and the authenticator, more details below. (there is also the UAF protocol which provides password-less authentication)

Later on the FIDO Alliance partnered with the W3C and created the FIDO2 project which defines the following standards:
- WebAuthn: a web API built into browsers for the creation and use of public key-based credentials in web applications. Whereas U2F describes the interactions between the client and the authenticator, WebAuthn deals with the interactions between the client and the relying party.
- CTAP1: just a new name for FIDO U2F
- CTAP2: an evolution of CTAP2 (all CTAP2-compatible devices should also support CTAP1)

Some links:
- https://fidoalliance.org/specifications/
- https://fidoalliance.org/specifications/download/

### FIDO U2F
The U2F protocol allows service providers to increate the security of their infrastructure by adding a strong second factor to the user login process. It supports two operations, registration and authentication. During the registration the authenticator generates a keypair and outputs the public key, which is uploaded to the relying party. During authentication the authenticator proves possession of the previously-registered keypair by signing a challenge from the relying party.

U2F authenticators communicate with the user's device over USB, NFC or Bluetooth. Most supports a test of presence feature: the authenticator performs the registration or authentication operation only after the user confirms their presence (typically by pressing a button on the authenticator).

They offer strong privacy guarantees: U2F devices do not include global identifiers visible across websites, keypairs are stored in a secure element and cannot be extracted from the device. As such it is possible to use the same U2F device for different online accounts, or re-use devices (person B can use U2F device previously used by person A).

#### Registration
Here is a break-down of the registration process:
1. the relying party sends a challenge to the client
2. the client contructs a message for the U2F device which includes:
  - challenge parameter: SHA256 hash of the client data (among other things the client data contains the challenge from the relying party as well as the website origin) 
  - application parameter: SHA256 hash of the U2F application id (typically the website url)
3. after confirming the user presence, the U2F token mints a new keypair and outputs the following:
  - the public key
  - the key handle (this a handle that allows the U2F token to identify the generated key pair)
  - a signature over the public key, the key handle, the challenge parameter and the application parameter
4. the client forwards the public key and the key handle to the relying party

The key handle could be a simple index to the private key. However to save memory U2F devices have the option to include the private key and the hash of the origin, encrypted with a wrapping key known only to the U2F device, into the key handle. During the authentication phase, the U2F device unwraps the key handle to retrieve the private key and the origin it was generated for.

#### Authentication
Here is a break-down of the authentication process:
1. the relying party sends a challenge to the client, as well as the key handle
2. the client constructs a message for the U2F device which includes:
  - challenge parameter: SHA256 hash of the client data (among other things the client data contains the challenge from the relying party as well as the website origin) 
  - application parameter: SHA256 hash of the U2F application id (typically the website url)
  - key handle
3. after confirming the user presence, the U2F token attempts to retrieve the private key using the key handle and outputs the following:
  - signature over the challenge parameter and the application parameter
4. the client forwards the signature to the relying party

If the U2F fails to retrieve the private key, or if there is an origin mismatch, the token returns an error.

### Security guarantees
The origin check ensures that the public keys and key handles issued by a U2F device to a particular online service or website cannot be used by a different online service or website. This provides a strong protection against phishing: the phishing website may pass along the challenge from the relying party however the U2F device will detect the origin mismatch and refuse to sign it. By contrast TOTP apps do not offer the same protection, as it is quite possible for a phishing website to pass along the time-based code from the client to the website, and neither will notice the attack.

Also U2F relies on public key cryptography, whereas TOTP relies on a shared secret between the user and the website. In case of compromise of the website, those shared secrets could be stolen.

## Models
### Yubikey 5 series
Yubikey 5 keys support FIDO U2F and FIDO2. They come in a variety of formats:
- USB-A+NFC
- USB-C+NFC
- USB-C+Lightning
- USB-A Nano
- ...

### Google Titan
Google Titan keys support the FIDO U2F protocol, they come in different models:
- Bluetooth/NFC/USB
- USB-A/NFC
- USB-C 

**note:** Google Titan are vulnerable to a [side-channel attack](https://ninjalab.io/wp-content/uploads/2021/01/a_side_journey_to_titan.pdf), although the bar to pull off the attack is quite high

### Solo Keys
Open-source FIDO U2F and FIDO2 keys, comes in USB-A, USB-C, USB-A+NFC and USB-C+NFS formats.

### Built-in security keys
Android 7.0+ and iOS 10+ phones leverage their secure enclave to provide the same features as a FIDO token. On iOS you need to install the SmartLock app to use the built-in security key. The security key device communicates with the other device over Bluetooth.

This seems quite convenient as most people carry their phone with them all the time. However there are a number of restrictions:
- it only works with Google account
- it only works with Chrome
- it only works on ChromeOS, macOS and Windows
- you can only add a built-in key from a phone where you are logged in with the account

## Operating Systems
### Android
You can use USB-C, Bluetooth or NFC security keys.

### iOS
Yubico is the only company which sells a security key with a lightning port.

The other options are to use a Bluetooth security key (you will have to install the Smart Lock app), or an NFC key.

The Smart Lock app is also used for enabling the iPhone built-in security key, or to communicate with an Android phone which has a built-in security key
