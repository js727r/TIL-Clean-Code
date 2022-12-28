# TIL-Clean-Code

> 클린 코드 내용 요약 정리

---

## 1장. 깨끗한 코드

깨끗한 코드란 무엇인가?

### 핵심 요약

**나쁜 코드** 가 쌓이면 쌓일수록, **생산성** 은 떨어진다.

### 나쁜 코드로 치르는 대가

-   코드를 고칠 때마다 문제가 발생함
-   스파게티 코드를 **해독** 하느라 오랜 시간이 걸린다
-   얽히고 설킨 코드를 더욱 쌓게된다

#### 결국 시스템을 다시 설계하려면 막대한 비용이 든다

> 빨리 가려면 깨끗한 코드를 유지해야 한다.
> `그렇다면 깨끗한 코드를 작성하는 방법은 무엇일까?`

### 많은 프로그래머들이 생각하는 깨끗한 코드의 요소

-   논리가 간단해야 버그가 숨어들지 못한다
-   오류는 명백한 전략에 의거해 철저히 처리
-   깨끗한 코드는 잘 쓴 문장처럼 읽힌다
-   설계자의 의도를 숨기지 않는다
-   모든 테스트를 통과한다
-   중복이 없다
-   클래스, 메서드, 함수 등을 최대한 줄인다.

### 이 후의 내용은, 이 책의 저자가 생각하는 '깨끗한 코드'에 대한 내용이다.

---

## 2장. 의미있는 이름

클린한 코드를 작성하기 위한 이름을 정하는 기본적인 가이드라인.

### 핵심 요약

-   이름을 보고 의도를 알 수 있어야함
-   이름에서 오해할만한 잘못된 정보를 제공하면 안됨
-   기존에 사용하던 이름과 비슷한 이름을 사용해서 헷갈리게 하지 마라
-   축약어같이 발음하기 어려운 이름은 피하라
-   나중에 검색하기 쉽도록 하라
-   가급적 인코딩은 피하라
-   자신의 지식을 자랑하지 말고 모두가 이해할 수 있는 이름을 사용하라
-   클래스 명명규칙, 메서드 명명규칙에 차이가 있으니 잘 확인해볼것
-   이름에 특정 문화의 용어 사용 지양
-   한 개념에 한 단어 사용 (get, retrieve, fetch)
-   위의 내용을 보고 일관성을 유지하려다가 비슷한 다른 개념을 한 단어로 표현하지 마라 (add / insert / append)
-   해법 영역 혹은 문제 영역에서 이름을 가져와라
-   불필요한 맥락을 없애라

### 단락

-   의도를 분명히 밝혀라
    -   int d; // 경과 시간(댠위:날짜) :x:
    -   int elapsedTimeInDays; :white_check_mark:
-   그릇된 정보를 피하라
    -   List 자료형이 아닌데 accountList라고 명명 :x: -> 사실 이름에 List도 쓰지 않는데 이는 뒤에서 다룬다
    -   흡사한 이름을 사용하지 말라
        -   XYZControllerForEfficientStorageOfStrings
        -   XYZControllerForEfficientHandlingOfStrings
-   의미있게 구분하라
    -   컴파일을 통과하기 위해 명명하는 경우
        -   klass :x:
    -   불용어를 붙이는 경우
        -   a1, a2, a3, ... :x:
        -   Product클래스 작성 후 ProductInfo, ProductData :x: -> Info, Data는 아무 의미도 제공하지 못함
        -   getAccount(), getAccounts(), getAccountList() :x: -> 세 가지 메서드가 모두 제공되면 어떤 메서드를 호출해야 할 지 혼란스러움
-   발음하기 쉬운 이름을 사용하라
    -   genymdhms(generate date, year, month, day, hour, minute, second) :x:
    -   generationTimestamp :white_check_mark:
-   검색하기 쉬운 이름을 사용하라
    -   grep으로 찾기 쉽도록 숫자 등을 상수로 명명
    -   5 -> const int WORK_DAYS_PER_WEEK = 5 :white_check_mark:
