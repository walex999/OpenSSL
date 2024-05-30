# OpenSSL | Using OpenSSL for PKI
Checking the content within a .pem file. 
``` bash
 openssl x509 -in file.pem -noout -inform PEM -text
```
- `-in` is used to specify the path and file
- `-noout` prevents output of the encoded version of the request which is otherwise outputted at the end of the certificate information
- `-inform` specifies the format of the input file which can be DER or PEM
- `-text` outputs the certificate information in text form
---
See only subject name.
```bash
openssl x509 -in cert.pem -noout -subject
```
---
Making a certificate request, being prompted the different DN elements and displaying the certificate request in the CLI.
```bash
openssl req -text -nodes -new
```
---
Marking a request based on a config file
```bash
openssl req -text -nodes -new -config file.conf
```

## OCSP
Verifying a certificate's validity through OCSP
```bash
openssl ocsp -CAfile trustchain.pem -issuer issuerCA.pem -cert cert.pem -url http://ocsp.pki
```
Not including the trustchain with the `-CAfile` tag may cause the following error: `Verify error:unable to get local issuer certificate`. 


## Make an authentication certificate 
Make a CSR for a user authentication certificate for example.
```bash
openssl req -new -out cert.csr -outform PEM -subj '/CN=User/C=FR/' -newkey rsa:2048 -nodes -keyout key.out -keyform PEM -verbose
```
Enroll this certificate on a TLS-client template.
Enroll this certificate on a Certificate Authority that is trusted for Client Authentication in the app to which you wish to connect.

---
Make a .p12 certificate from the certificate obtained after enrolling from the CSR and the unencrypted private key used for the CSR.
```bash
openssl pkcs12 -export -in cert.pem -inkey key.out -out toto.p12
```
A password will be required. Once this is done, this .p12 certificate can be imported inside the machine's certificate store along with the private key. 
This certificate might need to be edited within the certificate store to be trusted for specific use cases such as SSL, EAP...

## Check CRL information
```bash
openssl crl -in QASA-Authent-Certificat.crl -inform DER -text
```


## Helper links
[Config file documentation from openssl](https://www.openssl.org/docs/manmaster/man5/config.html)\
[Example configuration file](https://www.ibm.com/docs/en/hpvs/1.2.x?topic=reference-openssl-configuration-examples)
