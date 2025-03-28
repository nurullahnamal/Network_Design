# A-Yap-land-rmas-ve-Dinamik-Y-nlendirme
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


TELEKOMR1#SHOW ip interface brief
Interface IP-Address OK? Method Status Protocol
FastEthernet0/0 192.168.100.1 YES manual up up
FastEthernet0/1 192.168.101.1 YES manual up up
FastEthernet1/0 unassigned YES unset administratively down down
Serial2/0 unassigned YES unset administratively down down
Serial2/1 unassigned YES unset administratively down down
Serial2/2 unassigned YES manual up up
Serial2/3 unassigned YES manual up up
Multilink1 1.1.1.1 YES manual up up

### Router 1 (TELEKOMR1) - Yönlendirme Tablosu
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
IGNORE_WHEN_COPYING_END

TELEKOMR1#show ip route
Codes: C - connected, S - static, R - RIP, M - mobile, B - BGP
D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area
N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2
E1 - OSPF external type 1, E2 - OSPF external type 2
i - IS-IS, su - IS-IS summary, L1 - IS-IS level-1, L2 - IS-IS level-2
ia - IS-IS inter area, * - candidate default, U - per-user static route
o - ODR, P - periodic downloaded static route

Gateway of last resort is 1.1.1.2 to network 0.0.0.0

1.0.0.0/8 is variably subnetted, 3 subnets, 2 masks
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
IGNORE_WHEN_COPYING_END

C 1.1.1.0/24 is directly connected, Multilink1
C 1.1.2.0/24 [110/64] via 1.1.1.2, 05:42:18, Multilink1
C 1.1.1.2/32 is directly connected, Multilink1
9.0.0.0/24 is subnetted, 1 subnets
O 9.9.9.0 [110/96] via 1.1.1.2, 05:42:18, Multilink1
O 192.168.102.0/24 [110/74] via 1.1.1.2, 05:42:18, Multilink1
O 192.168.103.0/24 [110/74] via 1.1.1.2, 05:42:18, Multilink1
C 192.168.100.0/24 is directly connected, FastEthernet0/0
C 192.168.101.0/24 is directly connected, FastEthernet0/1
O*E2 0.0.0.0/0 [110/1] via 1.1.1.2, 05:40:55, Multilink1

## Konfigürasyon Örnekleri

Aşağıda her bir router'ın konfigürasyonlarının tamamı yer almaktadır.

### Router 1 (R1) Konfigürasyonu
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
IGNORE_WHEN_COPYING_END

enable
config terminal
interface fastethernet 0/0
ip address 192.168.100.1 255.255.255.0
no shutdown
interface fastethernet 0/1
ip address 192.168.101.1 255.255.255.0
no shutdown
Show ip interface brief

router ospf 1
router-id 1.1.1.1
network 1.1.1.0 0.0.0.255 area 0
network 192.168.100.0 0.0.0.255 area 0
network 192.168.101.0 0.0.0.255 area 0
exit

### Router 2 (R2) Konfigürasyonu
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
IGNORE_WHEN_COPYING_END

enable
config terminal
interface multilink 1
no shutdown
ip address 1.1.1.2 255.255.255.0
ppp multilink
ppp multilink group 1
exit

interface serial 2/2
no ip address
no shut down
encapsulation ppp
ppp multinlik
ppp multinlk group 1

interface serial 2/3
no ip address
no shut down
encapsulation ppp
ppp multinlik
ppp multinlk group 1

interface multilink 2
no shutdown
ip address 1.1.2.1 255.255.255.0
ppp multilink
ppp multilink group 2

interface serial 2/0
no ip address
encapsualion ppp
ppp multink
ppp multink gorup 2
no shutdown

interface serial 2/1
no ip address
no shutdown
encapsulation ppp
ppp multinkiş
ppp multink goup 2

router ospf 1
router-id 1.1.1.2
network 1.1.1.0 0.0.0.255 area 0
network 1.1.2.0 0.0.0.255 area 0

router bgp 100
neigbor 6.6.6.2 remote-as 300
neighbor 4.4.4.2 remote-as 200
network 1.1.1.0 mask 255.255.255.0
network 1.1.2.0 mask 255.255.255.0
netowrk 4.4.4.0 mask 255.255.255.0
netowrk 6.6.6.0 mask 255.255.255.0

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

### Router 7 (R7) Konfigürasyonu
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
IGNORE_WHEN_COPYING_END

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

### Router 10 (R10 - Müşteri Router'ı) Konfigürasyonu
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
IGNORE_WHEN_COPYING_END

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
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
IGNORE_WHEN_COPYING_END

Bu güncellenmiş README.md dosyası, tüm router konfigürasyonlarını ve show ip interface brief ile show ip route çıktısını içermektedir. Bu, depoyu kullanan kişilere daha kapsamlı bir genel bakış sunacaktır.

Lütfen unutmayın, yine de hassas bilgileri (parolalar, anahtarlar vb.) tüm dosyalardan kaldırmanız gerekmektedir.
