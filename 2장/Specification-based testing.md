## 명세 기반 테스트

- 명세 기반 테스트 기법을 적용하여 테스트 케이스를 작성하는 방법
- 프로그램 경계에 대한 테스트 케이스를 식별하고 작성하는 방법
### 💡 테스트를 도출하는 방법 7단계

```java
//str="axcaycaszc", open="a" close="c"라면, 출력은 ["x","y","z"] 가 된다.

public static String[] substringsBetween(final String str, final String open,final String close){
    if(str == null || isEmpty(open) || isEmpty(close)){
        return null;
    }

    int strlen = str.length();
    if(strlen == 0){
        return EMPTY_STRING_ARRAY;
    }

    int closeLen = close.length();
    int openLen = open.length();
    List<String> list = new ArrayList<>();
    int pos = 0;

    while (pos< strlen - closeLen){
        int start = str.indexOf(open, pos);

        if (start < 0){
            break;
        }
        start += openLen;
        int end = str.indexOf(close, start);
        if (end < 0 ){
            break;
        }

        list.add(str.substring(start, end));
        pos = end + closeLen;
    }
    if (list.isEmpty()){
        return null;
    }

    return list.toArray(EMPTY_STRING_ARRAY);
}
```

![Alt text](https://yihanseul.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F20d85277-ace6-4709-86c2-ef3c2a5a1f27%2F5e27d33b-ae16-4e74-8ebc-a3159ccea305%2FUntitled.png?table=block&id=b81a6d9d-7f38-4217-8063-325b683b1479&spaceId=20d85277-ace6-4709-86c2-ef3c2a5a1f27&width=1230&userId=&cache=v2)

1. 요구사항 이해
    - 요구사항에 대한 전반적 이해
    - 수행해야 하는 것/ 하지말아야하는ㄴ것
    - 코너 케이스
    - 입출력 변수 타입과 범위
    - 예시)
        - 프로그램 또는 메서드는 무엇을 수행해야하는지 확인
        - 어떤 데이터를 입력받는지 확인
        - 출력에 대한 추론 프로그램이 무엇을 수행하고 입력이 어떻게되는지 기대하는 출력값으로 변환하는지 확인
2. 프로그램 탐색
    - 프로그램을 직접 실행시켜보기(다양한 입력값으로 프로그램을 테스트해서 프로그램이 무엇을 출력하는지 확인)
    - 예시)
        - str = “abcd” , open=”a”, close =”d”
3. 구획 식별
    - 입력값의 범위 살피기( 변수의 타입을 살펴보고 정수형인지 문자열인지 받을 수 있는 값 범위 확인)
    - 각 변수 간의 상호작용을 살펴보기 변수는 종종 서로의 의존성이나 제약이 있
    - 출력값의 범위 살피기, 테스트 범위 정하기
    - 예시)
        - 어떤값을 넣어야하는가? 형은 어떤형인가?
        - 매개변수마다 null, 빈문자일경우 길이가 1일경우, 길이가 1보다 큰 문자열일경우를 고려함
4. 경계 분석
    - 경계 분석해서 목록에 추가
    - ex) 경계에있는 부분을 테스트를 하고 1~7이런 숫자는 다 할 필요없음
    
    ![“hiphip”과 “hooray” 구획 사이의 경계. 9까지의 숫자의 “hiphip” 구획에 속하고 9 이상의 숫자는 “hooray” 구획에 속한다.](https://yihanseul.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F20d85277-ace6-4709-86c2-ef3c2a5a1f27%2F6166a881-8e6e-4974-bc20-3994efffb378%2FUntitled.png?table=block&id=4ae6dff8-0203-44ae-b47e-751a1d274538&spaceId=20d85277-ace6-4709-86c2-ef3c2a5a1f27&width=610&userId=&cache=v2)
    
    “hiphip”과 “hooray” 구획 사이의 경계. 9까지의 숫자의 “hiphip” 구획에 속하고 9 이상의 숫자는 “hooray” 구획에 속한다.
    
    - 내점 : 조건이 참인 점 (11, 12, 25, 42)
    - 외점 : 조건이 거짓인 점 (8, 7, 2, -42)
5. 테스트 케이스 고안
    - 예외 케이스는 한 번만 테스트
    - ex) 널 문자열 구획은 한 번만 테스트하면 더 이상은 필요가 없다.
    - ex) 빈 문자열인 경우도 마찬가지로 단 하나의 테스트면 충분하다.
    - 예시)
        - 입력,출력,경계를 구분했으니 이때 테스트 케이스를 만든다.
6. 테스트 자동화 JUnit
    - vitest 와 같은 툴 이용하기
    - 테스트 중복 줄이기
    - 실패 시 알아보기 편하도록 하기
7. 강화(창의성과 경험)
    - 최종 점검
    - 테스트 고도

### 💡 실용적인 명세 테스트
---

- 단위에서의 가능한 한 조합의 수를 줄인다.
    - 도메인 지식을 활용해서 적용되지 않는 케이스를 제거하라
    - 다른 동작과 동떨어진 엣지 케이스를 테스트를 중심으로 테스트하자
- 메서드 수준에서 많은 조합이 발생하면 메서드를 분리하는 것이 좋을 수 있다.

### 💡합리적인 테스트
---

- 테스트 범위가 아닌 것에 대해서는 현실적인 값음 사용하자.( 자주 사용하는 값, 계산이 쉬운값.)

### 💡 현업에서의 명세 테스트
---

1. 프로세스는 연속적이 아니라 반복적이어야 한다.
2. 명세 테스트는 어느 정도로 수행해야 하는가?
3. 구획인가, 경계인가? 그것은 중요하지 않다!
4. 접점과 거점으로도 충분하지만 내점과 외점도 얼마든지 추가하자
5. 이해를 높이기 위해 입력을 변경해서 사용하자
6. 조합의 수가 폭발적으로 증가하나면 실용적이어야 한다.
7. 무엇을 입력할지 모르겠다면 간단한 입력을 넣어보자.
8. 관심 없는 입력에 대해 합리적인 값을 선택하자
9. 널과 예외 케이스는 의미가 있을 때만 사용하자
10. 테스트가 동일한 스켈레톤을 갖는 경우 매개변수화 테스트를 사용하자
11. 요구사항은 잘게 쪼갤 수 있다.
12. 이것은 클래스와 상태에 어떻게 동작하는가?
13. 경험과 창의성의 역할
<br>

### ✏️ 정리
<hr>

```

1. 요구사항은 테스트를 만드는 데 가장 중요한 참고자료다.
2. 명세 기반 텟트 기법은 체계적인 방식으로 요구사항을 살펴보는 더 도움된다.
  ex) 명세기반 테스트 기법은 사용하여 여러 입력변수의 도메인 공간과 변수가 어떻게 상호작용 하는 지를 조사할 수 있다.
3. 명세 테스트 7단계 접근법 제안
4. 버그는 경계를 좋아한다. 하지만 경계는 식별하는 일은 명세 테스트에서 가장 어려운 부분일 수 있다.
5. 단순한 프로그램에서도 테스트 케이스의 수가 매우 늘어날 수 있다. 무엇을 테스트해야 하는지, 무엇을 테스트해서는 안 되는지를 결정해야한다.
```