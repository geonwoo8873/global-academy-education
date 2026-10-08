# Global Academy 1Week Learn Note

---

* Keyword
  - 사용자 인터페이스(UI) 구성을 위한 JavaScript 라이브러리
  - Component 및 Virtual DOM 기반 화면 렌더링

---

# 1. 풀-스택 개발 구상 순서

1. **User**
2. **Frontend**
   * React
   * Blazor
3. **Communication**
   * API [Application Programing Interface]
   * JSON
4. **Network**
   * HTTP [Hyper Transfer Protocol]
   * DNS [Domain Name System]
   * VPN [Virtual Private Network]
5. **Backend**
   * Java
   * Golang - net/http (`lib`)
   * .NET - ASP.NET (`framework`)
6. **Database**
   * MySQL
   * PostSQL
   * Windows SQL
7. **Storage**
   * AWS S3 Bucket
   * Docker Volume 
   * HDD, SSD, NVMe [RIAD]

## 1.1 상호작용 흐름

#### 1. HTTP [Hyper Transfer Protocol]

<details>
<summary>HTTP Status</summary>

| TYPE   | DESCRIPTION         |
| ------ | ------------------- |
| GET    | 기존 정보 조회      |
| POST   | 새 데이터 처리 요청 |
| PUT    | 데이터 수정         |
| PATCH  | 일부 데이터 수정    |
| DELETE | 데이터 삭제         |

| Status Code | Description               | Example                 |
| ----------- | ------------------------- | ----------------------- |
| 400         | 잘못된 요청               | 지원하지 않는 파일 옵션 |
| 401         | 인증 필요 또는 인증 실패  | 유효하지 않은 Token     |
| 403         | 권한 없음                 | 다른 사용자의 문서 접근 |
| 404         | Resource 없음             | 문서를 찾을 수 없음     |
| 409         | 현재 상태와 충돌          | 중복 문서 등록          |
| 422         | 입력 데이터 검증 실패     | 필수 Field 누락         |
| 429         | 요청 한도 초과            | AI 호출 Rate Limit      |
| 500         | 예상하지 못한 서버 오류   | 코드 버그               |
| 502         | 외부 서비스의 잘못된 응답 | AI Provider 응답 오류   |
| 503         | 서비스 사용 불가          | AI Engine 일시 중단     |
| 504         | 외부 서비스 응답 Timeout  | LLM 응답 시간 초과      |

</details>

<details>
<summary>Curl request HTTP body output</summary>

```sh
curl www.microsoft.com
```

```sh
<!DOCTYPE html><html xmlns:mscom="http://schemas.microsoft.com/CMSvNext"
        xmlns:md="http://schemas.microsoft.com/mscom-data" lang="en-us"
        xmlns="http://www.w3.org/1999/xhtml"><head><link rel="shortcut icon"
                        href="//www.microsoft.com/favicon.ico?v2" /><link
                        type="text/css" rel="stylesheet"
                        href="https://assets.onestore.ms/cdnfiles/external/mwf/long/v1/v1.25.0/css/mwf-west-european-default.min.css"
<...>
```

</details>

#### 2. API [Application Programing Interface]

컴퓨터나 컴퓨터 프로그래밍 사이의 연결로 일종의 소프트웨어 인터페이스 (`Software Interface`)이며 다른 종류의 소프트웨어에 서비스를 제공한다. 연결 또는 인터페이스를 빌드하거나 사용하는 방법을 기술하는 문서 표준을 API 규격이라고 칭하여 이에 대한 표준을 충족하는 컴퓨터 시스템은 API가 구현 (`Implement`)되었다거나 노출 (`Expose`)되었다고 말하기 때문에 하나의 API라는 단어가 사양이나 구현체를 의미할 수 있다.

API의 목적은 시스템이 동작하는 방식에 관한 내부의 세세한 부분을 숨기는 것으로 내부의 세세한 부분이 나중에 변경되더라도 프로그래머가 사용할 수 있고 일관성을 유지한 관리를 목표로 통제가 가능한 부분들만 노출 시킨다. API는 특정 시스템용으로 커스텀하게 빌드될 수 있고, 아니면 수 많은 시스템간 상호운용성을 허용하는 공유가 되는 표준일 수 있다. 

