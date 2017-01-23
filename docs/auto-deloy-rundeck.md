# Tự động triên khai Rundeck bằng Vagrant và Ansible.

##1. Mô hình.
```sh
|                                               |------ rundeck.yml
|                             |-------- Ansible |
|                             |                 |------ hosts
|---- Kali Linux (26.26.26.1) |
|                             |
|                             |-------- Vagrant => Create VM Ubutuntu 14.04 (26.26.26.26)
|
```
##2. Thực hiện.

- Trước tiên chúng ta cần phải cài đặt `Vagrant` và `ansible` cho máy vật lý.

#### Cài đặt vagrant.

- Xem chi tiết tại [đây](https://github.com/datkk06/ghichep-vagrant-virtualbox-kvm/tree/master/Docs)

#### Cài đặt Ansible.

<i>Trên Ubuntu</i>

```sh
sudo apt-add-repository -y ppa:ansible/ansible
sudo apt-get update
sudo apt-get install -y ansible
```

<i>Trên Debian</i>

```sh
# debian 8
echo 'deb http://http.debian.net/debian jessie-backports main' > /etc/apt/sources.list.d/backports.list
apt-get update
apt-get -t jessie-backports install "ansible"
```

- Tạo file tự động cài đặt Rundeck .

```sh
sudo vi /etc/ansible/rundeck.yml
```

- Sau đó coppy đoạn playbook sau paste lại vào `rundeck.yml`: 

```sh
---
- hosts: rundekck
  sudo: yes
  tasks:
  - name: cai dat JDK 7
    apt: name=openjdk-7-jre update_cache=yes
  - name: config enviroment.
    lineinfile: dest=/etc/environmentine
                line="JAVA_HOME="/usr/lib/jvm/java-1.7.0-openjdk-amd64""
                state=present
  - name: dowload Rundeck.
    get_url:
      url=http://dl.bintray.com/rundeck/rundeck-deb/rundeck-2.7.1-1-GA.deb
      dest=/tmp
  - name: cai dat Rundeck.
    command: sudo dpkg -i /tmp/rundeck-2.2.1-1-GA.deb
  - name: start Rundeck.
    service: name=rundeckd state=started
  - name: restart machine
    command: shutdown -r now "Ansible updates triggered"
    async: 0
    poll: 0
    ignore_errors: true
```

- Chỉnh sửa file `hosts`

```sh
echo "[rundeck]" >> /etc/ansible/hosts
echo "26.26.26.26" >> /etc/ansible/hosts #IP mà chúng ta set cho VM tạo bằng vagrant.
```

- Thiết lập tự động tạo VM bằng `vagrant`

- Tạo một thư mục và tạo ra file cấu hình VM chứa trong thư mục đó:

```sh
sudo mkdir Rundeck
cd Rundeck
vagrant init
```

- Sau đó chúng ta tiến hành sửa file cấu hình :

```sh
sudo vi Vagrantfile
```

- Sửa lại các thiết lập như sau :

```sh
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  # config.vm.box = "ubuntu/trusty64"
  # config.ssh.insert_key = false
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "/etc/ansible/rundeck.yml"
    ansible.inventory_path = "/etc/ansible/hosts"
    ansible.sudo = true
    ansible.limit = "all"
  end
```

- Lưu lại file cấu hình và tiến hành chạy :

```sh
vagrant up
```

# OK !!!

- Như thế là chúng ta đã cấu hình để triển khai tự động `Rundeck` bằng Vagrant và Ansible và đây là kết quả :

![scr8](/image/scr8.png)
