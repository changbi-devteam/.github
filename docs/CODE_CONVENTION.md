# Changbi-devteam Code Convention 
---
`version 1.0`  
본 문서는 (주)창작과 비평의 디지털 사업부의 효율적인 협업과 코드 품질 유지를 위한 기본적인 코드 컨벤션을 정의하고있습니다.  
주력 언어는 Java이며, Spring Framework를 사용합니다.  
협의된 내용으로 확정된 컨벤션 규칙은 작업시에 반드시 준수해주시기를 부탁드립니다.  

- 작성자: 김종완 (디지털사업부 / 대리 / 내선 3743)
- 최초 작성일: 2025. 06.19. 

---

### 1. 명명 규칙 (Naming Conventions)

클래스와 메서드, 변수 등 일관적인 네이밍 작성법을 위한 규칙입니다.

* **클래스/인터페이스:**
    * **파스칼 케이스 (PascalCase)** 를 사용합니다.
    * 명사형으로 작성하며, **약어를 사용하지 않습니다**.
    * **예시:** `UserController`, `ProductService`, `UserRepository` 

* **메서드/변수:**
    * **카멜 케이스 (camelCase)** 를 사용합니다.
    * **메서드:** 동사 + 명사 형태로 작성합니다. (예: `getUserList()`, `getProductById(Long id)`)
    * **변수:** 명사 형태로 작성합니다. (예: `userName`, `productId`)

* **상수:**
    * **대문자 스네이크 케이스 (UPPER_SNAKE_CASE)**를 사용합니다.
    * **예시:** `MAX_PAGE_SIZE`, `DEFAULT_ENCODING`

* **패키지:**
    * **소문자 (lower case)**를 사용하며, 일반적으로 도메인 역순으로 작성합니다.
    * **예시:** `com.yourcompany.project.domain.user`

* **DTO/VO:**
    * DTO(Data Transfer Object)나 VO(Value Object)는 목적에 따라 명확한 **접미사**를 활용합니다.
    * **예시:** `UserCreateRequest`, `ProductResponse`, `ItemDto`

* **줄임말 사용 원칙 및 예외:**
    * **원칙적으로 줄임말 사용을 금지합니다.**
    * 단, **메서드명이 25글자를 초과할 경우** 명사에 대해 직관적으로 확인 가능한 축약을 허용합니다. 이 경우 아래 **자주 사용되는 축약어 목록**을 우선적으로 활용합니다.

    ---

    #### 자주 사용되는 축약어 목록

    다음은 코드 내에서 자주 사용되는 단어와 권장되는 축약어 목록입니다. 이 목록에 없는 단어의 축약이 필요할 경우, 팀원들과 논의하여 새로운 축약어를 정의하고 목록에 추가합니다.

    * **ID/식별자 관련:**
        * **ID (Identifier):** `Id`
        * **Number:** `No`
    * **정보/데이터 관련:**
        * **Information:** `Info`
        * **Message:** `Msg`
        * **Description:** `Desc`
    * **시간/날짜 관련:**
        * **Maximum:** `Max`
        * **Minimum:** `Min`
    * **관리/처리 관련:**
        * **Configuration:** `Config` or `Cfg`
        * **Transaction:** `Tx`
    * **기타:**
        * **Application:** `App`
        * **Utility:** `Util`
        * **Service:** `Svc`
        * **Controller:** `Ctrl`

    ---

---

### 2. 코드 형식 (Code Formatting)

일관된 코드 형식을 유지하여 가독성을 높이고 유지보수가 용이한 코드를 작성하기 위한 규칙입니다.  
**IDE의 자동 포맷팅 기능을 적극 활용**하여 아래 규칙들을 준수합니다.

* **들여쓰기:**
    * **스페이스 4칸**을 사용합니다.
    * **탭 사용은 금지**합니다. (IDE 설정에서 탭을 스페이스로 자동 변환하도록 설정 권장)

* **괄호 위치:**
    * **K&R 스타일**을 사용합니다. (클래스, 메서드, 조건문 등의 여는 중괄호 `{`는 선언과 같은 줄에 위치)
    * **예시:**
        ```java
        public class MyClass {
            public void myMethod() {
                if (condition) {
                    // code
                }
            }
        }
        ```

* **한 줄 최대 길이:**
    * **120자**를 넘지 않도록 합니다. 코드가 너무 길어지면 여러 줄로 나누어 작성합니다.

* **공백:**
    * 연산자(`=`, `+`, `-`, `*`, `/`, `==`, `!=`, `>=`, `<=`, `&&`, `||` 등) 주변에는 항상 **공백**을 추가합니다.
    * 괄호 뒤 (`if (`, `for (`, `while (` 등)에도 공백을 추가합니다.
    * **예시:** `int result = a + b;`, `if (condition) {`

* **변수 선언 순서:**
    * 클래스 내 변수 선언 시 다음 순서를 따르며, 논리적인 그룹 간에는 **한 줄의 빈 공백**으로 구분합니다.
        1.  **상수 (Constants):** `public static final` 변수
        2.  **클래스 변수 (Static Variables):** `static` 변수 (상수 제외)
        3.  **인스턴스 변수 (Instance Variables):** `static`이 아닌 변수

    * **예시:**
        ```java
        public class ExampleClass {
            // 1. 상수
            public static final int MAX_ATTEMPTS = 5;

            // 2. 클래스 변수
            private static int totalCount;

            // 3. 인스턴스 변수
            private Long userId;
            private String userName;

            // 생성자
            public ExampleClass(Long userId, String userName) {
                this.userId = userId;
                this.userName = userName;
                totalCount++;
            }

            // ... 나머지 메서드
        }
        ```

* **`equals()`, `hashCode()`, `toString()` 메서드 위치:**
    * 이 메서드들은 일반적으로 객체의 상태를 정의하고 디버깅에 활용되므로, 클래스 정의의 **마지막 부분**에 일관되게 작성합니다.

---
