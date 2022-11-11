```c
#include <stdio.h> // 이 파일의 니용을 가져옴(함수호출에 필요한 정보 존재)
int main (void) // 출력형태 함수이름 입력형태
{
	printf("hello"); // 함수의 몸체 (표현된 함수의 기능)
    return 0; // 함수를 호출한 영역으로 값을 전달(반환), 현재 실행중인 함수의 종료
}
```
문장의 끝은 세미콜론을 붙임; (줄 바뀜은 문장의 바뀜을 의미하는 것이 아님)
/* (여러 문장을 주석처리할 때 사용)
	문장1
	문장2
    문장3
\*/ [행 단위 주석(//)과 중복사용 불가]

변수 이름 규칙
1. 변수의 이름은 알파벳, 숫자, 언더바(_)로 구성
2. C언어는 대소문자 구분, 변수Num과 num은 서로 다른 변수
3. 숫자로 시작할 수 없고, 키워드도 변수의 이름으로 사용 불가
4. 이름 사이 공백 삽입 불가

변수 종류
1. 정수형 변수 : char, short, int, long
2. 실수형 변수 : float, double

||산술 연산자||복합 대입 연산자|
|:|:|:|:|
|더하기|+|a = a + b|a += b|
|빼기|-|a = a - b|a -= b|
|곱하기|\*|a = a * b|a \*= b|
|나누기|/|a = a / b|a /= b|
|나머지|%|a = a %  b|a %= b|

증감 연산자
++num 또는 --num (선 증가 또는 감소, 후 연산)
num++ 또는 num-- (후 증가 또는 감소, 선 연산)

2진수 : 0과 1로 구성, 두 개의 기호를 이용해서 값을 표현하는 방식
10진수 : 0~9로 구성, 열 개의 기호를 이용해서 값을 표현하는 방식
16진수 : 0~9와A~F로 구성, 16개의 기호를 이용해서 값을 표현하는 방식

컴퓨터 메모리의 주소 값은 1바이트당 하나의 주소가 할당
11111111 // 오른쪽부터 2^0~2^7

int num1 = 10; // 10진수의 표현
int num2 = 0xA; // 0x로 시작하면 16진수로 인식
int num3 = 012; // 0으로 시작하면 8진수로 인식

00000101
첫 번째 비트를 MSB(Most Significant Bit)라 한다(부호+,-를 나타낸다)

음의 정수 표현 방식
00000101 (정수 +5) -> 1의 보수를 취함 11111010 -> 1을 더함 11111011 (정수 -5)
 &nbsp 00000101 (+5)
+11111011 (-5)
\-------------
 &nbsp 100000000(올림수는 버려져서 0)

실수 표현식[±(1.m)X2^e-127]

|부호의 표현|e|m|
|:|:|:|
|1|00000001|00000101|
비트연산자

|연산지|연산자의 기능|결합 방향|
|:|:|:-:|
|&|비트단위로 AND 연산을 한다.<br/> ex)num1 & num2;|->|
|\||비트단위로 OR 연산을 한다<br/> ex)num1 \| num2;|->|
|^|비트단위로 XOR 연산을 한다.<br/> ex)num1 ^ num2;|->|
|~|단항 연산자로서 피연산자의 모든 비트를 반전시킨다.<br/> ex)~num; // num은 변화 없음, 반전 결과만 반환|<-|
|<<|피연산자의 비트 열을 왼쪽으로 이동시킨다.<br/> ex)num<<2; // num은 변화 없음, 두 칸 왼쪽 이동 결과만 반환|->|
|>>|피연산자의 비트 열을 오른쪽으로 이동시킨다.<br/> ex)num>>2; // num은 변화 없음, 두 칸 오른쪽 이동 결과만 반환|->|

