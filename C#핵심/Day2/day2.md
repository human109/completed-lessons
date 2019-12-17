# Day2

## Thread Safety

Thread간의 DeadLock 방지

[응용프로그램단]

- Lock
- 인터락

[커널단]

- Mutex - 이름있는 / 이름없는
- 세마포어 : 마지막 남은 자원 먼저 가져가고 나머지는 대기  
- 이벤트 기반 동기화도 있음
    auto : 자동으로 신호보내기
    manual : 수동으로 신호보내기
    countdown(4.0~) : 선착순

메서드(또는 프로세스) 스레드가 동시에 하나의 자원을 사용할 때 발생하는 것은 스레드 동기화 문제
lock / monitor(개체 단위로 하는 동기화)
프로세스 단위 ; Mutex, Semaphore, Event(AutoResetEvent, ManualResetEvent, CoundDownEvent)

## lock 실습

```C#
static object lockobj = new object();
.
.
lock (lockobj)
{
    counter++;

    for (int i = 0; i < counter; i++)
    {
        for (int j = 0; j < counter; j++)
        { }
    }
    Console.WriteLine(counter);
}
```

특정 코드 블럭만 잡는다 : Critical Section
Critical Section은 작은 범위만 잡고 쓰는 것을 원칙으로해서 빠름.
Lock으로 잡는건 개체 범위 이므로 어셈블리 단위는 못잡는다.()

## Monitor 실습

```C#
Monitor.Enter(lockobj);
try
{
    counter++;

    for (int i = 0; i < counter; i++)
    {
        for (int j = 0; j < counter; j++)
        {   }
    }
    Console.WriteLine(counter);
}
finally
{
    Monitor.Exit(lockobj);
}
```

***Lock과 같이 특정코드블록(Critical Section)을 배타적으로 Lock***

## Task

### Task vs Thread

### Task 실습

C# 4.0 이상부터 사용 가능
Task 클래스는 TPL(PPL) 병렬 프로그램 : Task Paralle Library
ThreadPool 사용

```C#
Task.Factory.StartNew(new Action<Object>(Process01), null);
Task.Factory.StartNew(new Action<Object>(Process01), "홍길동");
Task.Factory.StartNew(Process01, 20);
```

매개변수 없는 Task 생성

```C#
Task.Factory.StartNew(new Action(Process02));
```

### 쓰레드 하나씩 생성할땐

```C#
// Thread t1 = new Thread(Process02);
// Task.Factory 사용 시 스레드를 생성하고 동시에 시작하는 방식
// but, 하나씩 개체를 만들어서 사용할 경우는 아래처럼
Task t1 = new Task(new Action(Process02));
t1.Start();
t1.Wait(); // Thread 에서 Join() 메서드와 동일`
```

// Lambda Express

```C#
Task t2 = new Task(() =>
    {
        Process02();
    }
);
t2.Start();
t2.Wait();
```

ThreadPool은 return 타입으로 값을 받기 힘든 단점이 존재

이걸 해결하기 위해 Generic 형식을 사용

```C#
Task<int> t3 = Task.Factory.StartNew<int>(() => Process03("테스트데이터"));
int result = t3.Result;
Console.WriteLine($"현재 입력한 글자 수 : {result}");
```

## 병렬프로그래밍

포트란에선 PPL
C#에선 TPL

```C#
// 병렬 프로그램 반복 만 가능 : for / foreach
// 처리 순서가 중요하면 불가
// CPU와 스레드 번호를 동적으로 생성하고 처리
Parallel.For(0, 1000000, (i) =>
{
    Console.WriteLine($"i 값 : {i} / 스레드 ID 값 {Thread.CurrentThread.ManagedThreadId}");
});
```

**싱글코어일땐 병렬이 안좋다.**
