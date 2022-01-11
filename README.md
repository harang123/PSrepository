# 구름 ide - Factorial(계승)

	import 'dart:io';
	void main() {
		var line = stdin.readLineSync();
		int num = int.parse(line);

		List<int> arrNum = new List(num);
		int i = 1;  // 반복문에서 1씩 더해가며 n까지 곱해줄 변수 설정
		int result = 1;  // 결과값을 받을 변수 설정

		if(num > 0 && num <= 15)  // 조건에 해당하는 0보다 크고 15이하인 양수
		{
			arrNum.forEach((val){  // 입력받은 num의 크기만큼의 리스트를 설정하고 forEach를 이용해 num만큼 반복
				result *= i;  // 위에서 설정해놓은 result변수에 i를 계속 곱해 결과값에 넣어줌
				i++;
			});
		}
		print(result);
	}

# 구름 ide - 은행 예금 이자 구하기

	import 'dart:io';
	void main() {
		var line = stdin.readLineSync();
		List<String> arrLine = line.split(' ');
		List<double> arrIntLine = arrLine.map(double.parse).toList();  // 입력받은 값들을 String에서 double로 변환시켜 List에 넣음

		List<String> loop = new List(arrIntLine[2].floor());  // 입력받은 값들중 2번 인덱스값인 년차 수 만큼의 크기를 가진 List를 만들어 반복문을 만들어준다.
		double result = arrIntLine[0];  // 원금을 받아줄 변수를 설정해준다.

		loop.forEach((val){  // 위에서 만든 년차 수 만큼 반복하는 반복문 생성
			result += result * arrIntLine[1] / 100;  // 이자율만큼의 추가 이자액이 더해지는 것이므로 원금에 += 원금 * 이자율 / 100을 해줬다. 
		});
		print(result.toStringAsFixed(2));  // .toStringAsFixed 메서드를 사용하여 소수점 둘째 자리까지 출력한다.
	}
	
# 구름 ide - Knight's Move 안풀려서 다음에 시도 

