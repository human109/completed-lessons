# Day3

## Interface

데이터 교환을 위해서 사용

- 정보은닉
- 캡슐화와는 조금 다름

### Interface Type

인터페이스는 규칙

. 접근 한정자를 사용하지 않음 : 무조건 Public

. 선언만 하고 구현하지 않음

. 인터페이스 이름은 대문자 I로 시작하는 것을 권장
.. (코딩 가이드북을 판매중)

인터페이스는 중매쟁이

. 인스턴스의 대상이되는 클래스에서 구현
. 암시적구현
. 명시적구현
.. 다중상속을 받기위해

### 인터페이스 사용 이유

C# 에서 다중상속을 구현하기 위해

### 추상클래스와 인터페이스

추상클래스를 사용하는 이유는 전통적인 방식을 이용하게 하기 위해

## Delegate

Delegate Chain 을 MS 에서는 Multicast Delegate라고 함.

## 이벤트

1. 델리게이트 선언

2. 어쩌고 저쩌고

Event Driven Programming
WPF
.INotifyPropertyChanged
.

미세한터치는 WPF 기본적으론 안되므로 Event구현을 해야한다.

## Timer

타이머 오차 남.

용도에 맞는 타이머를 사용해야 함.

wpf에서는 Dispacher Timer를 사용

편하게 쓸때 Timers.Timer 사용

.NET 타이머 4개 있음

Winform 3개

Thread 사용해서 처리하는 것: 멀티 / 싱글 스레드로 타이머를 처리

System.Threading.Timer / System.Timers.Timer - Multi Thread

Windows Form Timer(System.Windows.Forms.Timer Class) -Single  Thread

Multi Thread Timer는 특정 간격으로 실행되는 이벤트 핸들러를 스레드 풀에 넣고 할당된 작업스레드(Worker Thread)를 이용해서 실행 WT가 실행될 때 항상 같은 스레드로 실행된다는건 보장하지 않음.

이벤트 핸들러가 다음 Interval 보다 실행시간이 길면 다른 작업 스레드로 핸들러를 실행하기 때문에 "Thread Safe"를 지원한다.

싱글 스레드는?? : Windows Form Timer는 단순/ UI 관련 된 것만 처리 : 짧은 시간에 처리가능한 것만 함: Thread Unsafe
. 동시성 문제때문에 시간 오류

오차가 발생함

## WPF에서의 Timer

WPF의 타이머는 System.Threading.Timer / System.Timer.Timer 가 존재
WPF의 폼 타이머와 같은 것(Single Thread) : System.Windows.Threading.DispatcherTimer

```C#
System.Windows.Threading.DispatcherTimer timer = newSystem.Windows.Threading.DispatcherTimer();

timer.Interval = TimeSpan.FromSeconds(1); // TimeSpan.FromMilliseconds(0.1);
// timer.Tick handler += new EventHandler(); 
timer.Tick += new EventHandler(TickTimerProcess);
// timer.Tick += TickTimerProcess; // C# 4.5 ~
timer.Start();
```

async / await로 대체 가능(Background Worker)

```C#
timer.Tick += TickTimerProcess;
```

Winform의 invokeRequired와 동일한 기능
.숨겨져 있음

```C#
if (textBoxMultiT.Dispatcher.CheckAccess())
{   // UI 스레드 일 경우
    textBoxMultiT.Text = "데이터 넣기";
}else
{
    textBoxMultiT.Dispatcher.BeginInvoke(new Action(
            () => textBoxMultiT.Text = "데이터 넣기 스레드"
        ));
}
```

## SDK

Profile 버전 : 프레임워크를 최소화 시킨거

VS 가 6000개 DLL rjsemfla

SDK를 건드리면 재부팅
VS2008
side-by-side 방식
리부팅 하라고하면 무시
VS2010이 중간버전

DDK
. Device Driver Kit
. 지금은 WDK
. 7 천만 / Year

ADK
. Win 8 이상에서 사용되는 도구

다른 SDK
. VS2010 부터는 VS Marketplace(googling) 에서 설치 가능
. VS2015 부터는 확장 및 업데이트 도구

## 전처리기

디버그 모드와 릴리즈 모드의 차이는  백만번 정도해야 차이남
메모리 구성이 다름

if, else, endif, dfine, undef,
waning / error

## Attribute

Attibute 를 보면 WCF / EF 를 이해하기 쉽다.

### WCF

보내기/ 받기

보내는 사람 - IP

형식 - X WS)

비동기

### EF

예약어

문법

DBA와 DB Delveloper 가 다를 때

O/R 연결(ORM)

[코드분석]

- 보안 규칙
- 관리 규칙

등 있음.

- SDL(Software Development Lifecycle)
- DevOps
- OSA

Practices 등 있음.

### 실습

전처리기를 이용해서 DEBUG / RELEASE 모드 수정
**절대 대문자로**

---

## 공부해야 할 것

- MTAThread
- smartclient 배포
