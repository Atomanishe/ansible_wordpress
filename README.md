# ansible_wordpress
1) Пошаговое описание и подготовка ансибл хоста+ключи:
  а) sudo apt install python ansible -y (установка ansible и python на основной машине)
  б) useradd -m -s /bin/bash tester,  passwd tester (Создаем пользователя и устанавливаем пароль)
  в) echo  -e 'tester\tALL=(ALL)\tNOPASSWD:\tALL' > /etc/sudoers.d/tester (добавляем нашего пользователя к SUDO и отключаем запрос пароля)
  г) mkpasswd --method=SHA-512, TYPE THE PASSWORD 'secret01' (создаем и шифруем пароль для пользователей на управляемых машинах)
  д) su - tester, ssh-keygen -t rsa (логинимся под tester и генерируем ssh ключ)
  е) mkdir -p ansible01/, nano inventory.ini, nano ansible.cfg (создаем папку с проектом, и создаем файлы inventory/ansible.cfg)
    A) [webserver]
       ansi01 ansible_host=192.168.107.98
       ansi02 ansible_host=192.168.107.93
    B)
      [defaults]
       inventory = /home/provision/ansible01/inventory.ini
  Ж) ssh-keyscan 192.168.107.98 >> ~/.ssh/known_hosts
     ssh-keyscan 192.168.107.98 >> ~/.ssh/known_hosts
     Сканируем и сохраняем отпечатки удаленных ssh машин и сохраняем
