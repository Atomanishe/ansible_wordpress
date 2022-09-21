# ansible_wordpress
1) Пошаговое описание и подготовка ансибл хоста+ключи:
- sudo apt install python ansible -y (установка ansible и python на основной машине)
- useradd -m -s /bin/bash tester,  passwd tester (Создаем пользователя и устанавливаем пароль)
- echo  -e 'tester\tALL=(ALL)\tNOPASSWD:\tALL' > /etc/sudoers.d/tester (добавляем нашего пользователя к SUDO и отключаем запрос пароля)
- mkpasswd --method=SHA-512, TYPE THE PASSWORD 'secret01' (создаем и шифруем пароль для пользователей на управляемых машинах)
- su - tester, ssh-keygen -t rsa (логинимся под tester и генерируем ssh ключ)
- mkdir -p ansible01/, nano inventory.ini, nano ansible.cfg (создаем папку с проектом, и создаем файлы inventory/ansible.cfg)
-    
       [webserver]
       ansi01 ansible_host=192.168.107.98
       ansi02 ansible_host=192.168.107.93
-
      [defaults]
       inventory = /home/provision/ansible01/inventory.ini
- Сканируем и сохраняем отпечатки удаленных ssh машин и сохраняем
- ssh-keyscan 192.168.107.98 >> ~/.ssh/known_hosts
- ssh-keyscan 192.168.107.98 >> ~/.ssh/known_hosts
- [nano deploy-ssh.yml](https://github.com/Atomanishe/ansible_wordpress/blob/main/deploy-ssh.yml) (создаем playbook по установке ключей на хостах)
- ansible-playbook deploy-ssh.yml --ask-pass (запускаем playbook и вводим пароль)
- ansible webserver -m ping (проверяем соединение)
- создаем основной [playbook](https://github.com/Atomanishe/ansible_wordpress/blob/main/playbook.yml)
- ansible-playbook playbook.yml (запускаем) 
