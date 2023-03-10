# Number 메서드

## 유한한 수인지 확인하기

1. Number.isFinite() vs isFinite()

   👉 Number.isFinite: 정말 유한한 수인 경우에 true

   👉 isFinite(): 인수를 한번 처리하고 유한수인지 확인하기 때문에 true = 1로 처리됨.

   👉 인수에 따른 반환값

   |       인수       | Number.isFinite() |              isFinite()              |
   | :--------------: | :---------------: | :----------------------------------: |
   |       개념       |    유한수 판단    | 유한수 판단하는 <br>빌트인 전역 함수 |
   |        0         |     **true**      |               **true**               |
   |       100        |     **true**      |               **true**               |
   |       -13        |     **true**      |               **true**               |
   |      1.3578      |     **true**      |               **true**               |
   |    -54.573277    |     **true**      |               **true**               |
   |     2\*\*53      |     **true**      |               **true**               |
   |    2\*\*53-1     |     **true**      |               **true**               |
   |       "1"        |       false       |               **true**               |
   |       true       |       false       |               **true**               |
   |      false       |       false       |               **true**               |
   |    undefined     |       false       |                false                 |
   |       NaN        |       false       |                false                 |
   |     Infinity     |       false       |                false                 |
   |    -Infinity     |       false       |                false                 |
   |   [ 0, 0, 0 ]    |       false       |                false                 |
   | { a: 10, b: 20 } |       false       |                false                 |

<br>
<br>

## 정수인지 확인하기

2.  Number.isInteger() vs Number.isSafeInteger()

    👉 Number.isInteger: 정수인 경우에 true

    👉 Number.isSafeInteger(): 2^53부터는 안전하지 않아 false

    👉 인수에 따른 반환값

    |    인수    | Number.isInteger() | Number.isSafeInteger() |
    | :--------: | :----------------: | :--------------------: |
    |    개념    |     정수 판단      |  안전한 && 정수 판단   |
    |     0      |      **true**      |        **true**        |
    |    100     |      **true**      |        **true**        |
    |    -13     |      **true**      |        **true**        |
    |   1.3578   |       false        |         false          |
    | -54.573277 |       false        |         false          |
    |  2\*\*53   |      **true**      |         false          |
    | 2\*\*53-1  |      **true**      |        **true**        |
    |    "1"     |       false        |         false          |

<br>

## 문자형으로 반환

3.  Number.prototype.toExponential vs Number.prototype.toPrecision

    👉 Number.prototype.toExponential

         - 기본형: (0.0).toExponential(0~100);
         - 변형(비권장): 0.0.toExponential(0~100)
         - 변형(비권장): (0).toExponential(0~100);
         - 결과: "0.0e+0";

    👉 Number.prototype.toPrecision

         - 입력: (0.0).toPrecision(1~100);
         - 결과: "00.000"/"0.0e+0";

    👉 인수에 따른 반환값

    | 인수 | (123.456).toExponential(인수) | (123.456).toPrecision(인수) |
    | :--: | :---------------------------: | :-------------------------: |
    |      |         "1.23456e+2"          |          "123.456"          |
    |  0   |         "1.23456e+2"          |              -              |
    |  1   |           "1.2e+2"            |           "1e+2"            |
    |  2   |           "1.23e+2"           |          "1.2e+2"           |
    |  3   |          "1.235e+2"           |            "123"            |
    |  5   |         "1.23456e+2"          |          "123.46"           |

