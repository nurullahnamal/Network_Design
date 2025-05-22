# Ağ Yapılandırması 
Ağ Yapılandırması ve Dinamik Yönlendirme


# Ağ Topolojisi ve Yapılandırma Deposu
Bu yapılandırma dosyası, farklı yönlendirme protokolleri ve ağ servislerini içeren bir ağ topolojisini tanımlar. İçerikte BGP, OSPF, EIGRP, PPPoE, CHAP ve Multilink gibi önemli ağ protokolleri bulunmaktadır.


#  1. Ağ Yapılandırması (Network Configuration)
Tanımlanan IP ağları ve subnet mask bilgileri

# 2. BGP (Border Gateway Protocol) Yapılandırması
BGP yönlendirme protokolü

 Otonom sistemler (AS) arasında bağlantılar
 Komşu (neighbor) yapılandırmaları

# 3. OSPF (Open Shortest Path First) Yapılandırması
OSPF yönlendirme protokolü
Alan (area) bazlı yönlendirme

# 4. EIGRP (Enhanced Interior Gateway Routing Protocol) Yapılandırması
EIGRP protokolü ile ağ yönlendirme

IPv4 adresleme ve statik yönlendirme

# 5. Arabirim (Interface) Yapılandırması
Seri port ve Ethernet arayüzü yapılandırmaları

IP adresleme ve yönlendirme

# 6. PPPoE (Point-to-Point Protocol over Ethernet) Yapılandırması
PPPoE bağlantıları ve kullanıcı doğrulama

# 7. CHAP (Challenge Handshake Authentication Protocol) Kullanımı
CHAP kimlik doğrulama mekanizması ile güvenli bağlantılar

# 8. Multilink Yapılandırması
MLPPP (Multilink PPP) ile birden fazla bağlantının tek bir mantıksal bağlantı olarak kullanılması


## Ağ Topolojisi

Ağ aşağıdaki cihazlardan oluşmaktadır:

*   **R1:** Türk Telekom ağına bağlı router.
*   **R2:** Area Border Router (OSPF ve BGP kullanıyor).
*   **R3:** İç ağ router'ı.
*   **R4 (Superonline):** Superonline otonom sistemine bağlı router.
*   **R5:** EIGRP kullanan router.
*   **R6 (Vodafone):** Vodafone otonom sistemine bağlı router.
*   **R7:** İç ağ router'ı.
*   **R8:** İç ağ router'ı.
*   **R9:** Dış dünyaya bağlantı sağlayan router (BGP kullanıyor).
*   **R10:** Müşteri router'ı (PPPoE kullanıyor).

[Resim: Ağ Topolojisi](network_topology.png)

## Router Konfigürasyonları

Aşağıdaki dizinde her bir router için yapılandırma dosyaları bulunmaktadır:

*   `router-configs/`

Her dosya, ilgili router'ın tam konfigürasyonunu içerir ve `.txt` uzantılıdır.

## Router Durum ve Yönlendirme Bilgileri

Aşağıda Router 1 (TELEKOMR1) için durum ve yönlendirme bilgileri bulunmaktadır.

### Router 1 (TELEKOMR1) - Arayüz Özeti




