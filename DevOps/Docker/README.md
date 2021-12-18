# Docker

# Docker

도커 등장 전 : 

자체 서버 운영 → 설정 관리 도구 등장(CHEF, puppet, **ansible**) → 가상 머신 등장 → 클라우드 등장 → PaaS 등장 → 도커 등장 → 쿠버네티스 등장 → 서비스메시 등장

## 설정 관리 도구 :

환경에 대한 설정을 명령어로 관리하는게 아니라, 코드로 관리한다.

형상관리, 코드리뷰 등이 가능해진다.

*  chef, puppet 의 단점 : 100대를 업데이트 해야할 때, 100대 모두 client 등록해야함.
    ansible은 target server에 설치해야할 게 없다. 통신만 되면됨.

 

## VM 등장 :

- 자체 서버 에서 A, B, C 등의 환경을 올렸을 때 A 의 문제로 B, C 가 영향 받을 수 있음.
- VM 에서는 A, B, C 가 독립적으로 처리됨.

### mutable vs immutable

- mutable : 기존의 것에서 업데이트
- immutable : 업데이트 된 것을 만들어서 교체.

## 클라우드

1. **서비스 아키텍처를 구성**할 수 있다는게 가장 큰 장점.
2. 하드웨어 파편화 문제 해결.
3. 이미지 기반이 좀 더 보강됨. 
    
    서버 상태 관리에 대한 새로운 접근.
    

서버 운영 문제는 여전히 남아있다.  (코드로 하던, 커맨드로 하던)

클라우드 이미지의 단점 : 스냅샷이 많아질수록 그 이미지 관리가 힘듬.

- 어떻게 구성되어있는지 모름.
- 처음부터 다시 만들 수 없음.
- 관리가 어려움.

## PaaS  : Platform as a Service

서비스 구성에 따라 패턴이 비슷하니까  이부분을 관리해주겠다.

사용자는 서버 운영을 안 할 수 있다.

- *창업을 하게 된다면  PaaS로 하는게 좋다.  서버 관리자 1명 영입보다 개발자 1명 영입 하고 PaaS에게 맡기는게 낫다.*

단점 : 

PaaS 방식에 맞춰줘야함.

서버에 대한 원격 접속 시스템 X → 서버 상태를 이용자가 바꿀 수는 없다.

새로운 패러다임을 적용 못한다. 제약적.

ex)

![Docker%200c562acb37ff45c8a0994e48f7142311/Untitled.png](Docker%200c562acb37ff45c8a0994e48f7142311/Untitled.png)

## 도커

격리된 환경을 제공해주는 프로세스

1. 기존 가상환경 보다 가볍다. 
    
    →  기존 :  Layer 가 더 있다. 
    
    →  도커 : guest OS가 필요없다.
    

![Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%201.png](Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%201.png)

2. Docker Engine만 있으면 환경 구성 가능.

**쉽게 개발 서버 만들고 테스트 서버 만들고 간편함. → Runtime 환경에 대한 영향이 없다.**

3. Blue-Green 배포 가능.

**도커를 제대로 쓰려면 배포방식도 도커 방식으로 바꾸면 좋다**

![Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%202.png](Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%202.png)

단점 : 
컨테이너가 많아진다.

⇒ 컨테이너 오케스트레이션  ( 쿠버네티스 , docker-swarm...)

쿠버네티스가 시장 점유 완료 ( docker-swarm 은 죽었다. ) 표준이 되어버렸다 PaaS 시장

## 컨테이너 오케스트레이션

- 스케줄링
    
    컨테이너를 적당한 서버에 배포해주는 작업. 애플리케이션의 요구사항이 합당한 서버로 배포. 없으면 pending
    
    컨테이너 개수가 여러개가 되면 적당히 나눠서 배포
    
    컨테이너가 죽으면 다른 서버에서 살려줌. ( 구동할 수 있는 리소스가 있을 때 )
    
- 클러스터링
    
    서버가 3개가 있다 치면  1개의 클러스터로 묶어서 1개의 서버인 것 처럼.
    
    사용자는 어느 서버에 해당 애플리케이션을 띄웠는지 알 필요 없음.
    
- 서비스 디스커버리
    
    서비스를 찾아주는 기능.
    
    다른 서버에서 서비스를 새로 띄웠을 때, 변하는 것 :  IP, port ( 이미 새로운 서버에서 해당 포트가 사용중이면 오케스트레이션이 랜덤하게 관리), ... 
    
