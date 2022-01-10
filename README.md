****
# **구름 ide 2단계**
## 구름 ide - 약수의 합

	import 'dart:io';

	void main() {
		var line = stdin.readLineSync();
		int num = int.parse(line);  // 약수를 구할 자연수 n을 입력받는다.
		List<int> arrLine = [];  // 약수들을 모아줄 리스트를 생성한다.

		for(int i = 1; i <= num; i++){  // 1부터 n까지 돌며 n의 약수를 찾는다.
			if(num % i == 0){
				arrLine.add(i);  // 찾은 약수를 arrLine 리스트의 값으로 넣어준다.
			}
		}
		int total = arrLine.reduce((total, element) => total + element);  // reduce 메서드를 이용해 총합을 계산한다.
		print(total);	
	}

# 구름 ide - 소수 판별

	import 'dart:io';
	void main() {
		var line = stdin.readLineSync();
		int num = int.parse(line);  // 소수인지 확인하고 싶은 값을 입력받는다.
		String bool = 'True';  // 기본 값을 True로 설정해 준다. 

		for(int i = 1; i < num; i++){  // 소수인지 확인하기 위한 반복문을 설정한다.
			if(num % i == 0 && i != 1){  // 입력받은 숫자의 1인 아닌 약수를 찾아서 약수가 존재하면 소수가 아니므로 False 값을 넣어준다.
				bool = 'False';
			}
		}
		print(bool);
	}

# 구름 ide - 문자열 뒤집기

	import 'dart:io';
	void main() {
		var line = stdin.readLineSync();  // 문자열 입력받기
		List<String> arrLine = line.split('');  // split 메서드로 문자열 리스트 생성하기

		print(arrLine.reversed.join(''));  // reversed 메서드사용해서 리스트 거꾸로 뒤집은 후 join 메서드로 String으로 변환시켜주기
	}

# 구름 ide - 완전수

	import 'dart:io';
	void main() {
		var line = stdin.readLineSync();
		List<String> arrLine = line.split(' ');
		List<int> arrIntLine = arrLine.map(int.parse).toList();  // 입력받은 값들을 정수로 나눠 리스트에 넣어줌 

		int total = 0;  // 약수들의 합을 구할 변수 설정
		List<int> result = [];  // 완전수인 수들을 모으기 위한 리스트 생성

		if(arrIntLine[0] < arrIntLine[1] && arrIntLine[0] <= 10000 && arrIntLine[1] <= 10000){  // 입력받은 값들로 초기 입력 조건을 설정하여준다.
			for(int i = arrIntLine[0]; i <= arrIntLine[1]; i++){  // 범위의 시작값과 끝값을 설정하여 반복문을 돌려줌
				for(int j = 1; j < i; j++){  // i의 범위 중에서 반복문을 돌려 i의 약수들을 찾아준다.
					if(i % j == 0) total += j;  // 그 약수들의 합을 구해준다.
				}
				if(total == i) result.add(i);  // 바로 위의 j를 이용한 반복문인 끝난 후 total == i이 인지 비교하여 결과값을 받는 result 리스트에 값을 담아준다.
				total = 0;  // 위에서 다시 반복문으로 다른값을 찾도록 약수들의 합을 구할 변수인 total을 0으로 초기화해준다.
			}
		}
		print(result.join(' ') + ' ');  // 출력 조건에 맞도록 설정해준다.
	}
	
# 구름 ide - 계산기
	
	import 'dart:io';
	void main() {
		var line = stdin.readLineSync();
		List<String> arrLine = line.split(' ');  // list의 가운데 사칙연산인 문자열이 있기때문에 바로 숫자로 전환하지 않고 String 형식으로 리스트를 생성하였다.

		int first = int.parse(arrLine[0]); // list의 값들이 String 형식이기 떄문에 int 형식으로 바꿔준다.
		int last = int.parse(arrLine[2]);

		switch(arrLine[1])  // 리스트의 사칙연산 부호를 switch문을 사용하여 경우를 나눠준다.
		{
			case '+' :
				print(first + last);
				break;
			case '-' :
				print(first - last);
				break;
			case '*' :
				print(first * last);
				break;
			case '/' :
				print((first / last).toStringAsFixed(2));  // .toStringAsFixed() 메서드를 사용하여 소수 둘째 자리까지 표시하였다.
				break;
		}
	}

# 구름 ide - 유클리드 호제법

	import 'dart:io';

	void main() {
		var line = stdin.readLineSync();
		List<String> arrLine = line.split(' ');
		List<int> arrIntLine = arrLine.map(int.parse).toList();
		int num;  // gcd() 메서드의 b에 들어갈 값을 받아줄 변수를 설정하였다.

		int gcd(int a, int b){  // gcd 메서드에 들어갈 매개변수 2개를 설정한다.
			while (b != 0){  // while 반복문을 사용해 b가 0이 될때까지 반복시킨다.
				num = b;  // 위에서 임의로 설정해준 변수 num에 b의 값을 넣어주고
				b = a % num;  // 기존의 b의 자리에 a % b를 계산한 값을 넣어준다.
				a = num;  // 계산한 값을 다시 a에 넣어준다.
			}
			return a;
		}
		print(gcd(arrIntLine[0], arrIntLine[1]));
	}
