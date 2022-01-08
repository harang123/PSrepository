# PSrepository
ProblemSolving about groomide

# 구름 ide - 약수 구하기

	import 'dart:io';
	void main() {
		var line = stdin.readLineSync();  // 입력스트림으로 입력값을 받아 line에 넣어준다.
		int num = int.parse(line);  // stdin.readLineSync()로 받은 값은 String상태로 line에 초기화됨으로 int.parse(line)을 이용하여 int 값으로 바꿔준다.
		
		for(int i = 1; i <= num; i++)
		{
			if(num % i == 0)
			{
				stdout.write('$i ');  /* 처음에 print('$i '')로 출력을 해보았는데 자바나 c와 다르게 한줄로 입력되지 않고 계속 줄이 바뀌는 것을 알게됨. 
				       이에따라 stdout.write()를 사용하면 한줄에 입력되는 것을 알게됨*/
			}
		}
	}	ㅇ
약수 구하기에서 반복문으로 출력문을 계속 돌리지 않고 다른 방법으로 구해보았다. (join() 메서드를 사용)

	import 'dart:io';
	void main() {
		var line = stdin.readLineSync();  // 입력스트림으로 입력값을 받아 line에 넣어준다.
		int num = int.parse(line);  // stdin.readLineSync()로 받은 값은 String상태로 line에 초기화됨으로 int.parse(line)을 이용하여 int 값으로 바꿔준다.
		
		List<int> arr = new List();
		for(int i = 1; i <= num; i++)
		{
			if(num % i == 0)
			{
				arr.add(i);  // 반복문으로 int List인 arr에 값을 추가해 주었다.
			}
		}
		print(arr.join(' ') + ' ');  
		// 원하는 출력의 값이 1 2 3 4 5 10 20 이렇게 공백으로 묶여있고 마지막에도 공백이 들어가야 했기에 List의 값을 공백으로 묶어준 후 마지막에 + ' '을 더해 완성하였다.
	}

# 구름 ide - 369게임

	import 'dart:io';
	void main() {
		var line = stdin.readLineSync();
		int num = int.parse(line);

		int count = 0;
		for(int i = 1; i < num; i++)
		{
			int one = i % 10;
			int ten = i ~/ 10;  /* 처음에 다른 언어들처럼 그냥 int ten = i / 10;을 했었다. 하지만 원하는 결과값이 안나와 계속 고민하다가 dart의 나눗셈이 다른 언어들과는 
			다르게 적용된다는 것을 알게 되었다. dart에서는 나눗셈을 하였을때 결과값이 double 형으로 나오게 된다. 
			따라서 정수형 ten으로 값을 구하고 싶을 때는 ~/(잘림 나누기)를 사용해야한다.*/
			
			if(ten % 3 == 0 && ten != 0)
			{
				count++;
			}

			if(one % 3 == 0 && one != 0)
			{
				count++;
			}
		}
		print(count);
	}
369게임에서 위와같이 문제를 풀었을 때 3자리 수를 입력받게 되면 오류가 발생한다는 것을 알게 되어 다른 방법을 찾다가 RegExp(정규 표현식 클래스)를 알게되어 다른 분의 코드를 참고하여풀어보았다.

	import 'dart:io';
	import 'dart:math';

	void main() {

		var line = stdin.readLineSync();
		int num = int.parse(line);

		int count = 0;  /* count라는 변수를 사용하여 해당 Sring 문자열에서 369라는 문자가 몇번이나 표시되었는지 카운트하기 위하여 변수를 선언하였다.*/

		for(int i = 1; i < num; i++)  // 숫자 1부터 입력받은 숫자까지 모두 확인하기 위해 for문을 사용하였다.
		{
			String myNum = i.toString();  /* RegExp(정규식표현)을 사용하여 문자열을 비교하여야 함으로 인트 i에 toString()함수를 사용하여 String으로 형변환하였다. */
			for(int j = 0; j < myNum.length; j++) /* 새로운 for문을 만들어 위에서 String으로 변환한 글자 수만큼 반복하도록 하였다. */
			{
				count += check(myNum.substring(j, j+1));  /* 아래에서 check라는 메소드를 만들어 String에 369문자가 포함되어 있으면 1을 반환하고 없으면 0을 반환하도록 하                                                                              여 369가 포함되어 있으면 count 변수에 1을 더하게하였다.*/
			}
		}

		print(count);
	}

	int check(String a)
	{
		if(a.contains(new RegExp('[369]')))
		{
			return 1;
		}
		else
		{
			return 0;
		}
	}
