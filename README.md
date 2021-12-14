# PHPIPAM
Docker Compose for [phpIPAM](https://phpipam.net/). Including HAProxy for SSL/TLS.

## Setup

1. Clone repo
```bash
git clone https://github.com/ryancbutler/phpipam-docker-compose.git
cd phpipam-docker-compose
```
2. Create password files to be used with docker-compose (protect this!)
```bash
echo -n mySQLRootPass >> MYSQL_ROOT_PASSWORD.txt
echo -n myPHPIPamDBPass >> DB_PASSWORD.txt
```
3. Create self-signed Certs for SSL/TLS (Adjust accordingly)
```bash
mkdir certs

openssl req -newkey rsa:4096 \
-x509 \
-sha256 \
-days 3650 \
-nodes \
-out certs/ipam.crt \
-keyout certs/ipam.crt.key \
-subj "/CN=phpipam.lab.local" \
-addext "subjectAltName = DNS:phpipam.lab.local"
```
4. Run `docker-compose up -d`

## First run
1. Access at http://dockerhost:8000 (HTTP) or https://dockerhost:8443 (HTTPS)
    - Ports can be customized in `docker-compose.yml`
2. Select **New phpipam Installation**
3. Select **Automatic database installation**
4. Enter **root** as username and password included in `MYSQL_ROOT_PASSWORD.txt`
5. Select **Install phpipam Database**
6. Select **Continue** and set *admin* password then **Save Settings**
7. Proceed to login