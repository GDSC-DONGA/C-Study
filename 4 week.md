# CH 16-19

## 다차원 배열

- 2차원 배열의 선언

```c
type형 배열명[세로길이][가로길이];
```

- 2차원 배열 선언과 동시에 초기화하기

```c
int arr[3][3] = {{1,2,3},{4,5,6},{7}};

//출력
1 2 3
4 5 6 
7 0 0 //자동으로 0이 채워짐

int arr[3][3] = { 1,2,3,4,5,6,7,8 };

//출력
1 2 3 
4 5 6 
7 8 0
//별도의 중괄호를 사용하지 않으면 좌 상단부터 차례대로 초기화가 됨
```

- 배열 크기 생략

```c
int arr[][] = { 1,2,3,4,5 }; //오류!! 채워넣지 못함

int arr[][2] = {1,2,3,4,5,6}; //세로길이 생략 가능 3으로 계산해줌
```

## 포인터의 포인터

### 이중 포인터 변수

```c
int main(void) {
	double num = 3.14;
	double *ptr = &num;
	double **dptr = &ptr;
	double *ptr2;

	printf("%9g %9g \n", ptr, *dptr);
	printf("%9g %9g \n", num, **dptr);
	ptr2 = *dptr; //==> ptr2 = ptr과 같은 말
	*ptr2 = 10.99
	printf("%9g %9g \n", num, **dptr);

	return 0;
}
```

(출력)

num주소값    num주소값

3.14          3.14

10.99        10.99

즉, ptr == *dptr / num == **dptr / *ptr2 == **dptr 임을 알 수 있다.

### 포인터 변수의 Swap

```c
#include <stdio.h>
#define _CRT_SECURE_NO_WARNINGS
#pragma warning(disable:4996)

void SwapIntPtr(int* p1, int *p2) {
	int* temp = p1;
	p1 = p2;
	p2 = temp;
}

int main(void) {
	int num1 = 10 , num2 = 20;
	int* ptr1, * ptr2;
	ptr1 = &num1, ptr2 = &num2;
	printf("*ptr1, *ptr2: %d %d \n", *ptr1, *ptr2);

	SwapIntPtr(ptr1, ptr2);
	printf("*ptr1, *ptr2: %d %d \n", *ptr1, *ptr2);

	return 0;
}
```

### 삼중 포인터

```c
int ***ptr; //이중 포인터 변수의 주소를 담는 용도
```

### 포인터의 필요성

- scanf함수와 같이 함수 내에서 함수 외부에 선언된 변수의 접근을 허용하기 위해
- 메모리의 동적 할당 등등
- 자료구조를 공부하게 되면 보다 넓게 필요성을 이해할 수 있음

### 2차원 배열이름의 포인터

- 형 결정 짓기
    
    ```c
    char (*arr1)[4];  //char형 변수를 가리키면서, 포인터 연산 시 sizeof(char)x4의 크기 단위로 증가 및 감소하는 포인터 변수
    double (*arr2)[7];//double형 변수를 가리키면서, 포인터 연산 시 sizeof(double)x7의 크기 단위로 증가 및 감소하는 포인터 변수
    ```
    

### 배열 포인터 vs 포인터 배열

```c
int (*whoA)[4]; //배열 포인터 : 배열을 가리킬 수 있는 포인터
int *whoB[4]; //포인터 배열 : 포인터 변수로 이루어진 배열
```

+
```
arr[i] == *(arr + 1) //같은 의미
*arr == arr[] //같은 의미
```
