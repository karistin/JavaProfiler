
# **Java Profiler**


[Notion](https://living-light-8ce.notion.site/JVM-Profiler-ffda565bf8344bc8ac23c70a37dc6bb7)

>서버가 실행시 또는 실행 중인 서버에 부착하여 기능을 테스트 하고 부하를 찾을 수 있다.   
- 서버가 실행시 로딩되는 class 목록    
- 서버에 있는 클래스의 메소드 관계  
- 현제 서버 내 에서 실행 중인 메소드들의 실시간 상태 
- 서버의 현제 상태(gc, thread, version, ..)


## 구성 환경 


### 파일 구조

```linux 
├── CodeSample  # Testing code 작성용
├── README.md  
└── agent-slave  # Java profiler
```

### 실행환경 

- Ubuntu-18.04 , window 11
- java version > 11 
- gradle 


## 실행 방법 
테스트 서버와 같이 실행하는 방법


### window powerShell or linux bash
```linux
  cd agent-slave 
  java -javaagent:app/build/libs/app.jar -Dspring.main.banner-mode=off -Dlogging.pattern.console= -jar TestCase.jar
```

### linux zsh
```linux
  cd agent-slave 
  ./sprintAgent
```


## Usage 
> Menu 

<image src="./image/img.png"
height=100
width=200>


### Method Profiling 

<image src="./image/profile.png"
height=300
width=1000>

- 실시간 메소드 추적 
- 값을 설정하여 **추적할 메소드 갯수 와 정렬 순서를** 정할 수 있다. 
- 1초 마다 갱신 
- lambda의 경우 따로 추적하지 않는다. 


### classInfo 

<image src="./image/classInfo.png"
height=300
width=400>

- JVM에서 클래스 로딩시 저장 
- 클래스내의 모든 정보를 가져온다. (어노테이션 제외) 
 

### classInfo 

<image src="./image/classList.png"
height=300
width=600>

- Class로딩 시간 순서대로 저장  
- grep 명령어로 특정 네이밍만을 찾을 수 있다. 
- 리눅스 환경에서만 필터링시 글자 색 변경 

```linux
grep {ClassName}
# grep jennifer
```


### searching  

> normal searching  
<image src="https://github.com/karistin/JavaProfiler/blob/develop/image/normal.png"
height=300
width=800>

> tree searching  
<image src="https://github.com/karistin/JavaProfiler/blob/develop/image/searching.png"
height=300
width=600>

- method searching 기능  
- grep 명령어로 특정 네이밍만을 찾을 수 있다. 
- 특정 메소드에 stack과 함수 호출 관계 호출 네이밍등을 알 수 있다. 
- tree 명령어시 메소드의 세부 호출 관계까지 정의해서 보여준다. 


## 사용된 라이브러리

[ASM](https://asm.ow2.io/)

[Java Instrumentation](https://docs.oracle.com/en/java/javase/11/docs/api/java.instrument/java/lang/instrument/Instrumentation.html)