&연산자 : 비트단위 AND
```c
#include <stdio.h>
int main(void) {
	int num1 = 15; // 00000000 00000000 00000000 00001111
    int num2 = 20; // 00000000 00000000 00000000 00010100
    int num3 = num1 & num2;
    printf("AND 연산의 결과: %d \n", num3);
    return 0;
}
```
```
  00000000 00000000 00000000 00001111
& 00000000 00000000 00000000 00010100
--------------------------------------
  00000000 00000000 00000000 00000100 // 4
```
\|연산자 : 비트단위 OR
```c
#include <stdio.h>
int main(void) {
	int num1 = 15; // 00000000 00000000 00000000 00001111
    int num2 = 20; // 00000000 00000000 00000000 00010100
    int num3 = num1 | num2;
    printf("OR 연산의 결과: %d \n", num3);
    return 0;
}
```
```
  00000000 00000000 00000000 00001111
| 00000000 00000000 00000000 00010100
--------------------------------------
  00000000 00000000 00000000 00011111 // 31
```
^연산자 : 비트단위XOR
```c
#include <stdio.h>
int main(void) {
	int num1 = 15; // 00000000 00000000 00000000 00001111
    int num2 = 20; // 00000000 00000000 00000000 00010100
    int num3 = num1 ^ num2;
    printf("XOR 연산의 결과: %d \n", num3);
    return 0;
}
```
```
  00000000 00000000 00000000 00001111
^ 00000000 00000000 00000000 00010100
--------------------------------------
  00000000 00000000 00000000 00011011 // 27
```
~연산자
```c
#include <stdio.h>
int main(void) {
	int num1 = 15; // 00000000 00000000 00000000 00001111
    int num2 = ~num1;
    printf("NOT 연산의 결과: %d \n", num2);
    return 0;
}
```
```
~연산 전 : 00000000 00000000 00000000 00001111
~연산 후 : 11111111 11111111 11111111 11110000
```
<<연산자 : 비트의 왼쪽 이동(shift)
```c
#include <stdio.h>
int main(void) {
	int num1 = 15; // 00000000 00000000 00000000 00001111
    int result1 = num<<1;
    int result2 = num<<2;
    int result3 = num<<3;
    printf("1칸 왼쪽 이동 결과 : %d \n", result1);
    printf("2칸 왼쪽 이동 결과 : %d \n", result2);
    printf("3칸 왼쪽 이동 결과 : %d \n", result3);
    return 0;
}
```
```
result1 : 00000000 00000000 00000000 00011110 // 10진수로 30
result2 : 00000000 00000000 00000000 00111100 // 10진수로 60
result3 : 00000000 00000000 00000000 01111000 // 10진수로 120
왼쪽으로 한 칸씩 이동할 때마다 정수의 값 2배 증가
```
\>>연산자 : 비트의 오른쪽 이동(shift)
```c
#include <stdio.h>
int main(void) {
	int num = -16; // 11111111 11111111 11111111 11110000
    printf("2칸 오른쪽 이동 결과 : %d \n", num>>2);
    printf("3칸 오른쪽 이동 결과 : %d \n", num>>3);
    return 0;
}
```
```
num>>2 : -4
num>>3 : -2
```
자료형 종류 & 데이터의 표현 범위

<table>
  <tr>
    <th colspan="2">자료형</th>
    <th>크기</th>
    <th>값의 표현 범위</th>
  </tr>
  <tr>
    <td rowspan="5">정수형</td>
    <td>char</td>
    <td>1byte</td>
    <td>-128 ~ +127</td>
  </tr>
  <tr>
    <td>short</td>
    <td>2byte</td>
    <td>-32,768 ~ +32,767</td>
  </tr>
  <tr>
    <td>int</td>
    <td>4byte</td>
    <td>-2,147,483,648 ~ +2,147,483,647</td>
  </tr>
  <tr>
    <td>long</td>
    <td>4byte</td>
    <td>-2,147,483,648 ~ +2,147,483,647</td>
  </tr>
  <tr>
    <td>long long</td>
    <td>8byte</td>
    <td>-9,223,372,036,854,775,808 ~ +9,223,372,036,854,775,807</td>
  </tr>
  <tr>
    <td rowspan="3">실수형</td>
    <td>float</td>
    <td>4byte</td>
    <td>±3.4X10^-37 ~ ±3.4X10^+38</td>
  </tr>
  <tr>
    <td>double</td>
    <td>8byte</td>
    <td>±1.7X10^-307 ~ ±1.7X10^+308</td>
  </tr>
  <tr>
    <td>long double</td>
    <td>greater than 8byte</td>
    <td>double 이상의 표현 범위</td>
