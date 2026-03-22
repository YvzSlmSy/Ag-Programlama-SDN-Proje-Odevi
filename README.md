🔹 SENARYO 1 – TEKİL CİHAZ ACL (Single Host ACL)
🎯 Amaç

Belirli tek bir cihazın (ör. lab1) başka bir cihaza (pc16) ICMP erişiminin engellenmesi.

1️⃣ Mininet Ortamını Temizle
sudo mn -c

2️⃣ POX Denetleyiciyi Başlat (Tekil ACL Aktif)
cd ~/Desktop/B221210086_Yavuz_Selim_Say_Ağ_Programlama_Proje/SDN_Proje/mininet/pox
./pox.py sdn_app


📌 Bu aşamada aktif olanlar:

acl.py

install_icmp_block_rule

handle_acl

POX terminalinde şu çıktıyı görmen normaldir:

ACL INSTALLED: BLOCK ICMP echo 10.0.0.101 -> 10.0.0.16

3️⃣ Mininet Topolojisini Başlat

Yeni bir terminal aç:

cd ~/Desktop/B221210086_Yavuz_Selim_Say_Ağ_Programlama_Proje/SDN_Proje
sudo mn --custom custom_topology.py --topo realcorp --controller=remote --mac

4️⃣ Test Komutları (Tekil ACL)
mininet> lab1 ping pc16


⛔ ENGELLENİR

mininet> lab2 ping pc16


✅ İZİN VERİLİR

🔹 SENARYO 2 – GRUP BAZLI ACL (Subnet Tabanlı ACL)
🎯 Amaç

Bir subnetin tamamının başka bir subnet’e erişiminin engellenmesi
(Örn: LAB → BRANCH)

1️⃣ Mininet’i Temizle
sudo mn -c

2️⃣ POX Denetleyiciyi Başlat (Grup ACL Aktif)
cd ~/Desktop/B221210086_Yavuz_Selim_Say_Ağ_Programlama_Proje/SDN_Proje/mininet/pox
./pox.py sdn_app


📌 Bu aşamada aktif olan:

scenario_group_acl.py

handle_group_acl()

POX terminalinde şu loglar görülür:

GROUP ACL: LAB → BRANCH BLOCKED (10.0.0.101 → 10.0.0.16)

3️⃣ Mininet Topolojisini Başlat
cd ~/Desktop/B221210086_Yavuz_Selim_Say_Ağ_Programlama_Proje/SDN_Proje
sudo mn --custom custom_topology.py --topo realcorp --controller=remote --mac

4️⃣ Test Komutları (Grup ACL)
mininet> lab1 ping pc16


⛔ ENGELLENİR

mininet> lab5 ping pc16


⛔ ENGELLENİR
(Aynı subnet içindeki farklı cihaz)

mininet> pc1 ping pc16


✅ İZİN VERİLİR
(LAB subneti dışında)

5️⃣ Log Doğrulama (POX Terminal)

Her engellenen paket için POX terminalinde:

GROUP ACL: LAB → BRANCH BLOCKED


uyarısı görülür.
