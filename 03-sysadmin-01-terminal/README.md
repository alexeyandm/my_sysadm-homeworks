# Домашнее задание к занятию "3.1. Работа в терминале, лекция 1"

1). Установите средство виртуализации [Oracle VirtualBox](https://www.virtualbox.org/).

**Ответ:** установил


2). Установите средство автоматизации [Hashicorp Vagrant](https://www.vagrantup.com/).

**Ответ:** установил


3). В вашем основном окружении подготовьте удобный для дальнейшей работы терминал. Можно предложить:

**Ответ:** подготовил


4). С помощью базового файла конфигурации запустите Ubuntu 20.04 в VirtualBox посредством Vagrant:

	* Создайте директорию, в которой будут храниться конфигурационные файлы Vagrant. В ней выполните `vagrant init`. Замените содержимое Vagrantfile по умолчанию следующим:

		```bash
		Vagrant.configure("2") do |config|
			config.vm.box = "bento/ubuntu-20.04"
		end
		```

	* Выполнение в этой директории `vagrant up` установит провайдер VirtualBox для Vagrant, скачает необходимый образ и запустит виртуальную машину.

	* `vagrant suspend` выключит виртуальную машину с сохранением ее состояния (т.е., при следующем `vagrant up` будут запущены все процессы внутри, которые работали на момент вызова suspend), `vagrant halt` выключит виртуальную машину штатным образом.

**Ответ:** выполнил

```bash
➜  Vagrant_dir vagrant up
Bringing machine 'default' up with 'virtualbox' provider...
==> default: Box 'bento/ubuntu-20.04' could not be found. Attempting to find and install...
    default: Box Provider: virtualbox
    default: Box Version: >= 0
==> default: Loading metadata for box 'bento/ubuntu-20.04'
    default: URL: https://vagrantcloud.com/bento/ubuntu-20.04
==> default: Adding box 'bento/ubuntu-20.04' (v202112.19.0) for provider: virtualbox
    default: Downloading: https://vagrantcloud.com/bento/boxes/ubuntu-20.04/versions/202112.19.0/providers/virtualbox.box
==> default: Successfully added box 'bento/ubuntu-20.04' (v202112.19.0) for 'virtualbox'!
==> default: Importing base box 'bento/ubuntu-20.04'...
==> default: Matching MAC address for NAT networking...
==> default: Checking if box 'bento/ubuntu-20.04' version '202112.19.0' is up to date...
==> default: Setting the name of the VM: Vagrant_dir_default_1649793823456_78277
Vagrant is currently configured to create VirtualBox synced folders with
the `SharedFoldersEnableSymlinksCreate` option enabled. If the Vagrant
guest is not trusted, you may want to disable this option. For more
information on this option, please refer to the VirtualBox manual:

  https://www.virtualbox.org/manual/ch04.html#sharedfolders

This option can be disabled globally with an environment variable:

  VAGRANT_DISABLE_VBOXSYMLINKCREATE=1

or on a per folder basis within the Vagrantfile:

  config.vm.synced_folder '/host/path', '/guest/path', SharedFoldersEnableSymlinksCreate: false
==> default: Clearing any previously set network interfaces...
==> default: Preparing network interfaces based on configuration...
    default: Adapter 1: nat
==> default: Forwarding ports...
    default: 22 (guest) => 2222 (host) (adapter 1)
==> default: Booting VM...
==> default: Waiting for machine to boot. This may take a few minutes...
    default: SSH address: 127.0.0.1:2222
    default: SSH username: vagrant
    default: SSH auth method: private key
    default: 
    default: Vagrant insecure key detected. Vagrant will automatically replace
    default: this with a newly generated keypair for better security.
    default: 
    default: Inserting generated public key within guest...
    default: Removing insecure key from the guest if it's present...
    default: Key inserted! Disconnecting and reconnecting using new SSH key...
==> default: Machine booted and ready!
==> default: Checking for guest additions in VM...
==> default: Mounting shared folders...
    default: /vagrant => /Users/almarchenko/Vagrant_dir
```


```bash
➜  Vagrant_dir vagrant suspend
==> default: Saving VM state and suspending execution...

➜  Vagrant_dir vagrant up
Bringing machine 'default' up with 'virtualbox' provider...
==> default: Checking if box 'bento/ubuntu-20.04' version '202112.19.0' is up to date...
==> default: Resuming suspended VM...
==> default: Booting VM...
==> default: Waiting for machine to boot. This may take a few minutes...
    default: SSH address: 127.0.0.1:2222
    default: SSH username: vagrant
    default: SSH auth method: private key
==> default: Machine booted and ready!
==> default: Machine already provisioned. Run `vagrant provision` or use the `--provision`
==> default: flag to force provisioning. Provisioners marked to run always will still run.
```

5). Ознакомьтесь с графическим интерфейсом VirtualBox, посмотрите как выглядит виртуальная машина, которую создал для вас Vagrant, какие аппаратные ресурсы ей выделены. Какие ресурсы выделены по-умолчанию?

**Ответ:**
   - RAM: 1024 MB
   - vCPU: 2
   - SATA: 64 GB
   - Video Memory: 4MB

