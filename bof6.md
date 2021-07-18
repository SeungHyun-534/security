# bof 6

가장 주목할 점은 쉘코드가 vuln 함수의 지역변수로서 스택에 들어있다는 점이다. 때문에 ret 주소에 해당 스택 주소를 넣어줄 수 있다면 쉘코드가 실행될 것이다. 다행히도 printf 함수에서 %p를 통해 shellcode의 주소를 출력해주므로 우리는 sfp까지 더미로 채우고 printf에 뜬 주소를 넣으면 될 것이다. 더미의 크기는 버퍼의 크기(128 byte) + sfp(8 byte) = 136byte


따라서 터미널에 입력해야 하는 명령은 다음과 같다.

``` bash
$ (python -c 'print "a"*136" + "\xf0\xea\xff\xff\xff\x7f\x00\x00"' ;cat) | ./bof6
```