- 로깅, 모니터링
    
    ### MSA
    
    아키텍처가 MSA 형태로 바뀌어 버렸음 쿠버네티스 때문에
    
    작고 작게 쪼개진 곳에서 로깅을 할 수 있을 까?
    
    ### 서비스 매시
    
    컨테이너가 누굴 호출했는지, 장애, 실패가 어디서 났는지 등을 다 연결해서 알아내줌.
    
    초록 : 컨테이너
    
    파랑 : 프록시 서버
    
    즉, 프록시 서버의 로그를 보면 원하는 로그를 다 알 수가 있음.
    
    ![Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%203.png](Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%203.png)
    
    ![Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%204.png](Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%204.png)
    

## cf) 서버리스

---

# Docker Overview

![Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%205.png](Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%205.png)

Hypervisor & Guest OS 없이,
App에 대한 Binary, Library만 있으면 되므로,
굉장히 가볍다.

리눅스 내장 가상머신 보다 훨씬 빠르다.

![Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%206.png](Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%206.png)

image, Container 영역

- image 영역 : 애플리케이션을 올리면서 서버의 상태가 변경될 때마다 새로운 image Layer가 생김.
- Container 영역 : 호스트가 실행 할 시점에 생기는 Layer → 이 영역만 건드릴 수 있음.

Base Image는 단 하나의 영역.

Image는 아래 Image를 ref하고 있음.
→ Apache 버전을 바꿔야 된다라고 할 때. 전체 이미지가 변경되지 않고, Apache 영역만 변경. 아래 image 영역은 캐싱

![Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%207.png](Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%207.png)

- os : 기본 os
- dockerd : 도커 데몬 : 도커 엔진
- remote : http/https 로 가능. (서버가 몇개 안될때는 자체적으로 ssh로 붙어서 CLI로 많이 작업함)
(도커만 쓴다고 하면 CLI로 많이 사용)  → OS or dockerd 로 연결.
(remote 쓴다고 하면 오케스트레이션을 많이 사용) → dockerd 로 연결.
    
    http는 거의 안씀 dockerd 가 해킹 당하면  모든 컨테이너 장악가능.
    
    CLI : 
    
    docker run nginx:1.14
    
    conatiner를 띄우라 했으니 nginx의 img를 찾는다.
    
    1. local Storage (file system)
    2. github와 같이 도커 허브라는 레지스트리(외부 저장소)에 요청.
        
        도커 허브의 IP : docker demon에 default setting
        
    3. Nginx:1.14를 local에 다운로드 (pull) 
    4. 기동
    
    고래 위에 Container 가 올라가게 된다.
    
    배꼽 : nginx가 뜨고 endUser가 붙어야 한다 ⇒ 브릿지 네트워크   **172.17.0.1**  이 도커 컨테이너로 갈 수 있는 IP 대역. ⇒ 도커제로 docker0
    
    외부에서 들어오는 Client는 호스트(10.0.2.15 내부 IP 예) 에 접근 후, 컨테이너 별로 IP 가 IP를 배정 받는다.
    
    컨테이너들은 대역이 다르다 ⇒  나트를 통해서 들어가야함.  ( VM 에서 네트워크  NAT ) : 다른 대역으로 전환해줌.
    
    ⇒ 즉 host에서 해당 컨테이너로 연결을 담당하는 것이 배꼽
    
    - 서비스 포트에 대한 포트 포워딩 기능도 제공.
        
        172.17.0.2 : 80
        172.17.0.3 : 80  이 있을 때, IP가 다르더라도, 10.0.2.15입장(사설 ip가 1개임)에서 포트가 같아서 8080 or 8090등으로 바꿔줘야함.
        
    
    ps) 7가지 정도(리소스 외 외부 자원 uid, network, namespace ...)  격리가 되는데 
    그 중 네트워크가 구성이 되어야 한다.
    

- Application Layer, Network Layer 등을 쓰지않고 커널단에서 커널기술만으로 끝낸다.
⇒ 그래서 빠르다.

### iptables

쿠버네티스의 단점 : 네트워크가 느리면 말짱 꽝.   ⇒ iptables 를 이용해서 관리.  ⇒ docker를 알아야 함.

---

# Microservice vs Monoliths

![Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%208.png](Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%208.png)

팀원 모두 MSA를 알지 않으면, 성공할 수 없음.

# 도커에 사용된 3가지 기술.  :  각 프로세스를 격리하기 위한 기술.

1. Chroot(Change Root Directory) : 리눅스 명령어
    
    루트를 바꾸는 명령어. ftp, ssh 등으로 접속했을 때 시작되는 root.
    
    ![Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%209.png](Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%209.png)
    
2. Cgroup
    
    block IO, cpu, ... 자원을 관리해주는 기술.
    
    **제한을 하지 않으면, 하나가 에러나면 다른데도 영향을 주게 됨**
    
    ![Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2010.png](Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2010.png)
    
