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
