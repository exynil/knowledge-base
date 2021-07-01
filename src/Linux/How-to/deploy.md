# Deploy

1. ssh root@x.x.x.x

2. sudo apt-get update

3. sudo apt-get upgrate

4. sudo apt install python3-pip python3-dev libpq-dev postgresql postgresql-contrib nginx
5. sudo apt install certbot python3-certbot-nginx

6. sudo -u postgres psql

7. CREATE DATABASE djackets;
8. CREATE USER djacketsuser WITH PASSWORD 'djacketspassword';
9. ALTER ROLE djacketsuser SET client_encoding TO 'urf8';
10. GRANT ALL PRIVILEGES ON DATABASE djackets TO djacketsuser;
11. \q


12. sudo -H pip3 install --upgrade pip
13. sudo -H pip3 install virtualenv

14. mkdir -p /webapps/djackets
15. cd /webapps/djackets/
16. sudo groupadd --system webapps
17. sudo useradd --system --gid webapps --shell /bin/bash --home /webapps/djackets djackets
18. pip install -r requirements.txt
19. pip install psycopq2-binary
