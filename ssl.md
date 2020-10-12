# Intro

## Create Pfx certificate to Azure
- We need crt and private key to generate pfx file
- or we ask client provide pfx file 
- openssl pkcs12 -export -out lb.pfx -inkey lb.key -in lb.crt
