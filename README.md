Nmap-Manual(korean)
===================
Nmap Reference Guide
--------------------

이름
    nmap - 네트워크 탐색 도구 및 보안 / 포트스캐너
개요
    nmap [스캔 유형...] [옵션] {대상 사양}
기술
    Nmap ( "Network Mapper")은 네트워크 탐색 및 보안 감사를 위한 오픈 소스 도구입니다.
    대규모 네트워크를 빠르게 스캔하도록 설계되었으며 단일 호스트에 대해 잘 작동하지만,
    네트워크에서 사용할 수 있는 호스트를 결정하는 새로운 방법으로 nmap은 raw IP 패킷을 사용합니다.
    해당 호스트가 제공하는 서비스 ( 어플리케이션 이름 및 버전), 실행중인 운영체제 ( OS 및 버전),
    사용중인 패킷 필터 / 방화벽 유형 및 기타 수십 가지 특성.
    
    nmap은 일반적으로 보안 감사에 사용되지만, 많은 시스템 및 네트워크 관리자는
    네트워크 인벤토리, 서비스 업그레이드 일정 관리, 호스트 또는 서비스 가동 시간 모니터링 같은 일상적인 작업에 유용하다고 생각한다.

    nmap의 출력은 스캔 된 대상 목록과 같이 사용 된 옵션에 따라 각각에 대한 정보를 출력한다.
    그 중 핵심 정보는 "흥미로운 포트 테이블" 입니다.
    그 표에는 포트 번호 및 프로토콜, 서비스 이름 및 상태를 나타낸다.
    
    상태는 open, filterd, closed 또는 not filterd 이 있다.
    
    open 은 애플리케이션이 대상 컴퓨터에서 해당 포트에서 연결 / 패킷을 수신합니다.
    
    filterd 은 방화벽, 필터 또는 기타 네트워크를 의미합니다. 장애물이 포트를 차단하여 nmap이 포트가 열려있는지 닫혀있는지 알 수 없다.
    
    closed 포트는 언제든지 열 수 있지만, 해당 포트에서 수신되는 응용 프로그램이 없습니다. 
    
    포트는 다음과 같이 분류됩니다.
    nmap의 프로브에 응답하는 경우는 필터링되지 않지만 nmap은 포트가 열려 있는지 닫혀 있는지여부를 판별합니다.
    
    nmap은 상태를 보고합니다.
    open | filterd 그리고 closed | filtered 결정 할 수 없을 때 두 상태 중 포트를 설명하는 상태입니다.

    포트 테이블은 버전 검출 시 소프트웨어 상세 버전을 포함하여 요청을 한다.
    IP 프로토콜 검색이 요청되면(-sO), nmap에서 제공하는 수신 포트 대신 지원되는 IP 프로토콜에 대한 정보를 제공합니다.

    nmap은 흥미로운 포트 테이블 외에도 추가 정보를 제공할 수 있습니다.
    리버스 DNS 이름, 운영 체제를 포함한 대상에 대한 정보 추측, 장치 유형 및 MAC 주소를 입력합니다.

    일반적인 nmap 스캔은 예제 1에 나와 있습니다.
    이 예에서는 사용된 유일한 nmap 인수는 -A, OS 및 버전 탐지를 활성화하는 스크립트, 검색 및 traceroute; -T4를 사용하면 고속 실행이 가능해지고, 호스트명을 지정합니다.

    예제 1. 대표적인 nmap 스캔
        # nmap -A -T4 scanme.nmap.org

        Nmap scan report for scanme.nmap.org (74.207.244.221)
        Host is up (0.029s latency).
        rDNS record for 74.207.244.221: li86-221.members.linode.com
        Not shown: 995 closed ports
        PORT     STATE    SERVICE     VERSION
        22/tcp   open     ssh         OpenSSH 5.3p1 Debian 3ubuntu7 (protocol 2.0)
        | ssh-hostkey: 1024 8d:60:f1:7c:ca:b7:3d:0a:d6:67:54:9d:69:d9:b9:dd (DSA)
        |_2048 79:f8:09:ac:d4:e2:32:42:10:49:d3:bd:20:82:85:ec (RSA)
        80/tcp   open     http        Apache httpd 2.2.14 ((Ubuntu))
        |_http-title: Go ahead and ScanMe!
        646/tcp  filtered ldp
        1720/tcp filtered H.323/Q.931
        9929/tcp open     nping-echo  Nping echo
        Device type: general purpose
        Running: Linux 2.6.X
        OS CPE: cpe:/o:linux:linux_kernel:2.6.39
        OS details: Linux 2.6.39
        Network Distance: 11 hops
        Service Info: OS: Linux; CPE: cpe:/o:linux:kernel

        TRACEROUTE (using port 53/tcp)
        HOP RTT      ADDRESS
        [Cut first 10 hops for brevity]
        11  17.65 ms li86-221.members.linode.com (74.207.244.221)

        Nmap done: 1 IP address (1 host up) scanned in 14.40 seconds
    nmap의 최신 버전은 https://nmap.org 에서 구할 수 있다.
    man 페이지의 최신 버전은 다음에서 사용할 수 있습니다.
    https://nmap.org/book/man.html
    네트워크에 대한 nmap 공식 프로젝트 가이드 검색 및 보안 검색(https://nmap.org/book/)참조.

옵션 요약
    이 옵션 요약은 nmap이 인수 없이 실행될 때 인쇄됩니다.
    최신 버전은 항상 다음에서 제공됩니다.
    https://svn.nmap.org/nmap/docs/nmap.usage.txt
    그것은 사람들이 기억하도록 도와준다.
    가장 일반적인 옵션이지만 심층적인 옵션 대신 사용할 수는 없습니다.
    이 설명서의 나머지 부분에 있는 문서입니다.
    일부 불명확한 옵션은 그렇지 않습니다.
    여기에 포함되기도 합니다.

        Nmap 7.90 ( https://nmap.org )
        Usage: nmap [스캔 유형] [옵션] {대상 사양}
        대상 사양:
            호스트 이름, IP 주소, 네트워크 등을 전달할 수 있습니다.
            Ex: scanme.nmap.org, microsoft.com/24, 192.168.0.1; 10.0.0-255.1-254
            -iL <input filename>: 호스트/네트워크 목록에서 입력
            -iR <num hosts>: 랜덤 대상 선택
            --exclude <host1[,host2][,host3],...>: 호스트/네트워크 제외
            --excludefile <exclude_file>: 파일에서 목록 제외
        호스트 검색:
            -sL: 목록 검색 - 검색할 대상을 나열하기만 하면 됩니다.
            -sn: Ping Scan - 포트 스캔을 비활성화합니다.
            -Pn: 모든 호스트를 온라인으로 처리 - 호스트 검색을 건너뜁니다.
            -PS/PA/PU/PY[포트리스트]: 지정된 포트에 대한 TCP SYN/ACK, UDP 또는 SCTP 검색
            -PE/PP/PM: ICMP 에코, 타임스탬프 및 넷마스크 요청 검색 프로브
            -PO[프로토콜 목록]: IP 프로토콜 핑
            -n/-R: DNS 확인 안 함/항상 해결 [기본값: 때떄로]
            --https-servers <serv1[,serv2],...>: 사용자 지정 DNS 서버 지정
            --시스템 통합: OS의 DNS 확인기 사용
            --추적 경로: 각호수트에 대한 홉 경로 추적
        스캔 기법:
            -s/sT/sA/sW/sM: TCP SYN/Connect(/ACK/윈도우/Maimon) 스캔
            -sU: UDP 스캔
            -sN/sF/sX: TCP Null, FIN 및 Xmas 스캔
            --스캔 플래그 <br>: TCP 검색 플래그 사용자 정의
            -sl <좀비호스트[:probeport]>: 유휴 검색
            -sY/sZ : SCTP INIT/COOKIE-ECHO 스캔
            -sO: IP 프로토콜 검색
            -b <FTP 릴레이 호스트>: FTP 바운스 스캔
        포트 사양 및 스캔 순서:
            -p <포트 범위>: 지정된 포트만 검색
            Ex: -p22;-p1-65535; -p U:53,111,137,T:21-25,80,139,8080,S:9
            --exclude-ports <포트 범위>: 지정된 포트를 검색에서 제외합니다.
            -F: 빠른 모드 - 기본 검색보다 적은 수의 포트를 검색합니다.
            -r: 포트 연속 스캔 - 임의 추출하지 않음
            --top-ports <number>: 가장 일반적인 포트 검색<number>
            --port-ratio <ratio>: <ratio> 보다 일반적인 포트 검색
        서비스/버전 감지:
            -sV: 개방형 포트를 탐색하여 서비스/버전 정보 확인
            --version-density <level>: 0에서 9(모든 프로브 시도)로 설정
            --version-light: 가능성이 가장 높은 프로브에 대한 한계(강도 2)
            --version-all: 모든 프로브 시도(강도 9)
            --version-trace: 세부 버전 검색 작업 표시(디버그용)
        OS 탐지:
            -O: OS 검출 활성화
            --osscan-limit: OS 탐지를 유망한 대상으로 제한
            --osscan-filen: OS를 보다 적극적으로 추측합니다.
        타이밍 및 성능:
            [시간]이 걸리는 옵션은 초 단위이거나 'ms'(밀리초)를 추가합니다.
            값(예: 30m)에 대한 's'(초), 'm'(분) 또는 'h'(시간)입니다.
            -T<0-5>: 타이밍 템플릿 설정(높은 것이 더 빠름)
            --min-hostgroup/max-hostgroup <size>: 병렬 호스트 검색 그룹 크기
            --min-parallelism/max-parallelism <numprobe>: 프로브 병렬화
            --min-rt-timeout/max-rt-timeout/initial-rt-timeout <time>: 왕복 시간을 지정하다
            --max-retries <try>: 포트 스캔 프로브 재전송 횟수를 제한합니다.
            --host-timeout <time>: 프로브 간 지연 조정
            --min-rate <number>: 초당 <number> 보다 느린 패킷 전송
            --max-rate <number>: 초당 <number> 보다 빠른 패킷 전송
        방화벽/ID 회피 및 스푸핑:
            -f; --mtu <val>:패킷 조작(옵션으로 지정된 MTU 포함)
            -D <decoy1, decoy2, [,ME],...>: 디스켓으로 스캔 은폐
            -S ip: 스푸핑 소스 주소
            -e <iface>: 지정된 인터페이스 사용
            -g/--소스 포트 <portnum>: 지정된 포트 번호 사용
            --discies <url1,[url2],...>: HTTP/SOCK4 프록시를 통해 연결 중계
            --data <hex 문자열>: 보낸 패킷에 사용자 지정 페이로드 추가
            --데이터 문자열 <문자열>: 보낸 패킷에 사용자 지정 ASCII 문자열 추가
            --data-length <num>: 전송된 패킷에 임의 데이터 추가
            --ip-options <options>: 지정된 IP 옵션으로 패킷 전송
            --ttl <val>: IP 실시간 필드 설정
            --spoph-mac <mac address/prefix/vendor name>: MAC 주소 스푸핑
            --badsum: 가짜 TCP/UDP/SCTP 체크섬을 사용하여 패킷 전송
        출력:
            -onN/-oX/-oS/-oG <file>: 정규, XML, s|<rIpt kIddi3>의 출력 검색,
            지정된 파일 이름에 대해 각각 Grepable 형식과 Grepable 형식을 지정합니다.
            -oA <기본 이름>: 세 가지 주요 형식으로 동시에 출력
            -v: 다원성 수준 증가(더 큰 효과를 위해 -vv 이상을 사용)
            -d: 디버깅 수준 증가(더 큰 효과를 위해 -dd 이상 사용)
            --이유: 포트가 특정 상태에 있는 이유 표시
            --열림: 열린(또는 열려 있을 가능성이 있는) 포트만 표시
            --iflist: 호스트 인터페이스 및 경로 인쇄(디버그용)
            --추가 출력: 지정된 출력 파일에 추가하지 않고 추가
            --resume <파일 이름>: 중단 된 스캔 재개
            --stylesheet<path/URL>: XML 출력을 HTML로 변환하는 XSL 스타일 시트
            --webxml: portable XML을 위한 NMAP.ORG의 참조 스타일 시트
            --no-stylesheet: XML 출력과 XSL 스타일시트의 연관성 방지
        MISC:
            -6: IPv6 검색 사용
            -A: OS 탐지, 버전 탐지, 스크립트 검색 및 추적 경로 사용
            --datadir <dirname>: 사용자 지정 nmap 데이터 파일 위치 지정
            --send-eth/--send-ip: 로우 이더넷 프레임 또는 IP 패킷을 사용하여 전송
            --보통: 사용자에게 완전한 권한이 있다고 가정합니다.
            --권한 부여: 사용자에게 로우 소켓 권한이 없다고 가정합니다.
            -V: 버전 번호 출력
            -h: 도움말 요약 페이지를 출력
        Example:
            nmap -v -A scanme.nmap.org
            nmap -v -sn 192.168.0.0/16 10.0.0.0/8
            nmap -v -iR 10000 -Pn -p 80
            자세한 옵션 및 예는 MAN 페이지 (https://nmap.org/book/man.html)를 참조하십시오


            
