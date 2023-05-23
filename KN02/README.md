# A

## 4.1

![](./screenshots/2023-05-16-11-10-09.png)

Hier sieht man das Hello World, welches angezeigt wird, wenn man auf die Website zugreift.

![](./screenshots/2023-05-16-11-10-59.png)

Hier sieht man die EC2 liste mit der Public-IP Adresse, welche im Screenshot oben verwendet wird.

## 4.2

![](./screenshots/2023-05-16-11-36-01.png)

Liste der Buckets

![](./screenshots/2023-05-16-11-36-26.png)

Objekte im Bucket

![](./screenshots/2023-05-16-11-36-35.png)

Statische Website Hosting des Buckets

![](./screenshots/2023-05-16-11-35-17.png)

Zugriff auf die Website mit dem index.html

# B

![](./screenshots/2023-05-23-08-43-32.png)
Successfull ssh-key connection in PuTTY with public-key-1

![](./screenshots/2023-05-23-08-45-00.png)
Unsuccessfull ssh-key connection in PuTTY with public-key-2

![](./screenshots/2023-05-23-08-45-56.png)
Instanz-Detail mit private-key-1

# C

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
packages: # liste von zu instalierenden paketen
  - curl # curl packet
  - wget # wget packet
```

# D

![](2023-05-23-09-05-42.png)
Instanz-Detail mit private-key-2

![](2023-05-23-09-03-48.png)
Successfull ssh-key connection in PuTTY with public-key-2

![](2023-05-23-09-05-04.png)
Unsuccessfull ssh-key connection in PuTTY with public-key-1