많이 찾아보았으나 아직 RegExp부분을 정확하게 이해하지 못하였다고 판단이 되며 나중에 좀더 공부할 시간을 가지려한다. 하지만 String 타입의 길이를 계산하여 RegExp로 문자열을 비교하는 푸는 방법을 알게되었으며 String변수에 .substring(j, j+1)로 구간을 나눠 비교하는 것도 인상적이었다. 

3,6,9문제를 다른방식으로 풀어보았다. 처음에는 배운 grammer를 바탕으로 문제를 풀어보았는데 자꾸 막히고 이해가 안되서 많은 시간이 걸렸다. 
결국에는 피드백으로 받은 코드를 참고삼아 문제플 풀게되었다.

	import 'dart:io';
	void main() {
		int num = int.parse(stdin.readLineSync());	

		int count = 0;	
		List<String> check = ['3', '6', '9'];  // 반복문에서 받은 값들을 비교하기 위한 List를 생성하였다.

		for(int i = 1; i < num; i++){

			i.toString().split('').forEach((value){ /* int로 들어온 값인 i를 .toString() 메서드를 사용하여 String으로 변환한 후 .split('')메서드를 이용해 한글자씩으로 나누                                                                    었다. 그런 후 .forEach를 사용하여 2글자 이상일 경우 모든 값들을 비교할 수 있도록 하였다. */
				if(check.contains(value)){ // 위에서 생성해놓았던 check 리스트를 사용하여 3, 6, 9중에 한 글자라도 포함하고 있는지를 비교한 후 count++로 값을 구하였다.
					count++;
				}
			});
		}
		print(count);
	}

	
# 구름 ide - 최소값

	import 'dart:io';
	void main() {
		int count = int.parse(stdin.readLineSync());  // 배열의 크기를 입력받는다.

		String data = stdin.readLineSync();  /* 문제에서 입력을 받을때 한줄에 공백으로 구분하여 n개의정수를 입력해야 함으로 for문을 쓰는것이 아닌 한개의 문자열 형식으로 입력받았                                                         다. ex) 1 3 5 6 <- 이런식의 공백을 포함한 문자열로 입력을 받는다. */
		List<String> arr = data.split(' ');  // split(' ')메소드를 사용하여 위에서 입력받은 문자열을 공백을 기준으로 찢어놓은 뒤 arr 리스트를 만들어 값을 넣어준다. 
		List<int> arrInt = arr.map(int.parse).toList();  /* 넣어준 값을 int형식으로 바꿔야 하기 때문에 위의 리스트를 .map(int.parse)로 바꾼뒤 .toList()로 리스트 형식으로 바꿔                                                                     arrInt에 값을 담아준다. */

		int min = arrInt[0];  /* 0번 인덱스의 요소를 최소값으로 설정하여 다른 인덱스들과 비교하게 하였다.*/
		for(int i = 1; i < count; i++)  // 배열의 크기만큼 반복하여 최소값을 찾아준다.
		{
			if(min > arrInt[i])
			{
				min = arrInt[i];
			}
		}
		print(min);
	}
문자열 형식으로 입력받아 리스트를 만드는 것을 생각못해 많은 시간을 잡아먹었던 문제였다. arr.map(int.parse)에 대한 이해가 아직 부족함으로 좀 더 공부할 예정이다. 

# 구름 ide - 최소값 개선방법
=> 피드백을 받고 배열내에서 최소값과 최대값을 찾는 방법이 있는지 찾아봤더니 배열변수.reduce(min) / 배열변수.reduce(max)를 사용하여 더욱 간단히 최대값 최소값을 찾는 방법을 알게되었다..reduce(min) / .reduce(max)는 다트 내장 라이브러리인 'dart:math'에 속해있기 때문에 import를 해주어야 한다. 

	import 'dart:io';
	import 'dart:math';

	void main() {
		int n = int.parse(stdin.readLineSync());

		String str = stdin.readLineSync();
		List<String> arr = str.split(' ');
		List<int> arrInt = arr.map(int.parse).toList();

		int minimum = arrInt.reduce(min);
		print(minimum);
	}

# 구름 ide - 리그 경기 횟수 구하기

	import 'dart:io';
	void main() {
		var line = stdin.readLineSync();
		var num = int.parse(line);

		List<int> arr = new List();
		for(int i = 1; i < num; i++)
		{
			arr.add(i);
		}
		int check = arr.reduce((total, element) => total + element);  
		/* 처음에는 그냥 for문에서 count+= i;를 사용하여 풀었는데 forEach문, reduce, fold문을 연습하기 위해 reduce를 사용하여 풀어보았다.*/
		print(check);
	}
