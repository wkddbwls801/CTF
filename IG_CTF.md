# IGRUS CTF

## MISC-vbcat      
![image](https://user-images.githubusercontent.com/59531805/80910656-fd5d7900-8d6b-11ea-8615-627829fcede7.png)   
확장자가 .xlsm로 매크로가 있는 엑셀 파일임을 알 수 있다.   
![image](https://user-images.githubusercontent.com/59531805/80910671-19f9b100-8d6c-11ea-9929-49e0d8cdc7ef.png)   
들어가면 귀여운 고양이가 있다. 매크로를 실행할 수 있는 버튼이 있을 줄 알았는데 없어서 당황...    
![image](https://user-images.githubusercontent.com/59531805/80910697-46adc880-8d6c-11ea-8936-23cff5a2ba3e.png)   
main이라는 매크로가 존재한다. 안에 코드를 보면 다음과 같다.
``` VB
Sub Main()

Dim YnVm(30) As Integer
Dim a2V5 As Integer
Dim aWR4 As Integer

aWR4 = 0
a2V5 = 111
YnVm(0) = 9
YnVm(1) = 3
YnVm(2) = 14
YnVm(3) = 8
YnVm(4) = 20
YnVm(5) = 22
YnVm(6) = 10
YnVm(7) = 14
YnVm(8) = 7
YnVm(9) = 48
YnVm(10) = 25
YnVm(11) = 13
YnVm(12) = 48
YnVm(13) = 12
YnVm(14) = 14
YnVm(15) = 27
YnVm(16) = 48
YnVm(17) = 3
YnVm(18) = 10
YnVm(19) = 14
YnVm(20) = 11
YnVm(21) = 48
YnVm(22) = 22
YnVm(23) = 0
YnVm(24) = 26
YnVm(25) = 48
YnVm(26) = 7
YnVm(27) = 10
YnVm(28) = 29
YnVm(29) = 10
YnVm(30) = 18

For aWR4 = 0 To 30
    YnVm(aWR4) = a2V5 Xor YnVm(aWR4)
    
End Sub
```
분석해 보면 YnVm(aWR4) 배열과 와 a2V5값을 XOR 연산하면 된다.(처음에는 누적인 줄 알고 숫자가 하나 나오길래 당황했는데 알고보니 누적이 아니었다.)
파이썬 코드를 작성해보면 다음과 같다.
``` python
YnVm=[9, 3,14, 8, 20, 22, 10, 14, 7, 48, 25, 13, 48, 12, 14, 27, 48, 3, 10,
      14, 11, 48, 22, 0, 26, 48, 7, 10, 29, 10, 18]

a2V5 = 111

for aWR4 in range(0,30):
    YnVm[aWR4]=bin(a2V5 ^ YnVm[aWR4])
    print(YnVm[aWR4])
```
출력을 해보면 숫자로 나와 문자로 바꾸면 되겠다고 생각하고 print(chr(YnVm[aWR4]))를 해보았으나 이유는 모르겠으나 잘 되지 않았다.
결과는 다음과 같다.
```
0b1100110
0b1101100
0b1100001
0b1100111
0b1111011
0b1111001
0b1100101
0b1100001
0b1101000
0b1011111
0b1110110
0b1100010
0b1011111
0b1100011
0b1100001
0b1110100
0b1011111
0b1101100
0b1100101
0b1100001
0b1100100
0b1011111
0b1111001
0b1101111
0b1110101
0b1011111
0b1101000
0b1100101
0b1110010
0b1100101
```
이 숫자들을 그냥 다 변환기에 넣고 돌렸다.   
![image](https://user-images.githubusercontent.com/59531805/80910813-229eb700-8d6d-11ea-8fe2-cb4ff63faeab.png)   
금방 flag를 얻을 수 있었다!!


