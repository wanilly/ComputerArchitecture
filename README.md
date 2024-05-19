
# **ComputerArchitecture**

### 목차

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1a4d405c-7b4b-480f-ba1a-b4a267c00168/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/10f1eb15-fe1b-45fb-aae7-fb1cb90f7e62/Untitled.png)

## Instruction Set Architecture(ISA)

Instruction  set(명령어 집합은 자연어에서 어휘에 해당하는 영역을 말한다.

- 마이크로프로세서가 인식해서 기능을 이해하고 실행할 수 있는 기계어로 된 명령어 구조를 의미
- 최하위 레벨의 프로그래밍 인터페이스, 프로세서가 실행할 수 있는 모든 명령어를 포함
- ISA는 Computer Architecture*의 구성요소 중 하나
- 마이크로프로세서의 종류에 따라 기계어 코드의 길이와 숫자 코드가 다름.
    
    (ISA는 제조사마다 차이가 있지만 기본적인 구조 측면에서는 공통점이 많다.)
    
- 기계어 명령어의 각 비트는 기능적으로 분할되어 의미가 부여되고 이진 숫자화
- 프로그래머가 숫자로 프로그래밍하기란 사실상 불가능에 가까워, 기계어와 일대일로 문자화한 것이 Assembly Language
- ISA를 물리적으로 구현하는 방법을 Microarchitecture (Computer Organization) 라 하며, 같은 ISA를 서로 다른 Microarchitecture로 구현

### ISA type🍅

1. **CISC (Complex Instruction Set Computer)**
- 복잡한 명령어 집합을 갖는 CPU Architecture이다.
- 하나의 Instruction이 여러 Job을 처리할 수 있다.
- 명령어의 길이가 가변적이다.
- 다양한 종류의 명령어가 존재 / 많은 주소 지정 모드 사용
- Operand 주소 표시법의 복잡하다.
- Load/Store 구조가 아니기 때문에, Load/Store 구조가 갖는 제약이 없다.
- 대량의 data를 처리하기에 적합하다.
- 명령어 SW적 호환성이 좋다. 명령어 해석한 후 명령어 실행
- 컴파일 과정이 쉽고 호환성이 좋지만, 속도가 느림
- 마이크로 프로그래밍 제어방식

ex) Intel x86

1. **RISC (Reduced Instruction Set Computer)**
- 비교적 단순한 명령어 집합을 갖는 CPU Architecture이다.
- 하나의 Instruction이 되도록 하나의 Job만을 처리하게 설계되었다.
- 명령어의 길이가 고정되어 있다, 해석 속도가 빠르다.
- 명령어의 종류가 비교적 많지 않다. (CISC에 비해 명령어 수가 적음)
- Operand 주소 표시법이 단순하다
- 대부분의 RISC는 Load/Store Architecture*를 채택한다.
- 하드 와이어드 (논리회로 하드웨어)적 제어 방식
- 효율적인 파이프라이닝 구조
- 명령어가 하드웨어적이므로 호환성이 낮다.
- 효율성이 떨어지고, 전력소모가 적으며, 처리 비트 단위가 변하거나 프로세서 구조가 바뀌어도 하위 프로세서와 호환성이 떨어짐.
- 많은 수 범용레지스터가 사용되며, 처리 속도가 빠르고 하드웨어구조가 간단함.

ex) ARM, MIPS, SPARC 등

## MIPS Instruction 종류

1. ALU : R-format, I-format, Immediate addressing mode
2. Data Transfer : I-format, Base addressing
3. Branch : R-format, I-format, J-format, PC-relative addressing, Pseudo direct addressing