정확하게 reduce의 개념이 잡혀있지 않았는데 이번 문제를 풀면서 reduce의 개념을 정확하게 잡을 수 있었다. 
int check = arr.reduce((total, element) => total + element); 파라미터안의 total은 arr리스트의 첫번째 값을 받아오고 첫번째 리턴값을 도출할때의 element에는 바로 2번째 값이 들어가게 된다.따라서 만약 arr = [1, 2, 3, 4, 5] 일 경우에는 처음 루핑을 돌때 total = 1, element = 2 값이 들어가 2번쨰 total의 값은 3이 된다. 

# 구름 ide - 시험성적 평균과 등급 구하기

	import 'dart:io';
	void main() {
		String line = stdin.readLineSync();
		List<String> arrLine = line.split(' ');  // String으로 입력받은 3과목의 점수를 리스트로 찢어놓았다.

		List<int> arrInt = arrLine.map(int.parse).toList(); /* 계산을 하기위해서는 List의 값들을 String에서 int로 바꿔야 하기 때문에 map 메서드를 사용하여 리스트의 값들을                                                                              String에서 int로 바꾼 새로운 배열을 생성하였다.*/

		int count = 0;
		arrInt.forEach((value){
			count += value;
		});
		double aver = count / 3; // if문에서 비교식에 사용하기 위하여 평균값을 변수에 받아주었다.
		String averStr = aver.toStringAsFixed(2);  // 나중에 출력문에서 사용하기 위해 소수점 아래 2자리에서 반올림한값을 String형식으로 변수를 받았다.

		if(aver >= 90)  // switch문은 비교식 사용이 불가능하기때문에 if문으로 처리하였다. 
		{
			print(averStr + ' A'); // if문 밖에서 따로 합칠 필요 없이 바로 결과를 출력하도록 하였다.
		}
		else if(aver >= 80)
		{
			print(averStr + ' B');
		}
		else if(aver >= 70)
		{
			print(averStr + ' C');
		}
		else if(aver >= 60)
		{
			print(averStr + ' D');
		}
		else
		{
			print(averStr + ' F');
		}
	}
배운점 : switch문의 정확한 정의, map, forEach, split 메서드들을 복습하였으며 ceil(올림), floor(버림), round(반올림), toStringAsFixed()함수에대해 알게되었다.  

## feedback에 대한 개선 ## 시험성적과 평균  

	int count = 0;
		arrInt.forEach((value){
			count += value;
		});
		double aver = count / 3; // if문에서 비교식에 사용하기 위하여 평균값을 변수에 받아주었다.
		
		---> 위의 코드를 reduce를 사용하여 아래와 같이 바꿨다.
		
	double aver = arrInt.reduce((total, element){
			return total + element;
		}) / 3;
		

# 구름 ide - Min 함수

	import 'dart:io';
	import 'dart:math';

	void main() {
		String line = stdin.readLineSync();  
		List<String> arrLine = line.split(' ');  // String으로 입력받은 값을 split 메서드를 사용하여 찢어 arrLine이라는 리스트에 넣어준다.
		List<int> arrInt = arrLine.map(int.parse).toList(); // 아래에서 reduce메서드로 값을 비교하려면 숫자로 인식되어야 함으로 map 메서드를 사용하여 String을 int로 바꿔준다.

		print(arrInt.reduce(min));  // 'dart:math'클래스를 import해서 사용하는 reduce메소드이다. 
	}

# 구름 ide - 네 수의 곱

	import 'dart:io';

	void main() {
		String line = stdin.readLineSync(); // 공백으로 값을 입력받기 때문에 String으로 입력받는다.
		List<String> arrLine = line.split(' ');  // 각각의 값들을 따로 사용해야 하기때문에 List에 값을 분리해 넣어준다.
		List<int> arrInt = arrLine.map(int.parse).toList();  // String형식의 List를 int형식의 List로 변환하여 준다.

		print(multi(arrInt[0], arrInt[1], arrInt[2], arrInt[3])); // multi 메서드를 만들어 사용하여 네 정수의 곱을 출력한다.
	}

	int multi(int a, int b, int c, int d)
	{
		return mul(mul(a, b), mul(c, d));  // mul 메서드를 생성하여 네 정수의 곱을 구하는 multi 메서드를 만든다.
	}

	int mul(int a, int b)
	{
		return a * b;
	}
	
	import 'dart:io';

## feedback에 대한 개선 ## 네 수의 곱
	void main() {
		String line = stdin.readLineSync(); // 공백으로 값을 입력받기 때문에 String으로 입력받는다.
		List<String> arrLine = line.split(' ');  // 각각의 값들을 따로 사용해야 하기때문에 List에 값을 분리해 넣어준다.
		List<int> arrInt = arrLine.map(int.parse).toList();  // String형식의 List를 int형식의 List로 변환하여 준다.

		int result = arrInt.reduce((total, element){ 
			return total * element;
		});
		print(result);
	}