3. Namespace
    
    uid, hostname, network ... 모두 독립되는 기술.
    
    container 별로 root가 다 있다 → UID를 다르게 할당하기 때문에.
    
    ![Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2011.png](Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2011.png)
    
    전체가 host 영역 : 1대1로 mapping되는 가상의 veth가 생김. Container와 연결할 수 있는.
    
    docker0 (브릿지)를 통해서 각각의 eth0으로 연결.
    
    ---
    

![Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2012.png](Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2012.png)

busybox latest 버전을 run 하면서 /bin/sh 쉘 하나 실행.

local 에 찾았는데 없어서, pull 받는다.

해시값에 따른 Image를 pull

image layer들은 Read/Only

## UFS (Union File System)

Container가 유실되면 데이터도 접근할 수 없는데, Volume mount 기능을 써서 데이터를 관리할 수 있음.

Union으로 연합,결합 하여 파일 시스템 하나로 결합.

Docker Storage Drivers ( 도커가 지원하는 파일 시스템 )

Storage driver category 

Union filesystems    ⇒ 

Snapshotting filesystems     ⇒  

Copy-on-write block devices     ⇒  

**Docker Storage drivers**

AUFS, Overlay, **Overlay2**

Btrfs, ZFS     단점 :  변경이력을 모두 관리하니 용량이 너무 커짐. inode가 꽉참.

Devicemapper

![Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2013.png](Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2013.png)

![Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2014.png](Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2014.png)

⇒ 단점 개선 : 알파인 리눅스   애초부터 가벼워서  공간 중복이 덜함.

---

---

---

![Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2015.png](Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2015.png)

1. 명령어를 이용해서 서버를 구성해야 했다.
2. 명령어 말고 코드를 이용해서 서버를 재연할 수 있게됐다.
3. 자체 서버 << 가상머신을 통한 여러개의 서버
4. 가상 머신 << 클라우드를 통한 성능 개선
5. PaaS : 코드에만 집중 할 수 있음. 서버에 관한 것을 마음대로 할 수 없음.
6. 클라우드 << 도커를 통한 이미지 관리(코드형태) + 프로세스 격리(like 가상머신)
7. 도커 + 도커 ⇒ 쿠버네티스  :  클러스터로 구성해서 하나의 서버처럼 사용.
8. 쿠버네티스 기반 MSA ⇒ 서비스메시 ( ex. Netflix )
쿠버네티스가 컨테이너 레이어는 관리해주지만 위의 애플리케이션은 관리해주지 못해서

가상 머신 :  논리적인 서버 Hypervisor위에  각각의 OS가 필요함. ⇒ 리소스 낭비.

도커 : 하이퍼바이저 OS 생략해서  리소스 낭비가 없음.

# 실습

도커 실행

docker run []  ⇒  local 에서 찾고 못찾으면 registry에서 찾고.

→ 실행되고 꺼져버림.

### ubuntu 최신 버전 + hello world 찍기

`docker run -dt ubuntu:latest echo hello, world!`

### background에서 nginx 실행

- -d  :  background
- —name : 컨테이너 이름 지정.

`docker run -d —name web nignx`

![Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2016.png](Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2016.png)

### background로 httpd 실행

`docker run -d —-name web2 httpd:latest`

![Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2017.png](Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2017.png)

독립적으로 돌아가는 것을 알 수 있음.

## 해당 컨테이너에 접속하기.

`docker container attach`   :   container가 OS 기반일 때  (자주 사용하지 않음)

background에 돌고 있는 OS기반 컨테이너를  foreground로 불러내고 shell에 접속.

docker run -it  

- i : standard input
- t : tty

![Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2018.png](Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2018.png)

각각 프로세스 별로 root가 존재하니까 root가 됨.

ctrl + p, q ⇒ 다시 백그라운드로 보냄.

![Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2019.png](Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2019.png)

ps로 백그라운드에 있는 것 확인 후

attach 명령어로 다시 접속.

`exit` ⇒ 종료  :  bash shell을 종료하고 나와버리니까 종료가 될 것.

`docker ps -l` :  최근에 사용했던 컨테이너 정보를 보여줌.

![Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2020.png](Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2020.png)

`docker container exec`  :  Application 기반 container일 때 프로세스 실행 시키면서 접속 ( 자주 사용 )

nginx / node.js와 같은 곳에 접속할 때 사용.

![Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2021.png](Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2021.png)

**nginx 기반 filesystem (/bin/bash)에 실행한 것.**

- `cat /etc/hosts`
- `curl localhost`
- `curl 172.17.0.2`

![Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2022.png](Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2022.png)

`docker container top` :  컨테이너 내부 프로세스 정보

`docker container logs` :  표준 출력 결과

