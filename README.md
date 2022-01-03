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
	
	
