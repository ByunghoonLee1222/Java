# Multi Thread

**Proccess 방식**

* 프로그램 다시 실행하면 메모리에 있는것(Proccess Data Code)을 그대로 복제 => fork
* 메모리 과부하 문제 발생

**자바(쓰레드 방식)**

* **쓰레드란** ? 프로세스를 구성하는 작은 실행 단위

* JVM 안에 프로그램을 동작시키는 쓰레드가 하나 있다
* 다시 실행하면 프로그램(Data,Code)은 그대로 있고 가벼운 쓰레드만 하나 추가 된다

**실행과정**

* Thread 생성시 **Runnable** 에서 쓰레드가 대기한다

* 스케쥴러가 대기하고 있는 Thread를 **Run** 시킨다
* **Blocked**(TimeWait) => I/O 실행 시, suspend(), sleep(ms)
* I/O 끝나면 Blocked 상태에서 다시 Runnable로 돌아가서 대기실에 서 대기
* 다시 스케쥴러에 의해 실행 
* yield() => 쓰레드 실행 중지 => 다시 Runnable로 돌아감
* **Dead** = > run() 종료 or stop()

리눅스 ,UNIX에서는 우선순위가 지켜진다. ( 윈도우에서는 X (round))

1. MAX_PRIORITY(10)
2. NORM_PRIORITY(5)
3. MIN_PRIORITY(1 우선순위 가장 낮음)

* 쓰레드는 Primitive Type을 공유하지 않는다 / Reference Type은 공유
* run중인 동기화된 객체에 lock Flag가 없는 경우 LockPool에 저장
* lock Flag를 획득하면 다시 Runnable로 이동

동기화 안하고 싱글쓰레드 인경우 => resume, suspend

동기화 하고 멀티쓰레드 이상인 경우 => notify, wait

wait pool / lock pool 존재

wait() 실행 시 wait pool에서 대기하며 lock pool에 lock flag 반납 

다음 객체가 lockflag를 받아 처리하면 notify()를 실행시켜 wait pool에서 꺼낸다