문제에서 주는 힌트에 너무 집중한것 같다. 매번 문제를 풀때 힌트에 기대는 것이 아닌 가장 효율적인 코드를 짜도록 시도하자!
	
	

# 구름 ide - 특정 문자 개수 구하기

	import 'dart:io';
	void main() {
		String line = stdin.readLineSync();  // 임의의 문장(50자 이내) 입력
		List<String> arrLine = line.split(' ');

		int count = 0;
		String alphavet = stdin.readLineSync();  // 문장에서 개수를 구하고 싶은 문자 입력
		arrLine.forEach((value){  // forEach구문을 이용하여 쨸 처음 입력받은 문장의 각 부분을 이용해 개수를 구하고 싶은 문자와 같은지를 비교해준다.
			if(value == alphavet)
			{
				count++;  // 같은 글자가 몇개가 있는지 구하는 것이므로 같을 때마다 count변수의 값을 1씩 올려준다.
			}
			if(value.length > 1)
			{
				List<String> arrStr = value.split('');  // 쨀 처음 입력받은 문장을 공백을 이용해 분리하였음에도 완전히 분리가 안되었기때문에 한번 더 분리하였다.
				arrStr.forEach((val){  // 분리한 단어들을 다시 같은 글자가 있는지 비교하는 방법이다.
					if(val == alphavet)
					{
						count++;
					}
				});
			}
		});	
		print(count);
	}

## feedback에 대한 개선 ## 특정문자 개수
	import 'dart:io';
	void main() {
		String line = stdin.readLineSync();  // 임의의 문장(50자 이내) 입력
		List<String> arrLine = line.split('');

		String alphabet = stdin.readLineSync();  // 입력된 문장내 개수를 알고 싶은 문자 입력
		int count = 0;
		arrLine.forEach((val){
			if(alphabet == val){
				count++;
			}
		});
		print(count);
	}


# 구름 ide - 3의 배수 게임

	import 'dart:io';
	void main() {
		String line = stdin.readLineSync();
		int num = int.parse(line);

		List<int> arrInt = new List(num);  // for문에서 값을 입력받기 쉽게 크기가 정해진 List를 먼저 선언해준다.

		for(int i = 1; i <= num; i++)
		{
			arrInt[i-1] = i;  // 리스트에 들어갈 값과 인덱스의 크기가 -1 차이기 때문에 인덱스 위치에 -1을 하여 값을 맞춰준다.

			if(i % 3 == 0)
			{
				arrInt[i-1] = 'X';  // 3의 배수일때 i-1 인덱스 자리에 'X' 값을 넣어준다.
			}
		}
		print(arrInt.join(' ') + ' ');  // arrInt에 들어있는 값들을 join(' ') 함수를 이용해 공백을 기준으로 String 값으로 합쳐준 후 출력한다.
	}
## feedback에 대한 개선 ##  3의배수
	import 'dart:io';
	void main() {
		String line = stdin.readLineSync();
		int num = int.parse(line);

		List<String> arr = new List(num);
		int i = 1;
		List<String> arrResult = arr.map((value){
			value = i++;
			if((i - 1) % 3 == 0)
			{
				value = 'X';
			}
			return value;
		});
		print(arrResult.join(' ') + ' ');
	}
for문을 사용하지 않고 map을 사용하여 새로운 리스트를 만들어 결과를 도출하였다. 입력받은 num많큼 반복해야하여 List의 값을 num만큼 설정하여 반복할 수 있었다.

# 구름 ide - 비트연산 기본 1

	import 'dart:io';
	void main() {
		String line = stdin.readLineSync();
		List<String> arrLine = line.split(' ');
		List<int> arrInt = arrLine.map(int.parse).toList();
		List<Operator> bg = [and, or, xor]; 

		bg.forEach((value){
			print(calculate(arrInt[0], arrInt[1], value));
		});
	}

	typedef Operator(int a, int b);

	int calculate(int a, int b, Operator oper){
		return oper(a, b);
	}

	int and(int a, int b)
	{
		if(a == 1 && b == 1){
			return 1;
		}
		else{
			return 0;
		}
	}

	int or(int a, int b)
	{
		if(a == 1 || b == 1){
			return 1;
		}
		else{
			return 0;
		}
	}

	int xor(int a, int b)
	{
		if(a == b){
			return 0;
		}
		else{
			return 1;
		}
	}
if, else if를 쓰면 어려운 문제는 아니였다. 그래서 일부러 forEach도 써보고, typedef도 처음으로 써본 문제이다. 여러가지 방법으로 풀어보고 싶어 다양하게 풀어봤던것 같다. 
만약 값을 입력받아 계산하는 문제였다면 typedef가 꽤나 유용했을 것 같다. 

