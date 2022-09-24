# Instal Server Wazuh di CentOS 7

Pada artikel ini, mari kita lihat instalasi arsitektur terdistribusi.

Manajer Wazuh dan Elastic Stack dikelola pada platform yang sama oleh implementasi host tunggal.

* Server Wazuh: Menjalankan API dan Wazuh Manager. Data dari agen yang dikerahkan dikumpulkan dan dianalisis.
* Elastic Stack: Menjalankan Elasticsearch, Filebeat, dan Kibana (termasuk Wazuh). Itu membaca, mem-parsing, mengindeks, dan menyimpan data peringatan manajer Wazuh.
* Agen Wazuh: Berjalan pada host yang dipantau, mengumpulkan log dan data konfigurasi, dan mendeteksi intrusi dan anomali.

Hari ini, mari kita lihat bagaimana Teknisi dukungan kami menginstal Wazuh.

# 1. Memasang Server Wazuh
Mari kita atur nama hostnya terlebih dahulu. Luncurkan Terminal dan masukkan perintah berikut:
```
# hostnamectl set-hostname wazuh-server
``
Pertama, perbarui CentOS dan paket:

# yum update -y
Selanjutnya, instal NTP dan periksa status layanannya.

# yum install ntp
# systemctl status ntpd
Jika layanan tidak dimulai, mulai menggunakan perintah di bawah ini:

# systemctl start ntpd
Kemudian, aktifkan NTP pada boot sistem:

# systemctl enable ntpd
Selanjutnya, ubah aturan firewall untuk mengizinkan layanan NTP. Jalankan perintah berikut untuk mengaktifkan layanan.

# firewall-cmd –add-service=ntp –zone=public –permanent
# firewall-cmd –reload
Menginstal Manajer Wazuh

Mari kita tambahkan kunci:

# rpm –import https://packages.wazuh.com/key/GPG-KEY-WAZUH
Edit repositori Wazuh:

# vim /etc/yum.repos.d/wazuh.repo
Tambahkan konten berikut ke file.

[wazuh_repo]
gpgcheck=1
gpgkey=https://packages.wazuh.com/key/GPG-KEY-WAZUH
enabled=1
name=Wazuh repository
baseurl=https://packages.wazuh.com/3.x/yum/
protect=1
Simpan dan keluar dari file.

Daftar repositori menggunakan perintah repolist.

# yum repolist
Pertama, instal manajer Wazuh menggunakan perintah di bawah ini:

# yum install wazuh-manager -y
Kemudian, instal Wazuh Manager dan periksa statusnya.

# systemctl status wazuh-manager
Memasang API Wazuh

NodeJS >= 4.6.1 is required to run the Wazuh API.
Kemudian, tambahkan repositori NodeJS resmi:

# curl –silent –location https://rpm.nodesource.com/setup_8.x | bash –
install NodeJS:
# yum install nodejs -y

Instal Wazuh API. Ini akan memperbarui NodeJS jika diperlukan:

# yum install wazuh-api
Kemudian, periksa status wazuh-api.

# systemctl status wazuh-api
Ubah kredensial default secara manual menggunakan perintah berikut:

# cd /var/ossec/api/configuration/auth
Tetapkan kata sandi untuk pengguna.

# node htpasswd -Bc -C 10 user bob
Mulai ulang API.

# systemctl restart wazuh-api
Jika kita membutuhkannya, kita dapat mengubah port secara manual. File /var/ossec/api/configuration/config.js berisi parameter:

// TCP Port used by the API.
config.port = “55000”;
Kami tidak mengubah port default.

Menginstal Filebeat

Filebeat adalah alat di server Wazuh yang secara aman meneruskan peringatan dan acara yang diarsipkan ke Elasticsearch. Untuk menginstalnya, jalankan perintah berikut:

# rpm –import https://packages.elastic.co/GPG-KEY-elasticsearch
Siapkan repositori:

# vim /etc/yum.repos.d/elastic.repo
Tambahkan konten berikut ke server:

[elasticsearch-7.x]
name=Elasticsearch repository for 7.x packages
baseurl=https://artifacts.elastic.co/packages/7.x/yum
gpgcheck=1
gpgkey=https://artifacts.elastic.co/GPG-KEY-elasticsearch
enabled=1
autorefresh=1
type=rpm-md
Instal Filebeat:

# yum install filebeat-7.5.1
Unduh file konfigurasi Filebeat dari repositori Wazuh. Ini telah dikonfigurasi sebelumnya untuk meneruskan peringatan Wazuh ke Elasticsearch:
```
# curl -so /etc/filebeat/filebeat.yml https://raw.githubusercontent.com/wazuh/wazuh/v3.11.0/extensions/filebeat/7.x/filebeat.yml
```
Ubah Izin file:

# chmod go+r /etc/filebeat/filebeat.yml
Unduh template peringatan untuk Elasticsearch:

# curl -so /etc/filebeat/wazuh-template.json https://raw.githubusercontent.com/wazuh/wazuh/v3.11.0/extensions/elasticsearch/7.x/wazuh-template.json
# chmod go+r /etc/filebeat/wazuh-template.json



Unduh modul Wazuh untuk Filebeat:
# curl -s https://packages.wazuh.com/3.x/filebeat/wazuh-filebeat-0.1.tar.gz | sudo tar -xvz -C /usr/share/filebeat/module

Tambahkan IP server Elasticsearch. Edit “filebeat.yml.”

# vim /etc/filebeat/filebeat.yml
Kemudian, ubah baris berikut.

output.elasticsearch.hosts: [‘http://ELASTIC_SERVER_IP:9200′]
Selanjutnya, aktifkan dan mulai layanan Filebeat:

# systemctl daemon-reload
# systemctl enable filebeat.service
# systemctl start filebeat.service
2. Memasang Tumpukan Elastis
Kita dapat mengkonfigurasi server CentOS kedua dengan ELK.

Lakukan konfigurasi pada server tumpukan elastis.

Pertama, mari kita atur nama host.

# hostnamectl set-hostname elk
Kemudian, perbarui sistem:

# yum update -y
Menginstal ELK

Instal Elastic Stack dengan paket RPM dan kemudian tambahkan repositori Elastic dan kunci GPG-nya:

# rpm –import https://packages.elastic.co/GPG-KEY-elasticsearch
Kemudian, buat file repositori:

# vim /etc/yum.repos.d/elastic.repo
Kemudian, tambahkan konten berikut ke file:

[elasticsearch-7.x]
name=Elasticsearch repository for 7.x packages
baseurl=https://artifacts.elastic.co/packages/7.x/yum
gpgcheck=1
gpgkey=https://artifacts.elastic.co/GPG-KEY-elasticsearch
enabled=1
autorefresh=1
type=rpm-md
Menginstal Elasticsearch
Pertama, Instal paket Elasticsearch:

# yum install elasticsearch-7.5.1
Elasticsearch mendengarkan secara default pada antarmuka loopback (localhost). Konfigurasikan Elasticsearch untuk mendengarkan alamat non-loopback dengan mengedit /etc/elasticsearch/elasticsearch.yml dan menghapus komentar konfigurasi network.host. Sesuaikan nilai IP yang ingin kita sambungkan:

jaringan.host: 0.0.0.0

Ubah aturan firewall.

# firewall-cmd –permanent –zone=public –add-rich-rule=’
rule family=”ipv4″
source address=”34.232.210.23/32″
port protocol=”tcp” port=”9200″ accept’
Selanjutnya, muat ulang aturan firewall:

# firewall-cmd –reload
Konfigurasi lebih lanjut akan diperlukan untuk file konfigurasi pencarian elastis.

Edit file “elasticsearch.yml”.

# vim /etc/elasticsearch/elasticsearch.yml
Ubah atau edit “node.name” dan “cluster.initial_master_nodes”.

node.name: <node_name>
cluster.initial_master_nodes: [“<node_name>”]
Aktifkan dan mulai layanan Elasticsearch:

# systemctl daemon-reload
Pertama, aktifkan pada boot sistem.

# systemctl enable elasticsearch.service
Kemudian, mulai layanan pencarian elastis.

# systemctl start elasticsearch.service
Check the status of the elastic search.
systemctl status elasticsearch.service

Selanjutnya, periksa file log untuk masalah apa pun.

# tail -f /var/log/elasticsearch/elasticsearch.log
Setelah Elasticsearch aktif dan berjalan, kita perlu memuat template Filebeat. Jalankan perintah berikut di server Wazuh:

filebeat setup –index-management -E setup.template.json.enabled=false
Memasang Kibana
Pertama, Instal paket Kibana:

# yum install kibana-7.5.1
Instal plugin aplikasi Wazuh untuk Kibana:

# sudo -u kibana /usr/share/kibana/bin/kibana-plugin install https://packages.wazuh.com/wazuhapp/wazuhapp-3.11.0_7.5.1.zip
Plugin Kibana diperlukan untuk memodifikasi konfigurasi Kibana untuk mengakses Kibana dari luar.

Edit file konfigurasi Kibana.

#vim /etc/kibana/kibana.yml
Ubah baris berikut.

server.host: “0.0.0.0”

Konfigurasikan URL instance Elasticsearch.

elasticsearch.hosts: [“http://localhost:9200”]
Kemudian, aktifkan dan mulai layanan Kibana:

# systemctl daemon-reload
# systemctl enable kibana.service
# systemctl start kibana.service
Menambahkan API Wazuh ke Konfigurasi Kibana

Sunting “wazuh.yml.”

# vim /usr/share/kibana/plugins/wazuh/wazuh.yml
Kemudian, edit nama host, nama pengguna, dan kata sandi.

Terakhir, simpan dan keluar dari file dan mulai ulang layanan Kibana.

# systemctl restart kibana.service
Kami menginstal server Wazuh dan server ELK. Sekarang kita akan menambahkan host menggunakan agen.

3. Memasang agen Wazuh
I. Menambahkan Server Ubuntu
sebuah. Pertama, menginstal paket yang dibutuhkan

# apt-get install curl apt-transport-https lsb-release gnupg2
Instal kunci GPG repositori Wazuh:

# curl -s https://packages.wazuh.com/key/GPG-KEY-WAZUH | apt-key add –
Tambahkan repositori lalu perbarui repositori.

# echo “deb https://packages.wazuh.com/3.x/apt/ stable main” | tee /etc/apt/sources.list.d/wazuh.list
# apt-get update
b. Kemudian, menginstal agen Wazuh

Perintah di bawah ini menambahkan IP “WAZUH_MANAGER” ke konfigurasi agen wazuh secara otomatis saat menginstalnya.

WAZUH_MANAGER=”52.91.79.65″ apt-get install wazuh-agent
II. Menambahkan host CentOS
Tambahkan repositori Wazuh.

# rpm –import http://packages.wazuh.com/key/GPG-KEY-WAZUH
Selanjutnya, edit dan tambahkan ke repositori:

vim /etc/yum.repos.d/wazuh.rep
Kemudian, tambahkan konten berikut:

[wazuh_repo]
gpgcheck=1
gpgkey=https://packages.wazuh.com/key/GPG-KEY-WAZUH
enabled=1
name=Wazuh repository
baseurl=https://packages.wazuh.com/3.x/yum/
protect=1
Kemudian, instal agen.

WAZUH_MANAGER=”52.91.79.65″ yum install wazuh-agent
4. Mengakses Dasbor Wazuh
Pertama, jelajahi Kibana menggunakan IP.

http://IP or hostname:5601/
Kemudian, Anda akan melihat antarmuka.

Kemudian, klik Ikon “Wazuh” untuk masuk ke Dashboard-nya. Kita akan melihat Dasbor “Wazuh”.

Akhirnya, di sini kita dapat melihat agen yang terhubung, manajemen informasi keamanan, dll. Ketika kita mengklik peristiwa keamanan; kita dapat melihat tampilan grafis dari peristiwa.




## Kesimpulan
Singkatnya, Wazuh adalah solusi pemantauan keamanan gratis, open-source, dan siap untuk perusahaan untuk deteksi ancaman, pemantauan integritas, respons insiden, dan kepatuhan. Hari ini, kami melihat bagaimana Teknisi Dukungan kami menginstalnya.

