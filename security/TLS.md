# Certificate validation
When you get or purchase a certificate the CA uses of one of the following validation methods:
- Domain Validation: the CA just checks you control the domain
- Organization Validation: the CA vets your org before issuing a certificate
- Enterprise Validation: the CA extreme-vets your org before issuing a certificate

Certificates are getting more and more expensive when you use stricter validation methods.

## How to tell DV from OV from EV when browsing a website
Until 2018-ish browsers would display a green box in the address bar for websites with EV certificates. This disappeared, as browsers instead focus on showing warnings for plain http websites.

However if you open the certificate details you can see what validation method was used:
- in both Chrome and Firefox if you click on the padlock the browser just says "Certificate (Valid)". For an EV certificate it also says "Issue to: <your org name>"
- open the certificate details and look at the Subject (or Subject Name) field. For DV certificates it only contains the Common Name, for OV/EV certificates it will contain a lot more information such as your organization name and location