-   인코딩을 피하라
    -   접두어를 사용하는 것
        -   멤버 변수 앞에 `m_`으로 시작하는 접두어 사용 :x:
        -   인터페이스 이름 앞에 "I"로 시작하는 접두어 사용 -> 필자는 추천하지 않음
            -   인코딩이 필요하다고 생각되는 경우 차라리 구현체에 "Imp" 접미사를 붙이는 것을 선호
-   자신의 기억력을 시험하지 마라
    -   LOS라는 이름이 Line of sight를 의미한다는 것을 알고 있다고 줄여쓰지 마라
    -   모두가 이해할 수 있도록 명료하게
-   클래스 이름
    -   명사나 명사구가 적합
    -   Customer, WikiPage, Account, AddressParser :white_check_mark:
    -   Manager, Processor, Data, Info :x:
-   메서드 이름
    -   동사나 동사구가 적합
    -   postPayment, deletePage, save :white_check_mark:
    -   생성자 중복정의시, 정적 팩토리 메서드 사용
        -   Complex fulcrumPoint = Complex.FromRealNumber(23.0); :thumbsup:
        -   Complex fulcrumPoint = new Complex(23.0); -> 나쁘진 않지만 위의 방법을 추천
-   기발한 이름은 피하라
    -   웃기자고 특정 문화에서 사용하는 농담을 사용하는것은 지양하라
-   한 개념에 한 단어를 사용하라
    -   똑같은 메서드를 클래스마다 fetch, retrieve, get처럼 제각각으로 부르는 것 :x:
    -   마찬가지로 controller, manager, driver를 혼재하여 사용 :x:
-   말장난을 하지 마라 (일관성을 잘못 적용하지 마라)
    -   산술 연산에 add라는 이름을 사용
    -   집합에 값 하나를 추가하는데 add 사용 :x: -> insert나 append를 사용하라
-   해법 영역에서 가져온 이름을 사용하라
    -   프로그래머에게 익숙한 기술 개념은 많다. 기술 개념에는 기술 이름을 선택하라
    -   JobQueue, AccontVisitor :white_check_mark:
-   문제 영역에서 가져온 이름을 사용하라
    -   적절한 '프로그래머 용어'가 없다면 문제 영역에서 이름을 가져온다
    -   문제 영역 개념과 관련이 깊은 경우에도 사용
-   의미 있는 맥락을 추가하라
    -   city, zipcode, state라는 변수가 있을 경우 state가 주소 일부라는 것을 알 수 있음
    -   그러나 어떤 메서드에서 state만 사용한다면 무슨 의미인지 파악하는것이 어렵다
    -   addrState로 변경 시 해결, 또는 Address 클래스를 추가하면 더욱 좋다
    -   Address가 IP 주소인지, 집 주소인지 헷갈릴 수 있으므로 PostalAddress로 할 수도 있겠다
-   불필요한 맥락을 없애라

    -   의미가 분명한 경우, 이름에 불필요한 맥락 추가 :x:
    -   Gas Station Deluxe라는 어플리케이션 개발을 위해 모든 클래스 이름을 'GSD'로 시작하겠다는 생각은 :x:

---

## 3장. 함수

함수를 잘 만드는 방법.

### 핵심 요약

-   작게 만들기
-   함수는 같은 추상화 수준을 유지 ex) 클래스에서 높은 추상화 수준은 public, 낮은 추상화 수준은 private이 되겠다
-   인수는 적을수록 좋다
-   함수가 몰래 하는 일이 없도록 한다
-   예외 활용
-   반복 절대 금지
-   계속 다듬으면서 리팩토링 하는게 답이다

### 단락

-   작게 만들어라
    -   함수의 들여쓰기 수준은 1단이나 2단을 넘어가선 안된다
    -   20줄도 긴 편이다
    -   더 작게 만들어라
-   함수가 한 가지만 하도록 해라
    -   함수 당 추상화 수준은 한 가지로 해라
    -   함수 내에서 의미 있는 다른 이름으로 함수를 추출할 수 있다면 여러 작업을 하는 셈이다
    -   switch문의 경우 다형성 객체를 생성할 때만 사용하라. 그 외의 경우는 다형성을 통해 해결하라