</table>

sizeof를 이용한 바이트 크기 확인
```c
#include <stdio.h>
int main(void) {
	int num = 10;
    int sz1 = sizeof(num);
    int sz2 = sizeof(int);
    return 0;
}
```
```c
#include <stdio.h>
int main(void) {
	char num1 = 1, num2 = 2, result1 = 0;
    short num3 = 3, num4 = 4, result2 = 0;
    printf("%lu \n", sizeof(num1 + num2));
    printf("%lu \n", sizeof(num3 + num4));
    result1 = num1 + num2;
    result2 = num3 + num4;
    printf("%lu \n", sizeof(result1));
    printf("%lu \n", sizeof(result2));
    return 0;
}
```
```
sizeof는 무부호 정수형, 가장 안전하게 형치환하는 방법은 unsigned long(%lu)로 출력
unsigned : 값의 표현 범위를 더함
ex) char : -128 ~ +127
	unsigned char : 0 ~ (128+127)
```
입력과 출력
```c
#include <stdio.h>
int main(void) {
  int num;
  int times;
  printf("입력 : ");
  scanf("%d", &num); //입력
  times = num * 2;
  printf("%d", times); // 출력
  return 0;
}
```
특수문자의 종류

|특수문자|의미|
|:|:|
|`\`a|경고음|
|`\`b|백스페이스|
|`\`f|폼 피드|
|`\`n|개 행|
|`\`r|캐리지 리턴|
|`\`t|수평 탭|
|`\`v|수직 탭|
|`\`'|작은 따옴표 출력|
|`\`"|큰 따옴표 출력|
|`\`?|물음표 출력|
|`\\`|역슬래쉬 출력|
`\f`와 `\v`는 프린터 출력을 위해 정의된 특수문자, 모니터 출력에 사용 시 이상한 문자 출력

서식문자의 종류

|서식문자|출력 대상(자료형)|출력 형태|
|:-:|:-:|:-:|
|%d|char, short, int|부호 있는 10진수 정수|
|%ld|long|부호 있는 10진수 정수|
|%lld|long long|부호 있는 10진수 정수|
|%u|unsigned int|부호 없는 10진수 정수|
|%o|unsigned int|부호 없는 8진수 정수|
|%x, %X|unsigned int|부호 없는 16진수 정수|
|%f|float, double|10진수 방식의 부동소수점 실수|
|%Lf|long double|10진수 방식의 부동소수점 실수|
|%e, %E|float, double|e 또는 E 방식의 부동소수점 실수|
|%g, %G|float, double|값에 따라 %f와 %e 사이에서 선택|
|%c|char, short, int|값에 대응하는 문자|
|%s|char \*|문자열|
|%p|void \*|포인터 주소 값|

\#을 이용한 n진수 표현
```c
#include <stdio.h>
int main(void){
	int num1 = 7, num2 = 13;
    printf("%o %#o \n", num1, num1); //8진수 양의 정수의 형태로 입력
    printf("%x %#x \n", num2, num2); // 16진수 양의 정수의 형태로 입력
    return 0;
}
```
```
7 07
d 0xd
```
실수 출력 e표기법

|실수|지수 표기법|e 표기법|
|:-:|:-:|:-:|
|0.00000000000000000001|1.0X10^-20|1.0e-20|
|1,200,000,000,000|1.2X10^+12|1.2e+12|
|0.00000000000115|1.15X10^-12|1.15e-12|

\%g의 실수 출력
```c
#include <stdio.h>
int main(void){
	double d1=1.23e-3;
    double d2=1.23e-4;
    double d3=1.23e-5;
    double d4=1.23e-6;
    int d5=1000000;
    int d6=999999;
    printf("%g \n", d1);
    printf("%g \n", d2);
    printf("%g \n", d3);
    printf("%g \n", d4);
    printf"%%g의 %%e 출력 : %d 이상 / %%g의 %%f 표현 출력 : %d 이하 \n", d5, d6);
    return 0;
}
```
```
0.00123 
0.000123 
1.23e-05 
1.23e-06 
%g의 %e 출력 : 1000000 이상 / %g의 %f 표현 출력 : 999999 이하
```
필드 폭을 지정하여 정돈된 출력 보이기
```c
#include <stdio.h>
int main() {
    printf("%6s %10s %4s \n", "이  름", "naver", "학년");
    printf("%6s %10s %4d \n", "홍길동", "daum", 3);
    printf("%6s %10s %4d \n", "손오공", "kakao", 2);
    printf("%6s %10s %4d \n", "박효신", "baemin", 4);
    return 0;
}
```
```
이  름      naver 학년 
홍길동       daum    3 
손오공      kakao    2 
박효신     baemin    4 
```
실수 기반 입력 형태
데이터 출력 : %f = float, double / %Lf = long double
데이터 입력 : %f = float / %lf = double / %Lf = long double

while
```c
#include <stdio.h>
int main() {
    int num=0;
    while(num<3) {
        printf("Hello world %d \n", num);
        num++;
    }
    return 0;
}
```
do~while
```c
#include <stdio.h>
int main() {
    int total=0, num=0;
    do {
        printf("정수 입력(0 to quit): ");
        scanf("%d", &num);
        total+=num;
    }while(num<10);
    printf("합계: %d \n", total);
    return 0;
}
```
for
```c
int num = 0;
while(num<3){
	printf("Hello");
	num++;
}
```
while을 for문으로
```c
for(int num=0; num<3; num++) // for(초기식; 조건식; 증감식)
	printf("Hello");