<br>

    👉 지수표기법(chatGPT) : 과학적 표기법이라고도 하는 **지수 표기법**은 매우 크거나 매우 작은 숫자를 간결하고 편리한 방식으로 나타내는 방법입니다. 이 표기법은 숫자를 10의 제곱으로 곱한 계수로 표현합니다. 여기서 10의 제곱은 소수점이 왼쪽이나 오른쪽으로 이동한 자리 수를 나타냅니다.
    코딩에서 지수 표기법은 수학적 또는 과학적 계산을 처리할 때와 같이 매우 크거나 매우 작은 숫자로 작업할 때 자주 사용됩니다. 지수 표기법을 사용하면 숫자 정밀도 문제를 방지하고 크거나 작은 값과 관련된 계산을 더 쉽게 수행할 수 있습니다..
    지수 표기법의 또 다른 이점은 코드를 더 읽기 쉽고 이해하기 쉽게 만들 수 있다는 것입니다. 숫자의 자릿수를 줄이는 데 도움이 될 수 있으므로 코드가 덜 어수선해지고 읽기 쉬워집니다. 또한 지수 표기법을 사용하면 동일한 숫자를 다른 기준 또는 다른 정밀도 수준으로 나타내는 데 사용할 수 있으므로 코드의 이식성을 높일 수 있습니다.
    전반적으로 지수 표기법은 매우 크거나 작은 숫자를 표현하고, 숫자 정밀도를 개선하고, 코드를 더 읽기 쉽고 이식 가능하게 만드는 코딩에 유용한 도구입니다.
    지수 표기법에는 많은 이점이 있지만 고려해야 할 몇 가지 잠재적인 단점도 있습니다.

    1. 소수점 값의 어려움: 지수 표기법은 특히 소수 자릿수가 많은 소수점 값을 표현하기 어렵게 만들 수 있습니다. 예를 들어, 숫자 0.000000001은 1 x 10^-9로 쓸 수 있지만, 이 표기는 익숙하지 않은 사람들에게는 혼란스러울 수 있습니다.

    2. 정밀도 손실 가능성: 프로그래밍 언어 또는 시스템의 구현에 따라 지수 표기법으로 인해 계산 정밀도가 떨어질 수 있습니다. 이것은 시스템이 너무 크거나 작아서 정확히 표현할 수 없는 숫자의 값을 반올림하거나 대략적으로 계산할 때 발생할 수 있습니다.

    3. 일부 사용자의 가독성 부족: 지수 표기법을 사용하면 일부 사용자는 코드를 더 쉽게 읽을 수 있지만 이 표기법에 익숙하지 않은 다른 사용자는 코드를 덜 읽을 수 있습니다. 특히 프로그래밍을 처음 접하거나 수학에 익숙하지 않은 사람들은 지수 표기법이 혼란스럽거나 겁이 날 수 있습니다.

    4. 인간 입력의 어려움: 지수 표기법은 특히 표현되는 값이 복잡하거나 소수 자릿수가 많은 경우 인간이 입력하거나 읽기 어려울 수 있습니다. 이로 인해 사용자가 키보드나 기타 입력 장치를 사용하여 값을 입력하거나 조작하기가 더 어려워질 수 있습니다.

    전반적으로 지수 표기법은 코딩에 많은 이점이 있지만 코드에서 사용하기 전에 제한 사항과 잠재적인 단점을 인식하는 것이 중요합니다.

<br>

4.  Number.prototype.toFixed

    👉 반올림하여 문자값 반환

    👉 숫자/인수에 따른 반환 값

    |  숫자  | Number.toFixed(0) | Number.toFixed(1) | Number.toFixed(5) |
    | :----: | :---------------: | :---------------: | :---------------: |
    | 1.1234 |        "1"        |       "1.1"       |     "1.12340"     |
    |  5.67  |        "6"        |       "5.7"       |     "5.67000"     |
    |  13.5  |       "14"        |      "13.5"       |    "13.50000"     |
    | 776.43 |       "776"       |      "776.4"      |    "776.43000"    |
    |  2.46  |        "2"        |       "2.5"       |     "2.46000"     |

<br>

5.  Number.prototype.toString

    👉 진법에 따라 변환 후 문자값으로 반환

    👉 인수가 없으면 기본 10진법

    👉 인수에 따른 반환 값

    | 인수 | (16).toString() |
    | :--: | :-------------: |
    |      |      "16"       |
    |  2   |     "10000"     |
    |  8   |      "20"       |
    |  10  |      "16"       |
    |  16  |      "10"       |

<br><br>

# Math 메서드

## 절대값/지수..