# 구름 ide - 모양찍기

	import 'dart:io';
	void main() {
		String line = stdin.readLineSync();
		int num = int.parse(line);

		List<String> arrLine = new List(num);  // num 크기의 List를 생성한다. 
		arrLine.forEach((value){  // forEach를 사용하여 반복구문을 만들어준다. 
			value = '*' * num;  // 처음 입력받은 크기인 num을 활용하여 *을 수만큼 출력해준다.
			num--;  // num--로 하나씩 줄여 다음 루핑때 *의 수를 조절한다.
			print(value);
		});
	}

# 구름 ide - Substring

	import 'dart:io';
	void main() {
		String line = stdin.readLineSync();  // 첫번째 입력받을 문자열을 받기 위한 입력스트림
		String Num = stdin.readLineSync();  // 두번째로 시작점과 시작점으로 부터 자를 문자 수를 받을 입력스트림
		List<String> strNum = Num.split(' ');  // 두번째 받은 입력값을 String에서 List로 바꿔주는 split 메서드
		List<int> intNum = strNum.map(int.parse).toList();  // String타입의 strNum 리스트를 int타입의 intNum 메서드로 바꿔주기 위한 map 메서드

		print(line.substring(intNum[0] - 1).substring(0, intNum[1]));	// String타입에 적용하는 .substring()메서드를 활용한 값 도출
	}

# 구름 ide - 가위바위보

	import 'dart:io';
	import 'dart:math';

	void main() {
		String line = stdin.readLineSync();
		List<String> arrLine = line.split(' ');
		List<int> arrInt = arrLine.map(int.parse).toList(); 

		List<int> checkNum = [1, 2, 3];  // 위에서 만든 arrInt 리스트가 어떠한 숫자로 구성되었는지 확인하기 위해 만든 리스트이다.
		int winner = 0; 
		int losser = 0;
		int count = 0;  

		checkNum.forEach((value){
			if(arrInt.contains(value)){
				count++;	
			}
		});

		if(count == 2){  // 서로다른 2개의 수로 이루어져있다는 뜻이다. 서로 같거나(1), 서로 다 다를경우(3)를 제외하고 계산하였다.
			if(arrInt.reduce(min) == 1){  // arrInt 리스트중 최소값을 구하여 리스트가 어떠한 수로 이루어져있는지 파악하기 위해 사용하였다.
					arrInt.forEach((val){
						if(val == 2){  // arrInt 리스트에 서로다른 두 값이 있는데 그 중 최소값이 1이라면 다른 나머지 2인 요소들의 수에따라 승자가 결정된다.
							winner++;
						} else if(val == 3){  // 다른 요소들이 3이라면 losser라는 임의의 변수를 만들어 그걸 총 수인 5에서 빼줌으로써 winner의 수를 구하였다.
							losser++;
							winner = 5 - losser;
						}
					});
				} else{  // else를 쓴 이유는 1, 2, 3중 최소값은 1, 2밖에 없기 떄문이다. 아래의 코드는 위와 같은 원리이다.
						arrInt.forEach((val){  
						if(val == 3){
							winner++;
						} else if(val == 1){
							losser++;
							winner = 5 - losser;
						}
					});
				} 
		}
		print(winner);
	}

# 구름 ide - Hello Goorm !

	import 'dart:io';
	void main() {
		String line = stdin.readLineSync();
		int num = int.parse(line);

		List<int> arr = new List(num);

		arr.forEach((val) => print('Hello Goorm !'));
	}

# 구름 ide - 공백 없애기

	import 'dart:io';
	void main() {
		String line = stdin.readLineSync();
		List<String> arrLine = line.split(' ');
		String result = arrLine.join('');

		print(result);
	}

# 구름 ide - 삼각형의 넓이

	import 'dart:io';
	void main() {
		String line = stdin.readLineSync();
		List<String> arrLine = line.split(' ');
		List<double> arrDouble = arrLine.map(double.parse).toList();

		double result = arrDouble.reduce((total, element) => total * element * 0.5);
		print(result.toStringAsFixed(1));
	}

