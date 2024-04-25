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
---
Verifying a certificate's validity through OCSP
```bash
openssl ocsp -CAfile trustchain.pem -issuer issuerCA.pem -cert cert.pem -url http://ocsp.pki
```
Not including the trustchain with the `-CAfile` tag may cause the following error: `Verify error:unable to get local issuer certificate`. 

[Config file documentation from openssl](https://www.openssl.org/docs/manmaster/man5/config.html)\
[Example configuration file](https://www.ibm.com/docs/en/hpvs/1.2.x?topic=reference-openssl-configuration-examples)
