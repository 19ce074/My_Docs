# SSL Certificates Cheat-Sheet
X.509 is an ITU standard defining the format of public key certificates. X.509 are used in TLS/SSL, which is the basis for HTTPS. An X.509 certificate binds an identity to a public key using a digital signature. A certificate contains an identity (hostname, organization, etc.) and a public key (RSA, DSA, ECDSA, ed25519, etc.), and is either signed by a Certificate Authority or is Self-Signed.
## Self-Signed Certificates

### Create a folder to store the ssl certificates
```bash
mkdir openssl && cd openssl
```
### Generate CA
1. Generate a key and public CA Cert (Change the fields CN, C and L).

```bash
openssl req -x509 \
            -sha256 -days 356 \
            -nodes \
            -newkey rsa:2048 \
            -subj "/CN=www.mywebsite.com/C=IN/L=AHMD" \
            -keyout rootCA.key -out rootCA.crt
```
+ We will use the rootCA.keyand rootCA.crt to sign the SSL certificate.

### Optional Stage: View Certificate's Content
```bash
openssl x509 -in ca.pem -text
openssl x509 -in ca.pem -purpose -noout -text
```

### Generate Certificate
#### 1. Create a RSA key (Private key)
```bash
openssl genrsa -out server.key 2048
```
#### 2. Create a Certificate Signing Request (CSR)
Change the fields, DNS and IP.
```bash
cat > csr.conf <<EOF
[ req ]
default_bits = 2048
prompt = no
default_md = sha256
req_extensions = req_ext
distinguished_name = dn

[ dn ]
C = IN      
ST = GJ
L = AHMD
O = 
OU =  
CN = www.mywebsite.com

[ req_ext ]
subjectAltName = @alt_names

[ alt_names ]
DNS.1 = www.mywebsite.com
DNS.2 = mywebsite.com
IP.1 = 192.168.1.5  
IP.2 = 192.168.1.6

EOF
```
#### 3. Generate Certificate Signing Request (CSR) Using Server Private Key. 
This will generate server.csr.
```bash
openssl req -new -key server.key -out server.csr -config csr.conf
```
#### 4. Create a external file. 
Change the DNS name.
```bash
cat > cert.conf <<EOF

authorityKeyIdentifier=keyid,issuer
basicConstraints=CA:FALSE
keyUsage = digitalSignature, nonRepudiation, keyEncipherment, dataEncipherment
subjectAltName = @alt_names

[alt_names]
DNS.1 = demo.mlopshub.com

EOF
```
#### 5. Generate SSL certificate With self signed CA.
Execute the following command to generate the SSL certificate that is signed by the rootCA.crt and rootCA.key created as part of our own Certificate Authority.
```bash
openssl x509 -req \
    -in server.csr \
    -CA rootCA.crt -CAkey rootCA.key \
    -CAcreateserial -out server.crt \
    -days 365 \
    -sha256 -extfile cert.conf
```
  