# 구름 ide - Bubble Sort 

	import 'dart:io';
	import 'dart:math';

	void main(){
		String line = stdin.readLineSync();
		int num = int.parse(line);  // 배열의 크기를 정해주는 num값을 받는다.

		String ns = stdin.readLineSync();
		List<String> arrNs = ns.split(' ');
		List<int> intNs = arrNs.map(int.parse).toList();  // 배열에 들어갈 갑들을 입력받는다.

		int m;  // 임시로 값을 가지고 있어줄 변수를 설정하였음

		for(int i = 0; i < num; i++)  // 반복문으로 배열의 앞자리에 올 인덱스를 나타내기 위해 설정하였음
		{
			for(int j = i+1; j < num; j++)  // 배열의 뒷자리에 올 인덱스를 나타내기 위해 설정하였음
			{
				if(intNs[i] > intNs[j])  // 배열의 앞자리와 인접한 뒷 자리를 비교함
				{
					m = intNs[i];  // 위에서 설정한 임시 변수에 앞자리 값을 넣어놓은뒤 
					intNs[i] = intNs[j];  // 뒷자리 값을 앞자리에 넣어주고 
					intNs[j] = m;  // 다시 받아놨던 변수의 값을 가져와 뒷자리 값에 넣어준다. 이걸 반복하여줌! 
				}
			}
		}
		print(intNs.join(' ') + ' ');
	}

# 구름 ide - 거스름돈

	import 'dart:io';
	void main() {
		String line = stdin.readLineSync();
		int price = int.parse(line);  // 물건 가격을 입력받음

		int maxPrice = 1000;  // 최대가격 설정;
		List<int> changeUnit = [500, 100, 50, 10];  // 리스트를 통해 각각의 거스름돈을 설정함
		List<int> arrResult = new List(4);  // 결과값들을 받아줄 리스트 생성

		int i = 0;  // 인덱스 값을 나타낼 변수 i 설정
		int change = maxPrice - price;  // 나머지 값을 나타낼 변수 설정 

		changeUnit.forEach((val){  // 거스름돈들이 몇개씩인지 나타낼 반복문 형성
			arrResult[i] = change ~/ val;  // 각각의 거스름돈의 개수를 arrResult 리스트에 값을 담아줌
			change %= val;  // change 변수를 활용하여 각각의 단위의 거스름돈으로 나눈 나머지 값을 받도록함
			i++;  // 인덱스의 수를 올려줌
		});
		String result = arrResult.join(' ');  // arrResult 리스트에 있는 값을 출력하기 좋게 String 변수에 담아줌
		print(result + ' ');  // 출력 형태에 따라 마지막에 공백을 넣어줌
	}

# 구름 ide - 몫과 나머지

	import 'dart:io';
	void main() {
		String line = stdin.readLineSync();
		List<String> arrLine = line.split(' ');
		List<int> arrInt = arrLine.map(int.parse).toList();  // 입력받은 String 값을 String List에서 int List로 변환하여줬다.
		List<int> result = new List(2);  // 값을 담을 크기 2의 리스트를 생성한다.

		result[0] = arrInt[0] ~/ arrInt[1];  // 입력받은 값들을 담고있는 arrInt 리스트의 0, 1번 인덱스를 가져와 result 메소드의 0번인덱스 자리에 넣어준다. ~/는 버림 연산자로                                                             double 형태로 결과값을 가지더라도 정수형태의 값만 나타내준다. 
		result[1] = arrInt[0] % arrInt[1];  // 마찬가지로 % 나머지 연산을 사용하여 값을 넣어줬다.
		print(result.join(' '));
	}

# 구름 ide - 16진수

	import 'dart:io';
	void main() {
		String line = stdin.readLineSync();
		int num = int.parse(line);

		print(num.toRadixString(16));  // 10진수를 16진수로 바꿔주는 메서드이다. int.toRadixString(16)
	}

# 구름 ide - ASCII 코드

	import 'dart:io';
	void main() {
		String line = stdin.readLineSync(); 

		print(line.codeUnitAt(0));  // 문자열을 ASCII코드 값으로 바꿔주는 메서드이다. String.codeUnitAt(0)
	}

# 구름 ide - 윤년

	import 'dart:io';
	void main() {
		String line = stdin.readLineSync();
		int year = int.parse(line);  // 년도값을 받을 변수 설정
		String result;  // 출력 값을 담을 변수 설정

		if(year % 4 == 0){  // 4로 나누어 떨어지는 해들을 구함, 조건에 부합하면 result 변수에 결과값을 담아줌
			result = 'Leap Year';
			if(year % 100 == 0){  // 4로 나누어 떨어지는 해들중에 100으로 나누어 떨어지면 윤년이 아니기 때문에 result 변수에 윤년이 아니라는 결과값을 담아줌
				result = 'Not Leap Year';
				if(year % 400 == 0){  // 4로 나누어 떨어지면서 100으로 나누어 떨어지는 년도들 중에 400으로 나누어 떨어지면 윤년이기 때문에 다시 결과값에 윤년이라고 값을                                                            넣어줌
					result = 'Leap Year';
				}
			}
		}else{
			result = 'Not Leap Year';  // 년도가 4로 나누어 지지 않으면 윤년이 아니기 떄문에 result 값에 윤년이 아니라는 값을 담아줌
		}
		print(result);  // 결과값을 담아줬던 result 변수 출력
	}