```
```
초기식 : 본격적으로 반복을 시작하기에 앞서 딱 한번 실행된다.
조건식 : 매 반복의 시작에 앞서 실행되며, 그 결과를 기반으로 반복유무를 결정
증감식 : 매 반복실행 후 마지막에 연산이 이뤄진다.
```
if
```c
#include <stdio.h>
int main() {
    int opt;
    double num1, num2;
    double result;
    printf("1. 덧셈 2. 뺄셈 3. 곱셈 4. 나눗셈 \n");
    printf("선택");
    scanf("%d", &opt);
    printf("두 개의 실수 입력: ");
    scanf("%lf %lf", &num1, &num2);
    if(opt==1)
        result = num1 + num2;
    if(opt==2)
        result = num1 - num2;
    if(opt==3)
        result = num1 * num2;
    if(opt==4)
        result = num1 / num2;
    printf("결과: %f \n", result);
    return 0;
}
// 4가지 중 하나만 선택해도 4번의 조건검사를 시행하게 되어 불합리함
```
if~else
```c
#include <stdio.h>
int main() {
    int opt;
    double num1, num2;
    double result;
    printf("1. 덧셈 2. 뺄셈 3. 곱셈 4. 나눗셈 \n");
    printf("선택");
    scanf("%d", &opt);
    printf("두 개의 실수 입력: ");
    scanf("%lf %lf", &num1, &num2);
    if(opt==1)
        result = num1 + num2;
    else if(opt==2)
        result = num1 - num2;
    else if(opt==3)
        result = num1 * num2;
    else
        result = num1 / num2;
    printf("결과: %f \n", result);
    return 0;
}
// 4가지 중 알맞은 조건검사를 시행하도록 만듬
```
삼 항 연산자
```c
#include <stdio.h>
int main() {
    int num, abs;
    printf("정수 입력: ");
    scanf("%d", &num);
    abs = num > 0 ? num : num * (-1); // 조건 ? 데이터1 : 데이터2
    printf("절댓값: %d \n", abs);
    return 0;
}
```
```
정수 입력:-56
 절댓값: 56
