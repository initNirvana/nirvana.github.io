 
# (PART) 2017 june {-}
# load를 불러오시겠습니까?  {#Take-your-load}
2017 june 

예전에 TAOCP 1권의 MMIX 부분을 읽고 있던 중 <b>적재(load)</b>라는 단어를 보게 되었다. LDA는 알고 있었으나 Load라는 단어의 뜻은 불러오기밖에 몰랐었다. 

일단 TAOCP 1권에서 LDA를 설명하는 인용[^5]을 보도록 하자.

> LDA (load A; A에 적재). C = 8; F = 필드 

> CONTENTS(M)의 지정된 필드로 레지스터 A의 이전 내용을 대체 한다. <br/> 부분 필드가 입력으로 쓰이는 모든 명령에서, 필드 자체에 부호가 포함되어 있으면 그 부호가 쓰이고, 그렇지 않으면 부호는 +로 간주된다. 레지스터에 **적재**될 때, 필드는 그 오른쪽 끝이 레지스터의 오른쪽 끝에 일치하도록 적절히 이동된다.

이해하기 어렵다. 책의 예제를 보자.

> 예 : F가 정규 필드 명세 (0:5)이면 장소 M의 모든 내용이 rA에 복사된다. F가 (1:5)이면 CONTENTS(M)의 절대값이 부호 +와 함께 적재된다. M에 어떤 명령 워드가 들어 있으며 F가 (0:2)이면 그 “±AA 필드”가 A에 다음과 같이 **적재**된다. 
> [±000AA]

이번엔 다른 책[^6]을 보자. 

> LOAD : 기억장치로부터 데이터를 읽어서 누산기(AC)에 **적재**

또 다른 책[^7]을 보자. 

> 명령어 LDA | LDA B | 피연산자의 자료 B(주소 B의 자료)를 레지스터에 **가져오는** 명령어

뭔가 조금 다르다. 같은 LDA가 맞는지 혼란스럽다. 다른 책 알아보는건 그만두고, 영문을 보자.

LDA X : Load the AC with the contents of memory address X.

- AC에 메모리 주소 X의 내용을 적재한다.
- AC에 메모리 주소 X의 내용을 불러온다.

누가 적절하지 않은 용어를 쓰고 있을까?

용어 이야기는 여기까지 하고 컴퓨터 내부로 가보자. 니모닉 LDA를 실행하면 내부에서 어떤일이 일어날까?

다음은 LOAD addr의 마이크로 연산이다.

1. t_0 : MAR <- IR(addr)
2. t_1 : MBR <- M[MAR]
3. t_2 : AC <- MBR

첫번째 주기에서는 명령어 레지스터 IR에 loaded한 명령어의 오퍼랜드인 주소(addr)를 MAR을 통하여 기억장치로 보낸다.  두번째 주기에는 주소가 지정하는 기억장소로부터 데이터를 인출하여 MBR에 저장하며, 그 데이터를 세번째 주기에서 AC 레지스터에 load함으로써 LOAD 명령어의 실행이 완료된다.

load(or loaded)를 적재나 불러오기로 읽어보라.

이번엔 다른 예문을 보자.
메모리 주소 X의 내용을 언급할때는, 주소가 X인 메모리 워드에 현재 저장된 정수를 말한다. AC에 메모리 주소 X의 내용을 간접적으로 **적재한다는** 의미는, 주소 X의 내용을 **적재하는 것이** 아닌(내용(contents)가 **적재됬을때**) 다른 주소의 내용으로 처리한다는 것을 의미한다.

**적재**를 **불러온다**로 바꿔보자.

AC에 메모리 주소 X의 내용을 간접적으로 **불러온다는** 의미는, 주소 X의 내용을 **불러오는**것이 아닌(내용(contents)을 **불러왔을때**) 다른 주소의 내용으로 처리한다는 것을 의미한다.

불러왔다는 의미보다는 **적재**라는 의미가 더 적절하다.

결론은 단어 공부는 꾸준하게, 안다고 생각하는 것도 다시 보자.

[^5]: 컴퓨터 프로그래밍의 예술 1 vols. 도널드 크누스 지음. 류광 옮김. 한빛미디어.  2006년. pp. 166 

[^6]: 컴퓨터 구조론. 김종현 지음. 생능출판. 2013년. pp. 97

[^7]: 컴퓨터 개론. 강환수, 조진형, 신용현, 강환일 공저. 인피니티북스. 2015년. pp. 125

