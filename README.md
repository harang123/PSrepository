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