```
break
```c
#include <stdio.h>
int main() {
    int sum = 0, num = 0;
    while(1){
        sum+=num;
        if(sum>5000)
            break; // 조건이 충족되면 반복문 탈출
        num++;
    }
    printf("sum: %d \n", sum);
    printf("num: %d \n", num);
    return 0;
}
```
continue
```c
#include <stdio.h>
int main() {
    int num;
    for(num=1; num<20; num++){
        if(num%2==0 || num%3==0)
            continue; // 조건이 충족되면 반복문 처음으로
        printf("%d, ", num);
    }
    return 0;
}
```
switch
```c
#include <stdio.h>
int main() {
    int num;
    printf("1이상 5이하의 정수 입력: ");
    scanf("%d", &num);
    switch(num){
        case 1:
            printf("1은 ONE \n");
            break;
        case 2:
            printf("2는 TWO \n");
            break;
        case 3:
            printf("3은 THREE \n");
            break;
        case 4:
            printf("4는 FOUR \n");
            break;
        case 5:
            printf("5는 FIVE \n");
            break;
        default:
            printf("I don`t know \n");
    }
    return 0;
}
```
switch 문과 if~else
```
switch 문이 더욱 간결하기에 사용한다.
하지만 if~else문을 전부 대체할 수 있는 것은 아니기에 더욱 적합한 것을 사용한다.
```
함수
```
1. 함수는 불필요한 부분을 줄이고 간결하게
2. 하나의 함수는 하나의 일만 담당하도록 디자인
3. printf 함ㅎ수도 값을 반환(단, 반환되는 값을 저장하지 않음)
```
```c
int Add(int num1, int num2){ // 반환형(int) 함수의 이름(Add) 매개변수(int num~)
	int result = num1 + num2;
    return result; // 값의 반환
}
```
return
```c
void NoReturnType(int num){
	if(num<0)
    	return; // 값을 반환하지 않는 리턴문
}
// 리턴문에는 '값의 반환' 과 '함수의 탈출' 이라는 두 가지 기능이 담겨 있다.
```
지역변수
```
: 함수 내에 선언되는 변수
: 선언된 이후로부터 함수 내에서만 접근 가능
: 한 지역(함수) 내에 동일한 이름의 변수 선언 불가
: 다른 지역에 동일한 이름의 변수 선언 가능
: 해당 지역을 빠져나가면 지역변수는 소멸, 호출될 때마다 새롭게 할당
: 지역변수 내에 매개변수가 있음(선언된 함수 내에서만 접근 가능)
```
전역변수
```c
#include <stdio.h>
void Add(int val);
int num; // 전역변수는 기본 0 으로 초기화
int main(void) {
    printf("1이상 5이하의 정수 입력: ");
    scanf("%d", &num);
    switch(num){
	~~~~~
}
// 함수 외부에 선언(언제 어디서든 접근 가능)
// 프로그램 시작과 동시에 메모리 공간에 할당되어 종료 시까지 존재
```
static 변수
```c
#include <stdio.h>
void Add(int val){
	static int num1=0; // 접근 범위를 Add로 제한, 범위가 좁아 안정적
    int num2=0;
    num1++, num2++;
    printf("static: %d, local: %d \n", num1, num2);
}
int main(void) {
    int num;
    printf("1이상 5이하의 정수 입력: ");
    scanf("%d", &num);
    switch(num){
	~~~~~
    return 0;
}
```
register
```c
int sample(void){
	register int num=3;
    ~~~
}
```
```
register는 힌트를 제공하는 키워드, 컴파일러는 이를 무시하기도 함
레지스터는 CPU내부에 존재함, 때문에 접근이 가장 빠른 메모리 장치
빈번히 사용하는 변수 -> 접근이 가장 빠른 레지스터에 저장하는 것이 성능 향상에 도움
```
재귀함수
```c
void Recursive(int num){
	if(num<=0) // 재귀의 탈출 조건
    	return;
	printf("Recursive call \n", num);
    Recursive(num-1); // 자신을 호출
}
int main(void){
	Recursive(3);
    return 0;
}
// 자신을 재호출하는 형태로 정의된 함수를 가리켜 재귀함수라 함
// 탈출 조건이 없을 시 계속된 반복
```
