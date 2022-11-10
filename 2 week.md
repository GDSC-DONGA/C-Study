# Ch 12-15 포인터

---

### 포인터 변수

: 주소 값을 저장하기 위해 사용되는 변수

- 선언

```c
int num = 7;
int *pnum; //포인터 변수 pnum 선언
pnum = &num; //num의 주소값을 포인터 변수에 대입
```

```c
int *punm1; //int형 변수를 가리키는 포인터
double *pnum2; //double형 변수를 가리키는 포인터

type *pnum3; //으로 선언할 수 있다
```

```c
pnum = &num;
pnum = 30; //하면 num의 주소값이 바뀜
*pnum += 30; //하면 num + 30됨
```

- ⭐ `*pnum == num`

### 포인터 배열

```c
int main(void) {
	int arr1[3] = {1, 2, 3};
	double arr2[3] = {1.1, 2.2, 3.3};

	printf("%d %g \n", *arr1, *arr2); //1 1.1 출력
	*arr1 += 100;
	*arr2 += 100;
	printf("%d %g \n", *arr1, *arr2); //100 100.1 출력
	return 0 ;
}
```

- `*배열명` 하면 배열[0]의 값을 불러옴 ⬇️ 밑의 코드 참고
- 인덱스 0  말고 다른 인덱스를 부르고 싶다면?  ⭐ `arr[i] == *(arr + i)`

```c
int arr[3] = [1, 2, 3};
int *ptr = &arr[0]; // int *ptr = arr; 와 같은 의미

printf("%d %d %d", *ptr, *(ptr+1), *(ptr+2)); // 1 2 3 순서대로 출력
```

- ptr (포인터 배열)로 arr (배열)을 부를 수 있음

```c
int arr[3] = [1, 2, 3};
int *ptr = &arr[0]; // int *ptr = arr; 와 같은 의미

printf("%d %d", ptr[0], arr[0]); //1 1 출력 
```

### 포인터로 문자열 표현

❓ str1[ ]과 *str2가 각각 어디에 저장되는 거지?

```c
char str1[] = "My String!"; //배열이 생성됨 
char *str2 = "Your String"; //❓
```

```c
#include <stdio.h>

int main(void) {
	char str1[] = "My String"; //변수 형태의 문자열
	char *str2 = "Your String"; //상수 형태의 문자열
	printf("%s %s \n", str1, str2);

    str2 = "Our String"; //str2의 값 변경
    printf("%s %s \n", str1, str2);

    str1[0] = 'X'; //str1의 인덱스 0 값 바꾸기
    //str2[0] = 'X'; 문자열 변경 실패! 상수 성향의 문자열이라 값변경 안됨 (그래서 주석처리함) 주석 뺴면 오류
    printf("%s %s \n", str1, str2);
    return 0;
}
```

![출력 결과](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2daf9fa9-0001-474e-8e31-5f9671277a68/Untitled.png)

출력 결과

### 인자 전달

- C언어에서는 배열 타입을 매개변수로 보낼 수 없음 ⇒ 배열 포인터를 보낸다!

```c
int main(void) { 
	int arr[3] = {1, 2, 3};

	SimpleFunc(arr);
}

void SimpleFunc(int * param) { //int param[]과 같은 의미
	printf("%d %d \n", param[0], param[1]); //포인터 변수를 이용해서 
                                          //배열의 형태로 접급 가능
}
```

단, int *ptr = arr; 대신  int ptr[ ] = arr; 는 불가능

### call-by-value

: `값`을 전달하는 형태의 함수 호출

```c
void Swap(int n1, int n2) {
	int temp = n1;
	n1 = n2;
	n2 = temp;
	printf("n1 n2: %d %d \n", n1, n2);
}

int main(void) { 
	int num1=10;
  int num2=20;
  printf("num1 num2 : %d %d \n", num1, num2); //10 20출력

  Swap(num1, num2); // 20 10 출력 
  printf("num1 num2 : %d %d \n", num1, num2); // 10 20 출력

  return 0;
}
```

Swap을 해줘서 num1, num2의 값도 바뀌길 원했지만 main에는 영향을 주지 않음 (함수 내에서의 결과는 외부에 영향X)

### call-by-reference

: `주소`를 전달하는 형태의 함수 호출

```c
void Swap(int *ptr1, int *ptr2) {
	int temp = *ptr1;
	*ptr1 = *ptr2;
	*ptr2 = temp;
	printf("n1 n2: %d %d \n", n1, n2);
}
int main(void) { 
	int num1=10;
  int num2=20;
  printf("num1 num2 : %d %d \n", num1, num2); // 10 20

  Swap(num1, num2); // 20 10
  printf("num1 num2 : %d %d \n", num1, num2); // 20 10

  return 0;
}
```

swap 함수 내에서의 *ptr1은 main 함수의 num1

매개변수 int *ptr1 = 입력받은 값 num1 

그러므로 int *ptr1 = num1 

⇒ 외부의 변수 값 변함

- scanf 함수 호출 시 & 연산자를 붙이는 이유
    - scanf 함수가 외부에서 선언된 변수에 접근하려면 주소값을 알아야함 (call-by-reference)
    - str은 배열의 이름이고 자체가 주소값임 [참고](https://www.notion.so/Ch-12-15-c9b4827127ae4265898885424b9b7fae) = &연산자 안붙임

### const 선언

: 값 변경 X ⇒ 안정성 높아짐

```c
const int * ptr = &num; 
```

- 포인터 변수 ptr을 이용하여 ptr이 가리키는 변수인 num의 값을 변경하는 것 허용X
    - num 자체의 값 변경X가 아닌 ptr을 이용하여 바꾸는 것이 불가능

```c
int *const ptr = &num1;
```

- 포인터 변수 ptr에 저장된 값을 상수화하겠다.
    - num의 값 변경 X

🔼 두개 동시에 선언 가능
