# Ağ Yapılandırma
Ağ Yapılandırması ve Dinamik Yönlendirme
Tamamdır, şimdi bu show ip interface brief ve show ip route çıktılarını da README dosyasına ekleyelim. Bu, ağın durumunu ve yönlendirme tablosunu daha iyi anlamanıza yardımcı olacaktır.

İşte güncellenmiş README.md dosyası:

# Ağ Topolojisi ve Yapılandırma Deposu

Bu depo, çoklu bağlantı (multilink) teknolojisi, OSPF, EIGRP ve BGP protokolleri kullanılarak yapılandırılmış bir ağın topolojisini ve tüm router konfigürasyonlarını içerir. Amacımız, ağ tasarımını ve konfigürasyonunu paylaşarak, ağ mühendisleri ve öğrencilerin bu konularda bilgi edinmelerine yardımcı olmaktır.

## İçerik

Bu depo aşağıdaki içeriği içerir:

*   **README.md:** Bu dosya, genel bilgiler, topoloji açıklaması ve katkıda bulunma yönergeleri içerir.
*   **router-configs/:** Her router için ayrı ayrı yapılandırma dosyalarını içeren bir dizin.
*   **network_topology.png:** Ağın görsel topolojisini gösteren bir resim.

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
config terminal <br>
interface fastethernet 0/0 <br>
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
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
IGNORE_WHEN_COPYING_END

enable <br>
config terminal <br>
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
ppp multinlik <br>
ppp multinlk group 1 <br>

interface multilink 2 <br>
no shutdown <br>
ip address 1.1.2.1 255.255.255.0 <br> 
ppp multilink <br>
ppp multilink group 2 <br>

interface serial 2/0 <br>
no ip address <br>
encapsualion ppp <br>
ppp multink <br>
ppp multink gorup 2 <br>
no shutdown <br>

interface serial 2/1 <br>
no ip address <br>
no shutdown <br>
encapsulation ppp <br>
ppp multinkiş <br>
ppp multink goup 2 <br>

router ospf 1 <br>
router-id 1.1.1.2 <br>
network 1.1.1.0 0.0.0.255 area 0 <br>
network 1.1.2.0 0.0.0.255 area 0 <br>

router bgp 100 <br>
neigbor 6.6.6.2 remote-as 300 <br>
neighbor 4.4.4.2 remote-as 200 <br>
network 1.1.1.0 mask 255.255.255.0 <br>
network 1.1.2.0 mask 255.255.255.0 <br>
netowrk 4.4.4.0 mask 255.255.255.0 <br>
netowrk 6.6.6.0 mask 255.255.255.0 <br>

