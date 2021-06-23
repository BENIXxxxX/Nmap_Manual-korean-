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
대상 사양
    nmap 명령줄에서 옵션(또는 옵션 인수)이 아닌 모든 항목은 대상 호스트 사양으로 처리됩니다.
    가장 간단한 경우는 검색할 대상 IP 주소 또는 호스트 이름을 지정하는 것입니다.

    호스트 이름이 대상으로 지정되면 DNS(Domain Name System)를 통해 확인할 IP 주소를 결정합니다.
    만약 이름이 두 개 이상의 IP 주소로 확인되면 첫 번째 IP 주소만 검색됩니다.
    nmap에서 첫 번째 주소만 검사하지 않고 모든 확인된 주소를 검사하도록 하려면 --resolve-all 옵션을 사용합니다.

    때로는 인접한 호스트의 전체 네트워크를 검색하려고 합니다.
    이를 위해 nmap은 CIDR 스타일 주소 지정을 지원합니다.
    IP 주소 또는 호스트 이름에 /numbits를 추가할 수 있으며 nmap은 제공된 참조 IP 또는 호스트 이름과 첫 번째 numbits가 동일한 모든 IP 주소를 검색합니다.
    
    예를들어, 192.168.10.0/24는 192.168.10.0(binary:11000000 10101000 00001010 00000000)과 192.168.10.255(binary:11000000 10101000 00001010 11111111)사이의 256개 호스트를 검색합니다.
    192.168.10.40/24는 정확히 동일한 대상을 검색합니다.

    scanme.nmap.org 호스트가 IP 주소 64.13.134.52에 있는 경우 scanme.nmap.org/16 사양은 64.13.0.0에서 64.13.255.255.사이의 65,536개의 IP 주소를 검색합니다.
    허용된 최소값은 /0으로 전체 인터넷을 대상으로 합니다.

    IPv4의 가장 큰 값은 /32 이며, 모든 주소 비트가 고정되어 있기 때문에 명명된 호스트 또는 IP 주소만 검색합니다.
    IPv6의 가장 큰 값은 /128 이며 동일한 작업을 수행합니다.

    CIDR 표기법은 짧지만 항상 충분히 유연하지는 않다.
    예를 들어, 192.168.0.0/16을 검색하지만 서브넷 네트워크 및 브로드캐스트 주소로 사용될 수 있으므로 .0 또는 .255로 끝나는 모든 IP는 건너뛸 수 있습니다.
    Nmap은 옥텟 범위 주소 지정을 통해 이를 지원합니다.
    일반 IP 주소를 지정하는 대신 각 옥텟에 대해 쉼표로 구분된 숫자 또는 범위 목록을 지정할 수 있습니다.
    예를 들어, 192.168.0-255.1-254는 .0 또는 .255로 끝나는 범위의 모든 주소를 건너뛰고 192.168.3-5,7.1은 4개의 주소 192.168.3.1, 192.168.4.1 및 192.168.7.1을 검색합니다.
    범위의 어느 한쪽은 생략할 수 있다;
    기본값은 왼쪽에 0, 오른쪽에 255입니다.
    사용 자체도 0-255와 동일하지만, 대상 사양이 명령줄 옵션처럼 보이지 않도록 첫 번째 옥텟에서는 0-을 사용해야 합니다.
    범위는 최종 옥텟으로 제한될 필요가 없습니다. 지정자 0-255.0-255.13.37은 13.37로 끝나는 모든 IP 주소에 대해 인터넷 전체 검색을 수행합니다.
    이러한 종류의 광범위한 샘플링은 인터넷 설문 조사 및 조사에 유용할 수 있습니다.

    IPv6 주소는 정규화 된 IPv6 주소 또는 호스트 이름 또는 서브넷에 대한 CIDR 표기법으로 지정할 수 있습니다.
    8진수 범위는 아직 IPv6에서 지원되지 않습니다.

    비전역 범위의 IPv6 주소에는 영역 IP 접미사가 있어야 합니다.
    UNIX 시스템에서 이것은 퍼센트 기호와 인터페이스 이름 입니다.
    완전한 주소는 fe80::a8bb:ccff:fed:eff%eth0 일 수 있습니다.
    Windows에서는 인터페이스 이름 대신 인터페이스 색인 번호를 사용하십시오.
    fe80::a8bb:ccff:fed:eff%1.
    netsh.exe interface ipv6 show interface 명령을 실행하여 인터페이스 인덱스 목록을 볼 수 있습니다.

    namp은 명령줄에서 여러 호스트 사양을 허용하며 동일한 유형일 필요는 없습니다.
    nmap scanme.nmap.org 192.168.0.0/8 10.0.0,1,3-7.- 명령은 예상대로 수행합니다.

    대상은 일반적으로 명령줄에 지정되지만 다음 옵션을 사용하여 대상 선택을 제어 할 수도 있습니다.

    -iL inputfilename(목록에서 입력)
        inputfilename에서 대상 스펙을 읽습니다.
        방대한 호스트 목록을 전달하는 것은 종종 명령줄에서 어색하지만 일반적인 욕구입니다.
        예를 들어, DHCP 서버는 스캔하려는 10,000개의 현재 임대 목록을 내보낼 수 있습니다.
        또는 인증되지 않은 고정 IP 주소를 제외한 모든 IP 주소를 검색 할 수 있습니다.
        스캔 할 호스트 목록을 생성하고 해당 파일 이름을 -iL 옵션에 대한 인수로 nmap에 전달하기만 하면됩니다.
        항목은 명령줄에서 nmap이 허용하는 모든 형식(IP 주소, 호스트 이름, CIDR, IPv6 또는 옥텟 범위) 일 수 있습니다.
        각 항목은 하나 이상의 공백, 탭 또는 줄 바꿈으로 구분되어야합니다.
        nmap이 실제 파일이 아닌 표준 입력에서 호스트를 읽도록하려면 파일 이름으로 하이픈(-)을 지정할 수 있습니다.

        입력 파일에는 #으로 시작하고 줄 끝까지 확장되는 주석이 포함될 수 있습니다.

    -iR 호스트 수(임의 대상 선택)
        인터넷 전반에 걸친 설문 조사 및 기타 연구의 경우 대상을 무작위로 선택할 수 있습니다.
        num hosts 인수는 생성 할 IP 수를 nmap에 알려줍니다.
        특정 개인, 멀티 캐스트 또는 할당되지 않은 주소 범위에있는 것과 같이 바람직하지 않은 IP는 자동으로 건너 뜁니다.
        끝없는 스캔을 위해 인수 0을 지정할 수 있습니다.
        일부 네트워크 관리자는 자사 네트워크에 대한 무단 스캔에 불만을 표출 할 수 있습니다.
        이 옵션은 자신의 책임하에 사용하십시오! 비오는 어느 날 오후에 정말 지루하다면 nmap -Pn -sS -p 80 -iR 0 --open 명령을 사용하여 검색 할 임의의 웹 서버를 찾으십시오.

    --exclude host1[, host2 [,...]] (호스트/네트워크 제외)
        지정한 전체 네트워크 범위의 일부인 경우에도 스캔에서 제외 할 쉼표로 구분 된 대상 목록을 지정합니다.
        전달하는 목록은 일반 nmap 구문을 사용하므로 호스트 이름, CIDR 넷 블록, 옥텟 범위 등을 포함 할 수 있습니다.
        이는 스캔하려는 네트워크에 손댈 수 없는 미션 크리티컬 서버, 포트 스캔에 불리하게 반응하는 것으로 알려진 시스템 또는 다른 사람이 관리하는 서브넷이 포함 된 경우 유용할 수 있습니다.

    --excludefile exclude_file(파일에서 목록 제외)
        제외 된 대상이 명령줄이 아닌 줄 바꿈, 공백 또는 탭으로 구분 된 exclude_file로 제공된다는 점을 제외하면 --exclude 옵션과 동일한 기능을 제공합니다.

        제외 파일에는 #으로 시작하고 행 끝까지 확장되는 주석이 포함될 수 있습니다.
    
