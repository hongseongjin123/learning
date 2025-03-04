# 클린 코드 원칙
팀규칙

보이 스카우트 규칙 (p50)

체크인 할 때보다 조금 더 클린 코드를 체크 아웃하라.
변수명 하나, 조금 긴 함수를 분리, 약간의 중복 제거 무엇이든 괜찮다


네이밍 의도를 밝혀라 (p54)
int d → int day

비슷한 이름을 사용하지 않는다 ****(p56)
XYZControllerForEfficientHandingOfStrings 와
XYZControllerForEfficientStorageOfStrings 의 차이가 한 눈에 들어오는가

*변수 이름에 타입을 넣지 않는다 *(p61)
PhoneNumber phoneString (x)
List<Integer> accountList (x) → accounts

클래스 이름은 명사나 명사구가 좋다 (p63)
Customer, Account, WikiPage 같은 이름은 좋다
Manager, Data, Info 같은 이름은 피한다
메서드 이름은 동사나 동사구가 좋다 (p63)

기발한 이름은 피해라 (p64)

일관성 있는 어휘를 사용해라 (p65)

역할이 비슷한 메서드에 클래스마다 get, fetch, retrieve라고 제각각 부르지 마라
문제 영역과 관련된 이름을 사용해라 (p66)
함수
작게 만들어라 (p75)
함수는 작을수록 좋고, 들여쓰기는 적을수록 좋다
한가지 일만 해라 (p76)

하나의 함수, 하나의 추상화 수준 (p77)

getHtml()의 추상화 수준은 높다
String pagePathName = PathParser.render(pagePath)의 추상화 수준은 중간이다
.append("\n")의 추상화 수준은 낮다
그리고 하나의 함수에 위의 서로 다른 추상화 수준을 섞으면 가독성이 떨어진다
서술적인 이름을 사용해라 (p81)
네이밍은 중요하다.
길어도 괜찮다. 이름을 정하느라 시간이 걸려도 괜찮다. 일관성있게 함수가 하는 일을 잘 표현하는 이름을 사용해라
함수 인수는 적을수록 좋다. (p82)
가장 이상적인 인수의 개수는 0개이다.
3개 이상은 가급적이면 피하는게 좋다.
플래그 인수는 추하다 (p83)
"함수가 여러 가지를 처리한다고 공표하는 셈이니까!"
인수 객체를 사용해라 (p84)
인수가 2~3개 이상 필요하다면 일부를 클래스 변수로 만드는 것을 고려해 봐라
그 과정에서이 개념이 포함된다. 
Try/Catch 블록을 분리해라 (p89)
try {
  deletePage(page);
  registry.deleteReference(page.name);
  configKeys.deleteKey(page.name.makeKey());
} catch(Exception e) {
  logger.log(e.getMessage());
}

위 코드 보다는 아래가 좋다.

public void delete(Page page) {
    try {
        deletePageAndAllReferences(page);
    } catch(Exception e) {
        logError(e);
    }
}

private void deletePageAndAllReferences(Page paage) throws Exception {
    deletePage(page);
  registry.deleteReference(page.name);
  configKeys.deleteKey(page.name.makeKey());
}

private void logError(Exception e) {
    logger.log(e.getMesssage());
}
반복하지 마라 (p91)
중복을 제거하라
주석
가급적이면 코드로 의도를 표현하라 (p99)
주석은 나쁜 코드를 보완하지 못한다
형식
개념은 빈 행으로 분리하라 (p128)

밀접한 개념은 세로로 가까이 두어라 (p131)

하나의 함수가 다른 함수를 호출한다면 두 함수는 세로로 가까이 두어라 (p134)