![image alt](https://github.com/nurullahnamal/A-Yap-land-rmas-ve-Dinamik-Y-nlendirme/blob/main/r3%20-%20show%20ip%20route.png)
![image alt](https://github.com/nurullahnamal/A-Yap-land-rmas-ve-Dinamik-Y-nlendirme/blob/main/r3-%20show%20ip%20interface%20brief.png)

### Router 3 (R3) Konfigürasyonu
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
IGNORE_WHEN_COPYING_END

interface multilink 1
ip address 1.1.2.2 255.255.255.0
no shotdown
ppp multink
ppp multinlk group 1

interface serial 2/0
no shutdown
no ip address
encalsupaion ppp
ppp multink
ppp multink group 1
exit

interface serial 2/1
no shutdown
no ip address
encapsulation ppp
ppp multilink
ppp multink gropu 1

interface fastEthernet 0/0
ip addres 192.168.103.1 255.255.255.0
no shutdown
exit

interface fastEthernet 0/1
ip addres 192.168.102.1 255.255.255.0
no shutdown
exit

router ospf 1
router-id 1.1.1.3
network 1.1.2.0 0.0.0.255 area 0
network 192.168.103.0 0.0.0.255 area 0
network 192.168.102.0 0.0.0.255 area 0
end
write

![image alt](https://github.com/nurullahnamal/A-Yap-land-rmas-ve-Dinamik-Y-nlendirme/blob/main/r4%20-%20show%20ip%20route.png)
![image alt](https://github.com/nurullahnamal/A-Yap-land-rmas-ve-Dinamik-Y-nlendirme/blob/main/r4%20-%20show%20ip%20interface%20brief.png)

### Router 4 (R4 - Superonline) Konfigürasyonu
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
IGNORE_WHEN_COPYING_END

interface multink 1
no shutdown
no ip address
ip address 2.2.1.1 255.255.255.0
pp multink
ppp multink grop 1

interface serial 2/0
no ip address
no shurdown
encapsulation ppp
ppp multilink
ppp multilnk group 1
exit

interface serial 2/1
no ip address
no shudown
encapsualion ppp
ppp multilink
ppp multink group 1

interface multilink 2
no ip address
no shutdown
ip address 4.4.4.2 255.255.255.0
ppp multink
ppp multink group 2
exit

interface serial 3/0
no shutdown
no ip address
encapsualtion ppp
ppp mutlink
ppp multink group 2
exit

interface serial 3/1
no shutdown
no ip address
encapsualtion ppp
ppp mutlink
ppp multink group 2
exit

interface multilink 3
no shutdown
no ip address
ip address 5.5.5.1 255.255.255.0
ppp multink
ppp multink group 3

interface serial 2/2
no shutdown
no ip address
encapsulation ppp
ppp multink
ppp mutlink group 3
exit

interface serial 2/3
no ip address
no shutdown
encapsualion ppp
ppp mutlink
ppp multink group 3

router eigrp 1
eigrp router-id 1.1.1.6
network 5.5.5.0
network 4.4.4.0
network 2.2.1.0

router bgp 200
neighbor 4.4.4.1 remote-as 100
neigbor 5.5.5.2 remote-as 300
network 5.5.5.0 mask 255.255.255.0
network 4.4.4.0 mask 255.255.255.0
netowrk 2.2.1.0 mask 255.255.255.0

interface serial 3/2
no shutdown
ip address 11.11.11.2 255.255.255.0
exit

router bgp 200
neighbor 11.11.11.1 remote-as 500
netowrk 11.11.11.0 mask 255.255.255.0
exit

router eigrp 10
netowrk 11.11.11.0
address-amily ipv4
redistribute static

reouter bgp 100
network 192.168.100.0 mask 255.255.255.0
network 192.168.101.0 mask 255.255.255.0
network 192.168.102.0 mask 255.255.255.0
network 192.168.103.0 mask 255.255.255.0
end
write
![image alt](https://github.com/nurullahnamal/A-Yap-land-rmas-ve-Dinamik-Y-nlendirme/blob/main/r5%20show%20ip%20route.png)
![image alt](https://github.com/nurullahnamal/A-Yap-land-rmas-ve-Dinamik-Y-nlendirme/blob/main/r5%20show%20ip%20interface%20brief.png)
### Router 5 (R5) Konfigürasyonu
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
IGNORE_WHEN_COPYING_END

enable
conf, termnianl
interface fastEthernet 0/0
no shurdown
ip address 172.16.100.1 255.255.255.0
exit

interface fastEthernet 0/1
no shutdown
ip address 172.16.101.1 255.255.255.0
exit

interface multilink 1
no shutdown
no ip address
ip address 2.2.1.2 255.255.255.0
ppp multilink
ppp multink group 1

inteface serial 2/0
no shutdown
no ip address
encapsulation ppp
ppp multilkink
ppp multink gruop 1

interface serial 2/1
no shutdown
no ip address
encapsulation ppp
ppp multink
ppp multink group 1

router eigrp 1
eigrp router-id 1.1.1.5

network 172.16.101.0
network 172.16.100.0
network 2.2.1.0
end
write

![image alt](https://github.com/nurullahnamal/A-Yap-land-rmas-ve-Dinamik-Y-nlendirme/blob/main/r6%20%20show%20ip%20interface%20brief.png)
![image alt](https://github.com/nurullahnamal/A-Yap-land-rmas-ve-Dinamik-Y-nlendirme/blob/main/r6%20-%20show%20ip%20route.png)
### Router 6 (R6 - Vodafone) Konfigürasyonu
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
IGNORE_WHEN_COPYING_END

enable, conf ter

interface serial 2/0
no shutdown
ip address 3.3.2.1 255.255.255.0
exit

interface serial 2/1
no shutdown
ip address 3.3.1.1 255.255.255.0
exit

interface multilink 1
no shutdown
ip address 6.6.6.2 255.255.255.0
ppp multilink
ppp multilink gorup 1
exit

interface serial 2/2
no shutdown
no ip address
encapsulaion ppp
ppp multilink
ppp multink group 1
exit

interface serial 2/3
no shutdown
no ip address
encapsulaiyon ppp
ppp mulitnk
ppp muıltink group 1
exit

interface multilink 2
no shutdwon
ip address 5.5.5.2 255.2555.255.0
pp multink
ppp multşink group 2
exit

interface serial 3/0
no ip address
no shutdown
encapsulation ppp
ppp multink
ppp multinlk grop 2

interface serial 3/1
no ip address
no shutdown
encapsulation ppp
ppp multink
ppp multinlk grop 2

router ospf 1
router-id 1.1.1.6
network 6.6.6.0 0.0.0.255 area 10
network 5.5.5.0 0.0.0.255 area 10
network 3.3.1.0 0.0.0.255 area 10
network 3.3.2.2 0.0.0.255 area 10

router bgp 300
neighbor 5.5.5.1 remote-as 200
neighbor 6.6.6.1 remote-as 100
network 6.6.6.0 mask 255.255.255.0
netowrk 5.5.5.0 mask 255.255.255.0
network 3.3.2.0 mask 255.255.255.0
netowrk 3.3.1.0 mask 255.255.255.0

interface serial 3/2
no shutdown
ip addres 7.7.7.2 255.255.255.0
exit

router ospf 1
network 7.7.7.0 0.0.0.255
default-information originate

router bgp 1
neighbor 7.7.7.1 remote-as 500
netowrk 7.7.7.0 mask 255.255.255.0
exit

ip route 0.0.0.0 0.0.0.0 7.7.7.1

router bgp 300
network 10.10.101.0 mask 255.255.255.0
network 10.100.100.0 mask 255.255.255.0
end write
![image alt](https://github.com/nurullahnamal/A-Yap-land-rmas-ve-Dinamik-Y-nlendirme/blob/main/r7%20-%20show%20ip%20interface%20brief.png)
![image alt](https://github.com/nurullahnamal/A-Yap-land-rmas-ve-Dinamik-Y-nlendirme/blob/main/r7%20-%20show%20ip%20interface%20brief.png)
### Router 7 (R7) Konfigürasyonu

enable conf termınal
interface fastEthernet 0/0
no shutdown
ip addres 10.100.100.1 255.255.255.0
exit
interface serial 2/0
no shutdwo
ip addres 3.3.2.2 255.255.255.0
exit

interface serial 2/1
no shutdown
ip addres 3.3.3.1
exit

router ospf 1
router-id 1.1.1.7
network 3.3.2.0 0.0.0.255 area 10
netowrk 3.3.3.0 0.0.0.255 area 10
netowrk 10.100.100.0 0.0.0.255 area 10
exit

![image alt](https://github.com/nurullahnamal/A-Yap-land-rmas-ve-Dinamik-Y-nlendirme/blob/main/r8%20-%20show%20ip%20interface%20brief.png)
![image alt](https://github.com/nurullahnamal/A-Yap-land-rmas-ve-Dinamik-Y-nlendirme/blob/main/r8%20-%20show%20ip%20route.png)

### Router 8 (R8) Konfigürasyonu
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
IGNORE_WHEN_COPYING_END

enable , configure terminal

interface fastEthernet 0/0
no shutdown
ip addres 10.10.101.1 255.255.255.0
exit

interface serial 2/1
NO SHUTDOWN
ip addres 3.3.3.2 255.255.255.0
exit

interface serial 2/0
NO SHUTDOWN
ip addres 3.3.1.2 255.255.255.0
exit

router ospf 1
router-id 1.1.1.8
netowrk 3.3.1.0 0.0.0.255 area 10
netowrk 3.3.3.0 0.0.0.255 area 10
network 10.10.101.0 0.0.0.255 area 10
exit

![image alt](https://github.com/nurullahnamal/A-Yap-land-rmas-ve-Dinamik-Y-nlendirme/blob/main/r9%20show%20bgp%20summary.png)
![image alt](https://github.com/nurullahnamal/A-Yap-land-rmas-ve-Dinamik-Y-nlendirme/blob/main/r9%20show%20ip%20interface%20brief.png)
![image alt](https://github.com/nurullahnamal/A-Yap-land-rmas-ve-Dinamik-Y-nlendirme/blob/main/r9%20show%20ip%20interface%20brief.png)

### Router 9 (R9) Konfigürasyonu
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
IGNORE_WHEN_COPYING_END

conf terminal
interfaca serial 2/2
no shutdown
ip address 7.7.7.1 255.255.255.0
exit

interface serial 2/0
no shutwon
ip address 9.9.9.1 255.255.255.0
exit

interface serial 2/1
no shutdown
ip addres 11.11.11.1 255.255.255.0
exit

configure termainal

interface fastEthernet 0/0
ip address 192.168.1.210 255.255.255.0
no shutdown
exit

router bgp 500
neigbhor 7.7.7.2 remote-as 300
neigbor 9.9.9.2 remote as 100
neighbor 11.11.11.2 remote-as 200
noetwork 9.9.9.0 mask 255.255.255.0
netowrk 11.11.11.0 mask 255.255.255.0
netowrk 7.7.7.0 mask 255.255.255.0

ip route 192.168.100.0 255.255.255.0 9.9.9.2
ip route 192.168.101.0 255.255.255.0 9.9.9.2
ip route 192.168.102.0 255.255.255.0 9.9.9.2
ip route 192.168.103.0 255.255.255.0 9.9.9.2
ip route 172.16.0.0 255.255.0.0 11.11.11.2
ip route 10.0.0.0 255.0.0.0 7.7.7.2
ip route 0.0.0.0 0.0.0.0 192.168.2.1

![image alt](https://github.com/nurullahnamal/A-Yap-land-rmas-ve-Dinamik-Y-nlendirme/blob/main/r10%20-show%20ip%20route.png)
![image alt](https://github.com/nurullahnamal/A-Yap-land-rmas-ve-Dinamik-Y-nlendirme/blob/main/r10%20show%20ip%20interface%20brief.png)
### Router 10 (R10 - Müşteri Router'ı) Konfigürasyonu

interface fastEthernet 0/0
ip address 192.168.200.1 255.255.255.0
no shutdown
exit

interface fastEThernet 0/1
no shutdown
pppoe enable
pppoe-client dial-pool-number 1
exit

interface dialer 1
mtu 1492
ip address negotiated
encapsualiton ppp
dialer pool 1
ppp authentication chap callin
ppp chap hostname test
ppp chap password CCNA
exit

ip route 0.0.0.0 0.0.0.0 dialer 1
interface fastethernet 0/1
ip nat outside
exit

interface fastethernet 0/0
ip nat inside
exit

ip nat inside source static 192.168.200.10 10.101.0.50

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
