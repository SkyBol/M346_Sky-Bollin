# A

## Yaml's

### cloud-init-db.yaml
```yaml
#cloud-config
users: # alle User
  - name: ubuntu # default user's name
    sudo: ALL=(ALL) NOPASSWD:ALL # sudo regeln
    groups: users, admin # gruppen vom User
    home: /home/ubuntu # home-verzeichnis
    shell: /bin/bash # default shell verzeichnis
    ssh_authorized_keys:
      - ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCy4y5kYQTQCpZO3EUHGXvAqgyp3+Pau9s8u088xPUhPLjLccZUW8I52ss2NKaP67GjGoKu+XcYHGDrpKU2C4aBPNgf2+Cz8I8VhfPIcCNZWvUidmq0Z83/hrJT84dnPtQn0ZCpXLea5Qqgko9UdL5iULQ9kPdVBnTuf9BRYXcc2Kgh4CN0G5icQ+UY+AxuRN19rp5ZzwWCjO9JOJ4ReS0/FH0Bbevf5gSWf5WM8Oh0IJPAeLtttB2NlpfXEe6pPH3nh4LxNEamq6CL+sqWHEcMWUgJjmEV+egunxd9MvrYSaHbHr2N8+JS8wkxRe5SyN7weykaIfhpq6Qxjm941TUT aws-key
ssh_pwauth: false
disable_root: false
package_update: true
packages:
  - mariadb-server
  - php-mysqli

runcmd:
 - sudo mysql -sfu root -e "GRANT ALL ON *.* TO 'admin'@'%' IDENTIFIED BY 'password' WITH GRANT OPTION;"
 - sudo sed -i 's/127.0.0.1/0.0.0.0/g' /etc/mysql/mariadb.conf.d/50-server.cnf
 - sudo systemctl restart mariadb.service
```

### cloud-init-web.yaml
```yaml
#cloud-config
users: # alle User
  - name: ubuntu # default user's name
    sudo: ALL=(ALL) NOPASSWD:ALL # sudo regeln
    groups: users, admin # gruppen vom User
    home: /home/ubuntu # home-verzeichnis
    shell: /bin/bash # default shell verzeichnis
    ssh_authorized_keys: # liste erlaubte ssh-keys
      - ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCy4y5kYQTQCpZO3EUHGXvAqgyp3+Pau9s8u088xPUhPLjLccZUW8I52ss2NKaP67GjGoKu+XcYHGDrpKU2C4aBPNgf2+Cz8I8VhfPIcCNZWvUidmq0Z83/hrJT84dnPtQn0ZCpXLea5Qqgko9UdL5iULQ9kPdVBnTuf9BRYXcc2Kgh4CN0G5icQ+UY+AxuRN19rp5ZzwWCjO9JOJ4ReS0/FH0Bbevf5gSWf5WM8Oh0IJPAeLtttB2NlpfXEe6pPH3nh4LxNEamq6CL+sqWHEcMWUgJjmEV+egunxd9MvrYSaHbHr2N8+JS8wkxRe5SyN7weykaIfhpq6Qxjm941TUT aws-key # shh-key
ssh_pwauth: false # shh-password authentizierung
disable_root: false  # gibt es root-login
package_update: true # packete beim start updaten
package_upgrade: true
packages: # liste von zu instalierenden paketen
  - apache2
  - php
  - libapache2-mod-php
  - php-mysqli
  - adminer

write_files:
 - encoding: b64 # db.php
   content: PD9waHAKICAgICAgICAvL2RhdGFiYXNlCiAgICAgICAgJHNlcnZlcm5hbWUgPSAiMTcyLjMxLjEwMC4zMSI7CiAgICAgICAgJHVzZXJuYW1lID0gImFkbWluIjsKICAgICAgICAkcGFzc3dvcmQgPSAicGFzc3dvcmQiOwogICAgICAgICRkYm5hbWUgPSAibXlzcWwiOwoKICAgICAgICAvLyBDcmVhdGUgY29ubmVjdGlvbgogICAgICAgICRjb25uID0gbmV3IG15c3FsaSgkc2VydmVybmFtZSwgJHVzZXJuYW1lLCAkcGFzc3dvcmQsICRkYm5hbWUpOwogICAgICAgIC8vIENoZWNrIGNvbm5lY3Rpb24KICAgICAgICBpZiAoJGNvbm4tPmNvbm5lY3RfZXJyb3IpIHsKICAgICAgICAgICAgICAgIGRpZSgiQ29ubmVjdGlvbiBmYWlsZWQ6ICIgLiAkY29ubi0+Y29ubmVjdF9lcnJvcik7CiAgICAgICAgfQoKICAgICAgICAkc3FsID0gInNlbGVjdCBIb3N0LCBVc2VyIGZyb20gbXlzcWwudXNlcjsiOwogICAgICAgICRyZXN1bHQgPSAkY29ubi0+cXVlcnkoJHNxbCk7CiAgICAgICAgd2hpbGUoJHJvdyA9ICRyZXN1bHQtPmZldGNoX2Fzc29jKCkpewogICAgICAgICAgICAgICAgZWNobygkcm93WyJIb3N0Il0gLiAiIC8gIiAuICRyb3dbIlVzZXIiXSAuICI8YnIgLz4iKTsKICAgICAgICB9CiAgICAgICAgLy92YXJfZHVtcCgkcmVzdWx0KTsKPz4K
   path: /var/www/html/db.php

 - encoding: b64 # info.php
   content: PD9waHAKICAgICAgICAvLyBTaG93IGFsbCBpbmZvcm1hdGlvbiwgZGVmYXVsdHMgdG8gSU5GT19BTEwKICAgICAgICBwaHBpbmZvKCk7CiAgICA/Pg==
   path: /var/www/html/info.php

runcmd:
 - sudo a2enconf adminer
 - sudo systemctl restart apache2
```
## Screenshots

### db

![](./screenshots/2023-05-30-10-30-19.png)

"mysql -u admin -p" im Terminal

![](./screenshots/2023-05-30-10-31-16.png)

Lokale Verbindung mit dBeaver

### web-server

![](./screenshots/2023-05-30-10-56-34.png)

db.php

![](./screenshots/2023-05-30-10-57-26.png)

info.php

![](./screenshots/2023-05-30-10-59-48.png)

index.html

![](./screenshots/2023-05-30-11-01-31.png)

adminer

![](./screenshots/2023-05-30-11-02-54.png)

successfull connection with adminer

# B

## a

Hot Storage:
Daten werden in SSD's abgespeichert um schnell zugreifbar zu sein.

## b

![](./screenshots/2023-05-30-11-38-19.png)

Instanz mit 2 Volume

![](./screenshots/2023-05-30-11-39-41.png)

Warnung:
Nur EBS Volumes mit "Delete on Termination" werden gelöscht. Unsere EBS Volume werden persistiert.

![](./screenshots/2023-05-30-11-43-52.png)

Nach dem Löschen: Daten im Volume werden Persistiert.