</details>

<details>
<summary>POST Request REST API call example</summary>

```go
package main
 
import (
   "bytes"
   "encoding/json"
   "fmt"
   "net/http"
)
 
type CreateUserRequest struct {
   Name string `json:"name"`
   Email string `json:"email"`
}
 
func main() {
   url := "https://jsonplaceholder.typicode.com/users"
    
   reqBody := CreateUserRequest{
      Name: "홍길동",
      Email: "hong@example.com",
   }
    
   jsonData, err := json.Marshal(reqBody)
      if err != nil {
      panic(err)
   }
    
   resp, err := http.Post(
      url,
      "application/json",
      bytes.NewBuffer(jsonData),
   )
      if err != nil {
      panic(err)
   }
   defer resp.Body.Close()
    
   fmt.Println("Status:", resp.Status)
}
```

</details>


#### 3. JSON [JavaScript Object Notation]

<details>
<summary>AWS IAM Policy apply editing JSON</summary>

```json
{
	"Version": "2012-10-17",
	"Statement": [
		{
			"Sid": "Statement1",
			"Effect": "Allow",
			"Action": [
				"ec2:DeleteSubnet",
				"ec2:DeleteRoute",
				"ec2:DeleteVpc",
				"ec2:DeleteVolume",
				"ec2:CreateVpc",
				"ec2:CreateVolume",
				"ec2:CreateSubnet",
				"ec2:CreateSnapshot",
				"ec2:CreateRoute",
				"ec2:CreateNatGateway",
				"ec2-instance-connect:*"
			],
			"Resource": [
                "arn:aws:ec2:{Region}:{Account}:instance/{InstanceId}",
                "*"
            ]
		}
	]0
}
```

</details>


## 1.2 네트워크 환경

#### 1. DNS [Domain Name System]

