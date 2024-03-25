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