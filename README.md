# 구름 ide - 파도 센서

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

