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
The above command will generate server.crt that will be used with our server.key to enable SSL in applications.

#### 7. Change your website.conf file. 
```bash
server {

listen   443;

ssl    on;
ssl_certificate    /etc/ssl/server.crt;
ssl_certificate_key    /etc/ssl/server.key;

server_name your.domain.com;
access_log /var/log/nginx/nginx.vhost.access.log;
error_log /var/log/nginx/nginx.vhost.error.log;
location / {
root   /home/www/public_html/your.domain.com/public/;
index  index.html;
}

}

```
#### 8. Go to Google Crome and import the certificate.
Go to Settings -> Privacy and Security -> Security -> Manage Certificates -> Authorities -> Import.
<br /> 
Clear the Browser Cache and Run the website. You should know see that the website is secure and the certificate is valid!!

### This is a Script file that will do all the above steps.
Create a certificate.sh file and paste the below code in that.
```bash
#!/bin/bash
# Generate a key and public CA certificate
echo "Enter the Domain name: ";
read DOMAIN;
echo "Enter IP on which the website is hosted locally: ";
read IP;
openssl req -x509 \
            -sha256 -days 356 \
            -nodes \
            -newkey rsa:2048 \
            -keyout rootCA.key -out rootCA.crt;
#Create a RSA key
openssl genrsa -out $DOMAIN.key 2048;

#Create a certificate signing request


echo "Enter Country name: ";
read country;
echo "Enter State or Province name: ";
read state;
echo "Enter locality: ";
read locality;
echo "Enter Organization name:";
read organization;
echo "Enter organization unit name:";
read ou;
cat > csr.conf <<EOF
[ req ]
default_bits = 2048
prompt = no
default_md = sha256
req_extensions = req_ext
distinguished_name = dn

[ dn ]
C = $country
ST = $state
L = $locality
O = $organization
OU = $ou
CN = $DOMAIN

[ req_ext ]
subjectAltName = @alt_names

[ alt_names ]
DNS.1 = $DOMAIN

IP.1 = $IP


EOF
# create CSR request using private key

openssl req -new -key ${DOMAIN}.key -out ${DOMAIN}.csr -config csr.conf

# Create a external config file for the certificate

cat > cert.conf <<EOF

authorityKeyIdentifier=keyid,issuer
basicConstraints=CA:FALSE
keyUsage = digitalSignature, nonRepudiation, keyEncipherment, dataEncipherment
subjectAltName = @alt_names

[alt_names]
DNS.1 = ${DOMAIN}

EOF

# Create SSl with self signed CA

openssl x509 -req \
    -in ${DOMAIN}.csr \
    -CA rootCA.crt -CAkey rootCA.key \
    -CAcreateserial -out ${DOMAIN}.crt \
    -days 365 \
    -sha256 -extfile cert.conf

#move the key and certificate file to /etc/ssl
sudo cp *.crt *.key *.conf *.csr /etc/ssl;

```
Give the file execute permission: 
```
sudo chmod +x certificate.sh
```


