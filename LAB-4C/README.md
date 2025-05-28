# WEEK 4 - OPDRACHT 3
----

## Gebruik een role van een andere student door deze te installeren van uit Ansible Galaxy

voorbeeld: role dbservers van gebruiker: vox-x

Zoek rol: __ansible-galaxy role search dbservers --author vox-x__

Instalatie: __ansible-galaxy riel install vox-x.dbservers__

----
## Issues

----
## status
>student@devhost:~/terraform/week-4$ ansible-galaxy role install vox-x.dbservers
>Starting galaxy role install process
>- downloading role 'dbservers', owned by vox-x
>- downloading role from https://github.com/vox-x/dbservers-role/archive/main.tar.gz
>- extracting vox-x.dbservers to /home/student/.ansible/roles/vox-x.dbservers
>- vox-x.dbservers (main) was installed successfully

----