-   서술적 이름을 사용하라
    -   함수가 하는 일을 잘 표현하는 이름을 쓴다
    -   이름이 길어도 괜찮다
    -   2장을 참조하라
-   함수의 인수
    -   인수는 개념을 이해하기 어렵게 한다
    -   이상적인 개수는 0개
    -   적으면 적을수록 좋다
    -   4개 이상부턴 특별한 이유가 없는 한 사용하면 안된다
    -   테스트 관점에서도 인수가 많으면 어렵다
    -   플래그 인수는 추하다. 인수로 bool값을 넘기는 관례는 끔찍하다.
    -   인수가 2~3개 필요하다면 독자적인 클래스 변수로 선언하는것을 고려한다
    -   단항 함수는 함수와 인수가 동사/명사 쌍을 이뤄야 한다 ex) writeField(name)
    -   이름에 키워드를 추가하여 인수 순서를 외울 필요가 없도록 한다 ex) assertExpectedEqaulsActual(expected, actual)
-   부수 효과를 일으키지 마라
    -   함수가 한 가지 일을 한다고 약속했으나 **남몰래** 숨겨진 일을 하는 것
    -   예상치 못하게 클래스 변수나 전역 변수를 수정한다거나 함수로 넘어온 인수를 수정하는 경우
    -   부수 효과는 시간적 결합이나 순서 종속석 문제를 초래한다
    -   출력 인수는 피해라. 함수에서 상태를 변경해야 하면 함수가 속한 객체의 상태를 변경하는 방식을 택한다 ex) appendFooter(report) :x: report.appendFooter() :white_check_mark:
-   명령과 조회를 분리하라
    -   함수는 무언가에 답하거나 수행하거나 둘 중 하나만 해야 한다
-   오류 코드보다 예외를 활용하라
    -   오류 코드를 반환하면 해당 함수를 호출하는 부분에서 if문으로 중첩되는 코드가 발생한다
    -   예외를 사용하면 오류 처리 코드가 원래 코드에서 분리되어 깔끔해진다
-   Try/Catch 블록 뽑아내기
    -   try/catch 블록은 원래 추하다. 코드 구조에 혼란을 일으키고 정상 동작과 처리 동작을 뒤섞는다
    -   try블록과 catch 블록을 각각 별도의 함수로 뽑아내는것이 좋다
    -   오류 처리도 한 가지 작업에 해당한다
-   반복하지 마라
    -   중복은 만악의 근원이다
    -   많은 원칙들이 중복을 없애기 위해 등장했다
-   구조적 프로그래밍
    -   함수는 return문이 하나여야 한다
    -   루프 안에서 break나 continue는 사용하면 안된다
    -   goto는 절대로 사용하지 마라
    -   라고는 하지만 return, break, continue를 여러 차례 사용해도 괜찮다. 오히려 의도를 잘 표현하기 쉽다
-   소프트웨어를 짜는 것은 글짓기와 비슷하다
    -   처음부터 탁 하고 내놓을 수는 없다
    -   코드를 다듬고, 이름을 바꾸고, 함수를 만들고, 중복을 제거해서 좋은 코드가 얻어진다

---

## 4장. 주석

주석은 필요할까?

### 핵심 요약

-   주석 없이 잘 읽히는 코드가 이상적인 코드다
-   대부분의 프로그래머는 코드를 수정하더라도 주석을 수정하지 않는다
-   따라서 주석이 잘못된 정보를 제공하는 경우가 발생한다
-   즉 주석은 정말 필요할 때가 아니면 달지 않는 것이 좋다
-   주석 없이 잘 읽히려면 코드를 잘 짜야한다...

### 단락

-   주석은 나쁜 코드를 보완하지 못한다
    -   주석을 쓰는 일반적인 이유는 코드의 품질이 나쁘기 때문에 보완하기 위해 작성한다
    -   코드 자체로 표현력이 풍부하고 깔끔한것이 어수선한 주석이 있는 것 보다 훨씬 좋다
    -   이상한 코드에 주석을 달 시간에 코드를 깨끗하게 만들어라
