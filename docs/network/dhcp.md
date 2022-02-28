# DHCP 동작원리

## DHCP 개념 및 동작원리

**DHCP(Dynamic Host Configuration Protocol)란?**

유무선 IP 환경에서 단말의 IP 주소, 서브넷 마스크(Subnet Mask), 디폴트 게이트웨이(Default Gateway) , IP 주소, DNS 서버 IP 주소, 임대기간(Lease Time) 등의 다양한 네트워크 정보를 DHCP 서버가 PC와 같은 이용자 단말에 자동으로 할당해 주는 프로토콜

**※ 장점**

이용자가 네트워크 정보를 직접 설정할 필요 없이 자동으로 그 설정이 가능하기 때문에 네트워크 관리의 용이성을 제공해준다.

1. IP 주소 할당 절차 (IP Address Allocation Procedure)

: PC와 같은 단말이 DHCP 서버로부터 IP 주소 등의 네트워크 정보를 할당받기 위해서는 4가지 단계를 거치게 된다.

1. DHCP Discover
2. DHCP Offer
3. DHCP Request
4. DHCP Ack

![](<../../.gitbook/assets/image (5).png>)

**1-1) DHCP Discover**

단말이 DHCP서버를 찾는 단계

DHCP 서버를 찾기 위해 Discover메시지를 이더넷에 Broadcasting한다. 동일 서브넷안에 있는 모든 단말들은 이 메시지를 수신한다.

**1-2) DHCP Offer** Discover메시지를 수신한 DHCP 서버는 자신을 알리기 위해 Offer메시지를 Broadcasting 한다. 위와 동일하게 동일 서브넷안에 있는 단말들은 Offer메시지를 수신한다.

**1-3) DHCP Request**

DHCP 서버 존재를 확인한 PC는 Request 메시지를 Broadcasting

**1-4) DHCP Ack**

DHCP 서버는 Request메시지 내에 Server Identifier에 기록된 IP 주소가 자신의 주소인지 확인 후 Offer메시지와 함께 다양한 네트워크 정보들을 전달(IP , Subnet , Gateway , DNS , Lease Time)

#### **2. 주소 임대기간 연장 절차 (IP Address renewal procedure)**

DHCP Ack 메시지에는 IP Lease Time 파라미터가 포함되어 있으며 , PC는 명시된 임대기간 동안만 해당 IP 주소를 사용 임대기간 이상 해당 IP 주소를 사용하기 위해서는 DHCP 서버에게 IP 주소 임대기간 연장을 요청해야 함

![](<../../.gitbook/assets/image (3) (1).png>)

**2-1) DHCP Request**

"1.1.1.254주소를 가진 DHCP 서버님 , 제가 IP주소 1.1.1.10 임대기간을 연장하고 싶은데요. 허락해주세요" request 메시지를 Unicasting으로 보냅니다. 단말과 서버 간에 서로 IP 주소를 알고 있기 때문에 임대기간 연장을 요청하는 단말 IP 주소를 포함하여 보냅니다.

**2-2) DHCP Ack**\
"요청을 수락하겠습니다. IP 주소 1.1.1.10을 2시간 더 사용하도록 하세요" 이것 또한 모든 정보를 포함해서 Unicasting으로 보낸다.

#### **3. IP 주소 반납 절차 ( IP Address Release Procedure )**

PC를 로그오프 or ipconfig /release를 하게 되면 단말은 할당된 IP 주소를 DHCP 서버에 반환

![](<../../.gitbook/assets/image (6) (1).png>)

3-1) DHCP Release " 1.1.1.254주소를 가진 DHCP 서버님. 그동안 사용했던 IP주소 1.1.1.10을 반납하겠습니다" DHCP Release 메시지를 Unicasting으로 서버에 전달, IP 주소를 반환

기술 문서를 통해 DHCP 프로토콜을 이용한 1) IP 주소 할당(임대), 2) IP 주소 임대기간 연장 3) IP 주소 반납 절차에 대해서 살펴보았다.
