
it is need to 

- Convention(Code style, Project Structure)
- Domain Information 
- Agent Workflow 



Always
- 항상 자동으로 참조 
- 코드 스타일 컨벤션 
- 모든 파일에서 항상 지켜야할 것 



Auto Attached 
Agent Requested 
Manual 
- 수동으로 참조
- 행동 단위 워크플로우 정의 (구현, 테스트, API 연동)
- 작업 순서를 단계적으로 서술 
- 최대한 자세하게

https://www.youtube.com/watch?v=5rCk0tjkvNM



Ctrl + L = ASK 모드 실행 
```
- 이 프로젝트 구조를 자세히 파악해줘.  
코드 컨벤션, 스타일, 디자인 규칙을 모두 분석해서 자세히 설명해줘.
 

```

Text를 그냥 붙여넣는게 아닌 Generate Cursor Rules 

chating window + enter / 

![[Pasted image 20250902171452.png]]

Agent 모드로 요청
내용은 영어로 작성해. 대표적인 프롬프트 엔지니어링 기법을 적용해서 최적하해줘 
반드시 지켜야할 규칙, 반드시 하지말아야할 것들을 특히 강조해서 적어줘. 


만약 rule setting 을 하더라도 Error가 발생하거나 만족스러운 결과가 아닐경우 
cursor rule을 setting 하도록 하면된다.

---


에러가 발생한경우 

```
에러가 발생했어. 이 에러가 발생한 원인을 알려주고 수정도 해줘 

~~ 에러메시지 ~~~ 

```

```
footer 문구는 변경되지 않았어. 이걸 고치고, 왜 이런 실수를 했는지 해명해
```

이렇게 나온 해명글을 다시 Generate Cursor Rules 를 이용하여 Setting 하여 추가해주면 된다.

생성된 rule에 대해서 설명을 읽어보고 Always, manual, agent generated 등 상황에 맞게 설정해주면 된다

error 관련 rule -> always 



Rule은 커서를 위한 온보딩 문서.
Always, Manual 유형이 있다.
보통 Always를 쓴다

초안은 Generate Cursor Rules, 
이후엔 스스로 개선시킨다.

---


How to write 

1.grasp code structure using Ask mode 
2.Generate Cursor Rules 로 생성 
- write use english 
- prompt engineering 
- include core keyword 

continuous improvement 

1. error explanation instruction
2. prevent recurrence instruction rule write 

---




Ctrl + L = ASK 모드 실행 
```
- 이 프로젝트 구조를 자세히 파악해줘.  
코드 컨벤션, 스타일, 디자인 규칙을 모두 분석해서 자세히 설명해줘.
 

```

Text를 그냥 붙여넣는게 아닌 Generate Cursor Rules 

chating window + enter / 

![[Pasted image 20250902171452.png]]

Agent 모드로 요청
내용은 영어로 작성해. 대표적인 프롬프트 엔지니어링 기법을 적용해서 최적하해줘 
반드시 지켜야할 규칙, 반드시 하지말아야할 것들을 특히 강조해서 적어줘. 


만약 rule setting 을 하더라도 Error가 발생하거나 만족스러운 결과가 아닐경우 
cursor rule을 setting 하도록 하면된다.

---


에러가 발생한경우 

```
에러가 발생했어. 이 에러가 발생한 원인을 알려주고 수정도 해줘 

~~ 에러메시지 ~~~ 

```

```
footer 문구는 변경되지 않았어. 이걸 고치고, 왜 이런 실수를 했는지 해명해
```

이렇게 나온 해명글을 다시 Generate Cursor Rules 를 이용하여 Setting 하여 추가해주면 된다.

생성된 rule에 대해서 설명을 읽어보고 Always, manual, agent generated 등 상황에 맞게 설정해주면 된다

error 관련 rule -> always 



Rule은 커서를 위한 온보딩 문서.
Always, Manual 유형이 있다.
보통 Always를 쓴다

초안은 Generate Cursor Rules, 
이후엔 스스로 개선시킨다.


---


How to write 

1.grasp code structure using Ask mode 
2.Generate Cursor Rules 로 생성 
- write use english 
- prompt engineering 
- include core keyword 

continuous improvement 

1. error explanation instruction
2. prevent recurrence instruction rule write 


![[Pasted image 20250903091451.png]]