- `docker logs web`

![Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2023.png](Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2023.png)

- **-f 옵션 : 실시간**
- —tail 10  :  뒤 부터 10개 보여준다.

`docker container rename` :  container 이름 변경

![Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2024.png](Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2024.png)

`docker container cp` : container ↔ local 양방향 데이터 복사

`**docker container cp <원본경로> <대상경로>**`

- nginx에 있는 index.html를 local로 복사.
    
    `docker container cp webserver:/usr/share/nginx/html/index.html .`
    
    ![Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2025.png](Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2025.png)
    
- host에 있는 file을 container로 복사.
    
    `docker cp index2.html webserver:/usr/share/nginx/html/`
    
    **확인**
    
    ![Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2026.png](Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2026.png)
    

### /bin/bash  vs  bash 차이

/bin/bash : 절대경로에 있는 bash 실행 후 접속.

bash : PATH에 있기 때문에 사용해서 접속.

**즉, 환경변수 또한 도커 파일을 정의할 때 고려해주어야 할 수 있음.**

`docker container diff`  :  container 기동 이후  파일 변경 이력

![Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2027.png](Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2027.png)

## 컨테이너 이미지 생성

- `docker container commit` : 컨테이너 이미지 생성
- `docker container export -o file.tar`  :  (자주 안씀) 컨테이너를 Tar 파일로 저장.
- `docker image import file.tar newimage:tag`  :  (자주 안씀) Tar 파일에서 이미지 생성.
- `docker image save -o file.tar`  : **(자주 사용)**  **이미지를 tar파일로 저장.**
- `docker image load -l file.tar`  : **(자주 사용)  Tar 파일의 이미지를 로딩**

실무 중 (금융권)은 4, 5번 후 ftp로 파일 전송.  ( 정해진 포트만 사용해야 하기 때문에 ftp 포트만 사용하기 위해서 )

- ex) `docker pull busybox`  :  이미지 가져오기
    
    ![Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2028.png](Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2028.png)
    
    `docker run busybox mkdir /home/test`
    
    busybox 이미지 실행 후 디렉토리 만들고 꺼짐.
    
    **이미지 저장하기**
    
    - docker commit
    
    ![Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2029.png](Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2029.png)
    
    표준 쉘로 실행해보기
    
    - docker run -it —name b2 busybox_modified /bin/sh
    
    ![Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2030.png](Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2030.png)
    
    → /home/test 가 생긴 이미지라는 것을 알 수 있음.
    

### 이미지의 레이어 구조 보기

- **`docker history ubuntu`**

![Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2031.png](Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2031.png)

도커 기반으로 앱을 배포 하면

1. 첫 배포 이후 → 캐싱 처리가 되어서 
⇒ 새롭게 변경된 애플리케이션  (위쪽 레이어)만 변경되서 배포가 됨.

### 모든 컨테이너 지우기

`docker rm -f $(docker ps -aq)`

한 개씩 모든 컨테이너 강제로 삭제

![Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2032.png](Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2032.png)

### 컨테이너 생성 후 이미지로 export

- docker run -it —name c2 ubuntu:latest
- docker export c2 > /tmp/c2.tar

![Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2033.png](Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2033.png)

**import 할 때 이름을 붙일 수 있다.**

![Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2034.png](Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2034.png)

### 모든 이미지 지우기

`docker rmi -f $(docker images -aq)`

![Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2035.png](Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2035.png)

새로 받은 이미지

`docker pull ubuntu:latest`

레이어를 3개 받았는데 

`docker image history ubuntu`

확인해보면 5개다.

⇒ 전부 물리적인 이미지를 만드는 것은 아니기 때문.

### 이미지 식별하기

함정) : 내가 사용하는 도커 이미지에 대한 버전 (TAG로 알 수 있음)을 확실히 알고 있어야 함.
default 가 latest 이기 때문에 다른 버전으로 변경될 수 있음

**→ latest 보다 특정 버전을 Tag 해서 쓰는 습관을 가져야함.**

`docker tag  []:v1  []:v2`

![Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2036.png](Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2036.png)

### 컨테이너를 계속 "독립적"으로 실행 시킬 수 있음.

계속 run 하면됨.

## 컨테이너로 구성한 서비스 실행

![Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2037.png](Docker%200c562acb37ff45c8a0994e48f7142311/Untitled%2037.png)

## Docker File

### ADD vs COPY

### CMD vs ENTRYPOINT

CMD : 

하나만 적용 가능하고, 여러 개 입력 시 마지막 것으로 적용.

컨테이너 동작시 다른 명령 전환.

ENTRYPOINT : 

docker run에서 전환 불가.

CMD와 함께 사용 시  ENTRYPOINT가 기본 명령어, CMD는 인수 적용.