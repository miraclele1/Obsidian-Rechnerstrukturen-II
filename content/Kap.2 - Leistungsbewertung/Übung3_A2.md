![[Pasted image 20260414225705.png]]

Gegeben:
 - Opcode: 1 Byte 
 -  Speicheradressen: 2 Byte 
 -  Datentypen: 4 Byte 
 -  Registerspezifikation: 4 Bit 
 - Variablen: A, B, C, D

> [!info]- Ответ a)
> ![[Pasted image 20260414231656.png]]
> Stack: принцип LIFO. Чтобы сложить 2 числа нужно пушнуть их сначала в стек. **ADD/SUB** забирает два верхних элемента и кладет результат обратно. **POP** записывает результат в память.
> Accumulator: Сначала загружаем превое число в аккумулятор, затем прибавляем второе. 
> Register-Register: Самая гибкая. Сначала копируем переменные из памяти в быстрые регистры(**LOAD**), проводим там все вычисления, в конце записываем результат в память(**STORE**)
> 

**POP** - извлекает с вершины стека. Значение уходит из стека. Меняется Stack Pointer. Стек нужно освобождать поэтому POP а не STORE.
**STORE** - копирует значение из регистра в память. Значение остается в регистре, никакие указатели не меняются.

>[!info]- Ответ b)
>
| Architektur | **Seq 1: Instr (b)** | **Seq 2: Instr (b)** |     |
| ----------- | -------------------- | -------------------- | --- |
| **Stack**   | 3+3+1+3 = **10 B**   | 10 * 3 = **30 B**    |     |
| **Accu**    | 3+3+3 = **9 B**      | 9 * 3 = **27 B**     |     |
| **Reg-Reg** | 4+4+3+4 = **15 B**   | 15+7+7 = **29 B**    |     |
| **Mem-Mem** | 1+2+2+2 =**7 B**     | 7 * 3 = **21 B**     |     |
> PUSH, LOAD, ADD, SUB, MUL, ... - это всё OPCODE = 1 Byte + добавляем Speicheradressen = 2 Byte итого 3 Byte
но в Stack где ADD это чисто Rechenwerk в ALU(Ariphmetic-Logic-Unit) поэтому там адрес не используется
в Seq. 2 просто то же самое 3 раза потому что вычисления такого же порядка, это наблюдается везде кроме Reg-Reg
>в Akku есть адрес поэтому везде по 3 Byte
>###### Register-Register
Только у **Reg-Reg** есть Register, который требует **RS**(Register Spezifikation) и просто каждый R весит 0.5 Byte
*LOAD(1) + Address B(2) + RS (4 **Bit** = 0,5 Byte) = 3.5*, но в задаче говорится можно округлить -> 4 Byte
*ADD(1) R3(0.5) R1(0.5) R2(0.5)  = 2.5  -> округляем 3 Byte*
Также у Reg-Reg есть Register Reuse, поэтому он лучше в лонгране т.к. экономит ресурсы - каждый LOAD не тратит байты.


>[!info]- Ответ  c)
>
|Architektur|**Seq 1: Data (c)**|**Seq 2: Data (c)**|
|---|---|---|
|**Stack**|4+4+4 = **12 B**|12 * 3 = **36 B**|
|**Accu**|4+4+4 = **12 B**|12 * 3 = **36 B**|
|**Reg-Reg**|4+4+4 = **12 B**|4+4+4+4+4 = **20 B***|
|**Mem-Mem**|4+4+4 = **12 B**|12 * 3 = **36 B**|
для Reg Reg: 1. Читаем `B`, читаем `C` (8 B). 2. Пишем `A` (4 B). 3. Для `B = A + C` и `D = A - B` данные уже в регистрах. Пишем только результаты `B` (4 B) и `D` (4 B). 4. Итого: $8 + 4 + 4 + 4 = 20 \text{ B}$.


>[!info]- Ответ  d)
>**Beste in Codelänge**: Speicher Speicher ist am effektivsten weil 7 Byte in Seq. 1 und 21 Byte in Seq. 2
>**Beste in Code _und_ Daten:** Speicher-Speicher für Seq. 1, Register-Register für Sequenz 2 
>Seq. 1:
>- 7 + 12 = 19 Byte
>- Seq. 2:
>  - 29 + 20 = 49 Byte