가능하다면 호출하는 함수를 먼저 배치한다
팀 규칙을 따라라 (p143)
객체와 자료구조
자료를 추상화 하라 (p148)
아무 생각 없이 조회/설정 함수를 추가하는 것보다 자료를 표현할 가장 좋은 방법을 고민해야 한다
객체 지향과 절차 지향을 상황에 맞게 선택하라 (p151)
객체 지향에서 어려운 변경은 절차적 코드에서 쉽다
디미터 법칙을 위반하지 마라(p153)
예외 처리
예외를 사용하라(p160)
발생가능한 오류를 분기로 처리하기보다 try-catch 예외처리를 사용하라
예외에 의미를 제공하라(p165)
예외를 던질 때는 전후 상황을 덧붙인다
null을 전달하지마라 그리고 반환하지마라(p169)
단위 테스트
TDD 법칙(p185)
1. 컴파일만 가능한 실패하는 단위 테스트를 작성한다
2. 현재 실패하는 단위 테스트를 통과할 정도만 실제 코드를 작성한다
클린 테스트 코드를 유지하라(p185)
테스트 코드가 복잡하고 지저분 할 수록 실제 코드를 변경하고 추가하기 어려워진다
클린 테스트 코드를 유지하는 방법? → 가독성(p187)
가독성을 유지하는 방법? -> 명료성 단순성 표현력
이중 표준(p191)
테스트 동작 환경과 실제 동작 환경은 다르다
가독성이 올라간다면 효율적이지 못한 코드라도 테스트 코드에서는 고려해볼만 하다
하나의 테스트에 assert문은 최대한 줄이는 것이 좋다(p194)

하나의 테스트 함수는 하나의 개념만 테스트하라(p195)

F . I . R . S . T(p196)

Fast: 테스트는 빨라야 한다
Independent: 테스트는 서로 의존하면 안된다
Repeatable: 테스트는 어떤 환경에서도 반복 가능해야한다(실행 가능해야 한다)
Self-Validating: 테스트는 스스로 성공 여부를 알려야 한다(로그 파일을 읽게 해서는 안된다)
Timely: 테스트는 적시에 작성해야 한다(실제 코드 구현전에 작성한다)
클래스
작게 만들어라(p200)

단일 책임 원칙(p203)

인스턴스 변수가 작게 유지함으로써 응집도를 높여라(p205)

응집도를 높이면 작은 클래스 여럿이 나온다
=======
클린 코드 원칙 100
팀규칙
보이 스카우트 규칙 (p50)
체크인 할 때보다 조금 더 클린 코드를 체크 아웃하라.
변수명 하나, 조금 긴 함수를 분리, 약간의 중복 제거 무엇이든 괜찮다
네이밍

의도를 밝혀라 (p54)
int d → int day

비슷한 이름을 사용하지 않는다 ****(p56)
XYZControllerForEfficientHandingOfStrings 와
XYZControllerForEfficientStorageOfStrings 의 차이가 한 눈에 들어오는가

*변수 이름에 타입을 넣지 않는다 *(p61)
PhoneNumber phoneString (x)
List<Integer> accountList (x) → accounts

클래스 이름은 명사나 명사구가 좋다 (p63)
Customer, Account, WikiPage 같은 이름은 좋다
Manager, Data, Info 같은 이름은 피한다
메서드 이름은 동사나 동사구가 좋다 (p63)

기발한 이름은 피해라 (p64)

일관성 있는 어휘를 사용해라 (p65)

역할이 비슷한 메서드에 클래스마다 get, fetch, retrieve라고 제각각 부르지 마라
문제 영역과 관련된 이름을 사용해라 (p66)
함수
작게 만들어라 (p75)
함수는 작을수록 좋고, 들여쓰기는 적을수록 좋다
한가지 일만 해라 (p76)

하나의 함수, 하나의 추상화 수준 (p77)

getHtml()의 추상화 수준은 높다
String pagePathName = PathParser.render(pagePath)의 추상화 수준은 중간이다
.append("\n")의 추상화 수준은 낮다
그리고 하나의 함수에 위의 서로 다른 추상화 수준을 섞으면 가독성이 떨어진다
서술적인 이름을 사용해라 (p81)
네이밍은 중요하다.
길어도 괜찮다. 이름을 정하느라 시간이 걸려도 괜찮다. 일관성있게 함수가 하는 일을 잘 표현하는 이름을 사용해라
함수 인수는 적을수록 좋다. (p82)
가장 이상적인 인수의 개수는 0개이다.
3개 이상은 가급적이면 피하는게 좋다.
플래그 인수는 추하다 (p83)
"함수가 여러 가지를 처리한다고 공표하는 셈이니까!"
인수 객체를 사용해라 (p84)
인수가 2~3개 이상 필요하다면 일부를 클래스 변수로 만드는 것을 고려해 봐라
그 과정에서이 개념이 포함된다. 
Try/Catch 블록을 분리해라 (p89)
try {
  deletePage(page);
  registry.deleteReference(page.name);
  configKeys.deleteKey(page.name.makeKey());
} catch(Exception e) {
  logger.log(e.getMessage());
}