호스트 검색
    네트워크 정찰 임무의 첫 번째 단계 중 하나는 (때로는 거대한) IP 범위 집합을 활성 또는 관심 호스트 목록으로 줄이는 것입니다.
    모든 단일 IP 주소의 모든 포트를 검색하는 것은 느리고 일반적으로 불필요합니다.
    물론 호스트를 흥미롭게 만드는 것은 스캔 목적에 따라 크게 달라집니다.
    네트워크 관리자는 특정 서비스를 실행하는 호스트웨만 관심이 있을 수 있지만 보안 감사자는 IP 주소가 있는 모든 단일 장치에 관심을 가질 수 있습니다.
    관리자는 내부 네트워크에서 호스트를 찾기 위해 ICMP 핑만 사용하는 것이 편할 수 있지만 외부 침투 테스터는 방화벽 제한을 회피하기 위해 다양한 프로브 세트를 사용할 수 있습니다.

    호스트 검색 요구 사항이 매우 다양하기 때문에 nmap은 사용되는 기술을 사용자 정의 하기 위한 다양한 옵션을 제공합니다.
    호스트 검색은 ping 스캔이라고도 하지만 유비쿼터스 핑 도구와 관련된 간단한 ICMP 에코 요청 패킷을 훨씬 뛰어 넘습니다.
    사용자는 목록 검색 (-sL)을 사용하거나 호스트 검색 (-Pn)을 비활성화하여 검색 단계를 완전히 건너 뛰거나 다중 포트 TCP SYN/ACK, UDP, SCTP INIT 및 ICMP 프로브의 임의 조합으로 네트워크에 연결할 수 있습니다.
    이러한 프로브의 목표는 IP 주소가 실제로 활성화되어 있음 (호스트 또는 네트워크 장치에서 사용중임)을 보여주는 응답을 요청하는 것입니다.
    많은 네트워크에서 주어진 시간에 활성화되는 IP 주소의 비율은 적습니다.
    이것은 10.0.0.0/8과 같은 개인 주소 공간에서 특히 일반적입니다.
    이 네트워크에는 1,600만개의 IP가 있지만 1,000대 미만의 컴퓨터를 사용하는 회사에서 사용하는 것을 보았습니다.
    호스트 검색은 드물게 할당 된 IP 주소 범위에서 이러한 시스템을 찾을 수 있습니다.

    호스트 검색 옵션이 제공되지 않으면 nmap은 ICMP 에코 요청, TCP SYN 패킷을 포트 443으로, TCP ACK 패킷을 포트 80으로, ICMP 타임 스탬프 요청을 보냅니다.
    (IPv6의 경우 ICMPv6의 일부가 아니므로 ICMP 타임 스탬프 요청이 생략됩니다.)
    이러한 기본값은 -PE -PS443 -PA80 -PP 옵션과 동일합니다. 이에 대한 예외는 로컬 이더넷 네트워크의 모든 대상에 사용되는 ARP(IPv4 용) 및 Neighbor Discovery (IPv6용) 스캔입니다.
    권한이 없는 unix 쉘 사용자의 경우 기본 프로브는 연결 시스템 호출을 사용하는 포트 80 및 443에 대한 SYN 패킷입니다.
    이 호스트 검색은 로컬 네트워크를 검색 할 때 종종 충분하지만 보안 감사에는 보다 포괄적인 검색 프로브 집합이 권장됩니다.

    -P* 옵션(핑 유형 선택)을 결합 할 수 있습니다.
    서로 다른 TCP 포트/플래그 및 ICMP 코드를 사용하여 여러 프로브 유형을 전송하여 엄격한 방화벽을 통과 할 확률을 높일 수 있습니다.
    또한 ARP/neighbor discovery는 다른 -P* 옵션을 지정한 경우에도 로컬 이더넷 네트워크의 대상에 대해 기본적으로 수행됩니다. 거의 항상 더 빠르고 효과적이기 때문입니다.

    기본적으로 nmap은 호스트 검색을 수행 한 다음 온라인 상태인 각 호스트에 대해 포트 스캔을 수행합니다.
    UDP 프로브(-PU)와 같은 기본이 아닌 호스트 검색 유형을 지정하는 경우에도 마찬가지입니다.
    -sn 옵션을 읽고 호스트 검색만 수행하는 방법을 알아 보거나 -Pn을 사용하여 호스트 검색을 건너뛰고 모든 대상 주소를 포트 검색합니다.
    다음 옵션은 호스트 검색을 제어합니다:

    -sL(목록 스캔)
        목록 스캔은 대상 호스트에 패킷을 보내지 않고 지정된 네트워크의 각 호스트를 단순히 나열하는 퇴화 된 형태의 호스트 검색입니다.
        간단한 호스트 이름이 얼마나 많은 유용한 정보를 제공하는지는 종종 놀랍습니다.
        예를 들어, fw.chi는 한 회사의 시카고 방화벽 이름입니다.

        nmap은 또한 끝에 총 IP 주소 수를 보고합니다.
        목록 스캔은 대상에 대한 적절한 IP 주소가 있는지 확인 하기 위한 좋은 온전성 검사입니다.
        호스트가 알지 못하는 도메인 이름을 사용하는 경우 잘못된 회사의 네트워크를 스캔하지 않도록 추가 조사를 할 가치가 있습니다.

        아이디어는 단순히 대상 호스트 목록을 인쇄하는 것이므로 포트 스캔, OS 탐지 또는 호스트 검색과 같은 고급 기능에 대한 옵션을 이 옵션과 결합 할 수 없습니다.
        더 높은 수준의 기능을 수행하면서 호스트 검색을 비활성화 하려면 -Pn(호스트 검색 건너 뛰기) 옵션을 읽어보십시오.

    -sn (포트 스캔 없음)
        이 옵션은 nmap에게 호스트 검색 후 포트 검색을 수행하지 않고 호스트 검색 프로브에 응답한 사용 가능한 호스트만 출력하도록 지시합니다.
        이를 종종 "ping 스캔" 이라고 하지만 traceroute 및 NSE 호스트 스크립트가 실행되도록 요청할 수도 있습니다.
        이것은 기본적으로 목록 스캔 보다 한 단계 더 방해가 되며 종종 동일한 목적으로 사용될 수 있습니다.
        너무 많은 주의을 끌지 않고 대상 네트워크의 경미한 정찰을 허용합니다.
        공격자의 경우 활성화 된 호스트 수를 아는 것이 각 IP 및 호스트 이름의 목록 스캔에서 제공하는 목록 보다 더 중요합니다.

        시스템 관리자는 종종 이 옵션이 유용하다고 생각합니다.
        네트워크에서 사용 가능한 시스템의 가용성을 계산하거나 서버의 가용성을 모니터링하는 데 쉽게 사용할 수 있습니다.
        이것은 일반적으로 ping 스캐닝이라고 하며 많은 호스트가 브로드 캐스트 쿼리에 응답하지 않기 때문에 ping 브로드 캐스트 주소 보다 더 안정적입니다.

        기본적으로 -sn 으로 수행되는 기본 호스트 검색에는 ICMP 에코 요청, TCP SYN에서 포트 443으로, TCP ACK에서 포트 80으로, ICMP 타임 스탬프 요청이 기본적으로 포함됩니다.
        권한이 없는 사용자가 실행하면 SYN 패킷만 연결 호출을 사용하여 대상의 포트 80 및 443으로 전송됩니다.
        권한이 있는 사용자가 로컬 이더넷 네트워크에서 대상을 스캔하려고 할 때 --send-ip가 지정되지 않으면 ARP 요청이 사용됩니다.
        -sn 옵션은 유연성을 높이기위해 모든 감지 프로브 유형(-P* 옵션)과 결합 될 수 있습니다.
        이러한 프로브 유형 및 포트 번호 옵션을 사용하는 경우 기본 프로브를 덮어 씁니다.
        이러한 고급 기술은 소스 호스트와 nmap을 실행하는 대상 네트워크 사이에 엄격한 방화벽이 있을 때 권장됩니다.
        그렇지 않으면 방화벽이 프로브 또는 응답을 삭제하면 호스트가 손실 될 수 있습니다.
        이전 버전의 nmap에서는 -sn을 -sP라고 했습니다.

    -Pn (핑 없음)
        이 옵션은 호스트 검색 단계를 완전히 건너 뜁니다.
        일반적으로 nmap은 이 단계를 사용하여 무거운 스캔을 위한 활성 시스템을 식별하고 네트워크 속도를 측정합니다.
        기본적으로 nmap은 시작된 것으로 확인 된 호스트에서 포트 검색, 버전 검색 또는 운영 체제 검색과 같은 많은 검색만 수행합니다.
        -Pn을 사용하여 호스트 검색을 비활성화하면 nmap이 지정된 각 대상 IP 주소에 대해 요청 된 스캔 기능을 시도합니다.
        따라서 명령 줄에 / 16 크기 네트워크를 지정하면 65,536개의 IP 주소가 모두 검색됩니다.
        목록 검색과 마찬가지로 올바른 호스트 검색을 건너 뛰지만 nmap은 대상 목록을 중지하고 인쇄하지 않고 각 대상 IP가 활성화 된 것처럼 요청 된 기능을 계속 수행합니다.
        기본 타이밍 매개 변수를 사용하면 스캔 속도가 느려질 수 있습니다.
        NSE 실행을 허용하면서 호스트 검색 및 포트 검색을 건너 뛰려면 -Pn -sn 두 옵션을 함께 사용하십시오.

        로컬 이더넷 네트워크에 있는 머신의 경우 NMAP이 대상 호스트를 추가로 스캔하기 위해 MAC 주소가 필요하기 때문에 ARP 스캔은 계속 수행됩니다(--disable-arp-ping 또는 --send-ip가 지정되지 않은 경우)
        이전 버전의 nmap에서 -Pn은 -P0 및 -PN 이었습니다.

    -PS 포트 목록 (TCP SYN Ping)
        이 옵션은 SYN 플래그가 설정된 빈 TCP 패킷을 보냅니다.
        기본 대상 포트는 80 입니다(컴파일시 nmap.h에서 DEFAULT_TCP_PROBE_PORT_SPEC을 변경하여 구성 가능).
        매개 변수로 대체 포트를 지정 할 수 있습니다.
        T: 와 같은 포트 유형 지정자는 허용되지 않는다는 점을 제외하고 구문은 -p의 구문과 동일합니다.
        예: -PS22 및 -PS22-25,80,113,1050,35000.
        -PS와 포트 목록 사이에는 공백이 없어야합니다.
        여러 프로브가 지정된 경우 병렬로 전송됩니다.

        SYN 플래그는 연결을 설정하려는 원격 시스템을 제안합니다.
        일반적으로 대상 포트는 닫히고 RST(재설정) 패킷이 다시 전송됩니다.
        포트가 열리면 대상은 SYN/ACK TCP 패킷으로 응답하여 TCP 3웨이 핸드 셰이크의 두 번째 단계를 수행합니다.
        그런 다음 NMAP을 실행하는 시스템은 ACK 패킷을 보내는 대신 RST에 응답하여 새 연결을 끊습니다. 그러면 3웨이 핸드 셰이크가 완료되고 완전한 연결이 설정됩니다.
        RST 패킷은 nmap 자체가 아니라 예상치 못한 SYN/ACK에 대한 응답으로 nmap을 실행하는 시스템의 커널에 의해 전송됩니다.

        nmap은 포트가 열려 있는지 닫혀 있는지 상관하지 않습니다.
        앞에서 설명한 RST 또는 SYN/ACK 응답은 호스트가 사용 가능하고 응답한다는 것을 nmap에 알려줍니다.

        unix 시스템에서는 일반적으로 권한이 있는 사용자 루트만 원시 TCP 패킷을 보내고 받을 수 있습니다.
        권한이 없는 사용자의 경우 각 대상 포트에 대한 연결 시스템 호출을 시작하는 해결 방법이 자동으로 채택됩니다.
        이것은 연결을 설정하려는 시도에서 SYN 패킷을 대상 호스트에 보내는 효과가 있습니다.
        연결이 빠르게 성공하거나 ECONNREFUSED가 반환되지 않으면 기본 TCP 스택이 SYN/ACK 또는 RST를 수신 했어야하며 호스트를 사용 가능한 것으로 표시해야합니다.
        제한 시간에 도달 할 때까지 연결 시도가 중단되면 호스트가 닫힌 것으로 표시됩니다.
        
    -PA 포트 목록 (TCP ACK Ping)
        TCP ACK 핑은 방금 설명한 SYN 핑과 매우 유사합니다.
        짐작할 수 있듯이 차이점은 SYN 플래그 대신 TCP ACK 플래그가 설정된다는 것 입니다.
        이러한 ACK 패킷은 설정된 TCP 연결을 통해 데이터를 확인한다고 주장하지만 그러한 연결은 없습니다.
        따라서 원격 호스트는 항상 RST 패킷에 응답하고 프로세스에 존재하는 것을 공개해야 합니다.
        
        -PA 옵션은 SYN 프로브 (80)와 동일한 기본 포트를 사용하며 대상 포트 목록의 동일한 형식을 사용할 수도 있습니다.
        권한이 없는 사용자가 이 작업을 시도하는 경우 앞에서 설명한 연결 솔루션을 사용하십시오.
        connect가 실제로 ACK 대신 SYN 패킷을 보내기 때문에 이 솔루션은 완벽하지 않습니다.

        SYN 및 ACK ping 탐지를 제공하는 이유는 방화벽을 우회 할 가능성을 최대화 하기 위한 것입니다.
        많은 관리자가 회사 웹 사이트 또는 메일 서버와 같은 공용 서비스로 전송되는 패킷을 제외하고 들어오는 SYN 패킷을 차단하도록 라우터 및 기타 간단한 방화벽을 구성합니다.
        이렇게 하면 조직에 대한 다른 들어오는 연결을 방지하는 동시에 사용자가 방해 받지 않고 인터넷에 나가는 연결을 설정 할 수 있습니다.
        이 상태 비 저장 방법은 방화벽/라우터에서 리소스를 거의 차지하지 않으며 하드웨어 및 소프트웨어 필터에서 널리 지원됩니다.
        Linux Netfilter/iptables 방화벽 소프트웨어는 이 상태 비 저장 방법을 수현하기 위해 --syn 편의 옵션을 제공합니다.
        이와 같은 상태 비 저장 방화벽 규칙이 있는 경우 SYN 핑 프로브 (-PS)는 닫힌 대상 포트로 전송 될 때 차단 될 수 있습니다.
        이 경우 이러한 규칙이 직접 전달되면 ACK 감지가 작동합니다.

        또 다른 일반적인 유형의 방화벽은 예기치 않은 패킷을 삭제하는 상태 저장 규칙을 사용합니다.
        이 기능은 원래 주로 고급 방화벽에서 발견되었지만 수년에 걸쳐 점점 더 보편화 되었습니다.
        Linux Netfilter/iptables 시스템은 연결 상태에 따라 패킷을 분류하는 --state 옵션을 통해 이를 지원합니다.
        예상치 못한 ACK 패킷은 일반적으로 위조 및 폐기되는 것으로 간주되기 때문에 SYN 감지는 이러한 시스템에서 작동 할 가능성이 더 높습니다.
        이 딜레마에 대한 해결책은 -PS 및 -PA 를 지정하여 SYN 및 ACK 프로브를 보내는 것 입니다.

    -PU port list (UDP ping)
        또 다른 호스트 검색 옵션은 UDP 패킷을 지정된 포트로 보내는 UDP ping 입니다.
        대부분의 포트에서 데이터 패킷은 비어있지만 일부는 응답을 유발할 가능성이 더 높은 프로토콜별 페이로드를 사용합니다.
        페이로드 데이터베이스는 https://nmap.org/book/nmap-payload.html 에 설명되어 있습니다.

        패킷 내용은 --data, --data-string 및 --data-length 옵션의 영향을 받을 수도 있습니다.

        포트 목록은 앞에서 설명한 -PS 및 -PA 옵션과 동일한 형식을 사용합니다.
        포트가 지정되지 않은 경우 기본값은 40125입니다.
        이 기본값은 컴파일 타임에 nmap.hdml DEFAULT_UDP_PROBE_PORT_SPEC 을 변경하여 구성 할 수 있습니다.
        이 특정 유형의 스캔의 경우 일반적으로 열린 포트로 전송하지 않기 때문에 매우 특이한 포트가 기본적으로 사용됩니다.

        대상 컴퓨터에서 닫힌 포트에 도달하면 UDP 감지는 ICMP 포트에 연결할 수 없는 패킷을 반환해야 합니다.
        이것은 nmap에 기계가 가동되고 사용 가능함을 나타냅니다.
        호스트/네트워크 액세스 불가능 또는 TTL 초과와 같은 다른 많은 유형의 ICMP 오류는 호스트가 다운되었거나 액세스 할 수 없음을 나타냅니다.
        응답의 부족도 이런 식으로 설명 할 수 있습니다.
        열린 포트에 도달하면 대부분의 서비스는 빈 패킷을 무시하고 응답을 반환하지 않습니다.
        이것이 기본 검색 포트가 40125이며 사용 가능성이 거의 없는 이유입니다.
        문자 생성기(유료) 프로토콜과 같은 일부 서비스는 빈 UDP 패킷으로 응답하여 컴퓨터를 사용할 수 있음을 nmap에 공개합니다.

        이 검색 유형의 주요 장점은 TCP만 차단하는 방화벽 및 필터를 우회한다는 것 입니다.
        예를 들어, 저는 Linksys BEFW11S4 무선 광대역 라우터를 소유했습니다.
        기본적으로 이 장치의 외부 인터페이스는 모든 TCP 포트를 필터링하지만 UDP 감지는 여전히 포트에 연결할 수 없는 메시지를 발생시켜 장치가 누출됩니다.
    
    -PY port list (SCTP INIT Ping)
        이 옵션은 가장 작은 INIT 블록을 포함하는 SCTP 패킷을 보냅니다.
        기본 대상 포트는 80입니다.(컴파일 할 때 nmap.h에서 DEFAULT_SCTP_PROBE_PORT_SPEC을 변경하여 구성 할 수 있음)
        매개 변수로 대체 포트를 지정 할 수 있습니다.
        구문은 S: 와 같은 포트 유형 지정자가 허용되지 않는다는 점을 제외하면 -p와 동일합니다.
        예는 -PY22 및 -PY22,80,179,5060 입니다.
        -PY와 포트 목록 사이에는 공백이 없어야 합니다.
        여러 프로브가 지정된 경우 병렬로 전송됩니다.

        INIT 블록은 연결을 설정하려는 원격 시스템을 제안합니다.
        일반적으로 대상 포트가 닫히고 ABORT 블록이 다시 전송됩니다.
        포트가 열리면 대상은 INIT-ACK 블록에 응답하여 SCTP 4 웨이 핸드 셰이크의 두 번째 단계를 수행합니다.
        nmap을 실행하는 머신에 기능적인 SCTP 스택이 있는 경우 4 웨이 핸드 셰이크의 다음 단계가 될 COOKIE-ECHO 블록을 보내는 대신 ABORT 블록에 응답하여 새 연결을 끊습니다.
        ABORT 패킷은 nmap 자체가 아닌 예상치 못한 INIT-ACK에 대한 응답으로 nmap을 실행하는 시스템의 커널에 의해 전송됩니다.

        nmap은 포트가 열려 있는지 닫혀 있는지 상관하지 않습니다.
        앞서 논의한 ABORT 또는 INIT-ACK 응답은 nmap 호스트에 사용 가능하고 응답한다는 것을 알려줍니다.

        Unix 시스템에서는 일반적으로 권한이 있는 사용자 루트만 원시 SCTP 패킷을 보내고 받을 수 있습니다.
        권한이 없는 사용자는 현재 SCTP INIT Ping을 사용할 수 없습니다.

    -PE; -PP; -PM (ICMP Ping Types)
        앞서 설명한 비정상적인 TCP, UDP 및 SCTP 호스트 검색 유형 외에도 nmap은 유비쿼터스 핑 프로그램에서 보낸 표준 패킷을 보낼 수도 있습니다.
        nmap은 ICMP 유형 8 (에코 요청) 패킷을 대상 IP 주소로 전송하여 사용 가능한 호스트에서 유형 0 (에코 응답)을 반환 할 것으로 예상합니다.
        불행히도 웹 브라우저의 경우 많은 호스트와 방화벽이 RFC 1122 [2]에서 요구하는대로 응답하는 대신 이러한 패킷을 차단합니다.
        따라서 인터넷에서 알 수 없는 대상의 경우 ICMP 검색만 신뢰할 수 있는 경우는 거의 없습니다.
        그러나 내부 네트워크를 모니터링 하는 시스템 관리자에게는 실용적이고 효과적인 방법이 될 수 있습니다.
        이 에코 요청 동작을 활성화 하려면 -PE 옵션을 사용하십시오.

        에코 요청은 표준 ICMP 핑 쿼리이지만 nmap은 여기서 멈추지 않습니다.
        ICMP 표준(RFC 792 [3] 및 RFC 950 [4])은 또한 타임 스탬프 요청, 정보 요청 및 주소 마스크 요청 패킷을 각각 코드 13, 15 및 17로 지정합니다.
        이러한 쿼리의 명백한 목적은 주소 마스크 및 현재 시간과 같은 정보를 이해하는 것이지만 호스트 검색에 쉽게 사용할 수 있습니다.
        응답 시스템이 작동 중이며 사용 가능합니다.
        nmap은 현재 널리 지원되지 않는 정보 요청 패키지를 구현하지 않습니다.
        RFC 1122는 "호스트가 이러한 메시지를 구현해서는 안됩니다" 라고 주장합니다.
        -PP 및 -PM 옵션을 사용하여 각각 메일 및 주소 마스크 쿼리를 보낼 수 있습니다.
        타임 스탬프 응답(ICMP 코드 14) 또는 주소 마스크 응답(코드 18)은 호스트를 사용할 수 있음을 나타냅니다.
        이 두 쿼리는 관리자가 특별히 에코 요청 패킷을 방지하고 다른 ICMP 쿼리를 동일한 목적으로 사용할 수 있다는 사실을 잊어 버린 경우 유용할 수 있습니다.

    