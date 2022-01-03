# PSrepository
ProblemSolving about groomide

// 구름 ide - 약수 구하기
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
}
