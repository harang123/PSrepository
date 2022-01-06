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
문제에서 주는 힌트에 너무 집중한것 같다. 매번 문제를 풀때 힌트에 기대는 것이 아닌 가장 효율적인 코드를 짜도록 시도하자

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