-   코드로 의도를 표현하라
    -   코드는 충분히 의도를 설명하기 충분하다
    -   많은 경우에 주석으로 달려는 설명을 함수로 만들어 표현해도 충분하다
-   좋은 주석
    -   어떤 주석은 유용하다. 아래에 설명된 것들에 해당하는 주석이 유용한 주석이다
        -   법적인 주석
        -   정보를 제공하는 주석
            -   그래도 이왕이면 함수 이름에 정보를 담거나 클래스를 만들어 없애는 편이 좋다
        -   의도를 설명하는 주석
            -   때때로 주석은 구현을 이해하게 도와주는 것을 넘어 의도까지 설명하기도 한다
        -   의미를 명료하게 밝히는 주석
            -   이해를 돕도록 읽기 쉽게 표현하는 것을 말한다 ex) assertTrue(a.compareTo(b) == 0); // a == b
            -   이 경우도 마찬가지로 잘못된 주석으로 오류를 범할 수 있기 때문에 각별히 주의하자
        -   결과를 경고하는 주석
            -   ex) // 결과 시간이 충분하지 않다면 호출하지 마십시오
            -   ex) // SimpleDateFormat은 스레드 세이프하지 않으므로 독립적인 인스턴스를 생성해야 합니다
        -   TODO 주석
            -   `앞으로 할 일`들을 TODO주석으로 남겨두면 편하다
            -   TODO를 많이 남겨두는건 좋지 않으므로 주기적으로 점검하자
        -   중요성을 강조하는 주석
            -   자칫하면 대수롭지 않다고 여겨질 수 있는 뭔가의 중요성을 강조할 때
-   나쁜 주석
    -   대다수 주석이 나쁜 주석에 속한다
        -   코드는 자주 바뀌고 옮겨지지만, 현실적으로 주석까지 수정하는 프로그래머는 적다
        -   오래된 주석이 잘못된 정보를 제공하는 일이 자주 발생한다
    -   주절거리는 주석
        -   특별한 이유 없이 의무감으로 마지못해 다는 주석
        -   모든 함수에 Javadocs를 달거나 모든 변수에 주석을 달아야 한다는 규칙은 코드를 복잡하게 만든다
    -   같은 이야기를 중복하는 주석
        -   자칫하면 코드를 읽는 시간보다 주석을 읽는 시간이 더 길다
        -   주석은 코드보다 더 많은 정보를 제공해야 한다
        -   멤버 변수 하나하나에 모두 한 줄씩 주석을 달아놓는 경우도 포함된다
    -   오해할 여지가 있는 주석
        -   의도는 좋으나 엄밀하게 주석을 달지 못하는 경우도 있다
        -   주석으로 잘못된 정보를 제공하여 코드의 동작을 오해하게끔 하지 마라
    -   있으나 마나한 주석
        -   너무 당연한 사실을 굳이 언급하지 마라 ex) // 기본생성자
    -   함수나 변수로 표현할 수 있다면 주석을 달지 마라
        -   주석을 달고 코드를 작성 :x:
            ```Java
             // 전역 목록 <smodule>에 속하는 모듈이 우리가 속한 하위 시스템에 의존하는가?
             if (smodule.getDependSubsystems().contains(subSysMod.getSubSystem()))
            ```
        -   주석이 필요하지 않도록 코드를 개선 :white_check_mark:
            ```Java
             ArrayList moduleDependees = smodule.getDependSubsystems();
             String ourSubSystem = subSysMod.getSubSystem();
             if (moduleDpendees.contains(ourSubSystem))
            ```
    -   닫는 괄호에 다는 주석
        -   중첩이 굉장하고 장황한 함수라면 의미가 있을수도 있으나 우리가 선호하는 작은 함수에는 잡음이다
        -   위와 같이 긴 함수로 인해 달아야겠다는 생각이 들면? 함수를 줄이자
    -   공로를 돌리거나 저자를 표시하는 주석
        -   요즘은 소스 코드 관리 시스템이 알아서 해준다
        -   절대 주석으로 표현하지 마라
    -   주석으로 처리한 코드
        -   절대로 하지 마라
        -   그냥 하지 마라
    -   전역 정보
        -   주석을 달아야 한다면 근처의 코드만 기술하라
        -   일부에 주석을 달면서 시스템의 전반적인 정보를 기술하지 마라
        -   그 외부 정보가 바뀌었을 때 주석이 바뀌리라는 보장이 없다
    -   모호한 관계
        -   주석과 설명하려는 코드의 관계가 명확해야 한다
        -   ex) 배열의 사이즈에 숫자를 더하는데 `왜 더하는지` 알려줘야지, 무엇을 더한건지는 별로 도움이 되지 않는다

