# VPC 개념 정리

### VPC란 무엇인가?
Virtual Private Cloud의 약자로서 기존의 네티워크와 아주 유사한 가상 네트워크를 지칭함.  
하나의 공유기와 같은 개념으로 고정 ip는 instance(EC2...)에서 연결하며 해당 고정 ip 내 사설 ip를 나타내는 것을 의미한다.  
CIDR을 통하여 Public ip안에서 사설 네트워크(private Network)를 사용하여 로컬에서 만드는 것을 의미한다.
(AWS에서는 처음 시작 시 기본적인 VPC가 있으며 따로 VPC를 생성해서 만들 수도 있음.)  

### VPC 이해를 위한 구조도 
**Client to Server : Client > 인터넷 게이트웨이 > VPC > 라우터 > 라우터 테이블 > NACL(네트워크 ACL) > 서브넷 > Security Group > Instance  
Server to Client : Instance > Security Group(outbound) > 서브넷 > NACL(네트워크 ACL) > 라우터 테이블(outbound) > 라우터 > VPC > 게이트웨이 > Client**
서브넷(Subnet) : VPC의 IP 주소 범위를 의미한다. Subnet을 통해서 AWS에 리소스 배포가 가능하다. (VPC의 CIDR을 더 세세하게 쪼개는 방식)
IP 주소 지정(Elastic IP): AWS의 경우에는 기본적으로 변동 ip를 가지고 있으나 이것을 고정 ip로 변경할지 여부를 확인한다.
라우팅 테이블(Routing Table) : 라우팅하여 서브넷 또는 트래픽 전달 위치를 결정합니다.
인터넷 게이트웨이 : VPC를 다른 네트워크에 연결함(해당 게이트웨이를 거쳐야 인터넷으로 연결이 가능하다.)
엔드포인트 : NAT을 거치지 않고 AWS 서비스로 게이트웨이가 연결될 수 있게 하는 장치

### VPC 대쉬보드 각각의 기능

#### VPC
1. VPC ID : 만든 VPC 고유의 ID값(해당 ID를 통하여 서브넷/라우터 등을 연결)
2. 상태 : 현재 해당 VPC가 사용가능한지를 알려줌
3. IPv4 CIDR : VPC 내 인스턴스 및 리소스에 할당되는 IP주소를 결정하는 것을 의미함. IP주소는 기본적으로 2^32개로 되어있으며 앞에 몇번째까지를 같은 CIDR 그룹으로 만들 것인가에 대해서 나타낸다.(/16 : 앞의 16자리, /8 : 앞의 8자리) 
  * CIDR 숫자가 클수록 앞의 자리수로 묶는 것이 커지기 때문에 그만큼 네트워크 개수가 줄어드는 것이라고 볼 수 있다.
  * **결국 네트웨크를 얼마나 사용할 것인지에 대하여 생각하고 풀어내야한다.**
  * 서브넷(Subnet)의 경우에는 VPC의 CIDR을 또 다시 쪼개서 사용하는 것이라고 생각하면 된다.  
4. DHCP 옵션 세트 : 도메인 이름과 도메인 이름 서버(DNS)가 있는 곳으로 AWS 컴퓨터와 연결하고 상호작용할 수 있도록 하는 AWS 자체 옵션(동적 호스트 구성 프로토콜)  
  * 도메인 이름(Domain name) : 클라이언트가 사용해야하는 도메인 이름
  * 도메인 이름 서버(Domin name servers : DNS) : 네트워크 인터페이스가 도메인 이름 확인에 사용할 DNS 서버
  * NTP 서버 : 네트워크의 인스턴스에 시간을 제공하는 NTP 서버
5. 기본 라우팅 테이블 : 1개의 VPC 안에 있는 여러가지 Routing Table 중에서 기본적으로 사용할 것
6. 기본 네트워크 ACL(NACL) : VPC에서 규칙 생성을 통하여 어떤 호스트를 막을지를 판단하는 가장 중요한 보안규칙
  * 인바운드 : 외부에서 해당 VPC로 들어오는 요청을 어떤 호스트를 들여보낼 것인가를 확인(보통 VPC에서는 모든 트래픽을 받는 것이 일반적이다.)
  * 아웃바운드 : 내부에서 외부로 내보낼 때 어떤 대상(IPv4)에서 요청할 때 보낼 것인가를 확인(보통 VPC에서는 모든 트래픽을 보내는 것이 일반적이다.)
  * 네트워크 ACL의 경우는 결론적으로 VPC와 인스턴스를 연결했을 때 어떤 IPv4와 유형을 들여보낼 것인가에 대한 가장 큰 보안 방화벽이다.
7. 테넌시(tenancy) : tenant의 집합여부를 확인하는 것으로 예를 들면 어떤 하나의 프로젝트에 여러 개의 VPC가 있을 수 있는데 이 때 VPC를 묶는 것을 의미한다.(기본 : Default)

