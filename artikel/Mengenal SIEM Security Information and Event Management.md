

## Peneliti keamanan komputer Chris Kubecka mengidentifikasi kasus penggunaan SIEM berikut, yang dipresentasikan pada konferensi peretasan 28C3 (Kongres Komunikasi Chaos)
- Visibilitas SIEM dan deteksi anomali dapat membantu mendeteksi zero-days atau kode polimorfik . Terutama karena tingkat deteksi anti-virus yang rendah terhadap jenis malware yang berubah dengan cepat ini.
- Parsing, normalisasi log dan kategorisasi dapat terjadi secara otomatis, terlepas dari jenis komputer atau perangkat jaringan, selama dapat mengirim log.
- Visualisasi dengan SIEM menggunakan peristiwa keamanan dan kegagalan log dapat membantu dalam deteksi pola.
- Anomali protokol yang dapat menunjukkan kesalahan konfigurasi atau masalah keamanan dapat diidentifikasi dengan SIEM menggunakan deteksi pola, peringatan, garis dasar, dan dasbor.
- SIEMS dapat mendeteksi komunikasi rahasia, berbahaya, dan saluran terenkripsi.
- Cyberwarfare dapat dideteksi oleh SIEM dengan akurat, menemukan penyerang dan korban.

## Contoh aturan korelasi 
Sistem SIEM dapat memiliki ratusan dan ribuan aturan korelasi. Beberapa di antaranya sederhana, dan beberapa lebih kompleks. Setelah aturan korelasi dipicu, sistem dapat mengambil langkah-langkah yang tepat untuk mengurangi serangan cyber. Biasanya, ini termasuk mengirimkan pemberitahuan kepada pengguna dan kemudian mungkin membatasi atau bahkan mematikan sistem.

### Deteksi Brute Force 
Deteksi brute force relatif mudah. Pemaksaan kasar berhubungan dengan terus-menerus mencoba menebak variabel. Ini paling sering mengacu pada seseorang yang mencoba terus-menerus menebak kata sandi Anda - baik secara manual atau dengan alat. Namun, ini dapat merujuk pada mencoba menebak URL atau lokasi file penting di sistem Anda.

Brute force otomatis mudah dideteksi karena seseorang yang mencoba memasukkan kata sandi mereka 60 kali dalam satu menit tidak mungkin.

### Impossible Travel
Ketika pengguna masuk ke sistem, secara umum, itu membuat stempel waktu acara. Seiring waktu, sistem mungkin sering merekam informasi berguna lainnya seperti perangkat yang digunakan, lokasi fisik, alamat IP, upaya login yang salah, dll. Semakin banyak data yang dikumpulkan, semakin banyak penggunaan yang dapat dikumpulkan darinya. Untuk perjalanan yang tidak mungkin, sistem melihat tanggal/waktu login saat ini dan terakhir serta perbedaan antara jarak yang direkam. Jika dianggap tidak mungkin terjadi, misalnya menempuh jarak ratusan mil dalam satu menit, maka itu akan memicu peringatan.

Banyak karyawan dan pengguna sekarang menggunakan layanan VPN yang dapat mengaburkan lokasi fisik. Ini harus dipertimbangkan ketika membuat aturan seperti itu.

### Excessive File Copying
Jika Anda memikirkan aktivitas Anda sehari-hari, kemungkinan besar Anda tidak menyalin atau memindahkan banyak file di sistem Anda. Oleh karena itu, penyalinan file yang berlebihan pada suatu sistem dapat dikaitkan dengan seseorang yang ingin membahayakan perusahaan Anda. Sayangnya, ini tidak sesederhana menyatakan seseorang telah mendapatkan akses ke jaringan Anda secara ilegal dan ingin mencuri informasi rahasia. Bisa juga seorang karyawan yang ingin menjual informasi perusahaan, atau mereka hanya ingin membawa pulang beberapa file untuk akhir pekan.

### Serangan DDoS
Serangan DDoS (Distributed Denial of Service) akan menyebabkan masalah bagi hampir semua perusahaan. Serangan DDoS tidak hanya membuat properti web Anda offline, tetapi juga dapat membuat sistem Anda lebih lemah. Dengan aturan korelasi yang sesuai, SIEM Anda harus memicu peringatan tepat di awal serangan sehingga Anda dapat mengambil tindakan pencegahan yang diperlukan untuk melindungi sistem Anda.

### Perubahan Integritas File 
Integritas File dan Pemantauan Perubahan (FIM) adalah proses pemantauan file di sistem Anda. Perubahan tak terduga dalam file sistem Anda akan memicu peringatan karena kemungkinan indikasi serangan dunia maya.





# Daftar SIEM Open Source : 
1. OSSIM
2. The ELK Stack
3. OSSEC
4. Wazuh
5. Apache Metron
6. SIEMonster
7. Prelude
8. SecurityOnion
9. MozDef
10. Snort
11. Suricata

Dari beberapa SIEM Open Source diatas yang akan di bahas kali ini adalah Wazuh.
  <div class="separator" style="clear: both;"><a href="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj2w1Voz2age90lT4lv4eq8TJV-FuZ4tdkjdtO_7QawIEr7HzruyaMmAvXke6g2sbHVS2NZtxCIRFS2EyPXKkkc6nORVnBmPB-ugYZCI3srBHz0xAcWrGGKj8Wly5faJRFpRC-h_LZi3WB3OY-e26eRxlXGFpJU-qyZ5iHM4sg719cqibOUpnO3rRud/s1600/wazuh.png" style="display: block; padding: 1em 0; text-align: center; "><img alt="" border="0" width="320" data-original-height="888" data-original-width="1600" src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj2w1Voz2age90lT4lv4eq8TJV-FuZ4tdkjdtO_7QawIEr7HzruyaMmAvXke6g2sbHVS2NZtxCIRFS2EyPXKkkc6nORVnBmPB-ugYZCI3srBHz0xAcWrGGKj8Wly5faJRFpRC-h_LZi3WB3OY-e26eRxlXGFpJU-qyZ5iHM4sg719cqibOUpnO3rRud/s320/wazuh.png"/></a></div>

## Kenapa memilih WAZUH 

Wazuh adalah salah satu dari sekian banyak aplikasi SIEM, tetapi Wazuh memiliki fitur yang yang sangat banyak dibandingkan dengan aplikasi open source sejenisnya. Tentunya  Security Analysis menggunakan aplikasi Open Source Wazuh ini.

- Pengumpulan, korelasi, dan analisis peristiwa keamanan.
- Pemantauan integritas file (FIM).
- Deteksi malware dan rootkit.
- Penilaian konfigurasi keamanan (SCA).
- Deteksi kerentanan berbasis agen.
- Pemantauan keamanan untuk aplikasi cloud-native, container, dan Kubernetes.
- Deteksi ancaman untuk solusi SaaS dan penyedia cloud.
- MITRE ATT&CK dan pemetaan kepatuhan terhadap peraturan.
- Respons otomatis terhadap ancaman yang terdeteksi.

untuk lebih jelasnya silahkan kunjungi website resmi [https://wazuh.com/](https://wazuh.com/)
Cara install [WAZUH](wazuh)