6). Ознакомьтесь с возможностями конфигурации VirtualBox через Vagrantfile: [документация](https://www.vagrantup.com/docs/providers/virtualbox/configuration.html). 
Как добавить оперативной памяти или ресурсов процессора виртуальной машине?
**Ответ:** Изменить в конфиге: _v.memory = 1024_

7). Команда `vagrant ssh` из директории, в которой содержится Vagrantfile, позволит вам оказаться внутри виртуальной машины без каких-либо дополнительных настроек. Попрактикуйтесь в выполнении обсуждаемых команд в терминале Ubuntu.

**Ответ:** подключение по SSH
```bash
➜  Vagrant_dir vagrant ssh-config
Host default
  HostName 127.0.0.1
  User vagrant
  Port 2222
  UserKnownHostsFile /dev/null
  StrictHostKeyChecking no
  PasswordAuthentication no
  IdentityFile /Users/almarchenko/Vagrant_dir/.vagrant/machines/default/virtualbox/private_key
  IdentitiesOnly yes
  LogLevel FATAL

➜  Vagrant_dir 
➜  Vagrant_dir 
➜  Vagrant_dir ssh vagrant@127.0.0.1 -p 2222 -i /Users/almarchenko/Vagrant_dir/.vagrant/machines/default/virtualbox/private_key
Welcome to Ubuntu 20.04.3 LTS (GNU/Linux 5.4.0-91-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Tue 12 Apr 2022 08:27:29 PM UTC

  System load:  0.05               Processes:             123
  Usage of /:   11.6% of 30.88GB   Users logged in:       0
  Memory usage: 18%                IPv4 address for eth0: 10.0.2.15
  Swap usage:   0%


This system is built by the Bento project by Chef Software
More information can be found at https://github.com/chef/bento
Last login: Tue Apr 12 20:08:33 2022 from 10.0.2.2
vagrant@vagrant:~$ 
vagrant@vagrant:~$ pwd
/home/vagrant
vagrant@vagrant:~$ 
```

8). Ознакомиться с разделами `man bash`, почитать о настройках самого bash:
    * какой переменной можно задать длину журнала `history`, и на какой строчке manual это описывается?
    * что делает директива `ignoreboth` в bash?
    
**Ответ:** HISTSIZE (default 500) is saved. line 853
ignorespace — не сохранять строки начинающиеся с символа <пробел>
ignoredups — не сохранять строки, совпадающие с последней выполненной командой
ignoreboth — использовать обе опции ‘ignorespace’ и ‘ignoredups’
    
9). В каких сценариях использования применимы скобки `{}` и на какой строчке `man bash` это описано?

**Ответ:** Compound Commands -> { list; } - line 257

10). С учётом ответа на предыдущий вопрос, как создать однократным вызовом `touch` 100000 файлов? Получится ли аналогичным образом создать 300000? Если нет, то почему?

**Ответ:** touch f{0..100000}.txt
300000 - не получится, срабатывает ограничение: "Argument list too long"

11). В man bash поищите по `/\[\[`. Что делает конструкция `[[ -d /tmp ]]`

**Ответ:** возвращает статус 0 или 1, условие: существует ли /tmp и является ли данный файл директорией


12). Основываясь на знаниях о просмотре текущих (например, PATH) и установке новых переменных; командах, которые мы рассматривали, добейтесь в выводе type -a bash в виртуальной машине наличия первым пунктом в списке:

	```bash
	bash is /tmp/new_path_directory/bash
	bash is /usr/local/bin/bash
	bash is /bin/bash
	```

	(прочие строки могут отличаться содержимым и порядком)
    В качестве ответа приведите команды, которые позволили вам добиться указанного вывода или соответствующие скриншоты.

**Ответ:**
```bash
vagrant@vagrant:~$ mkdir /tmp/new_path_directory/
vagrant@vagrant:~$ mkdir /usr/local/bin/
mkdir: cannot create directory ‘/usr/local/bin/’: File exists
vagrant@vagrant:~$ cp -p /bin/bash /tmp/new_path_directory/bash
vagrant@vagrant:~$ type -a bash
bash is /tmp/new_path_directory/bash
bash is /usr/bin/bash
bash is /bin/bash
vagrant@vagrant:~$ 

vagrant@vagrant:~$ cp -p /bin/bash /usr/local/bin/bash
cp: cannot create regular file '/usr/local/bin/bash': Permission denied
vagrant@vagrant:~$ chmod o+rwx /usr/local/bin/
chmod: changing permissions of '/usr/local/bin/': Operation not permitted
vagrant@vagrant:~$ sudo chmod o+rwx /usr/local/bin/
vagrant@vagrant:~$ cp -p /bin/bash /usr/local/bin/bash
vagrant@vagrant:~$ type -a bash
bash is /tmp/new_path_directory/bash
bash is /usr/local/bin/bash
bash is /usr/bin/bash
bash is /bin/bash
vagrant@vagrant:~$ 
```

13). Чем отличается планирование команд с помощью `batch` и `at`?

**batch** - планирует задания и выполняет их если позволяет уровень загрузки системы (по умолчанию 1.5). Если средняя загрузка системы выше указанной, задания будут ждать в очереди
**at** -  используется для назначения и выполнения задания без учета средней загрузки системы

14). Завершите работу виртуальной машины чтобы не расходовать ресурсы компьютера и/или батарею ноутбука.

**Ответ:** done

```bash
vagrant@vagrant:~$ sudo poweroff
Connection to 127.0.0.1 closed by remote host.
Connection to 127.0.0.1 closed.
 ```