1. Math.abs() vs Math.sqrt() vs Math.pow()

   👉 Math.abs() : 절대값(0/양수)으로 변환

   👉 Math.sqrt() : 제곱근 변환

   👉 Math.pow(밑, 지수) : 거듭제곱 변환

   👉 인수에 따른 반환 값

   |       인수       |  Math.abs(인수)  |  Math.sqrt(인수)   |    Math.pow(2,인수)    |
   | :--------------: | :--------------: | :----------------: | :--------------------: |
   |       개념       |   절대값 반환    |    제곱근 반환     |     거듭제곱 반환      |
   |        0         |        0         |         0          |           1            |
   |       100        |       100        |         10         | 1.2676506002282294e+30 |
   |       -13        |        13        |        NaN         |    0.0001220703125     |
   |      1.3578      |      1.3578      | 1.1652467549836816 |   2.562940524692071    |
   |    -54.573277    |    54.573277     |        NaN         | 3.7308403173367306e-17 |
   |     2\*\*53      | 9007199254740992 | 94906265.62425156  |        Infinity        |
   |    2\*\*53-1     | 9007199254740991 | 94906265.62425154  |        Infinity        |
   |                  |       NaN        |        NaN         |                        |
   |       "1"        |        1         |         1          |          NaN           |
   |       true       |        1         |         1          |           2            |
   |      false       |        0         |         0          |           1            |
   |    undefined     |       NaN        |        NaN         |          NaN           |
   |       NaN        |       NaN        |        NaN         |          NaN           |
   |       null       |        0         |         0          |           1            |
   |     Infinity     |     Infinity     |      Infinity      |        Infinity        |
   |    -Infinity     |     Infinity     |        NaN         |           0            |
   |   [ 0, 0, 0 ]    |       NaN        |        NaN         |          NaN           |
   | { a: 10, b: 20 } |       NaN        |        NaN         |          NaN           |

<br>

## 첫 번째 소수점 처리

2.  Math.round() vs Math.ceil() vs Math.floor()

    👉 Math.round() : 반올림 변환

    👉 Math.ceil() : 올림 변환

    👉 Math.floor() : 내림 변환

    👉 인수에 따른 반환 값

    |       인수       | Math.round(인수) | Math.ceil(인수)  | Math.floor(인수) |
    | :--------------: | :--------------: | :--------------: | :--------------: |
    |       개념       |   반올림 반환    |    올림 반환     |    내림 반환     |
    |        0         |        0         |        0         |        0         |
    |       100        |       100        |       100        |       100        |
    |       -13        |       -13        |       -13        |       -13        |
    |      1.3578      |        1         |        2         |        1         |
    |    -54.573277    |     **-55**      |       -54        |       -55        |
    |     2\*\*53      | 9007199254740992 | 9007199254740992 | 9007199254740992 |
    |    2\*\*53-1     | 9007199254740991 | 9007199254740991 | 9007199254740991 |
    |       "1"        |        1         |        1         |        1         |
    |       true       |        1         |        1         |        1         |
    |      false       |        0         |        0         |        0         |
    |    undefined     |       NaN        |       NaN        |       NaN        |
    |       NaN        |       NaN        |       NaN        |       NaN        |
    |       null       |        0         |        0         |        0         |
    |     Infinity     |     Infinity     |     Infinity     |     Infinity     |
    |    -Infinity     |     Infinity     |     Infinity     |     Infinity     |
    |   [ 0, 0, 0 ]    |       NaN        |       NaN        |       NaN        |
    | { a: 10, b: 20 } |       NaN        |       NaN        |       NaN        |

<br>

## 큰수/작은수 반환

3.  Math.max() vs Math.min()

    👉 Math.max() : 가장 큰 값 반환

    👉 Math.min() : 가방 작은 값 반환

    👉 특징

        - ()안에 요소들을 넣어야 함. array로 넣을 수 없음.
        - ()안에 빈 array([])를 넣으면 둘다 0이 출력됨.

    👉 인수에 따른 반환 값

    |        인수        | Math.max(...인수) | Math.min(...인수) |
    | :----------------: | :---------------: | :---------------: |
    |        개념        |    반올림 반환    |     올림 반환     |
    |         []         |   **-Infinity**   |   **Infinity**    |
    |        [0]         |         0         |         0         |
    |      [1,2,3]       |         3         |         1         |
    |    [-100,0,100]    |        100        |       -100        |
    |    [-22,-4,-1]     |        -1         |        -22        |
    |  [Infinity,0,100]  |     Infinity      |         0         |
    | [-Infinity,0,-100] |         0         |     -Infinity     |
    |     ["1",0,-1]     |         1         |        -1         |
    |     ["a",0,1]      |        NaN        |        NaN        |
    |     [true, -1]     |         1         |        -1         |
    |    [false, -1]     |         0         |        -1         |
    |     [NaN, -1]      |        NaN        |        NaN        |
    |     [null, -1]     |         0         |        -1         |
    |  [undefined, -1]   |        NaN        |        NaN        |

<br>

## 기타

4. Math.random

   👉 반환: 임의의 난수(0 이상 1미만) 생성 후 반환