---

## 5장. 형식 맞추기

코드를 작성하는 규칙.

### 핵심 요약

-   프로그래머라면 깔끔한 형식에 맞춰 코드를 짜야 한다
-   형식을 맞추기 위해 간단한 규칙을 정하고 그 규칙을 착실히 따라야 한다

### 단락

-   형식을 맞추는 목적
    -   코드 형식은 의사소통의 일환이다
    -   맨 처음 잡아놓은 구현 스타일과 가독성 수준은 유지보수 용이성과 확장성에 계속 영향을 미친다
-   적절한 행 길이를 유지하라
    -   세로 길이
        -   계속 언급했듯이 짧을수록 좋다
        -   FitNesse의 경우 평균 파일 크기는 약 65줄
    -   신문 기사처럼 작성하라
        -   이름은 간단하면서도 설명이 가능하게 작명
        -   소스 파일의 첫 부분은 고차원 개념과 알고리즘을 설명
        -   아래로 내려갈수록 의도를 세세하게 묘사
        -   마지막에는 가장 저차원 함수와 세부 내역이 나타난다
-   개념은 빈 행으로 분리하라
    -   일련의 행 묶음은 완결된 하나의 생각을 표현한다
    -   생각 사이에는 빈 행을 넣어 분리해야 마땅하다
-   세로 밀집도
    -   줄바꿈이 개념을 분리한다면 세로 밀집도는 연관성을 의미한다
    -   서로 밀집한 코드 행은 세로로 가까이 놓여야 한다
    -   함수 연관 관계와 동작 방식을 이해하려고 이 함수 저 함수 오가며 소스코드를 탐색하면 혼란스럽다
    -   서로 밀접한 개념은 세로로 가까이 둬야 한다
-   변수 선언
    -   변수는 사용하는 위치에 최대한 가까이 선언한다
    -   루프를 제어하는 변수는 흔히 루프문 내부에 선언한다
    -   인스턴스 변수는 클래스 맨 처음에 선언한다
        -   변수간에 세로로 거리를 두지 않는다
-   종속 함수
    -   한 함수가 다른 함수를 호출한다면 두 함수는 세로로 가까이 배치한다
    -   또한 가능하다면 호출하는 함수를 호출되는 함수보다 먼저 배치한다
-   개념적 유사성
    -   개념적으로 비슷한 코드는 가까이 배치한다
        -   ```Java
              static public void assertTrue(String message, boolean condition);
              static public void assertTrue(boolean condition);
              static public void assertFalse(String message, boolean condition);
              static public void assertFalse(boolean ccondition);
            ```
-   가로 형식 맞추기
    -   가로행 역시 짧은 것이 바람직하다
        -   조사결과 20 ~ 60자 사이가 약 40%에 해당했다
    -   가로 공백과 밀집도
        -   할당 연산자 양 쪽에 공백을 줌으로써 왼쪽 요소와 오른쪽 요소를 분리
        -   함수이름과 이어지는 괄호에는 공백을 주지 않는다
        -   함수의 인수는 띄어쓰기
        -   수식에 곱셈은 붙이기, 나머지는 띄어쓰기 -> 자동 정렬로 지켜지지 않을 수 있다
    -   들여쓰기
        -   들여쓰기는 가독성을 높여준다
        -   짧은 코드의 들여쓰기를 무시하고 싶은 충동이 들어도 자제하자
