# DNS Record

DNS(Domain Name System) : 인터넷의 모든 사이트에서 IP 주소, 도메인 이름, 호스팅 및 기타 등록 정보를 포함하는 대규모 정보 시스템

### DNS Record란? <a href="#ed6bd121-8c82-433f-81a2-60106f8a189b" id="ed6bd121-8c82-433f-81a2-60106f8a189b"></a>

: DNS서버가 해당 패킷을 받았을 때 어떤식으로 처리할지를 나타내는 지침

즉, 도메인에 관한 설정을 하기 위해 사용 되는 일련의 문자들을 통칭함

* 서버가 요청에 응답하는 방법에 대한 다양한 구문과 명령이 포함되어 있다.



### 일반적인 Record <a href="#484826b2-0d84-4918-8c02-30ca64e21a55" id="484826b2-0d84-4918-8c02-30ca64e21a55"></a>

**A record**

: 도메인과 연결된 실제 IP 주소

* 하나의 도메인에 여러 개의 IP 주소 등록 가능
*   ex.

    [naver.com](http://naver.com/)의 A레코드 조회하였을 때 4개의 IP주소 매핑됨

    Non-authoritative answer: Address: 223.130.195.95 Address: 223.130.200.107 Address: 223.130.200.104 Address: 223.130.195.200



**AAAA record**

: A의 확장형으로 도메인에 IPv6 매핑되어 있는 레코드

* IPv6가 대중적이지 않아 거의 없다.



**CNAME(Canonical NAME) record**

: 현재 도메인 아래에 나열되거나 현재 도메인과 연결된 하위 도메인을 나타내는데 사용

즉, Alias라고 하여 기존 도메인에 별명을 붙인 레코드

*   ex.

    [goldsony.tistory.com](http://goldsony.tistory.com/) 도메인이 있을 때 도메인의 CNAME이 [gsony.tistory.com](http://gsony.tistory.com/)이면

    gsonry.tistory.com 입력 시 접근 가능!



**MX(Mail eXchanger) record**

: 도메인에 따라 사용될 수 있는 모든 메일 서버

* 해당 도메인과 연동되어있는 메일서버 확인시 사용
*   ex.

    [naver.com](http://naver.com/) 경우 당연히 연동되어있는 메일서버가 있을 것이고

    이 도메인에 대한 MX 레코드는 10:mx1.naver.com, 10:mx2.naver.com, 10:mx3.naver.com



**NS record**

: 현재 도메인에 사용중인 네임 서버를 보여줌

*   ex.

    [naver.com](http://naver.com/)의 NS레코드 : e-ns.naver.com, ns1.naver.com, ns2.naver.com



**PTR record**

: IP주소에 대한 도메인 주소를 확인할 수 있는 레코드

* [naver.com](http://naver.com/)의 경우 등록이 안되어있는 것으로 보인다.



**SOA record**

: 도메인이 마지막으로 업데이트 된 시기 및 관련 연락처 정보와 같이 도메인에 대한 중요한 정보 저장

*   ex.

    naver : ns1.naver.com webmaster.naver.com 2021012809 21600 1800 1209600 180

    마스터 네임서버, 존 관리자 연락처, 존 데이터 동기화 시간, 갱신주기, 시도 , 만료 등 정보를 나타내고있다.



**TXT(Text) record**

: 현재 목록에 없는 도메인에 대한 추가 정보를 포함하도록 편집 가능

* 주로 메모를 남기는 레코드



**CAA**

: 도메인 인증기관에 관련된 레코드



### DNS Record를 확인하는 방법 <a href="#35e73540-0299-407a-8386-5a3845cf1e21" id="35e73540-0299-407a-8386-5a3845cf1e21"></a>

1. `nslookup` 사용

* Windows : cmd, Mac : iterm 명령어를 이용해 확인할 수 있다.
*   ex.

    네이버 mx record 확인 : `nslookup -query=MX naver.com`

    네이버 a record 확인 : `nslookup naver.com`

``

&#x20; 2\. whatmydns.net

* 터미널 명령보다 간단하게 dns record를 확인할 수 있다.

[![](https://www.whatsmydns.net/images/logo-og.png)](https://www.whatsmydns.net/)
