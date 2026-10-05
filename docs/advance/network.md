# 1. DNS

## 1.1 DNS Type

**1. 재귀형 DNS (Recursive DNS)**

웹 도메인 이름 같은 인터넷 리소스에 대한 IP 주소를 생성하는 일련의 이벤트 중 첫 번째 도착지 개념으로 일반적으로 ISP (`Internest Service Provider`) 또는 CSP (`Content Service Provider`) 같은 DNS 공급업체에서 관리하기 때문에, 이전 DNS 쿼리에 대한 답변 (`또는 조회`)을 일정 기간 동안 로컬 캐시에 저장해 DNS 요청을 해결하는 데 걸리는 시간을 줄여준다.

**2. 권한형 DNS (Authoritative DNS)**

IP 주소 같은 도메인 이름에 해당하는 고식 레코드 (`Record`)를 보관하는 시스템으로 도메인 이름은 브라우저 같은 애플리케이션을 URL (`www.google.com`)와 같은 웹사이트로 안내하여 사람이 읽을 수 있는 IP 주소의 이름이다. IP 주소는 `125.45.67.189`와 같이 머신이 읽을 수 있는 숫자와 `.`으로 이루어진 문자열로 저장된다.

**3. Root Name**

Root 네임 서버는 DNS 계층 구조의 최상위에 위치하며 루트 존 (`DNS의 중앙 데이터베이스`)을 제공하는 역할을 한다. A부터 M까지의 문자로 식별되는 13개의 루트 네임 서버 `Identity` 또는 `Authoer`이 존재하며, 루트 존에 저장된 레코드에 대한 쿼리에 응답하고 적절한 TLD 네임 서버로 요청을 전달한다.

**4. TLD Name (Top Level Domain)**

TLD 서버는 일반 최상위 도메인 (`gTLD`)을 비롯한 계층 구조의 다음 수준을 관리하는 역할을 담당한다. 해당 TLD 내의 특정 도메인에 대한 권한 있는 이름 서버로 쿼리를 전달하여, 즉 `.cod` TLD 네임 서버는 `.com`으로 끝나는 도메인을 전달하여 각 끝에 있는 도메인에 대한 일관성으로 처리한다.

<!-- ## 1.2 DNS Cache -->


---

# ETC. 참조

[DNS Server Types](https://www.cloudflare.com/learning/dns/what-is-dns/)