# 구름 ide - 피라미드

	import 'dart:io';
	void main() {
		string line = stdin.readLineSync();
		int num = int.parse(line);  // 배열의 층수에 해당하는 값을 입력받음

		List<String> arrLine = new List(num);  // 배열의 반복인 forEach를 쓰기위해 num만큼의 크기인 List를 생성함
		int i = 1;  // 배열의 요소에 대입할 변수 i 선언

		arrLine.forEach((val){  // forEach 메서드를 사용하여 num만큼 반복하는 반복문을 만듬
			val = i;  // arrLine 리스트의 요소에 1부터 num까지 커지는 값을 대입함
			print(' ' * (num - i) + '*' * (2 * i - 1));  // 리스트의 요소의 크기에 따라 피라미드를 만들 구문을 입력함
			i++;
		});
	}

# 구름 ide - 세로 순서 사각형

	import 'dart:io';
	void main() {
		String line = stdin.readLineSync();
		int num = int.parse(line);

		List<int> arrInt = new List(num);  // num크기를 가진 List를 생성 후, forEach를 사용하여 반복문을 만들어줌
		List<int> arrName = new List(num);  // 도출된 값을 담을 arrName List를 생성 함
		int i = 1;  // 1씩 증가하는 값을 받을 변수 i 설정

		arrInt.forEach((val){
			for(int j = 0; j < num; j++)  // 반복문 생성
			{
				arrName[j] = (num * j + i);	// 일정한 규칙을 찾아 도출된 값을 담을 arrName 리스트에 담음!
			}
			String k = arrName.join(' ');  // 완성된 리스트인 arrName의 값을 String으로 합쳐 출력하기 좋게 함
			print(k + ' ');
			i++;
		});
	}

# 구름 ide - 인공지능 청소기

	import 'dart:io';
	void main() {
		String line = stdin.readLineSync();
		int num = int.parse(line); // 몇번의 테스트 케이스를 진행할지 수를 입력받는다.

		List<String> arrLine = new List(num);
		List<String> result = new List(num);
		int i = 0;

		arrLine.forEach((val){
			String test = stdin.readLineSync();  // String값을 입력받는 입력메소드
			List<String> arrTest = test.split(' ');  // 입력받은 메소드를 split()메소드를 써서 String 리스트로 값을 넣어줌
			List<int> intTest = arrTest.map(int.parse).toList();  // String 리스트를 map 메소드를 써서 int자료형 리스트로 바꿔줌

			result[i] = 'NO';  // result 리스트의 기본값을 NO로 설정하고 만약 조건에 부합하면 YES값을 넣도록 설정하였다.

			if(intTest[2] >= 1 && intTest[2] <= 2000000000 && intTest[0].abs() <= 1000000000 && intTest[1].abs() <= 1000000000) 
			// 조건에 따라 입력한 값인 X, Y좌표 값은 10억 이하인 정수, N은 1이상 20억 이하의 자연수로 조건을 달아주었다. 
			{
				for(int x = 0; x <= intTest[2]; x++)  // x는 작으면 0부터고 최대로 해봤자 N보다 크기가 작아야 하므로 0이상 N이하로 크기를 정하였다.
				{
					for(int y = 0; y <= intTest[2]; y++)
					{
						if(intTest[0].abs() + intTest[1].abs() <= intTest[2] && (intTest[0].abs() * x) + (intTest[1].abs() * y) == intTest[2]) 
						// 입력한 좌표값의 절대값들을 더하면 N보다 이하이고, 좌표값들의 절대값들 * (x, y)를 곱해 N으로 떨어져야 해서 조건문을 설정하였다.
						{
							result[i] = 'YES';
						}
					}
				}
			}
			i++;
		});
		result.forEach((val) => print(val));
	}