![image](https://github.com/wanilly/ComputerArchitecture/assets/49769190/99fa1527-a071-4ef5-b10b-74540bfb43b7)

### Immediate addressing mode

Constant에 대해 sign extension / unsigned extension

> Sign extension
> 

### Register Operand

- MIPS는 32개 레지스터를 가지고, 각 레지스터는 32비트
- 프로그램 실행을 위한 데이터나 실행 도중 발생하는 데이터를 저장
- 컴파일러나 어셈블리 프로그래밍에서는 어셈블러가 결정
- 레지스터 32개이므로 구분하기 위해서 5개의 비트만 필요
- 레지스터 32개가 적당 / 개수는 operand 길이를 결정 / 많은 레지터는 instruction에서 다른 부분을 위해 사용한 비트의 수가 줄어듬

### Memory Organization

- 메모리 구조에는 Byte addressing을 사용 / 주소 1개당 1byte의 데이터를 저장한다.
- 데이터는 주로 word로 이루어지므로, 32bit의 구조를 맞추기 위해 4개를 묶어서 배열
- word는 aligned되어 있어서 word들은 4의 배수를 시작 주소로 가지며 시작 주소의 끝 2bit는 항상 00
    
    ***word = 4byte(32bit)***
    

### Base addressing mode

offset addressing mode : 기준 레지스터(base) + offset 

direct mode? → base 레지스터와 offset 같이 제공 

- 절대적주소를 사용한 경우, instruction 길이가 32비트를 넘는다.
- 32비트 길이 맞춰줄 경우, 2개 word에 저장 → fetch 2번 수행하여 성능이 저하됨.

### Register addressing mode

operand는 register만 가능함.

### PC relative addressing mode

PC기준 상대적인 위치 사용함. beq, bne conditional jump instruction이 PC relative addressing mode 사용함.

### Pseudo- direct addressing mode

j(unconditional jump instruction) jump word 단위 - 하위 2비트를 생략하여 표현함.


![image](https://github.com/wanilly/ComputerArchitecture/assets/49769190/75447865-224a-42ee-a037-7ec328b6dc59)

1. R-type : Register ALU instruction, jr( unconditional jump register ), register addressing mode

![image](https://github.com/wanilly/ComputerArchitecture/assets/49769190/51fa5c54-68c0-489d-aa53-fbd85b3dd6bb)

> add $t0, $s1, $s2 → rd: $t0, rs: $s1, rt: $s2
> 

opcode | RS | RT | RD | shamt | funct  ⇒ 0 | 17($s1) | 18($s2) | 8($t0) | 0 | 32 

funct 사용하는 이유?? → operation은 2^6 = 64 보다 휠씬 많음 

→ ALU instruction은 opcode 0임

1. 🕐I-type → opcode | RS | RT | imm(constant)→16bits


![image](https://github.com/wanilly/ComputerArchitecture/assets/49769190/6edddc14-9b98-4211-bd94-2723699fa738)

- Data transfer instruction
    - base addressing mode → lw(load), sw(store)
- ALU
    - immediate addressing mode → addi
    - branch → bne, beq

> lw $t0, 32($s2)  → rs : $s2, rt: $t0
> 

Offset 32 ⇒ 8*4 byte 

Opcode | RS | RT | Imm(constant), offset ⇒ 35 | rs | rt | 32 

- immediate - 레지스터는 들어있는 값을 가져와야 함, 메모리에 한번 갔다와야 함, 상수는 그 자체의 값
- Sign Extension : 값을 그대로 유지하면서 bit 늘림
    - 레지스터 offset 차이는 ALU 이루어짐, ALU은 32bit, 32bit끼리 연산가능
    - offset: imm 부분에 저장(16bit) ⇒ 연산을 위해 16비트 → 32비트
- Unsigned : 상위를 0으로 채움

1. J-type 

![image](https://github.com/wanilly/ComputerArchitecture/assets/49769190/aea3a147-da19-40e9-94db-d1949cf095e8)

- j, jal (unconditional jump instruction)
- jump - 맨 하위 2비트 ⇒ 00
- 28비트 표현범위 가정 - 하위 2비트 생략!
- address 32비트 - 상위 4개 비트는 현재 PC값 상위 4비트 그대로 사용

> 
> 

### ALU instruction  산술, 논리연산

1. Register Arithmetic 
    
    R-format , Register addressing 데이터, 변수 → 레지스터에 저장
    
    3개 operand 가짐  ⇒ 2 source, 1 destination
    
2. Immediate Arithmetic
    
    immediate address, I-format 사용
    
    subi → 존재 하지 않음 ⇒ addi $s2, $s1, -1
    
   ![image](https://github.com/wanilly/ComputerArchitecture/assets/49769190/6d7d1d89-f2a4-47fd-a3e2-0d54b45e8170)

    
3. Logical

| $v0 ~ $v1 | 레지스터 2, 3번 | 2개인 이유 → 64비트 사이즈를 처리하기 위해서 |
| --- | --- | --- |
| $a0 ~ $a3 | 레지스터 4~7번 | 매개변수  |
| $t0 ~ $t9 | 임시값 | callee 보존되지 않는다 / caller에서 사용된 값이 덮어 쓰여질 수 있음 |
| $s0 ~ $s7 | 저장된 값  | Callee(피호출자)에 의해 저장, 다시 복원 / 사용하던 값을 다시 복원하여야 함. |

### 디자인 설계 원리

1. 규칙적인 것이 간단성을 위해 좋음 → 3개 피연산자 (2 source, 1 destination)
2. 자주 발생하는 사항을 빨리 처리 → 
3. 적을수록 빠름 → MIPS는 적은 수의 레지스터를 포함 (32개)
    
    레지스터의 수가 적으면 데이터를 획득하는 속도가 빠름
    

**01.01_load 명령어 (lw)**

*lw (destination) (source)*

**lw $s3, 1($0)**       # word1번지(1+0=1)에서 데이터를 가져와 $3레지스터에 저장해라.

F2F2AC07값이 $3에 저장됨

word1번지 : 0000 0001

**01.02_store 명령어 (sw)**

*store (source) (destination)*

**sw $t4, 0x3($0)**    # t4레지스터 값을 word3번지((16진수)3+0 )에 저장

word 3번지 는 0000 00003

### **Load/Store Architecture**

오직 Load 명령과 Store 명령으로만 메모리에 액세스할 수 있는 구조이다.

Memory to Memory 연산을 지원하지 않는 구조이다.

ex) 메모리에 있는 값과 레지스터에 있는 값을 곧 바로 더할 수 없고,  load 명령어를 통해 메모리에 있는 값을 레지스터에 옮긴 후 더할 수 있다.

- Memory → Registers, value를 Load
- 연산 수행
- Registers → Memory, result를 Store

### Register

피연산자를 레지스터에서 가져온다. 32개의 32bit 레지스터를 가짐.

![image](https://github.com/wanilly/ComputerArchitecture/assets/49769190/22f183b6-ea64-411e-ac77-2ec900b9c68f)


### Mips Instruction

---

### <Memory Opreations>

## Hazards

Pipeline 방식의 마이크로 아키텍처, 현재 명령어를 처리하면서 다음 명령어에 대한 처리 사이클이 진행되지 못하는 상태임

1. Structure Hazard
    - 내가 사용해야 하는 H/W 자원끼리의 충돌이 발생한 경우
    - 동시에 처리되는 명령어들에서 같은 H/W 자원을 동시에 요구하면 구조 헤저드가 발생
    
2. Data Hazard
    - 순차적으로 수행되는 명령어들 간에, 전후 명령어끼리 의존관계에 있는 경우
    - 파이프라인 기법은 명령어가 완전히 수행되기 이전에 다음 명령어가 실행되는 것이기 떄문에, 전후 명령어가 의존관계에 있으면 파이프이닝이 정상적으로 진행되기 어려움
    

---

💡Qusetion

- 의문점을 가지는 부분들
    1. RISC vs CISC
    2. 왜 RISC로 발전할 수 있었

🖥 체크해야 할 부분 : RISC vs CISC 차이점 어떻게 발전을 가지고 있고 왜 그런 것인지 명확하게 설명할 수 있어야 함

MIPS 명령어 해석 가능 / 기계어 변환 / 역변환 가능 / 

🍅RISC : 

```
적은 수의 명령어를 수행하도록 설계된 마이크로프로세서이다. 복잡한 명령어를 제거하여 사용빈도가 높은 명령어 위주로 처리속도를 향상한 프로세서이다. 컴퓨터의 실행 속도를 높이기 위해 복잡한 처리는 소프트웨어에게 맡기는 방법을 채택하였다. ARM 계열의 프로세서가 RISC 프로세서
```

- CPU의 명령어를 최소화하여 단순하게 제작된 프로세서
- 효율적이고 특화된 CPU 구조
- 하드웨어가 간단한 대신 소프트웨어가 복잡하고 크기가 커짐(컴파일러의 최적화가 요구됨)
- 하위 호환을 위해 에뮬레이션 방식을 채택, 호환성 부족
- 전력 소모가 적음, 속도가 빠르고 가격이 저렴, 용도에 최적화가 요구되는 환경에 사용
- 명령어의 길이가 같기 때문에 병렬 처리가 용이함

🍎CISC :

```
연산에 처리되는 복잡한 명령어 집합을 수백 개 이상 탑재하고 있는 프로세서이다. 인텔 계열의 모든 프로세서는 CISC 프로세서
```

- 복잡하고 기능이 많은 명령어로 구성된 프로세서
- 복합 명령을 가짐으로써 하위 호환성을 확보
- 트랜지스터 집적에 있어 효율성이 떨어짐
- 전력 소모가 큼, 속도가 느리고 가격이 비쌈, 호환성이 절대적으로 필요한 PC환경
- 명령어 해석에 필요한 회로가 복잡 → 병렬 처리가 쉽지 않음

❤️



![image](https://github.com/wanilly/ComputerArchitecture/assets/49769190/ac075f1b-c13c-476b-9dd7-24dfadfbe207)

![image](https://github.com/wanilly/ComputerArchitecture/assets/49769190/427b00a3-adf7-4a32-a2d7-1a3dc3d482c0)

![image](https://github.com/wanilly/ComputerArchitecture/assets/49769190/fa0c41b8-4861-4549-8b79-0bd49b8d8bd6)



### Performance

### 🖥 참고

- https://dad-rock.tistory.com/56?category=765016
- https://ezeun.tistory.com/135?category=959802
- https://gofo-coding.tistory.com/entry/Good-ISA?category=970815
- http://www.kyobobook.co.kr/product/detailViewEng.laf?mallGb=ENG&ejkGb=ENG&barcode=9780124077263
    - Computer Organization and Design The Hardware/Software Interface 5/E
     | Paperback (교재)
- https://parksb.github.io/article/25.html#computer-abstractions-and-technology
- [https://velog.io/@clover7kso/MIPS의-ALU](https://velog.io/@clover7kso/MIPS%EC%9D%98-ALU)
- [https://0o0deng.tistory.com/entry/컴퓨터구조-CH4-RISC-V-RISC-V-Instruction-2](https://0o0deng.tistory.com/entry/%EC%BB%B4%ED%93%A8%ED%84%B0%EA%B5%AC%EC%A1%B0-CH4-RISC-V-RISC-V-Instruction-2)
- [https://velog.io/@www_castlehi/2.-명령어-컴퓨터-언어](https://velog.io/@www_castlehi/2.-%EB%AA%85%EB%A0%B9%EC%96%B4-%EC%BB%B4%ED%93%A8%ED%84%B0-%EC%96%B8%EC%96%B4)
- https://pururing-log.tistory.com/48
- https://mjso9805.tistory.com/3
- https://covenant.tistory.com/67
- https://code-lab1.tistory.com/174
- https://jeongminhee99.tistory.com/64?category=890683
- https://gofo-coding.tistory.com/entry/2-MIPS-Program-Execution?category=970815
