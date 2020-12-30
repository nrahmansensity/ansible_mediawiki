
# [MediaWiki](#mediawiki)

The goal of the challenge is to setup a MediaWiki on a linux (Ubuntu 20.04) server using functional ansible playbook. MediaWiki as web application requires a frontend and backend service and a database. Here apache web server serves as frontend, where the php serves the backend operation which also communicate with a mysql database [1]. 



An ansible mater can be used to deploy MediaWiki on any number of host machines define by the user. 
 

The deployment configuration in organized based on the objectives provided in the task. The configuration is divided in roles, based on the installation of different packages required by the MediaWiki. Roles are divided as apache, db, common, php, web that defined the tasks to complete the installation. These roles are reusable to perform individual task for installation. 


-	Inside the `ansible_mediawiki` directory `mediawiki.yaml` file contain installation configuration that uses different roles to complete the setup. 
-	The `hosts` files contain the list of hosts that can be used to deploy at a scale. Also, the hosts file contains include the authentication process that would be used by anisble master to access that host. 

  ```yaml
  ---
  [webservers]
  <ip> ansible_ssh_user=ubuntu ansible_ssh_private_key_file=</directory/of/key.pem>
  ```

-	All the credentials (username and password) are stored in `group_vars/all.yaml` file. The file has been protected using ansible vault. 

  ```ansible-playbook -i hosts  mediawiki.yaml --ask-vault-pass```


## Run the playbook:
-	In order to run the playbook, first need to add the IP address and authentication process i.e. username and key location on the hosts file. 
-	Then run the below command from  `ansile_mediawiki` directory .

    `ansible-playbook -i hosts  mediawiki.yaml --ask-vault-pass`

## Roles:
- `roles/apache/tasks` installs apache server 
- `roles/common/tasks` installs update and upgrades 
- `roles/db/tasks` installs mysql 
- `roles/php/tasks` installs php
- `roles/web/tasks` run the necessary command for MediaWiki server

## References:
1.	https://www.mediawiki.org/wiki/Manual:Running_MediaWiki_on_Debian_or_Ubuntu
2.	https://docs.ansible.com
3.	https://docs.ansible.com/ansible/latest/index.html
