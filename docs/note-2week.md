# Global Academy 2Week Learn Note

---

* Keyword
  - FastAPI 요청과 응답 흐름을 파악
  - AI에 필요한 개념들을 파악

> [!NOTE]
> **API에 대한 기본 개념은 [note-1week](note-1week.md/#2-api-application-programing-interface)에서 확인하면 된다. 학습 내용의 예제 코드는 Python과 Golang으로 작성 예정**

---

# 1. FastAPI

![alt text](../img/FastAPI-logo.png)

FastAPI는 현대적인 `웹 프레임워크`로 개발되어 빠른 속도와 파이썬 기반 표준 타입 힌트를 기초로 고성능 퍼포먼스를 도달하기 위한 API라고 보면된다. 최근에 성장하고 있는 Go와 유사한 성능을 검증될 정도로 생산성을 높여 빠른 개발이 가능하도록 구조화 설계되었다.

<details>
<summary>FastAPI example code</summary>

```py
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def read_root():
    return {"Hello": "World"}

@app.get("/items/{item_id}")
def read_item(item_id: int, q: str | None = None):
    return {"item_id": item_id, "q": q}
```

</details>

## 1.1 HTTP와 REST API 관계

HTTP가 웹 통신의 기본 프로토콜로 클라이언트와 서버 간의 데이터 전송을 위한 규칙을 정의한 것이라면, REST API는 HTTP를 기반으로 하여 REST의 원칙을 준수를 목표로 설계된 API이다. REST API는 자원, 행위, 표현의 세 가지의 요소로 구성되어 자원은 `URL`로 표현되고, 행위는 `HTTP Method`로 표현되며 RESTful API는 이러한 원칙들을 따르면서 클라이언트와 서버 간의 통신을 효율적으로 설계하고 리소스를 전달하는 방식이다.

서버는 클라이언트의 상태를 저장하지 않기 때문에 클라이언트는 요청 (`Request`)만 보내고, 서버는 필요한 리소스만 응답 (`Response`)으로 제공하여 서도 독립적으로 발전할 수 있다.

## 1.2 REST API와 FastAPI 차이

REST API와 FastAPI의 차이는 역할에 있다. REST API는 웹에서 데이터를 주고받기 위한 API를 설계하는 아키텍처 스타일로, 자원(Resource)을 URL로 표현하고 HTTP 메서드(GET, POST, PUT, DELETE 등)를 활용하여 데이터를 처리하는 규칙을 정의한다. 반면 FastAPI는 Python 기반의 웹 프레임워크로, 이러한 REST API를 쉽고 효율적으로 개발할 수 있도록 지원하는 도구이다.

즉, REST API가 "어떤 방식으로 API를 설계할 것인가"를 정의하는 개념이라면, FastAPI는 "그 설계를 실제 코드로 구현하는 방법"을 제공하는 프레임워크라고 할 수 있다. 따라서 둘은 경쟁 관계가 아니라 상호 보완적인 관계에 있으며, 개발자는 FastAPI를 사용하여 REST API를 구현할 수 있다. 또한 FastAPI는 높은 성능, 비동기 처리 지원, 데이터 검증 기능, 그리고 Swagger 기반의 자동 API 문서 생성 기능을 제공하여 현대적인 웹 서비스와 백엔드 개발에서 널리 활용되고 있다.

<details>
<summary>Go REST API </summary>

```go
package main

import (
	"net/http"
	"strconv"

	"github.com/gin-gonic/gin"
)

type User struct {
	ID   int    `json:"id"`
	Name string `json:"name"`
	Age  int    `json:"age"`
}

var users = []User{
	{ID: 1, Name: "Alice", Age: 25},
	{ID: 2, Name: "Bob", Age: 30},
}

func main() {
	r := gin.Default()

	// RESTful Routes
	r.GET("/users", getUsers)
	r.GET("/users/:id", getUser)
	r.POST("/users", createUser)
	r.PUT("/users/:id", updateUser)
	r.DELETE("/users/:id", deleteUser)

	r.Run(":8080")
}

// GET /users
func getUsers(c *gin.Context) {
	c.JSON(http.StatusOK, users)
}

// GET /users/:id
func getUser(c *gin.Context) {
	id, _ := strconv.Atoi(c.Param("id"))

	for _, user := range users {
		if user.ID == id {
			c.JSON(http.StatusOK, user)
			return
		}
	}

	c.JSON(http.StatusNotFound, gin.H{
		"message": "user not found",
	})
}

// POST /users
func createUser(c *gin.Context) {
	var newUser User

	if err := c.ShouldBindJSON(&newUser); err != nil {
		c.JSON(http.StatusBadRequest, gin.H{
			"error": err.Error(),
		})
		return
	}

	newUser.ID = len(users) + 1
	users =
```

</details>


## 1.3 Lifespan

FastAPI 애플리케이션의 Lifespan 매개변수와 `컨텍스트 매니저`를 사용하여 시작과 종료 로직을 정의할 수 있지만, 


# 2. 동기와 비동기 [Async and Await]

#### 비동기 [Asynchronous]

비동기는 작업이 서로 독립적으로 실행되는 방식으로, 요청 (`Request`)를 보낸 후 결과를 기다리지 않고 다음 작업 (`Task`)를 수행할 수 있도록 하는 라이브러리다. 한 작업이 완료될 때까지 전체 프로그램의 흐름이 멈추지 않고, 여러 작업을 병렬적으로 처리할 수 있어 시스템 리소스를 효율적으로 사용할 수 있게된다.

```py
async def fetch_data():
    await asyncio.sleep(2)
    return "Data fetched"
```

#### 동기 [Synchronous]

```py
import time

def task(name, delay):
    """Simulates a task that takes 'delay' seconds."""
    print(f"Starting task: {name}")
    time.sleep(delay)  # Blocking call
    print(f"Finished task: {name}")

def main():
    start_time = time.time()

    # Tasks run sequentially
    task("Task 1", 2)
    task("Task 2", 3)
    task("Task 3", 1)

    end_time = time.time()
    print(f"Total execution time: {end_time - start_time:.2f} seconds")

if __name__ == "__main__":
    main()
```


## 2.1 동시성과 병렬성 [Concurrency & Parallelism]

동시성은 여러 작업을 일정 단위 시간으로 잘개 나누어 돌아가며 처리하는 방식으로 한 번의 여러 작업이 동일한 시간 내에 진행되는 것을 허용한다. 병렬성은 여러 작업을 실제로 동시에 처리하기 때문에 여러 CPU Core가 각기 다른 작업을 처리한다.

# 3. I/O Bound

- CPU 연산보다 **입출력(I/O)** 작업에 더 많은 시간이 소요되는 작업
- 대표적인 예
  - 데이터베이스 조회
  - 외부 API 호출
  - 파일 읽기/쓰기
  - 네트워크 통신
- FastAPI의 비동기 처리(`async/await`)가 가장 효과적인 영역

```python
async def get_user():
    await db.fetch_one(...)
```

# 4. Event Loop

- 비동기 작업을 관리하는 실행 엔진
- I/O 작업이 대기 상태일 때 다른 작업을 수행하여 자원을 효율적으로 사용
- Python에서는 `asyncio` Event Loop를 사용
- FastAPI도 내부적으로 Event Loop 기반으로 동작

동작 흐름

```md
요청 수신 → Event Loop 등록 → I/O 대 → 다른 작업 수행 → 처리 완료 후 응답 반환
```

# 5. Health Check

- 서버가 정상 동작 중인지 확인하는 기능
- 주로 `/health`, `/ping` 엔드포인트를 사용
- 로드밸런서, Kubernetes 등이 서버 상태를 확인할 때 활용

```python
@app.get("/health")
def health():
    return {"status": "ok"}
```

응답

```json
{
  "status": "ok"
}
```

---

# 6. Router

- API를 기능별로 그룹화하는 기능
- 프로젝트 구조를 깔끔하게 유지할 수 있음
- 사용자(User), 상품(Product), 주문(Order) 등으로 분리

```python
from fastapi import APIRouter

router = APIRouter()

@router.get("/")
def get_users():
    return []
```

```python
app.include_router(
    router,
    prefix="/users",
    tags=["users"]
)
```

결과

```http
GET /users/
```

---

# 7. Life Cycle

- 애플리케이션 시작(Startup)과 종료(Shutdown) 시 실행되는 과정
- DB 연결, 캐시 초기화, 리소스 정리에 사용

```python
from contextlib import asynccontextmanager

@asynccontextmanager
async def lifespan(app):
    print("startup")
    yield
    print("shutdown")
```

실행 순서

```md
서버 시작 → startup → 애플리케이션 실행 → shutdown → 서버 종료
```

# 8. Dependency Injection (DI)

- 필요한 객체를 직접 생성하지 않고 외부에서 주입받는 방식
- 코드 재사용성과 테스트 편의성이 높아짐
- FastAPI에서는 `Depends()`를 사용

```python
from fastapi import Depends

def get_db():
    return DB()

@app.get("/users")
def get_users(db=Depends(get_db)):
    return db.select_all()
```

장점

- 결합도 감소
- 코드 재사용 가능
- 단위 테스트 용이

## 8.1 Return 과 Raise

### Return

- 함수의 정상 결과를 반환

```python
return {"message": "success"}
```

응답

```json
{
  "message": "success"
}
```

### Raise

- 예외를 발생시켜 오류를 전달

```python
from fastapi import HTTPException

raise HTTPException(
    status_code=404,
    detail="User not found"
)
```

응답

```json
{
  "detail": "User not found"
}
```

### 차이점

| 구분      | Return            | Raise          |
| --------- | ----------------- | -------------- |
| 목적      | 결과 반환         | 예외 발생      |
| 상태      | 정상 처리         | 오류 처리      |
| 실행 흐름 | 함수 종료 후 반환 | 즉시 예외 발생 |

---

## 8.2 Self

- 클래스 자기 자신(인스턴스)을 가리키는 참조 변수
- 인스턴스 변수와 메서드에 접근할 때 사용

```python
class UserService:
    def __init__(self, name):
        self.name = name

    def hello(self):
        return f"Hello {self.name}"
```

사용 예시

```python
user = UserService("Kim")
user.hello()
```

# 9. Expression

- 값을 계산하여 결과를 반환하는 코드 조각
- 실행 결과가 항상 하나의 값으로 평가됨

예시

```python
10 + 20
```

```python
name.upper()
```

```python
a if a > b else b
```

## 9.1 RAG (Retrieval-Augmented Generation)

### 개념

- LLM이 외부 문서를 검색(Retrieval)한 후 답변을 생성(Generation)하는 방식
- 최신 정보나 사내 문서를 활용 가능

동작 과정

```md
질문 → 문서 검색 → 관련 문서 추출 → LLM 답변 생성
```

### 장점

- 최신 정보 반영 가능
- 환각(Hallucination) 감소
- 사내 문서 활용 가능

---

## 9.2 CAG (Cache-Augmented Generation)

### 개념

- 자주 사용하는 정보나 이전 결과를 캐시에 저장하여 활용하는 방식
- 동일하거나 유사한 질문에 빠르게 응답 가능

동작 과정

```md
질문 → 캐시 확인 → 캐시 존재 → 즉시 응답 or 캐시 없음 → 검색 수행 → 캐시 저장 → 응답 생성
```

### 장점

- 응답 속도 향상
- 비용 절감
- 반복 질의에 효율적

## 9.3 TAG (Tool-Augmented Generation)

### 개념

- LLM이 외부 도구(Tool)를 호출하여 결과를 얻고 답변하는 방식
- API, DB, 검색엔진, 계산기 등을 사용할 수 있음

동작 과정

```md
질문 → 도구 선택 → API/DB 호출 → 결과 수집 → 답변 생성
```

### 장점

- 실시간 데이터 사용 가능
- 정확성 향상
- 계산 및 외부 서비스 활용 가능

---

## RAG / CAG / TAG 비교

| 구분      | 핵심 개념              | 사용 대상        |
| --------- | ---------------------- | ---------------- |
| RAG       | 문서 검색 후 답변 생성 | 문서 기반 QA     |
| CAG       | 캐시 데이터 활용       | 반복 질의        |
| TAG       | 외부 도구 활용         | 실시간 정보 조회 |
| RAG + TAG | 문서 검색 + 도구 사용  | Agent 시스템     |

---
---

# Etc. 참조

* [1. FastAPI Offical Home](https://fastapi.tiangolo.com/)
* [2. RFC Internet Standards Offical Home](https://www.rfc-editor.org/)