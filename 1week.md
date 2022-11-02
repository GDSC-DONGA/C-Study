# CH 1~9

**프로그래밍 언어**란 

- 사람과 컴파일러가 이해할 수 있는 형태의 언어

**컴파일러** 

- 프로그래밍 언어를 기계어로 번역

**기계어**

- 0과 1로 구성된 형태의 언어

## c언어의 장점

- 절차지향적
- 이식성이 좋다 (cpu에 따라 재작성할 필요가 없다.)
- 좋은 성능 :  메모리 용량이 적고 속도 저하도 최소화할 수 있다.

## c언어 흐름

1. 프로그램 작성
2. 컴파일 (compile)
3. 링크 (link)
4. 실행파일 생성 (.exe)

### 기본 툴

```c
int main(void) {
	return 0; 
} //아무것도 안하는 코드, 반환 0
```

### 연산자

```c
int num = 1;

printf(++num); //2 출력
printf(num++); //2 출력 하고 num은 +1됨 (후위 연산)
printf(num); //3 출력
```

### 명시적 형 변환 : 강제로 형 변환 시킴

```c
double num1 = 5.14 + 9;  // int 9를 double형 9.0으로 변환해서 계산함
```

### printf 함수

“”로 묶어줌 , 문자열 중간에 따옴표를 넣고 싶다면 

1️⃣ \” 사용     

2️⃣ “큰 따옴표로 묶었다면 ‘ 사용, ‘작은 따옴표로 묶었다면 “사용

```c
printf("%d", 변수명); //정수형 출력
printf("%c", 변수명); //문자형 출력

//아스키 코드
printf("%d %c", 'A', 65); //'A'의 정수형 65 출력, 65의 문자형 A 출력
```

- 필드 폭 지정하여 출력하기
    
    %8d : 필드 폭을 8로 확보하고, 오른쪽 정렬해서 출력
    
    %-8d : 필드 폭을 8로 확보하고, 왼쪽 정렬 출력
    
- %s : 문자열 입출력에 사용

### 반복문

- **while**
    - 중첩 반복
    - while조건이 참일 때 실행
    
    ```c
    //구구단 출력 반복문
    
    int main(void) {
    	int cur = 2;
    	int is = 0;
    	
    	while(cur<10) {
    		is = 1;
    		while(is<10) {
    			printf("%d X %d = %d", cur, is, cur*is);
    		}
    	cur++;
    	}
    	return 0;
    }
    ```
    
- **do-while**
    - 일단 실행 후 조건 비교 =⇒ 적어도 1번은 실행됨
    
    ```c
    do {
    	printf("heelo world! \n");
    	num++;
    } while(num<3);
    ```
    
- **for**
    - for(변수 초기식; 조건식; 증감식){} 으로 구성
    
    ```c
    for(int num=0; num<3; num++) {
    	printf("hi~");
    }
    ```
    

```c
//구구단 출력
int main(void) {
	int cur, is;
	
	for(cur=2; cur<10; cur++) {
		for(is=1; is<10; is++) {
			printf("%d X %d = %d \n" , cur, is, cur*is);
		}
		printf("\n");
	}
	return 0;
}
```

2 X 1 = 2 (여기 한 줄 띄는 게  두번째 for문의 \n)

2 X 2 = 4 

‘’’

(여기가 첫번째 for문의 printf(”\n”);

3X1=3

‘’’

이렇게 출력됨