열심히 생각해서 풀었다. 아무리 생각해도 맞는거 같은데 통과하지 못한 테스트 케이스가 있다고 해서, 내일 아침에 물어보려한다. 자기전에 좀 더 생각해보다가 잘것이다(업데이트가 안될수있음)

	import 'dart:io';
	void main() {
		String line = stdin.readLineSync();
		int num = int.parse(line); // 몇번의 테스트 케이스를 진행할지 수를 입력받는다.

		List<String> arrLine = new List(num);
		List<String> result = new List(num);
		int i = 0;

		arrLine.forEach((val){
			String test = stdin.readLineSync();  // String값을 입력받는 입력메소드
			List<String> arrTest = test.split(' ');  // 입력받은 메소드를 split()메소드를 써서 String 리스트로 값을 넣어줌
			List<int> intTest = arrTest.map(int.parse).toList();  // String 리스트를 map 메소드를 써서 int자료형 리스트로 바꿔줌

			result[i] = 'NO';  // result 리스트의 기본값을 NO로 설정하고 만약 조건에 부합하면 YES값을 넣도록 설정하였다.
			int z;

			if(intTest[2] >= 1 && intTest[2] <= 2000000000 && intTest[0].abs() <= 1000000000 && intTest[1].abs() <= 1000000000) 
			// 조건에 따라 입력한 값인 X, Y좌표 값은 10억 이하인 정수, N은 1이상 20억 이하의 자연수로 조건을 달아주었다. 
			{
				z = intTest[2] - (intTest[0].abs() + intTest[1].abs());  
				// intTest[0].abs() + intTest[1].abs()의 값은 무조건 N의 값보다 작을 수 밖에 없는데 N에서 x, y좌표의 절대값을 더한 값을 뺀 값을 변수로 받는다. 
				if(intTest[0].abs() + intTest[1].abs() <= intTest[2] && z % 2 == 0){  
		// 앞의 조건은 당연하고 뒤의 조건인 N에서 x,y좌표의 절대값을 뺀 값이 2로 나누어 지면 그 좌표는 어디던 N번째에 도착을 할 수 있다는 뜻이므로 조건으로 사용할 수 있다.
					result[i] = 'YES';
				}
			}
			i++;
		});
		result.forEach((val) => print(val));
	}
뭐가 빠졌는지 계속 생각해보다가 원칙적인 규칙을 찾다보니 알게되었다. 문제를 자세히 읽고 원하는 결론을 유도리있게 생각하는 방법을 더욱 키워야 겠다.. 

# 구름 ide - 파도 센서 (1/ 8)

	import 'dart:io';
	import 'dart:math';

	void main() {
		String line = stdin.readLineSync();
		List<String> arrLine = line.split(' ');
		List<int> arrIntLine = arrLine.map(int.parse).toList();  // 쨸 처음인 물결파의 x,y좌표와 r의 값을 입력받아 리스트에 넣어준다.

		List<int> findMin = new List(5);  // 각 좌표들의 r값을 모으기 위한 리스트 생성
		int check;  // 각 좌표들의 r값중 쨀 가까운 좌표의 값을 받기 위한 변수 설정

		if(arrIntLine[0].abs() <= 1000 && arrIntLine[1].abs() <= 1000 && arrIntLine[2] <= 1000)
			// 조건인 물결파의 중심 좌표인 x, y의 값들이 1000이하인 정수이며, r은 1000이하의 자연수임을 조건으로 설정하였다.
		{
			for(int i = 0; i < 5; i++)  // 5번의 센서의 좌표를 입력받아야 하기에 반복문을 형성했다.
			{
				String location = stdin.readLineSync();
				List<String> arrLocation = location.split(' ');
				List<int> arrIntLocation = arrLocation.map(int.parse).toList();

				findMin[i] = sqrt(pow(arrIntLocation[0] - arrIntLine[0], 2) + pow(arrIntLocation[1] - arrIntLine[1], 2)).round();
				// 여러 메서드를 사용했는데 우선 제곱을 나타내는 pow()메서드와, 제곱근을 나타내는 sqrt, 마지막으로 소수점 이하를 반올림해주는 round()메소드를 사용하여 r값                                    을 구하였다.
			}
			check = findMin.reduce(min);  // .reduce(min) 메서드를 사용하여 여러 좌표들의 r값중 가장 최소값을 변수 check에 담아주었다.
			if(check <= arrIntLine[2])  // 그 최소값이 쨸 처음 입력받은 물결파의 r(반지름)의 길이보다 작거나 같아야 센서가 감지되기 떄문에 체크해주었다.
			{
				print(findMin.indexOf(check) + 1);  // List를 찾는 방법중 하나인 .indexOf메서드를 사용하여 해당 값에 대한 인덱스를 찾아준후 + 1을 하여 센서의 순서를 출                                                                        력한다.
			} else{
				print(-1);  // 최소값이 처음 입력받은 물결파의 r(반지름)보다 클 경우 감지되는 센서가 없을 때에 출력한 -1을 나타냈다.
			}
		}
	}
다양한 math 라이브러리의 메서드를 사용해 볼 수 있는 문제였다. pow(int x, 지수) 제곱을 나타내주는 pow메서드와, sqrt(int x) x의 제곱근을 나타내는 sqrt 메서드, 소수점 이하를 반올림해주는 round 메서드, index값을 찾아주는 indexOf(값) 메서드, 리스트의 최소값을 찾아주는 .reduce(min) 메서드 등 여러가지를 사용해보고 익힐 수 있었다. 