-   팀 규칙
    -   개개인의 스타일로 일관성을 해치지 마라
    -   팀과 회의를 통해 규칙을 정하고 IDE 코드 형식기를 설정하라

---

## 6장. 객체와 자료구조

### 핵심 요약

-   클래스는 구현을 감춰야 한다
-   다른 클래스의 세부사항을 몰라도 사용할 수 있도록 디미터 법칙을 준수해라
-   자료구조와 객체의 trade-off를 잘 따지고 상황에 맞게 사용하라

### 단락

-   자료 추상화
    -   클래스는 구현을 감춰야 한다(캡슐화)
        -   변수를 private으로 설정해도 getter/setter를 제공한다면 구현을 외부로 노출하는것이나 마찬가지다
    -   구현을 감추기 위해선 추상화가 필요하다
        -   추상 인터페이스를 제공해 사용자가 구현을 모른 채 자료의 핵심을 조작할 수 있어야 진정한 의미의 클래스이다
        -   단순히 인터페이스 제공만으로 되는것은 아니다
    -   객체가 포함하는 자료를 표현할 가장 좋은 방법을 고민해야 한다
        -   아무 생각없이 getter/setter를 추가하는 방법이 가장 나쁘다
-   자료/객체 비대칭
    -   자료구조와 객체간에는 상호 보완적인 특징이 있다
        -   객체 지향에서 어려운 변경은 절차적 코드에서 쉽고 반대도 마찬가지이다
    -   자료구조
        -   자료를 그대로 공개하며 별다른 함수는 제공하지 않는다
        -   새로운 함수를 추가하더라도 기존의 자료구조에 아무런 영향을 미치지 않는다
        -   그러나 새로운 자료구조를 추가하고 싶다면 기존에 자료구조를 다루는 함수를 모두 고쳐야 한다
    -   객체
        -   추상화 뒤로 자료를 숨긴 채 자료를 다루는 함수만 제공한다
        -   새로운 객체를 추가하더라도 기존 함수에 아무런 영향을 미치지 않는다
        -   그러나 새로운 함수를 추가하고 싶다면 기존 클래스를 전부 고쳐야 한다
    -   결론
        -   새로운 자료 타입이 필요한 경우 클래스와 객체 지향 기법이 가장 적합
        -   새로운 자료 타입이 아니라 새로운 함수가 필요한 경우 절차적 코드와 자료구조가 더 적합
-   디미터 법칙
    -   자신이 조작하는 객체의 속사정을 몰라야 한다는 법칙
    -   정의 : 클래스 C의 메서드 f는 다음과 같은 객체의 메서드만 호출해야 한다
        -   클래스 C
        -   f가 생성한 객체
        -   f 인수로 넘어온 객체
        -   C 인스턴스 변수에 저장된 객체
    -   이를 위반하면 기차 충돌과 같은 `'.'`으로 연결된 긴 코드가 나타난다
        -   기차 충돌은 중간중간 변수로 받아서 표현하면 해결된다
    -   디미터 법칙을 위반하는 코드를 개선
        -   ```Java
                // 디미터 법칙 위반 & 기차 충돌 코드
                final String outputDir = ctxt.getOptions().getScratchDir().getAbsolutePath();
                // 디미터 법칙 준수
                BufferedOutputStream bos = ctxt.createScratchFileStream(classFileName);
            ```
        -   저렇게 바뀌는 이유는 예시에서 `outputDir`을 통해 결국 파일을 생성하기 위한 목적이었기 때문이다