#### 서브넷(SUBNET)
1. Name : Sunnet의 이름으로 Instance에 연결할 때 사용하며 Instance를 어디 Subnet 안에 넣을 것인가를 확인하는 방식
  * Private Subnet : 외부에서 다이렉트로 접근이 불가능한 네트워크 영역(인터넷 게이트웨이 라우팅이 없음) => 내부에서 외부로만 접근 가능하게 할 수 있음(NAT 게이트웨이)
  * Public Subnet : 외부에서 접근이 가능한 네트워크 영역(subnet이 인터넷 게이트웨이로 향하는 라우팅이 있다면 퍼블릿 서브넷이라고 칭함)
  * **Subnet과 게이트웨이 연결 여부 확인 방법 : Router Table에서 Routing이 게이트웨이와 연결되어 있는지 확인 필요**
  * Private Subnet은 AWS Instance에서 사용 불가(외부에서 접근이 불가)하므로 SSH를 내부에서 연결해서 사용해야함 ( 인트라넷과 같은 개념 )
  * Public Subnet은 AWS Instance에서 사용이 가능함(외부 접속 가능) 따라서, 어느 컴퓨터에서든지 파일을 고칠 수 있다.
2. 서브넷 ID : Subnet 고유 ID
3. VPC : 해당 Subnet이 어디 VPC에 연관되어 있는지를 확인
4. IPv4 CIDR : VPC에서 정의된 IPv4 CIDR 안에 블록을 추가적으로 나누는 방식을 의미함.
5. 사용 가능한 IP 주소 : 해당 주소를 통하여 연결할 수 있음(Private => 내부에서만 가능 , Publiv => 인터넷에서 가능)
6. 플로우 로그(Flow Log) : 특정 유형의 트래픽을 감지 / 트래픽 변화와 패턴 파악 => 로그 정보를 Amazon S3에 저장됨 (보통 Input/output 모니터링이라 생각하면 됨)(유료)
7. 라우팅 테이블(Routing Table) : 어떤 라우팅 테이블을 사용할 건지를 확인한다.(Routing에서 인바운드/아웃바운드 설정)
8. 네트워크 ACL (NACL) : VPC에서 사용중인 ACL과 같은 의미
9. CIDR 예약 : 그냥 기존 CIDR에서 추가로 나누는 기능인듯? (정확하지 않음)
10. 리소스 공유(서브넷 공유) : 다른 AWS 계정의 VPC에 해당 Subset을 등록하고 싶을 때 사용 (개발 단계에서 AWS Skeleton(최고 root)의 개념이 있는 것 같음.)
11. 태그 : 그냥 ID값만 들어가 있음.

#### 라우팅 테이블(Routing Table)
1. 라우팅(Routing) : 네트워크에서 경로를 선택하는 프로세스 
2. 서브넷 연결
  * 명시적 서브넷 연결 : 직접 Subnet을 연결할 때 사용함.
  * 명시적 연결이 없는 서브넷 : 기본 라우팅 테이블에 연결되어 있는 상태를 의미함 (그냥 VPC가 만들 때 기본적으로 연결된 것...)
3. 엣지 연결(Edge Assosiation) : IGW or VGW에서 특정 인스턴스의 ENI로 라우팅 할 수 있도록 하는 서비스 (아웃바운드 : 라우팅 테이블, 인바운드 : Edge Associations)(다시 공부)
4. 라우팅 전파 : 가상 프라이빗 게이트웨이가 라우팅 테이블에 라우팅을 자동으로 전파 (다른 VPC에 있는 게이트웨이와 연결하는 방식) (VPN ??) (여기서부터!)

#### 인터넷 게이트웨이(Internet GateWay : IGW)

#### 송신 전용 인터넷 게이트웨이
#### 캐리어 게이트웨이
#### 엔드포인트 (End Point)
#### NAT 게이트웨이


### VPC 이해를 위한 기본적인 명칭
1. CIDR(Classless Inter-Domain Routing) : 도메인간 라우팅에 사용되는 인터넷 주소를 능동적으로 사용할 수 있게 할당하여 지정하는 방식 (Router 내 네트워크 주소를 지정하는 방식)
2. Router : Routing table과 같은 의미로 자동으로 IP(인터넷 프로토콜)를 호스트하는 IP 주소 
3. DHCP(Dynamic Host Configuration) : 동적 호스트 구성 프로토콜로 DN / DNS을 통해서 VPC 안에서의 CIDR을 자연스럽게 이동할 수 있게 하는 것
4. ACL(Access Control List) : 특정 주소를 가진 호스트의 접근을 막거나 방화벽을 구축하는데 중요한 요소
5. ENI(Elastic Network Interface) : Elastic Ip를 만들어서 인스턴스에 부착시키는 것을 의미한다.

### AWS VPC의 구성요소
VPC ID :
IPv4 CIDR : 
DHCP 옵션세트 : 
기본 라우팅 테이블 :
기본 네트워크 ACL :
