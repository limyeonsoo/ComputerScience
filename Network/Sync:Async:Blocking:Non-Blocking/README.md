# Sync, Async, Blocking, Non-Blocking

---

# Sync

---

2가지 이상의 대상(function or application)이 시간을 맞춰 동작하는 것.

A, B 작업이 순서대로 수행될 때, B는 A가 끝날 때 까지 기다림.
(A 작업 종료 == B 작업 시작)

Caller는 Callee에게서 결과값을 반환받고 이를 직접 처리.
→ Caller는 Callee의 종료 여부가 중요.

# Async

---

대상들이 서로 시간을 맞추지 않고 동작하는 것.

A, B작업은 서로 관계없이 동작.

Callee에서 Callback을 통해 결과값을 처리.
→ Caller는 Callee의 종료 여부에 관심이 없음.

# Blocking

---

## Block

네트워크 성능은 CPU, Memory, Disk 속도보다도 매우 느린 편.

문제) CPU가 Network가 느려서 기다리게 됨 → 블록되었다.

## Blocking

Blocking은 일반적으로 속도가 느린 I/O(Network, Disk, Console)에서 필연적으로 발생하는 제어권 이탈 상황을 말함.

Caller가 Callee를 호출하는 순간 제어권이 Callee에게 넘어가고, Callee는 종료전까지 제어권을 반환하지 않음.
→ Caller는 제어권이 없어서 작업 수행 불가.

# Non-Blocking

---

Caller가 Callee를 호출할 때 짧은 시간동안 Callee가 제어권을 가진 후, 작업  종료와 관계없이 바로 Caller에게 제어권을 반환.

Caller는 제어권을 반환받았으므로, 다른 작업을 수행할 수 있다.

# Sync+Async vs Blocking+Non-Blocking

---

## Sync/Async ⇒ 결과값 return, 작업 완료를 중점.

## (Non)Blcoking ⇒ 제어권에 중점.

1. Sync + Blocking
    
    반환 값: Callee가 종료될 때
    
    제어권: Callee
    
    ![Untitled](Sync,%20Asyn%20b9b94/Untitled.png)
    
2. Sync + Non-Blocking
    
    반환 값: Callee가 종료될 때
    
    제어권: Caller
    
    **⇒ Caller는 제어권이 있어서 다른 작업을 수행할 수 있으나, Callee의 종료 여부를 계속 체크해야하는 비효율적인 상황.**
    
    ![Untitled](Sync,%20Asyn%20b9b94/Untitled%201.png)
    
3. Async + Blocking
    
    반환 값: 관심 없음
    
    제어권: Callee
    
    **⇒ 반환 값은 관심없지만, Callee에게 제어권이 있으므로, 기다려야하는 비효율적인 상황**.
    
    ![Untitled](Sync,%20Asyn%20b9b94/Untitled%202.png)
    
4. Async + Non-Blocking
    
    반환 값: 관심 없음
    
    제어권: Caller
    
    ![Untitled](Sync,%20Asyn%20b9b94/Untitled%203.png)
    

## Non-Blocking은 항상 옳은가?

I/O 작업에 비해 CPU가 작업하는 양이 많다면 효과가 없을 수 있음.

Block상태는 CPU가 Network를 기다려서 생기는 상황이기 때문.