# ANSIBLE AUTOMATION REPOSITORY RSMP

## Getting started

- Sebelum memulai menggunakan ansible pastikan tersedia 1 komputer untuk Control Node.
  Rekomendasi : Ubuntu 20.04
- Pastikan antara control node dengan remote node sudah terkoneksi dengan ssh
- Rekomendasi ansible versi 8

## Installation

Update dan upgrade repository Ubuntu 20.04

```
apt update && apt upgrade -y
```

Install ansible dari repository Ubuntu

```
apt install ansible -y
```

Cek versi ansible

```
ansible -v
```

## Usage

Koneksikan antara Control Node dengan dengan Server yang akan di eksekusi dengan Ansible.
Ansible tidak perlu agent seperti jenkin atau gitlab, ansible langsung mengeksekusi syntax dengan ssh.

Pada control Node, buat ssh key, pada contoh diberi nama 'ansible'

```
ssh-keygen
```

Cek apakah ada file key nya di

```
~/.ssh/
```

Copy public key ke server yang akan di eksekusi ansible, di asumsikan server target menggunakan port ssh 73

```
ssh-copy-id -i ~/.ssh/ansible.pub -p 73 root@10.0.3.x
```

Menguji koneksi

```
ssh -i ~/.ssh/ansible root@10.0.3.x -p 73
```

Sebelum menjalankan ansible pastikan file Inventory sudah terkoneksi dengan server target, lakukan test ping. Perhatikan juga lokasi file private key di file inventori pada Controler Node nya. Perhatikan juga Hosts pada playbook.yml nya. Perhatikan juga terkait user pada file inventory pastikan menggunakan user root

```
ansible -i inventory all -m ping
```

Menjalankan playbook ansible

```
ansible-playbook -i inventory playbook.yml
```

## Catatan

Ketika akan mengeksekusi job pada ansible, baca dulu scriptnya, karena ada beberapa komentar yg harus di ganti dan di sesuaikan sesuai kebutuhan. Seperti pada file `mysql57.yml` ada inventory yg harus diganti, ada password yang harus di ganti dan ada ansible galaxy colletion yang harus di install.

## Link Referensi

Tutorial Install Manual:

- https://www.vultr.com/docs/how-to-install-mysql-5-7-on-ubuntu-20-04/ (install database)
- https://php.tutorials24x7.com/blog/how-to-install-mcrypt-for-php-7-on-ubuntu-20-04-lts

Repository:

- https://dev.mysql.com/doc/mysql-apt-repo-quick-guide/en/#repo-qg-apt-repo-manual-setup (Repository mysql)
- https://bugs.mysql.com/bug.php?id=113427 (GPG MySql 5.7 Update)
