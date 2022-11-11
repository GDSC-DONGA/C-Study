1차원 배열
```c
int oneDimArr[4];
// 배열을 이루는 요소(변수)의 자료형(int) 배열의 이름(oneDimArr) 배열의 길이[4}

arr[idx]=20; // 배열 arr의 index+1번째 요소에 20을 저장
arr[0]=10; // 첫 번째 요소 10 저장
arr[1]=12; // 두 번째 요소 12 저장
arr[2]=13; // 세 번째 요소 13 저장
```
배열 선언과 초기화
```c
int arr1[5]={1, 2, 3, 4, 5}; // 초기화 리스트로 초기화(순서대로)
int arr2[5]={1, 2}; // 값이 부족한 경우 부족한 부분 0으로 채워짐
int arr3[]={1, ,2, 3, 4, 5} // 길이정보 생략 시 컴파일러가 배열의 길이정보 채움
```
1차원 배열의 선언, 초기화 및 접근
```c
#include <stdio.h>
int main(void){
    int arr1[5]={1, 2, 3, 4, 5};
    int arr2[]={1, 2, 3, 4, 5, 6, 7};
    int arr3[5]={1, 2};
    int ar1Len, ar2Len, ar3Len, i;
    printf("배열 arr1의 크기: %d \n", sizeof(arr1));
    printf("배열 arr2의 크기: %d \n", sizeof(arr2));
    printf("배열 arr3의 크기: %d \n", sizeof(arr3));

    ar1Len = sizeof(arr1) / sizeof(int);
    ar2Len = sizeof(arr2) / sizeof(int);
    ar3Len = sizeof(arr3) / sizeof(int);

    for (i = 0; i < ar1Len; i++)
        printf("%d", arr1[i]);
    printf("\n");
    for (i = 0; i < ar2Len; i++)
        printf("%d", arr2[i]);
    printf("\n");
    for (i = 0; i < ar3Len; i++)
        printf("%d", arr3[i]);
    printf("\n");
    return 0;
}
```
```
배열 arr1의 크기: 20
배열 arr2의 크기: 28
배열 arr3의 크기: 20
12345
12o3r4n5i6n7g
!12000
``:|:|:|`
char형\\0 배열&#9\``c:|
char str[14]="Good morning!";
```
|G|o|o|d|&nbsp&nbsp|m|o|r|n|i|n|g|!|\\0||
|:|:|:|:|:|:|:|::|:|:|:|:|:|:|
|[0]|[1]|[2]|[3]|[4]|[5]|[6]|[7]|[8]|[9]|[10]|[11]|[12]|[13]|
```
\0 : 널 문자는 문자열의 끝을 의미
널 문자를 %c를 이용해 출력 시 아무것도 출력되지 않지만, 공백과는 다르다
아스키 코드 : 널=0, 공백=32
널 문자의 존재 여부로 문자 배열인지, 문자열인지 판단
```
scanf 문자열 입력 특성
```c
#include <stdio.h>
int main(void){
    char str[50];
    int idx=0;
    printf("문자열 입력: ");
    scanf("%s", str);
    printf("입력 받은 문자열: %s \n", str);
    printf("문자 단위 출력: ");
    while(str[idx] != '\0'){
        printf("%c", str[idx]);
        idx++;
    }
    return 0;
}
```
```
문자열 입력:나는 나야 두비두밥
 입력 받은 문자열: 나는