![](https://assets.ibm.com/is/image/ibm/dns-hierarchy?fmt=png-alpha&dpr=on%2C1&fit=fit%2C1&wid=1536&hei=633)

DNS (`Domain Name System`)이라는 이름으로 사용자가 긴 숫자 형태보다 쉽게 식별하기 위해 사용하여 웹을 탐색할 수 있도록 해준다. 일반적으로 IP 주소 같은 기록을 보관하는 역할을 하기 때문에 인터넷의 전화번호부라고 의미하기도 한다.

N개의 많은 컴퓨터와 디바이스가 IP 주소 및 Web, App, Etc 등 리소스를 빠르게 찾을 수있도록 도메인과 IP 주소의 거대한 중앙 데이터베이스가 아닌 분산된 서버 시스템을 사용한다. 분산 시스템에는 [Authoritative DNS](../docs/advance/network.md/#11-dns-type) (`권한형`) 서버와 [Recursive DNS](../docs/advance/network.md/#11-dns-type) (`재귀형`) 서버를 비롯한 여러 종류로 포함된다.

Authoriative DNS는 특정 도메인의 이름과 IP 주소에 대한 공식 정보를 보관을 하는 반면, Recursive DNS는 해당 정보를 쉽게 사용할 수 있도록 도와주는 하나의 Helper 시스템으로 분류된다.


<details>
<summary>DNS Example 1</summary>

```ps
PS C:\Windows\System32> nslookup www.google.com
-> |
Server:  acns.uplus.co.kr
Address:  1.214.68.2

Non-authoritative answer:
Name:    www.google.com
Addresses:  2001:4860:4828:7700::
          2001:4860:4827:7700::
          2001:4860:482d:7700::
          2001:4860:482a:7700::
          2001:4860:4829:7700::
          2001:4860:482c:7700::
          2001:4860:482b:7700::
          2001:4860:4826:7700::
          142.251.152.119
          142.251.151.119
          142.251.150.119
          142.251.153.119
          142.251.154.119
          142.251.155.119
          142.251.157.119
          142.251.156.11
```

</details>

<details>
<summary>DNS Example 2</summary>

```ps
PS C:\Windows\System32> nslookup www.microsoft.com
Server:  acns.bora.net
Address:  1.214.68.2

Non-authoritative answer:
Name:    e13678.dscb.akamaiedge.net
Addresses:  2600:140e:3:780::356e
          2600:140e:3:7a3::356e
          2600:140e:3:7b4::356e
          2600:140e:3:7ab::356e
          2600:140e:3:7b6::356e
          184.29.45.214
Aliases:  www.microsoft.com
          www.microsoft.com-c-3.edgekey.net
```

</details>

#### 2. VPN [Virtual Private Network]

VPN은 개인 데이터를 암호화 (`Encryption`)하고 승인되지 않은 제 3자로부터 활동을 숨겨 사용자에게 안전한 비공개 인터넷 연결을 제공한다. 컴퓨터 네트워킹의 성장과 인터넷 확상에 근본적인 역할을 지탱해 개인 정보를 보호하는 보안 솔루션의 필요성이 커졌다. 이는 강력한 암호화와 개인 인터넷 연결과 공용 인터넷 연결 사이의 보안 장벽인 방화벽을 우회하는 기능으로 알려졌다.

컴퓨터 네트워킹은 리소스를 통신하고 공유하도록 설계된 모바일 디바이스, 라우터, 데이터 센터와 같이 상호 연결된 디바이스의 시스템이다. 디바이스가 네트워크를 통해 데이터를 전송하거나 교환할 수 있는 방법을 지시하는 규칙인 통신 프로토콜에 의존하여 작동하기 때문에 최신 디바이스 네트워크는 개인 커뮤니케이션 및 엔터테인먼트부터 기업의 비즈니스 프로세스에 디지털 경험을 뒷받침을 하게된다. 또한 컴퓨터 네트워킹과 함께 클라우드가 발전함에 따라 클라우드 컴퓨팅이라는 새로운 개념도 생겨났다. 클라우드 컴퓨팅은 종량제 BM을 바탕으로 인터넷을 통해 정보와 컴퓨팅 소스에 `온디맨드` 방식으로 액세스가 가능하다.

리소스는 광범위하면서 서버, 데이터 스토리지, 소프트웨어, 네트워킹 디바이스, 애플리케이션 개발 도구 등이 포함될 수 있기에 규모의 상관 없이 대부분 기업들이 인터넷의 힘을 활용해 협업과 유연성을 개선함으로써 효율성과 확장 가능성을 높일 수 있도록 지원하게된다.

## 1.3 스토리지 [Storage]

기본적인 스토리지의 개념은 사용중인 마더보드에 장착되어 있는 구성 부품중 하나로 데이터 및 지침을 저장하는 컴퓨터 구성 요소이다.

기본 스토리지는 메인 메모리라고도 불려, 중앙처리장치 (`CPU`)와 직접적인 데이터 수신호가 진행되기 때문에 읽고 쓰는 것이 간단하다. 이를 통해 프로세스는 기본 스토리지가 보유하고 있는 데이터 및 명령에 더욱 빠른 액세스가 가능하다. 또한 내부 메모리라고 부르는 주 메모리 또는 기본 메모리는 컴퓨터가 작동할 때 액세스할 수 있는 비교적 적은 양의 데이터를 저장한다. 보조 메모리라고도 하는 외부 메모리에는 지속적인 방식으로 데이터를 저장할 수 있는 스토리지 장치가 포함된다.

<details>
<summary>Storage Size CMD</summary>

```bash
$ df
Filesystem     1K-blocks      Used Available Use% Mounted on
D:/Git         208539644  22809868 185729776  11% /
C:             767090684 130434468 636656216  18% /c
```

```bash
$ df -BG
Filesystem     1G-blocks  Used Available Use% Mounted on
D:/Git              199G   22G      178G  11% /
C:                  732G  125G      607G  18% /c
```

</details>

### 1.3.1 기본 스토리지 작동 원리

기본 스토리지는 CPU에서 현재 사용 중인 데이터와 명령어를 유지 관리하여 작동한다. 프로그램 실행하기 위해 CPU는 기본 스토리지에 연결하여 필요한 명령을 가져오고 컴퓨터 처리에 필수적인 운영 작업을 담당한다.

**운영 체제 (OS, Operating System) 로드**

컴퓨터가 작동하기 시작하면 운영 체제의 필요한 구성 요소가 하드 디스크 (`HDD`, `Hard Disk Drive`)나 고체 상태 드라이브 (`SSD`, `Solid State Drive`)에서 RAM으로 추가되는 부팅 주기를 거친다. OS가 로드되면 시스템은 작업을 관리할 준비가 된 것이다.

**앱 실행 (Application Run)**

애플리케이션을 실행하기 전에 먼저 기존 디스크 위치에서 RAM으로 로드되며, RAM은 앱 실행을 조정하고 원래 표시했던 것보다 빠른 데이터 검색을 제공한다.

**데이터 처리**

RAM에 로드되는 것은 앱뿐만 아니라 애플리케이션에서 처리해야 하는 모든 데이터도 포함된다. 고등 수학 부터 렌더링된 이미지 및 편집된 파일을 처리하는 앱과 같은 다양한 앱의 데이터를 포함한다.

## 1.4 데이터베이스 [Database]

데이터베이스는 체계적인 데이터를 컬렉션 형태로 저장하거나 관리 및 보호하기 위한 디지털 방식 저장소라고 보면된다. 다양한 유형의 데이터베이스가 존재하고 동시에 각기다른 유형의 데이터를 관리하기 때문에 데이터 베이스는 재무 기록과 같은 구조화된 데이터에 적합하다 본다. 비관계형는 미디어와 텍스트와 같은 비정형 데이터 유형에 적합하지만 생성형 AI와 애플리케이션에서 사용하는 벡터 데이터 형태는 벡터 데이터베이스의 벡터 임베딩형태로 데이터를 저장한다.

또한 데이터베이스는 다양한 데이터 아키텍처를 구축하기 위한 뼈대로 단순히 정보만을 저장하기 위한 도구가 아니라 중앙에서 데이터를 관리하고 무결성 및 보안 표준을 시행하며, 데이터 접근을 용이하게 할 수 있도록 지원한다.

# 2. React

> [!IMPORTANT]
> **React에 대한 내용은 [Docs Advance React.md](../docs/advance/react.md)에서 설치와 기초 개념들을 정리중이다.**

# 3. Python

> [!IMPORTANT]
> **Python에 대한 튜토리얼 개념의 샘플은 [tour-learn-collection](https://github.com/geonwoo8873/tour-learn-collection/tree/main/programming-language/python) Repository 에서 확인할 수 있다.**

---
---

# ETC. 참조

* [1. MDN HTTP Methods](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Methods)
* [2. JSON Syntax](https://github.com/geonwoo8873/tour-learn-collection/blob/main/aws-credentials/solutions-architect-associate/2-aws-iam-introduction.md#53-%EA%B6%8C%ED%95%9C-%EB%B6%80%EC%97%AC-%EB%B0%8F-%EA%B6%8C%ED%95%9C-%EC%A0%95%EC%B1%85-%EA%B8%B0%EB%B3%B8)
* [3. DNS](https://www.ibm.com/kr-ko/think/topics/dns)
  * [3.1 DNS Type Advance](../docs/advance/network.md/#11-dns-type) 
* [4. VPN](https://www.ibm.com/kr-ko/think/topics/vpn)
  * [4.1 VPN Process Advance]()
* [5. API](https://www.ibm.com/kr-ko/think/topics/api)
* [6. JSON](https://www.json.org/json-en.html)
* [7. Sotrage](https://www.ibm.com/kr-ko/think/topics/api)
  * [7.1 Data Storage](https://www.ibm.com/kr-ko/think/topics/data-storage)
* [8. Database](https://www.ibm.com/kr-ko/think/topics/database#1003835715)