![image alt](https://github.com/nurullahnamal/A-Yap-land-rmas-ve-Dinamik-Y-nlendirme/blob/e3c1d81191116244c92df278002abee175d26f4f/Topoloji.png)

## Konfigürasyon Örnekleri

Aşağıda her bir router'ın konfigürasyonlarının tamamı yer almaktadır.
![image alt](https://github.com/nurullahnamal/A-Yap-land-rmas-ve-Dinamik-Y-nlendirme/blob/main/R1-%20SHOW%20IP%20ROUTE.png)
![image alt](https://github.com/nurullahnamal/A-Yap-land-rmas-ve-Dinamik-Y-nlendirme/blob/main/R1-%20show%20ip%20interface%20brief.png)

enable <br>
configure  terminal <br>
interface fastEthernet 0/0 <br> 
ip address 192.168.100.1 255.255.255.0 <br>
no shutdown <br>
interface fastethernet 0/1 <br>
ip address 192.168.101.1 255.255.255.0 <br>
no shutdown <br>


Show ip interface brief <br>

router ospf 1 <br>
router-id 1.1.1.1 <br>
network 1.1.1.0 0.0.0.255 area 0 <br>
network 192.168.100.0 0.0.0.255 area 0 <br>
network 192.168.101.0 0.0.0.255 area 0 <br>
exit

![image alt](https://github.com/nurullahnamal/A-Yap-land-rmas-ve-Dinamik-Y-nlendirme/blob/main/r2%20-%20show%20ip%20route.png)
![image alt](https://github.com/nurullahnamal/A-Yap-land-rmas-ve-Dinamik-Y-nlendirme/blob/main/r2-%20show%20ip%20interface%20brief.png)

### Router 2 (R2) Konfigürasyonu 

enable <br>
configure terminal <br>
interface multilink 1 <br>
no shutdown <br>
ip address 1.1.1.2 255.255.255.0 <br>
ppp multilink <br>
ppp multilink group 1 <br>
exit <br>

interface serial 2/2 <br>
no ip address <br>
no shut down <br>
encapsulation ppp <br>
ppp multinlik <br>
ppp multinlk group 1  <br>

interface serial 2/3 <br>
no ip address
no shut down <br>
encapsulation ppp <br>
ppp multilink <br>
ppp multilink group 1 <br>

interface multilink 2 <br>
no shutdown <br>
ip address 1.1.2.1 255.255.255.0 <br> 
ppp multilink <br>
ppp multilink group 2 <br>

interface serial 2/0 <br>
no ip address <br>
encapsulation ppp <br>
ppp multilink <br>
ppp multilink gorup 2 <br>
no shutdown <br>

interface serial 2/1 <br>
no ip address <br>
no shutdown <br>
encapsulation ppp <br>
ppp multilink <br>
ppp multilink group 2 <br>

router ospf 1 <br>
router-id 1.1.1.2 <br>
network 1.1.1.0 0.0.0.255 area 0 <br>
network 1.1.2.0 0.0.0.255 area 0 <br>

router bgp 100 <br>
neigbor 6.6.6.2 remote-as 300 <br>
neighbor 4.4.4.2 remote-as 200 <br>
network 1.1.1.0 mask 255.255.255.0 <br>
network 1.1.2.0 mask 255.255.255.0 <br>
network 4.4.4.0 mask 255.255.255.0 <br>
netowrk 6.6.6.0 mask 255.255.255.0 <br>

![image alt](https://github.com/nurullahnamal/A-Yap-land-rmas-ve-Dinamik-Y-nlendirme/blob/main/r3%20-%20show%20ip%20route.png)
![image alt](https://github.com/nurullahnamal/A-Yap-land-rmas-ve-Dinamik-Y-nlendirme/blob/main/r3-%20show%20ip%20interface%20brief.png)

### Router 3 (R3) Konfigürasyonu

interface multilink 1 <br>
ip address 1.1.2.2 255.255.255.0 <br>
no shotdown <br>
ppp multilink <br>
ppp multilink group 1 <br>

interface serial 2/0 <br>
no shutdown <br>
no ip address <br>
encapsulation ppp <br>
ppp multilink <br>
ppp multilink group 1 <br>
exit <br>

interface serial 2/1 <br>
no shutdown <br>
no ip address <br>
encapsulation ppp <br>
ppp multilink <br>
ppp multilink gropu 1 <br>

interface fastEthernet 0/0 <br>
ip addres 192.168.103.1 255.255.255.0 <br>
no shutdown <br>
exit <br>

interface fastEthernet 0/1 <br>
ip addres 192.168.102.1 255.255.255.0 <br>
no shutdown <br>
exit <br>
  
router ospf 1 <br>
router-id 1.1.1.3 <br>
network 1.1.2.0 0.0.0.255 area 0 <br>
network 192.168.103.0 0.0.0.255 area 0 <br>
network 192.168.102.0 0.0.0.255 area 0 <br>
end <br>
write <br>

![image alt](https://github.com/nurullahnamal/A-Yap-land-rmas-ve-Dinamik-Y-nlendirme/blob/main/r4%20-%20show%20ip%20route.png)
![image alt](https://github.com/nurullahnamal/A-Yap-land-rmas-ve-Dinamik-Y-nlendirme/blob/main/r4%20-%20show%20ip%20interface%20brief.png)

### Router 4 (R4 - Superonline) Konfigürasyonu

interface multink 1 <br>
no shutdown <br>
no ip address <br>
ip address 2.2.1.1 255.255.255.0 <br>
pp multilink <br>
ppp multilink grop 1 <br>

interface serial 2/0 <br>
no ip address <br>
no shurdown <br>
encapsulation ppp <br>
ppp multilink <br>
ppp multilink group 1 <br>
exit <br>

interface serial 2/1 <br>
no ip address <br>
no shudown <br>
encapsulation ppp <br>
ppp multilink <br> 
ppp multilink group 1 <br>

interface multilink 2 <br>
no ip address <br>
no shutdown <br>
ip address 4.4.4.2 255.255.255.0 <br>
ppp multilink <br> 
ppp multilink group 2 <br>
exit <br>

interface serial 3/0 <br>
no shutdown <br>
no ip address <br>
encapsulation ppp <br>
ppp multilink <br>
ppp multilink group 2 <br>
exit <br>

interface serial 3/1 <br>
no shutdown <br>
no ip address <br>
encapsulation ppp <br>
ppp multilink <br>
ppp multilink group 2 <br>
exit <br>

interface multilink 3 <br>
no shutdown <br> 
no ip address <br>
ip address 5.5.5.1 255.255.255.0 <br>
ppp multilink <br>
ppp multilink group 3 <br>

interface serial 2/2 <br>
no shutdown <br>
no ip address <br>
encapsulation ppp <br>
ppp multilink <br>
ppp multilink group 3 <br>
exit <br>
 
interface serial 2/3 <br>
no ip address <br>
no shutdown <br>
encapsulation ppp <br> 
ppp multilink <br>
ppp multilink group 3 <br>

router eigrp 1 <br>
eigrp router-id 1.1.1.6 <br>
network 5.5.5.0 <br>
network 4.4.4.0 <br>
network 2.2.1.0 <br>
  
router bgp 200 <br>
neighbor 4.4.4.1 remote-as 100 <br>
neighbor 5.5.5.2 remote-as 300 <br>
network 5.5.5.0 mask 255.255.255.0 <br>
network 4.4.4.0 mask 255.255.255.0 <br>
network 2.2.1.0 mask 255.255.255.0 <br>

interface serial 3/2 <br>
no shutdown <br>
ip address 11.11.11.2 255.255.255.0 <br>
exit <br>

router bgp 200 <br>
neighbor 11.11.11.1 remote-as 500 <br>
network 11.11.11.0 mask 255.255.255.0 <br>
exit <br>
 
router eigrp 10 <br>
network 11.11.11.0 <br>
address-amily ipv4 <br>
redistribute static  <br>

reouter bgp 100 <br>
network 192.168.100.0 mask 255.255.255.0 <br>
network 192.168.101.0 mask 255.255.255.0 <br> 
network 192.168.102.0 mask 255.255.255.0 <br>
network 192.168.103.0 mask 255.255.255.0 <br>
end <br>
write <br>
![image alt](https://github.com/nurullahnamal/A-Yap-land-rmas-ve-Dinamik-Y-nlendirme/blob/main/r5%20show%20ip%20route.png)
![image alt](https://github.com/nurullahnamal/A-Yap-land-rmas-ve-Dinamik-Y-nlendirme/blob/main/r5%20show%20ip%20interface%20brief.png)
### Router 5 (R5) Konfigürasyonu

enable <br>
configure terminal  <br>
interface fastEthernet 0/0 <br>
no shutdown <br>
ip address 172.16.100.1 255.255.255.0 <br>
exit <br>

interface fastEthernet 0/1 <br>
no shutdown <br>
ip address 172.16.101.1 255.255.255.0 <br>
exit <br>

interface multilink 1 <br>
no shutdown v
no ip address <br>
ip address 2.2.1.2 255.255.255.0 <br>
ppp multilink <br>
ppp multilink group 1 <br>

inteface serial 2/0 <br>
no shutdown <br>
no ip address <br>
encapsulation ppp <br>
ppp multilink <br>
ppp multilink gruop 1 <br>

interface serial 2/1 <br>
no shutdown <br> 
no ip address <br>
encapsulation ppp <br>
ppp multilink <br>
ppp multilink group 1 <br>

router eigrp 1<br>
eigrp router-id 1.1.1.5 <br>
network 172.16.101.0 <br>
network 172.16.100.0 <br>
network 2.2.1.0 <br>
end <br>
write <br>

![image alt](https://github.com/nurullahnamal/A-Yap-land-rmas-ve-Dinamik-Y-nlendirme/blob/main/r6%20%20show%20ip%20interface%20brief.png)
![image alt](https://github.com/nurullahnamal/A-Yap-land-rmas-ve-Dinamik-Y-nlendirme/blob/main/r6%20-%20show%20ip%20route.png)
### Router 6 (R6 - Vodafone) Konfigürasyonu

enable <br>
configure terminal <br>
interface serial 2/0 <br>
no shutdown <br>
ip address 3.3.2.1 255.255.255.0 <br>
exit <br>

interface serial 2/1 <br>
no shutdown <br>
ip address 3.3.1.1 255.255.255.0 <br>
exit <br>

interface multilink 1 <br>
no shutdown <br>
ip address 6.6.6.2 255.255.255.0 v
ppp multilink <br>
ppp multilink gorup 1 <br>
exit <br>

interface serial 2/2 <br>
no shutdown <br>
no ip address <br>
encapsulation ppp <br>
ppp multilink <br>
ppp multilink group 1 <br>
exit <br>

interface serial 2/3 <br>
no shutdown <br>
no ip address <br>
encapsulation ppp <br>
ppp multilink <br>
ppp multilink group 1 <br>
exit <br>

interface multilink 2 <br>
no shutdown <br>
ip address 5.5.5.2 255.2555.255.0  <br>
ppp multilink <br>
ppp multilink group 2 <br>
exit <br>

interface serial 3/0 v
no ip address <br>
no shutdown <br>
encapsulation ppp <br>
ppp multilink <br>
ppp multilink group 2 <br>

interface serial 3/1 <br>
no ip address <br>
no shutdown <br>
encapsulation ppp <br>
ppp multilink <br> 
ppp multilink group 2 <br>

router ospf 1 <br>
router-id 1.1.1.6 <br>
network 6.6.6.0 0.0.0.255 area 10 <br>
network 5.5.5.0 0.0.0.255 area 10 <br>
network 3.3.1.0 0.0.0.255 area 10 <br>
network 3.3.2.2 0.0.0.255 area 10 <br>

router bgp 300 <br>
neighbor 5.5.5.1 remote-as 200 <br>
neighbor 6.6.6.1 remote-as 100 <br>
network 6.6.6.0 mask 255.255.255.0 <br>
network 5.5.5.0 mask 255.255.255.0 <br>
network 3.3.2.0 mask 255.255.255.0 <br>
network 3.3.1.0 mask 255.255.255.0 <br>

interface serial 3/2 <br>
no shutdown <br>
ip addres 7.7.7.2 255.255.255.0 <br>
exit <br>
 
router ospf 1 <br>
network 7.7.7.0 0.0.0.255 <br> <br>
default-information originate <br> <br>
router bgp 1 <br>
neighbor 7.7.7.1 remote-as 500 <br> <br>
network 7.7.7.0 mask 255.255.255.0 <br> <br>
exit <br> <br>

ip route 0.0.0.0 0.0.0.0 7.7.7.1 <br>

router bgp 300 <br>
network 10.10.101.0 mask 255.255.255.0 <br>
network 10.100.100.0 mask 255.255.255.0 <br>
end <br> 
write <br>
![image alt](https://github.com/nurullahnamal/A-Yap-land-rmas-ve-Dinamik-Y-nlendirme/blob/main/r7%20-%20show%20ip%20interface%20brief.png)
![image alt](https://github.com/nurullahnamal/A-Yap-land-rmas-ve-Dinamik-Y-nlendirme/blob/main/r7%20-%20show%20ip%20interface%20brief.png)
### Router 7 (R7) Konfigürasyonu

enable <br>
configure  terminal <br>
interface fastEthernet 0/0 <br>
no shutdown <br>
ip addres 10.100.100.1 255.255.255.0 <br>
exit <br>
interface serial 2/0 <br>
no shutdown <br>
ip addres 3.3.2.2 255.255.255.0 <br>
exit <br>
 
interface serial 2/1 <br>
no shutdown <br>
ip addres 3.3.3.1 <br>
exit <br>

router ospf 1 <br>
router-id 1.1.1.7 <br>
network 3.3.2.0 0.0.0.255 area 10 <br>
network 3.3.3.0 0.0.0.255 area 10 <br>
network 10.100.100.0 0.0.0.255 area 10 <br>
exit <br> 

![image alt](https://github.com/nurullahnamal/A-Yap-land-rmas-ve-Dinamik-Y-nlendirme/blob/main/r8%20-%20show%20ip%20interface%20brief.png)
![image alt](https://github.com/nurullahnamal/A-Yap-land-rmas-ve-Dinamik-Y-nlendirme/blob/main/r8%20-%20show%20ip%20route.png)

### Router 8 (R8) Konfigürasyonu

enable  <br>
configure terminal  <br>
interface fastEthernet 0/0 <br>
no shutdown  <br>
ip addres 10.10.101.1 255.255.255.0 <br>
exit <br>

interface serial 2/1 <br>
NO SHUTDOWN <br>
ip address 3.3.3.2 255.255.255.0 <br>
exit <br>

interface serial 2/0 <br>
NO SHUTDOWN <br>
ip addres 3.3.1.2 255.255.255.0 <br>
exit <br>

router ospf 1 <br>
router-id 1.1.1.8 <br>
network 3.3.1.0 0.0.0.255 area 10 <br>
network 3.3.3.0 0.0.0.255 area 10 <br>
network 10.10.101.0 0.0.0.255 area 10 <br>
exit <br>

![image alt](https://github.com/nurullahnamal/A-Yap-land-rmas-ve-Dinamik-Y-nlendirme/blob/main/r9%20show%20bgp%20summary.png)
![image alt](https://github.com/nurullahnamal/A-Yap-land-rmas-ve-Dinamik-Y-nlendirme/blob/main/r9%20show%20ip%20interface%20brief.png)
![image alt](https://github.com/nurullahnamal/A-Yap-land-rmas-ve-Dinamik-Y-nlendirme/blob/main/r9%20show%20ip%20interface%20brief.png)

### Router 9 (R9) Konfigürasyonu

configure  terminal <br>
interfaca serial 2/2 <br>
no shutdown <br>
ip address 7.7.7.1 255.255.255.0 <br>
exit <br>

interface serial 2/0 <br>
no shutwon <br>
ip address 9.9.9.1 255.255.255.0 <br>
exit <br>

interface serial 2/1 <br>
no shutdown <br>
ip addres 11.11.11.1 255.255.255.0 <br>
exit <br>

configure termainal <br>
interface fastEthernet 0/0 <br>
ip address 192.168.1.210 255.255.255.0 <br>
no shutdown <br> 
exit <br>

router bgp 500 <br>
neigbhor 7.7.7.2 remote-as 300 <br>
neigbor 9.9.9.2 remote as 100 <br>
neighbor 11.11.11.2 remote-as 200 <br>
noetwork 9.9.9.0 mask 255.255.255.0 <br>
network 11.11.11.0 mask 255.255.255.0 <br>
network 7.7.7.0 mask 255.255.255.0 <br>

ip route 192.168.100.0 255.255.255.0 9.9.9.2 <br>
ip route 192.168.101.0 255.255.255.0 9.9.9.2 <br>
ip route 192.168.102.0 255.255.255.0 9.9.9.2 <br>
ip route 192.168.103.0 255.255.255.0 9.9.9.2 <br>
ip route 172.16.0.0 255.255.0.0 11.11.11.2 <br>
ip route 10.0.0.0 255.0.0.0 7.7.7.2 <br>
ip route 0.0.0.0 0.0.0.0 192.168.2.1 <br>

![image alt](https://github.com/nurullahnamal/A-Yap-land-rmas-ve-Dinamik-Y-nlendirme/blob/main/r10%20-show%20ip%20route.png)
![image alt](https://github.com/nurullahnamal/A-Yap-land-rmas-ve-Dinamik-Y-nlendirme/blob/main/r10%20show%20ip%20interface%20brief.png)
### Router 10 (R10 - Müşteri Router'ı) Konfigürasyonu

interface fastEthernet 0/0 <br>
ip address 192.168.200.1 255.255.255.0 <br>
no shutdown <br>
exit <br>

interface fastEThernet 0/1 <br>
no shutdown <br>
pppoe enable <br> 
pppoe-client dial-pool-number 1 <br>
exit <br>

interface dialer 1 <br>
mtu 1492 <br>
ip address negotiated <br> 
encapsualiton ppp <br>
dialer pool 1 <br>
ppp authentication chap callin <br>
ppp chap hostname test <br>
ppp chap password CCNA <br>
exit <br>

ip route 0.0.0.0 0.0.0.0 dialer 1 <br>
interface fastethernet 0/1 <br>
ip nat outside <br>
exit <br>

interface fastethernet 0/0 <br>
ip nat inside <br>
exit <br>

ip nat inside source static 192.168.200.10 10.101.0.50 <br>

## Katkıda Bulunma

Bu projeye katkıda bulunmak için lütfen aşağıdaki adımları izleyin:

1.  Depoyu fork edin.
2.  Değişikliklerinizi içeren bir branch oluşturun (`git checkout -b my-new-feature`).
3.  Değişikliklerinizi commit edin (`git commit -am 'Add some feature'`).
4.  Branch'inizi remote'a push edin (`git push origin my-new-feature`).
5.  Çekme isteği (pull request) oluşturun.

## Lisans

Bu depo MIT lisansı altında yayınlanmıştır. Daha fazla bilgi için [LICENSE](LICENSE) dosyasına bakın.


Bu güncellenmiş README.md dosyası, tüm router konfigürasyonlarını ve show ip interface brief ile show ip route çıktısını içermektedir. Bu, depoyu kullanan kişilere daha kapsamlı bir genel bakış sunacaktır.

Lütfen unutmayın, yine de hassas bilgileri (parolalar, anahtarlar vb.) tüm dosyalardan kaldırmanız gerekmektedir.