-   자료 전달 객체
    -   자료 구조체의 전형적인 형태는 `public` 변수만 있고 함수가 없는 클래스
    -   DTO라고도 한다
    -   일반적인 형태는 `bean` 구조로 `private`변수를 `getter/setter` 함수로 조작하는 일종의 사이비 캡슐화 형태
    -   활성 레코드
        -   DTO의 특수한 형태로 `public`변수가 있거나 `private`변수에 `getter/setter` 함수가 있는 자료구조
        -   대개 save나 find같은 탐색 함수도 제공
        -   활성 레코드는 DB 테이블이나 다른 소스에서 자료를 직접 변환한 결과이다
        -   활성 레코드에 비즈니스 규칙 메서드를 추가하는것은 바람직하지 않다
            -   이러한 형태는 어느 축에도 속하지 않는 잡종 구조이다
        -   활성 레코드는 자료구조로 취급한다
            -   비즈니스 규칙을 담으면서 내부 자료를 숨기는 객체는 따로 생성해야 한다
            -   이 때 내부 자료는 활성 레코드의 형태일 가능성이 높음

---

## 7장. 오류 처리

### 핵심 요약

-   깨끗한 코드는 읽기도 좋아야 하지만 안정성도 높아야 한다
    -   이 둘은 상충되는 목표가 아니다
-   오류코드보단 예외를
-   예외 발생 가능한 코드는 `Try-Catch`블록부터 만들기
-   `unchecked exception`사용하기
-   wrapper 클래스 적극 활용
-   특수 사례 패턴
-   `null` 반환 금지, 인수로 넘기는 것도 금지

### 단락

-   오류 코드보다 예외를 사용하라
    -   오류 코드를 리턴하게되면 호출자에서 if문으로 분기처리를 하게 되므로 복잡해진다
    -   예외를 던지는 편이 더 깔끔하고 오류 처리 코드와 뒤섞이지 않게된다
-   `Try-Catch-Finally` 문부터 작성하라
    -   예외가 발생할 코드를 짤 때는 `try-catch-finally`문부터 시작해라
    -   try블록은 트랜잭션과 비슷하다
    -   catch블록은 프로그램 상태를 일관성 있게 유지해야 한다
    -   그러면 try 블록에서 무슨 일이 발생하든지 호출자가 기대하는 상태를 정의하기 쉬워진다
-   `Unchecked Exception`을 사용하라
    -   이건 논쟁이 끝난 일이다
    -   `checked exception`은 OCP를 위반한다
        -   하위 단계에서 코드를 변경하면 상위 단계 메서드 선언부를 전부 고쳐야 한다는 뜻이다
        -   모듈과 관련된 코드가 전혀 바뀌지 않았어도 선언부가 바뀌었기 때문에 모듈을 다시 빌드해야 한다
        -   throws 경로에 위치한 모든 함수가 최하위 함수에서 던지는 예외를 알아야 하므로 캡슐화가 깨진다
-   예외에 의미를 제공하라
    -   예외를 던질 때는 전후 상황을 충분히 덧붙인다
        -   호출 스택만으로 파악하기엔 부족하다
        -   오류 메세지에 실패한 연산 이름과 실패 유형도 언급한다
        -   애플리케이션이 로깅을 지원하면 catch블록에서 오류를 기록하도록 충분한 정보를 제공한다
-   호출자를 고려해 예외 클래스를 정의하라

    -   오류를 정의할 때 프로그래머에게 중요한 관심사는 **_오류를 잡아내는 방법_**이다
    -   오류를 잘 분류하는 방법

        -   ```JAVA
            // 형편없는 분류
             ACMEPort port = new ACMEPort(12);
             try {
                port.open();
             } catch (DeviceResponseException e) {
                reportPortError(e);
                logger.log("Device response exception",e);
             } catch (ATM1212UnlockedException e) {
                reportPortError(e);
                logger.log("Unlock exception",e);
             } catch (GMXError e) {
                reportPortError(e);
                logger.log("Device response exception",e);
             } finally {
                ...
             }

             // 예외 클래스를 정의하여 리팩토링한 코드
             LocalPort port = new LocalPort(12);
             try {
                port.open();
             } catch (PortDeviceFailure e) {
                reportPortError(e);
                logger.log(e.getMessage(),e);
             } finally {
                ...
             }
            ```

        -   여기서 LocalPort클래스는 단순히 ACMEPort 클래스가 던지는 예외를 잡아 변환하는 wrapper 클래스일 뿐이다
        -   ```Java
            public class LocalPort {
                private ACMEPort innerPort;

                public LocalPort(int portNumber) {
                    innerPort = new ACMEPort(portNumber);
                }

                public void open() {
                    try {
                        innerPort.open();
                    }  catch (DeviceResponseException e) {
                        throw new PortDeviceFailure(e);
                    } catch (ATM1212UnlockedException e) {
                        throw new PortDeviceFailure(e);
                    } catch (GMXError e) {
                        throw new PortDeviceFailure(e);
                    }
                }
            }
            ```

    -   이처럼 감싸기 클래스를 사용하는것은 특히 외부 API를 사용할 때 매우 유용하다
        -   외부 라이브러리와 프로글매 사이에 의존성이 크게 줄어들게 된다
        -   나중에 다른 라이브러리로 갈아타는 비용이 적다
        -   특정 업체가 API를 설계한 방식에 발목 잡히지 않는다