위 코드 보다는 아래가 좋다.

public void delete(Page page) {
    try {
        deletePageAndAllReferences(page);
    } catch(Exception e) {
        logError(e);
    }
}

private void deletePageAndAllReferences(Page paage) throws Exception {
    deletePage(page);
  registry.deleteReference(page.name);
  configKeys.deleteKey(page.name.makeKey());
}

private void logError(Exception e) {
    logger.log(e.getMesssage());
}
반복하지 마라 (p91)
중복을 제거하라
주석
가급적이면 코드로 의도를 표현하라 (p99)
주석은 나쁜 코드를 보완하지 못한다
형식
개념은 빈 행으로 분리하라 (p128)

밀접한 개념은 세로로 가까이 두어라 (p131)

하나의 함수가 다른 함수를 호출한다면 두 함수는 세로로 가까이 두어라 (p134)

가능하다면 호출하는 함수를 먼저 배치한다
팀 규칙을 따라라 (p143)
객체와 자료구조

자료를 추상화 하라 (p148)
아무 생각 없이 조회/설정 함수를 추가하는 것보다 자료를 표현할 가장 좋은 방법을 고민해야 한다

객체 지향과 절차 지향을 상황에 맞게 선택하라 (p151)
객체 지향에서 어려운 변경은 절차적 코드에서 쉽다

디미터 법칙을 위반하지 마라(p153)
예외 처리

예외를 사용하라(p160)
발생가능한 오류를 분기로 처리하기보다 try-catch 예외처리를 사용하라

예외에 의미를 제공하라(p165)
예외를 던질 때는 전후 상황을 덧붙인다

null을 전달하지마라 그리고 반환하지마라(p169)

단위 테스트
TDD 법칙(p185)
1. 컴파일만 가능한 실패하는 단위 테스트를 작성한다
2. 현재 실패하는 단위 테스트를 통과할 정도만 실제 코드를 작성한다

클린 테스트 코드를 유지하라(p185)
테스트 코드가 복잡하고 지저분 할 수록 실제 코드를 변경하고 추가하기 어려워진다

클린 테스트 코드를 유지하는 방법? → 가독성(p187)
가독성을 유지하는 방법? -> 명료성 단순성 표현력
이중 표준(p191)
테스트 동작 환경과 실제 동작 환경은 다르다
가독성이 올라간다면 효율적이지 못한 코드라도 테스트 코드에서는 고려해볼만 하다
하나의 테스트에 assert문은 최대한 줄이는 것이 좋다(p194)

하나의 테스트 함수는 하나의 개념만 테스트하라(p195)

F . I . R . S . T(p196)

Fast: 테스트는 빨라야 한다
Independent: 테스트는 서로 의존하면 안된다
Repeatable: 테스트는 어떤 환경에서도 반복 가능해야한다(실행 가능해야 한다)
Self-Validating: 테스트는 스스로 성공 여부를 알려야 한다(로그 파일을 읽게 해서는 안된다)
Timely: 테스트는 적시에 작성해야 한다(실제 코드 구현전에 작성한다)
클래스
작게 만들어라(p200)

단일 책임 원칙(p203)

인스턴스 변수가 작게 유지함으로써 응집도를 높여라(p205)

응집도를 높이면 작은 클래스 여럿이 나온다
>>>>>>> caa73e212348e1d1f16ca3918b271b1cbcf6bc5e
추상화된 것에 의존하여 본경으로부터 격리하라(p213)