문자 단위 출력: 나는
```
포인터 변수 : 정수 형태의 주소 값을 저장하는 목적으로 선언되는 것
포인터 변수 선언 : type * ptr; (type 형 포인터 변수 ptr의 선언)
```c
int main(void){
	int num = 5;
    int *pnum = &num; // &연산자의 반환 값은 포인터 변수에 저장
    ~~~
}
```
```c
#include <stdio.h>
int main(void) {
    int num = 5;
    int *pnum = &num; // num과 pnum 이 같음
    *pnum = 20; // pnum이 가리키는 공간(변수)에 20을 저장
    printf("%d", *pnum);
    printf("%d", num);
    return 0;
}
```
```
20
20
```
잘못된 포인터 연산 막기
```c
int main(void){
	int *ptr1 = 0;
    int *ptr2 = NULL; // 널 포인터 NULL은 숫자 0을 의미, 아무것도 가리키지 않음
}
// 특정 값으로 초기화 하지 않는 경우 널 포인터로 초기화하는 것이 안전
```
||포인터 변수|배열의 이름|
|:|:|:|
|이름이 존재하는가?|존재|존재|
|무것을 나타내거나 저장하나?|메모리 주소 값|메모리 주소 값|
|주소 값의 변경이 가능한가?|가능|불가능|
\* 배열의 이름은 변수가 아닌 상수 형태의 포인터이기에 대입연산이 불가
	(int *ptr = &arr[0] 으로 메모리 공간에 접근하여 증감연산 가능)

```c
#include <stdio.h>
int main(void) {
    int arr[3] = {15, 25, 35};
    int *ptr1 = &arr[0];
    int *ptr2 = &arr[1];
    *ptr1 += 1;
    *ptr2 -= 1;
    printf("%d \n", *ptr1);
    printf("%d \n", *ptr2);
    return 0;
}
```
포인터를 대상으로 하는 증감연산
```c
#include <stdio.h>
int main(void) {
    int *ptr1 = (int *) 0x0010; // int *ptr1 = 0x0010; 과 같음
    double *ptr2 = (double *) 0x0010;
    printf("%p %p \n", ptr1 + 1, ptr1 + 2); // +1이 4바이트(int)만큼 증가
    printf("%p %p \n", ptr2 + 1, ptr2 + 2); // +1이 8바이트(double) 만큼 증가
    printf("%p %p \n", ptr1, ptr2);
    ptr1++;
    ptr2++;
    printf("%p %p \n", ptr1, ptr2);
    return 0;
}
```
```
포인터를 대상으로 연산 시 sizeof(type)의 크기만큼 증감한다.
0000000000000014 0000000000000018
0000000000000018 0000000000000020
0000000000000010 0000000000000010
0000000000000014 0000000000000018
```
arr[i] == *(arr+i)
```c
#include <stdio.h>
int main(void) {
    int arr[3]={15, 25, 35};
    int * ptr = arr;
    printf("%d %d %d \n", *ptr, *(ptr+1), *(ptr+2));
    printf("%d %d %d \n", ptr[0], ptr[1], ptr[2]);
    printf("%d %d %d \n", *(arr+0), *(arr+1), *(arr+2));
    printf("%d %d %d \n", arr[0], arr[1], arr[2]);
    return 0;
}
```
```
15 25 35
15 25 35
15 25 35
15 25 35
```
두 가지 형태의 문자열 표현
```c
char str1[] = "My String"; // 문자열이 저장된 배열(변수성향의 문자열)
char * str2 = "Your String"; // 문자열의 주소값을 저장(상수성향의 문자열)
```
포인터 배열
```c
#include <stdio.h>
int main(void) {
    int num1=10, num2=20, num3=30;
    int *arr[3]={&num1, &num2, &num3};
    printf("%d \n", *arr[0]);
    printf("%d \n", *arr[1]);
    printf("%d \n", *arr[2]);
    return 0;
}
```
```
// 일반 배열과 차이점은 자료형을 표시하는 위치에 int * 나 double * 이 온다.
10
20
30
```
문자열 포인터 배열
```c
#include <stdio.h>
int main(void) {
    char *strArr[3]={"JIINNN", "HY", "JINHY"};
    printf("%s \n", strArr[0]);
    printf("%s \n", strArr[1]);
    printf("%s \n", strArr[2]);
    return 0;
}
```
```
JIINNN
HY
JINHY
```
배열을 함수의 인자로 전달
```c
#include <stdio.h>
void ShowArayElem(int * param, int len){ // (int param[], ~)와 동일(매개변수만)
    int i;
    for(i=0; i<len; i++)
        printf("%d ", param[i]);
    printf("\n");
}

void AddArayElem(int *param, int len, int add){
    int i;
    for(i=0; i<len; i++)
        param[i] += add;
}

int main(void) {
    int arr[3]={1, 2, 3};
    AddArayElem(arr, sizeof(arr)/sizeof(int), 1);
    ShowArayElem(arr, sizeof(arr)/sizeof(int));
    AddArayElem(arr, sizeof(arr)/sizeof(int), 2);
    ShowArayElem(arr, sizeof(arr)/sizeof(int));
    AddArayElem(arr, sizeof(arr)/sizeof(int), 3);
    ShowArayElem(arr, sizeof(arr)/sizeof(int));
}
```
```
2 3 4
4 5 6
7 8 9
```
Call-by-value : 함수를 호출할 때 <u>단순 값</u>을 전달하는 형태의 함수호출
\* 함수 외부에 선언된 변수에 접근 불가능
Call-by-reference : 메모리의 접근에 사용되는 <u>주소 값</u>을 전달하는 형태의 함수호출
\* 함수 외부에 선언된 변수에 접근 가능

변수 앞에 & 연산자를 붙이는 이유
scanf, swap 등의 함수를 사용할 때 변수의 주소값을 필요로 하기 때문

포인터 변수의 참조대상에 대한 const
```c
int main(void){
	int num=29;
    const int * ptr=&num;
    *ptr=30; // 컴파일 에러
    num=40; // 컴파일 성공
    ~~~
}
```
```
포인터 변수 ptr을 이용해서 ptr이 가리키는 변수에 저장된 값을 변경하는 것을 허용하지 않음
변수 num에 저장된 값 자체의 변경이 불가능한 것은 아님
다만 ptr을 통한 변경을 허용하지 않음
```
포인터 변수의 상수화
```c
int main(void){
	int num1=20;
    int num2=30;
    int * const ptr=&num1; // 포인터 변수 ptr에 저장된 값을 상수화
    ptr=&num2; // 컴파일 에러
    ptr=40; // 컴파일 성공
    ~~~
}
```
```
ptr에 저장된 값은 변경이 불가능, ptr이 가리키는 대상의 변경을 허용하지 않음
const int*ptr=&num; 와 int*const ptr=&num; -> const int*const ptr=&num;
* 두 가지 const 선언을 동시에 할 수 있다.
```
안선정을 높이는 const
```c
int main(void){
	const double PI=3.1415;
    double rad;
    PI=3.07; // 컴파일 시 발견되는 오류상황
	scanf("circle area %f \n", rad*rad*PI);
    return 0;
}
```
```
const 선언은 추가적인 기능을 제공하기 위한 것이 아니라, 코드의 안전성을 높이기 위한것이다.
따라서 이러한 const의 선언을 소홀히하기 쉬운데,
const의 선언과 같이 코드의 안전성을 높이는 선언은 가치가 매우 높은 선언이다.
```