-   정상 흐름을 정의하라
    -   때로는 오류 발생 시 중단이 적합하지 않은 때도 있다
    -   ```Java
        try {
            MealExpenses expenses = expenseReportDAO.getMeals(emoloyee.getID());
            m_total += expenses.getTotal();
        } catch(MealExpensesNotFound e) {
            m_total += getMealPerDiem();
        }
        ```
    -   위 코드의 비즈니스 로직은 다음과 같다
        -   식비를 비용으로 청구했을시 청구한 식비를 총계에 더한다
        -   식비를 비용으로 청구하지 않았다면 일일 기본 식비를 총계에 더한다
        -   그러나 예외로 인해 코드만 봐서는 위의 논리를 따라가기 어렵다
    -   특수 상황을 처리할 필요가 없다면 다음과 같이 훨씬 코드가 간결해진다
        -   ```Java
            MealExpenses expenses = expenseReportDAO.getMeals(emoloyee.getID());
            m_total += expenses.getTotal();
            ```
        -   ExpenseReportDAO를 고쳐 언제나 `MealExpenses`객체를 반환하도록 하였고, 청구한 식비가 없다면 일일 기본 식비를 반환하는 `MealExpenses`객체를 반환하도록 하였다
        -   ```Java
              public class PerDiemMealExpenses implements MealExpenses {
                  public int getTotal() {
                      // 기본값으로 일일 기본 식비를 반환한다
                  }
              }
            ```
        -   이러한 것을 특수 사례 패턴이라 부른다
            -   클래스를 만들거나 객체를 조작해 특수 사례를 처리하는 방식이다
            -   클래스나 객체가 예외 상황을 캡슐화해서 처리하므로 클라이언트 코드가 예외를 처리할 필요가 없어진다
-   `null`을 반환하지 마라
    -   아주 흔히 저지르는 실수다
    -   호출자에서 계속 `null`을 체크하는 코드가 생기게 된다
    -   호출자에게 문제를 넘기는 나쁜 코드다
    -   누군가 `null` 체크를 빼먹는다면 애플리케이션이 통제 불능에 빠질지도 모른다
    -   메서드에서 `null`을 반환하고 싶은 충동이 들면 예외를 던지거나 특수 사례 객체를 반환해라
        -   외부 API가 null을 반환한다면 wrapper 클래스로 처리해라
    -   다음 코드의 `getEmployees`는 null도 반환한다
    -   ```Java
        List<Employee> employees = getEmployees();
        if (employees != null) {
            for(Employee e: employees) {
                totalPay += e.getPay();
            }
        }
        ```
    -   하지만 `getEmployees`를 변경해 빈 리스트(`Collections.emptyList()`)를 반환한다면 코드가 훨씬 깔끔해진다
    -   ```Java
        List<Employee> employees = getEmployees();
        for(Employee e: employees) {
            totalPay += e.getPay();
        }
        ```
-   `null`을 전달하지 마라
    -   반대로 메서드로 `null`을 인수로 전달하는 방식은 더 나쁘다
    -   인수로 `null`이 들어왔을 때 다른 예외를 던지는 것은 결국 문제를 해결하지 못한다
    -   그렇다면 애초에 `null`을 넘기지 못하도록 금지하는 정책이 합리적이다
