다차원 배열
```c
int arrOneDim[10]; // 길이가 10인 1차원 int형 배열
int arrTwoDim[5][5]; // 가로, 세로의 길이가 각각 5인 2차원 int형 배열
int arrThreeDim[3][3][3]; // 가로, 세로, 높이의 길이가 각각 3인 3차원 int형 배열
// 문법적으로 4, 5차원 배열 선언 가능하지만 의미부여가 힘든 배열
```

2차원 배열
```c
TYPE arr[세로길이][가로길이]; // [행][열]; 배열이 생성된 후 좌측상단부터 1행 & 1열 
int arr[N][M];
arr[N-1][M-1]=Value;
printf("d", arr[N-1][M-1];
```
선언 및 초기화
```c
int arr[3][3]={
	{1},
    {3, 7},
    {2, 5, 8}
};
// 채우지 않은 공간은 0으로 채워짐
int arr[3][3]={1,2,3,4,5,6,7}; // 한 줄로 표현해도 빈 공간 0으로 채워짐

int arr[][3]={1, 2, 3, 4, 5, 6, 7}; // 세로길이는 생략 가능
```

3차원 배열
```c
int arr[높이][세로길이][가로길이]; // 세로길이와 가로길이의 배열이 높이만큼 겹친 상태
2차원 배열을 높이만큼 선언(for문 2중중첩으로 사용가능)
```

이중 포인터 변수
```c
double num=3.14;
double *ptr=&num;
double **dptr=&ptr;
double *ptr2;
ptr2=*dptr; // ptr2=ptr과 같음
// ptr과 *dptr은 메모리주소값을 가짐
// num과 **dptr은 값을 가짐
```
포인터 변수의 swap
```c
void SwapIntPtr(int **dp1, int **dp2){
	int *temp=*dp1;
    *dp1=*dp2;
    *dp2=temp;
}
int main(void){
	int num1=10, num2=20;
    int *ptr1, *ptr2;
    ptr1=&num1, ptr2=&num2;
    printf("*ptr1, *ptr2: %d %d \n", *ptr1, *ptr2);
    
    SwapIntPtr(&ptr1, &ptr2); // 주소 값을 전달
    printf("*ptr1, *ptr2: %d %d \n", *ptr1, *ptr2);
    return 0;
} // 포인터변수에 저장된 값을 변경하려면 주소값을 함수에 전달하여야 한다.
```
2차원 배열이름의 포인터 형
// 포인터 형은 int형 포인터, double형 포인터와 같이 딱 떨어지는 명칭이 존재하지 않는다.

포인터 배열 // 포인터 변수로 이루어진 배열 int \*whoA[3];
배열 포인터 // 배열을 가리킬 수 있는 포인터 변수 int (\*whoB)[3];
```c
#include <stdio.h>
int main(void){
	int num1=10, num2=20, num3=30;
    int arr2d[2][3]={1, 2, 3, 4, 5, 6};
    int i, j;
    int *whoA[3]={&num1, &num2, &num3}; // 포인터 배열
    int (*whoB)[3]=arr2d; // 배열 포인터
    printf("%d %d %d \n", *whoA[0], *whoA[1], *whoA[2]);
    for(i=0; i<2; i++){
	    for(j=0; j<3; j++){
   		printf("%d ", whoB[i][j]);
    	}
        printf("\n");
    }
    return 0;
}
```
```
10 20 30
1 2 3
4 5 6
```
2차원 배열을 함수의 인자로 전달하기
```c
int main(void){
	inr arr1[2][7]; //   <==> int (*parr1)[7]
    double arr2[4][5]; //   <==> double (*parr2)[5]
    SimpleFunc(arr1, arr2);
    ~~~
}

void SimpleFunc(int (*parr1)[7], double (*parr2)[5]){~~~}
// 동일한 선언
void SimpleFunc(int parr1[][7], double parr2[][5]){~~~}
```
arr[i] == \*(arr+i)
```c
#include <stdio.h>
int main(void){
    int a[3][2]={{1, 2}, {3, 4}, {5, 6}};
    printf("a[0]: %p \n", a[0]);
    printf("*(a+0): %p \n", *(a+0));
    printf("a[1]: %p \n", a[1]);
    printf("*(a+1): %p \n", *(a+1));
    printf("a[2]: %p \n", a[2]);
    printf("*(a+2): %p \n", *(a+2));
    printf("%d, %d \n", a[2][1], (*(a+2))[1]);
    printf("%d, %d \n", a[2][1], *(a[2]+1));
    printf("%d, %d \n", a[2][1], *(*(a+2))+1);
    return 0;
}
```
```
a[0]: 000000ebd7fffce0
*(a+0): 000000ebd7fffce0
a[1]: 000000ebd7fffce8
*(a+1): 000000ebd7fffce8
a[2]: 000000ebd7fffcf0
*(a+2): 000000ebd7fffcf0
6, 6
6, 6
6, 6
```
함수의 포인터 형 결정
```c
Type:반환형 Func (Type:매개변수 name)
// 반환형과 매개변수 선언이 동일한 두 함수의 포인터 형은 일치
int (*fptr)(int) // 반환형이 int 형이고 매개변수 선언이 int 하나인 함수포인터
int Func(int num1, num2){~~}
int (*fptr)(int, int);
fptr=Func; // 상수 값 변수에 저장
fptr(3, 4); // Func(3, 4)와 동일한 결과
```
형(Type)이 존재하지 않는 void 포인터
```c
void \*ptr;
// 어떠한 주소 값도 저장이 가능한 void형 포인터
// 형 정보가 존재하지 않는 포인터 변수이기에 어떤 주소 값도 저장 가능
// 형 정보가 존재하지 않기 때문에 메모리 접근을 위한 \*연산 불가능

#include <stdio.h>
void Func(void){
    printf("test");
}
int main(void){
    int num=20;
    void *ptr;
    ptr=&num;
    printf("%p\n", ptr);
    *ptr=20; // void형이라 형 정보가 없어 값 지정 불가
    *ptr++; // 형 정보가 없어 연산 실행 불가
    ptr=Func;
    printf("%p\n", ptr);
    return 0;
}
```
main 함수를 통한 인자의 전달
```c
#include <stdio.h>
int main(int argc, char *argv[]){
	int i=0;
    for(i=0; i<argc; i++)
    	printf("%s \n", i+1, argv[i]); // 입력된 문자열을 argc수만큼 argv[]내용을 출력
    return 0;
}
```
char \*argv[]
```c
void Func(Type *arr) // 매개 변수 선언에서는 예외적으로 (Type arr[])로 선언 가능
void Func(Type **arr) // (Type *arr[])와 같음 -> char *arr[]는 char형 이중 포인터

#include <stdio.h>
void Func(int argc, char *argv[]){
    for(int i=0; i<argc; i++)
        printf("%s \n", argv[i]);
}
int main(void){
    char *fun[3]={
            "C pgm",
            "C++ pgm",
            "java pgm"
    };
    Func(3, fun);
    return 0;
}
```
```
C pgm
C++ pgm
java pgm
```
