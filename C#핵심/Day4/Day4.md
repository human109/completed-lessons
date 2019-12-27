# Day4

## VS Debugging

* VS2010 권장 *

SVR Programming 에서는 싱글스레드

join 하고 abort하는게 좋다.

## 포인터

C언어와 C++에서 가져온 dll을 사용할때

H/W Dependancy 한 것을 사용할땐 C언어 
그걸 Wrapping할 때 C#

VMware는 바로 접근
Win Hypervisor 는 한번 완충 작용 & 가상메모리도 사용
그러므로 느리다.

## Assembly

CLR 안에 JIT 컴파일러를 어쩌고해서 MSIL

ASSEMBLY ->  기계어로 : JIT 컴파일러

C:\windows\Assembly

System.task.Thr

닷넷프레임워크 위치 알아두기

manifest

5개의 클래스정도로 제한 (권장 : 유지보수를 쉽게 하기 위해)

### 위성 어셈블리(Satellite Assembly)

.C++에서는 리소스
..다국어 만들때 사용

.기본언어(영어)위에
..al utility를 이용해서

Wrapping해서 가져오는 것을 - 상호운용성이라 함.

interop -> 상호운용성으로 만들어진.

virtual -> override 가능

기본출력 -> 공용/전역 어셈블리

## 프로젝트

### 문제해결능력

Science vs Engineering

최적의 방법을 찾는 과정이 필요. (실무)

설계와 요구사항에 맞게.

프로젝트가 성공하기위해선 사람을 안바꿔야한다.

## 디버깅

진단도구 2015

### 중단점

조사식과 적중횟수

#### IntelliTrace

VS2010 ~

Ultimate / Enterprise 기능에 포함

디버깅하는 것 녹화.(오류재현)

이전 행동으로 복귀

.NET 환경에서만 제공

### Remote Debugging

원격디버깅도구는 ms홈페이지에서 다운받을 수 있음.
상위버전은 하위버전을 호환

## Process Dump

BlueScreen 분석

Windbg -

### Dump 분석

mps 리포트
. PC 상태정보와 덤프 정보를 툴에 돌림(case open)

### 예외처리

method를 끝내고 싶을 때는 return.

#### try ~ catch와 finally

connection state를 확인해서 finally에서 dispose 또는 close()

## dump분석

전체 메모리 덤프나 활성 메모리 덤프를 떠야 확인 할수 있다.

windbg로 symbol 연결 , 코드연결

