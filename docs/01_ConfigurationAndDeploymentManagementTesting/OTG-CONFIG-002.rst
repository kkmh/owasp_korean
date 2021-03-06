==========================================================================================
OTG-CONFIG-002 (어플리케이션 플랫폼 설정 테스트)
==========================================================================================

|

개요
==========================================================================================

애플리케이션 아키텍처를 구성하는 단일 요소의 올바른 구성은 전체 아키텍처의 보안을 손상시킬 수 있는 실수를 방지하는 데 중요합니다.
구성 검토 및 테스트는 아키텍처를 만들고 유지 관리하는 중요한 작업입니다.
많은 다른 시스템은 대개 그들이 설치되어 있는 특정 사이트에서 수행할 작업에 적합하지 않을 수도 있는 일반적인 구성을 제공하기 때문입니다.

일반적인 웹 및 응용 프로그램 서버 설치에는 응용 프로그램 예제, 문서, 테스트 페이지와 같은 많은 기능이 포함되지만 설치 전에 악용되지 않도록 배포 전에 제거해야합니다.

|

테스트 방법
==========================================================================================

|

Black Box Testing
-----------------------------------------------------------------------------------------

**샘플 및 알려진 파일 및 디렉토리**

대부분의 웹 서버 및 응용 프로그램 서버는 기본 설치에서 개발자의 이익을 위해 제공되는 샘플 응용 프로그램과 파일을 제공하고 설치 직 후 서버가 제대로 작동하는지 테스트합니다. 
그러나 많은 기본 웹 서버 응용 프로그램은 나중에 그 파일로 인해 취약한 것으로 알려져 있습니다. 
예를 들어, CVE-1999-0449 (Exair 샘플 사이트가 설치되었을 때 IIS에서 서비스 거부), CAN-2002-1744 (Microsoft IIS 5.0의 CodeBrws.asp에서 디렉터리 통과 취약점), CAN -2002-1630 (Oracle 9iAS에서 sendmail.jsp 사용) 또는 CAN-2003-1172 (Apache`s Cocoon의보기 소스 샘플에서 디렉토리 탐색)가 그것입니다.

CGI 스캐너에는 다양한 웹 또는 응용 프로그램 서버에서 제공하는 알려진 파일 및 디렉토리 샘플의 세부 목록이 포함되어 있으며 이러한 파일이 있는지를 빠르게 확인할 수 있습니다. 
그러나 실제로 확실한 방법은 웹 서버 또는 응용 프로그램 서버의 내용을 전체적으로 검토하고 응용 프로그램 자체와 관련이 있는지 여부를 결정하는 것입니다.

**주석 검토**

프로그래머가 소스 코드에 대한 자세한 주석을 포함시켜 다른 프로그래머가 특정 기능을 코딩 할 때 주어진 결정이 왜 취해진 것인지 더 잘 이해할 수 있도록 하는 것은 매우 일반적이며 권장되는 방법입니다.
프로그래머는 일반적으로 대형 웹 기반 응용 프로그램을 개발할 때 주석을 추가합니다. 
그러나 HTML 코드의 인라인에 포함 된 주석은 공격자가 사용할 수 없는 내부 정보를 나타낼 수 있습니다.
때로는 기능이 더 이상 필요 없기 때문에 소스 코드 조차도 주석 처리 되었지만,이 주석은 의도하지 않게 사용자에게 반환된 HTML 페이지로 유출됩니다.
주석 검토를 통해 정보가 주석을 통해 유출되었는지 확인해야합니다. 
이 검토는 웹 서버 정적 및 동적 컨텐츠 분석과 파일 검색을 통해서만 철저히 수행 할 수 있습니다. 
자동 또는 가이드 방식으로 사이트를 탐색하고 검색된 모든 컨텐츠를 저장하는 것이 유용 할 수 있습니다. 
그런 다음 코드에서 사용할 수있는 HTML 주석을 분석하기 위해 검색된 컨텐츠를 검색 할 수 있습니다.

|

Gray Box Testing 
-----------------------------------------------------------------------------------------

**설정 검토*

웹 서버 또는 응용 프로그램 서버 구성은 사이트의 내용을 보호하는 데 중요한 역할을하므로 일반적인 설정 실수를 방지하기 위해 신중하게 검토해야합니다. 
물론 권장 설정은 사이트 정책 및 서버 소프트웨어에서 제공해야하는 기능에 따라 다릅니다. 
그러나 대부분의 경우 서버가 올바르게 보호되었는지 확인하기 위해 설정 지침 (소프트웨어 공급 업체 또는 외부 업체에서 제공)을 따라야합니다.

대체로 서버를 설정하는 방법을 일반적으로 말하는 것은 불가능하지만 몇 가지 일반적인 지침을 고려해야합니다.

- 응용 프로그램에 필요한 서버 모듈(IIS의 경우 ISAPI 확장)만 사용 가능하게 설정하십시오. 이렇게하면 소프트웨어 모듈이 비활성화되어 서버의 크기와 복잡성이 줄어들기 때문에 공격 대상이 줄어 듭니다. 또한 이미 비활성화 된 모듈에만 해당되는 경우 공급업체 소프트웨어에 나타날 수 있는 취약점이 사이트에 영향을 주는 것을 방지합니다.

- 기본 웹 서버 페이지 대신 사용자 정의 페이지로 서버 오류(40x 또는 50x)를 처리하십시오. 특히 모든 응용 프로그램 오류가 최종 사용자에게 반환되지 않으며 공격자를 도울 것이므로 이러한 오류를 통해 누출된 코드가 없는지 확인하십시오. 개발자는 사전 제작 환경에서 이 정보가 필요하기 때문에 실제로 이 점을 잊어 버리는 것이 일반적입니다.
- 서버 소프트웨어가 운영 체제에서 최소화된 권한으로 실행되는지 확인하십시오. 이렇게하면 공격자가 코드를 웹 서버로 실행한 후에 권한을 강화할 수는 있지만 서버 소프트웨어의 오류로 인해 전체 시스템이 직접 손상되지 않습니다.
- 서버 소프트웨어가 적법한 액세스와 오류를 올바르게 기록하는지 확인하십시오.
- 서버가 과부하를 적절히 처리하고 DoS (Denial of Service) 공격을 차단하도록 서버가 구성되어 있는지 확인하십시오. 서버가 제대로 성능이 조정되었는지 확인하십시오.
- 관리자가 아닌 사용자는 applicationHost.config, 리디렉션에 액세스 할 수 없습니다. config 및 administration.config를 참조하십시오. 여기에는 네트워크 서비스, IIS_IUSRS, IUSR 또는 IIS 응용 프로그램 풀이 사용하는 사용자 지정 ID가 포함됩니다. IIS 작업자 프로세스는 이러한 파일에 직접 액세스하지 않습니다.
- 네트워크에서 applicationHost.config, redirection.config 및 administration.config를 절대로 공유하지 마십시오. 공유 구성을 사용하는 경우 applicationHost.config를 다른 위치로 내보내는 것이 좋습니다.
- 모든 사용자는 기본적으로 .NET Framework machine.config 및 root web.config 파일을 읽을 수 있습니다. 관리자의 눈에만 사용해야하는 경우 중요한 정보를 이 파일에 저장하지 마십시오.
- 시스템의 다른 사용자가 아닌 IIS 작업자 프로세스에서만 읽어야하는 중요한 정보를 암호화하십시오.
- 웹 서버가 공유 applicationHost.config에 액세스하는 데 사용하는 ID에 대한 쓰기 권한을 부여하지 마십시오. 이 ID는 읽기 액세스 권한 만 가져야합니다.
- 별도의 ID를 사용하십시오. 웹 서버가 공유 applicationHost.config에 액세스하는 데 사용하는 ID에 대한 쓰기 권한을 부여하지 마십시오. 이 ID는 읽기 액세스 권한 만 가져야합니다. applicationHost.config를 공유에 게시합니다. 이 ID를 웹 서버의 공유 구성에 대한 액세스 구성에 사용하지 마십시오.
- 공유 구성에서 사용할 암호화 키를 내보낼 때 강력한 암호를 사용하십시오.
- 공유 구성 및 암호화 키를 포함하는 공유에 대한 제한된 액세스를 유지합니다. 이 공유가 손상되면 침입자는 웹 서버의 IIS 구성을 읽고 쓸 수 있고 웹 사이트의 트래픽을 악의적 인 원본으로 리디렉션 할 수 있으며 경우에 따라 IIS 작업자 프로세스에 임의의 코드를 로드하여 모든 웹 서버를 제어 할 수 있습니다.
- 방화벽 규칙 및 IPsec 정책으로이 공유를 보호하여 구성원 웹 서버 만 연결할 수 있도록하십시오.

|

**로깅**

로깅은 응용 프로그램 아키텍처의 보안에 중요한 자산입니다. 응용 프로그램의 결함 (사용자가 끊임없이 존재하지 않는 파일을 검색하려고하는 사용자)은 물론 불량 사용자의 지속적인 공격을 탐지하는 데 사용할 수 있기 때문입니다. 로그는 일반적으로 웹 및 기타 서버 소프트웨어에 의해 올바르게 생성됩니다. 로그에 작업을 제대로 기록하는 응용 프로그램을 찾는 것이 일반적이지 않으며 응용 프로그램 로그의 주요 목적은 프로그래머가 특정 오류를 분석하는 데 사용할 수있는 디버깅 출력을 생성하는 것입니다.

두 경우 모두 (서버 및 응용 프로그램 로그) 로그 내용을 기반으로 몇 가지 문제를 테스트하고 분석해야합니다.

- 로그에 중요한 정보가 포함되어 있습니까?
- 로그가 전용 서버에 저장되어 있습니까?
- 로그 사용이 서비스 거부 상태를 생성 할 수 있습니까?
- 어떻게 회전 시켰지? 충분한 시간 동안 기록을 보관하고 있습니까?
- 로그는 어떻게 검토됩니까? 관리자가 이러한 검토를 사용하여 대상 공격을 탐지 할 수 있습니까?
- 로그 백업은 어떻게 보존됩니까?
- 기록되는 데이터가 기록되기 전에 유효성이 검사됩니까 (최소 / 최대 길이, 문자 등)?

|

**로그의 민감한 정보**

일부 응용 프로그램은 예를 들어 GET 요청을 사용하여 서버 로그에 표시되는 양식 데이터를 전달할 수 있습니다. 즉, 서버 로그에 중요한 정보가 포함될 수 있습니다. 이 민감한 정보는 침입자가 관리 인터페이스나 알려진 웹 서버 취약점 또는 잘못된 구성 을 통해 로그를 얻은 경우 악의적으로 사용될 수 있습니다.

이벤트 로그에는 공격자에게 유용한 정보 (정보 유출)가 있거나 공격에 직접 사용될 수있는 데이터가 포함되는 경우가 많습니다.

- 디버그 정보
- 스택 트레이스
- 사용자 이름
- 시스템 구성 요소 이름
- 내부 IP 주소
- 덜 민감한 개인 데이터 (예: 이름이 지정된 개인과 관련된 이메일 주소, 우편 주소 및 전화 번호)
- 비즈니스 데이터

또한 일부 관할 지역에서는 일부 개인 정보와 같은 로그 파일에 중요한 정보를 저장하면 백 엔드 데이터베이스에 적용 할 데이터 보호 법률을 로그 파일에도 적용해야 할 수 있습니다. 
그렇게하지 않으면 무의식적으로 적용되는 데이터 보호법에 따라 처벌을받을 수 있습니다.

더 중요한 정보의 목록은 다음과 같습니다.

- 응용 프로그램 소스 코드
- 세션 식별 값
- 액세스 토큰
- 중요한 개인 정보 및 개인 식별 정보 (PII)의 일부 형태
- 인증 암호
- 데이터베이스 연결 문자열
- 암호화 키
- 은행 계좌 또는 지불 카드 소지자 데이터
- 로깅 시스템보다 높은 보안 등급의 데이터를 저장할 수 있음
- 상업적으로 민감한 정보
- 사용자가 수집을 거부했거나 동의하지 않은 관련 관할 구역에서 수집하는 것은 불법입니다.

|

**로그 위치**

일반적으로 서버는 서버가 실행 중인 시스템의 디스크를 사용하여 작업 및 오류에 대한 로컬 로그를 생성합니다. 
그러나 서버가 손상되면 침입자가 로그를 지우고 공격 및 방법의 모든 흔적을 정리할 수 있습니다. 
이러한 일이 발생하면 시스템 관리자는 공격이 어떻게 발생했는지 또는 공격 소스가 어디에 위치해 있는지 알 수 없습니다. 
사실, 대부분의 공격 도구 키트에는 주어진 정보를 포함하는 모든 로그를 정리할 수 있는 로그 재퍼가 포함되어 있으며, 공격자의 시스템 수준 루트 킷에 일상적으로 사용됩니다.

따라서 로그를 웹 서버 자체가 아닌 별도의 위치에 보관하는 것이 현명합니다. 또한 웹 서버 팜과 같은 동일한 응용 프로그램을 참조하는 여러 소스의 로그를보다 쉽게 집계 할 수 있으며 서버 자체에 영향을주지 않고 로그 집약(CPU 집약적 일 수 있음)을 쉽게 수행 할 수 있습니다.

|

**로그 저장소**

로그가 제대로 저장되지 않으면 로그에 서비스 거부 조건이 발생할 수 있습니다. 
충분한 자원을 가진 공격자는 특별히 금지되지 않은 경우 로그 파일에 할당 된 공간을 채울 충분한 수의 요청을 생성 할 수 있습니다. 
그러나 서버가 올바르게 구성되지 않은 경우 로그 파일은 운영 체제 소프트웨어 또는 응용 프로그램 자체에 사용 된 디스크 파티션과 동일한 디스크 파티션에 저장됩니다. 
즉, 디스크를 가득 채우거나 디스크에 쓸 수 없기 때문에 운영 체제가 작동하지 않을 수 있습니다.

일반적으로 UNIX 시스템에서 로그는 /var에 있습니다. 
로그가 저장된 디렉토리가 별도의 파티션에 있는지 확인하는 것이 중요합니다. 
경우에 따라 시스템 로그가 영향을 받지 않도록 하려면 서버 소프트웨어 자체의 로그 디렉토리를 전용 파티션에 저장해야합니다.

로그가 파일 시스템을 채우도록 커져야한다는 말은 아닙니다. 
서버 로그의 증가는 공격의 징후 일 수 있으므로이 상태를 감지하기 위해 모니터링 해야합니다. 
이 조건을 테스트하는 것은 프로덕션 환경에서 쉽고 위험하며, 이러한 요청이 로깅되는지 여부 및 이러한 요청을 통해 로그 파티션을 채울 가능성이 있는지를 확인하기 위해 충분하고 지속적인 요청 수를 해고하는 것과 같습니다. 
GET 또는 POST 요청을 통해 생성되는지 여부에 관계없이 QUERY_STRING 매개 변수도 기록되는 일부 환경에서는 일반적으로 단일 요청으로 인해 데이터의 양이 적어 질 수 있기 때문에 날짜 및 시간, 소스 IP 주소, URI 요청 및 서버 결과와 같이 기록된 로그를 빠르게 채우는 큰 쿼리를 시뮬레이션 할 수 있습니다 

|

**로그 순환**

대부분의 서버(그러나 몇몇 사용자 정의 응용 프로그램)는 로그가 순환하는 파일 시스템을 채우지 않도록 로그를 순환시킵니다. 로그를 회전 할 때의 가정은 제한된 시간 동안만 정보가 필요하다는 것입니다. 

이 기능은 다음을 보장하기 위해 테스트되어야합니다.

- 로그는 보안 정책에 정의된 시간 동안 유지되며 그 이상은 유지되지 않습니다.
- 로그는 한 번 회전하면 압축됩니다.
- 회전된 로그 파일의 파일 시스템 사용 권한은 로그 파일 자체의 사용 권한과 동일하거나 더 엄격합니다. 예를 들어, 웹 서버는 사용하는 로그에 쓰기를 해야하지만 회전된 로그에 실제로 쓸 필요는 없습니다. 즉, 웹 서버 프로세스가 수정하지 못하도록 파일의 권한을 변경할 수 있습니다.

일부 서버는 주어진 크기에 도달하면 로그를 순환시킬 수 있습니다. 
이런 일이 발생하면 침입자가 로그를 숨기려면 로그를 강제로 로테이션 할 수 없도록 해야합니다.

|

**로그 액세스 제어**

최종 사용자는 이벤트 로그 정보를 볼 수 없습니다. 
웹 관리자 조차도 관세 분리 통제를 깰 수 있으므로 이러한 로그를 볼 수 없어야 합니다. 
원시 로그에 대한 액세스를 보호하는 데 사용되는 액세스 제어 스키마와 로그를 보거나 검색 할 수 있는 기능을 제공하는 모든 응용 프로그램이 다른 응용 프로그램 사용자 역할에 대한 액세스 제어 스키마와 연결되어 있지 않은지 확인 하십시오. 
또한 인증되지 않은 사용자가 로그 데이터를 볼 수 있어야합니다.

|

**로그 검토**

로그 검토는 웹 서버의 파일 사용 통계 (일반적으로 대부분의 로그 기반 응용 프로그램에서 집중적으로 다루는)의 추출 이외에도 웹 서버에서 공격이 발생하는지 확인하는 데 사용될 수 있습니다.

웹 서버 공격을 분석하려면 서버의 오류 로그 파일을 분석해야합니다. 검토는 다음 사항에 집중해야합니다.

- 40x (찾을 수 없음) 오류 메시지 동일한 출처의 많은 양은 웹 서버에 대해 사용되는 CGI 스캐너 도구를 나타낼 수 있습니다.
- 50x (서버 오류) 메시지. 이는 예기치 않게 실패한 공격자의 응용 프로그램 악용을 나타낼 수 있습니다. 예를 들어 SQL 주입 공격의 첫 번째 단계는 SQL 쿼리가 제대로 구성되지 않았고 백 엔드 데이터베이스에서 실행이 실패 할 때 이러한 오류 메시지를 생성합니다.

로그 통계 또는 분석은 로그를 생성하는 동일한 서버에서 생성되거나 저장되어서는 안됩니다. 
그렇지 않으면 공격자가 웹 서버의 취약성이나 부적절한 구성을 통해 액세스 권한을 얻고 로그 파일 자체에서 공개하는 것과 유사한 정보를 검색 할 수 있습니다.

|

참고 문헌
==========================================================================================

[1] Apache 

- Apache Security, by Ivan Ristic, O`reilly, March 2005. 
- Apache Security Secrets: Revealed (Again), Mark Cox, November 2003 http://www.awe.com/mark/apcon2003/ 
- Apache Security Secrets: Revealed, ApacheCon 2002, Las Vegas, Mark J Cox, October 2002 - http://www.awe.com/mark/apcon2002 
- Performance Tuning -http://httpd.apache.org/docs/misc/perf-tuning.html 

[2] Lotus Domino 
 
- Lotus Security Handbook, William Tworek et al., April 2004, available in the IBM Redbooks collection 
- Lotus Domino Security, an X-force white-paper, Internet Security Systems, December 2002 
- Hackproofing Lotus Domino Web Server, David Litchfield, October 2001, 
- NGSSoftware Insight Security Research, available at http://www. nextgenss.com 

[3] Microsoft IIS 
 
- IIS 6.0 Security, by Rohyt Belani, Michael Muckin, - http://www. securityfocus.com/print/infocus/1765 
- IIS 7.0 Securing Configuration - http://technet.microsoft.com/enus/library/dd163536.aspx Securing Your Web Server (Patterns and Practices), Microsoft Corporation, January 2004 
- IIS Security and Programming Countermeasures, by Jason Coombs 
- From Blueprint to Fortress: A Guide to Securing IIS 5.0, by John Davis, Microsoft Corporation, June 2001 
- Secure Internet Information Services 5 Checklist, by Michael Howard, Microsoft Corporation, June 2000 
- "INFO: Using URLScan on IIS" - http://support.microsoft.com/default.aspx?scid=307608 

[4] Red Hat`s (formerly Netscape`s) iPlanet 

- Guide to the Secure Configuration and Administration of iPlanet Web Server, Enterprise Edition 4.1, by James M Hayes, The Network Applications Team of the Systems and Network Attack Center (SNAC), NSA, January 2001 

[5] WebSphere 

- IBM WebSphere V5.0 Security, WebSphere Handbook Series, by Peter Kovari et al., IBM, December 2002. 
- IBM WebSphere V4.0 Advanced Edition Security, by Peter Kovari et al., IBM, March 2002. 

[6] General 

- Logging Cheat Sheet, OWASP 
- SP 800-92 Guide to Computer Security Log Management, NIST 
- PCI DSS v2.0 Requirement 10 and PA-DSS v2.0 Requirement 4, PCI Security Standards Council 

[7] Generic: 
 
- CERT Security Improvement Modules: Securing Public Web Servers - http://www.cert.org/security-improvement/ 
- Apache Security Configuration Document, InterSect Alliance http://www.intersectalliance.com/projects/ApacheConfig/index.html 
- "How To: Use IISLockdown.exe" -http://msdn.microsoft.com/library/en-us/secmod/html/secmod113.asp 

|