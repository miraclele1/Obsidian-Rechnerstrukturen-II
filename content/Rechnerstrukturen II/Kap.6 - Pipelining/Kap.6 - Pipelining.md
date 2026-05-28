### Stufen (стадии)
IF - Instruction Fetch
- Проц идет в память и забирает команды
ID/OF - Instruction Decode / Operand Fetch
- расшифровка и понимает какие регистры
EX - Execute
- вычислитель (ALU)
MEM - Memory Access
- если нужно прочитать/записать в RAM
WB - Write Back
- запись результата в регистр

### Mehrfachzyklus vs Pipelining
[[Kap.1#Пояснения|CLK]] - Clock - меняется с 0 на 1.

Singe Cycle - всегда одинаковое время такта. Это время выполнения самой длинной [[Kap.6 - Pipelining#Befehlsformat (Типы инструкций)|инструкции]](здесь =5).
Mehrfachzyklyus - 
![[Pasted image 20260426210451.png]]

### Befehlsformat (Типы инструкций)

**R-Type (Register):** ADD, SUB, DIV, MUL R1, R2, R3, ...
- Проходить все кроме MEM (память не нужна) и записывает в регистр(WB)
**LOAD**: данные из RAM в проц
- все 5 стадий, на полную мощность
**STORE:** из проца в RAM
- без WB т.к. в регистры ничего не возвращается
**BRANCH:** «Если А = В, прыгни сюда.»
- без MEM, WB
JUMP:  «Просто иди на строку 999.»
- Самая быстрая. Может завершиться уже на стадии **ID**, как только процессор понял, куда надо прыгнуть.

P.S. - пропуски только в Multi Cycle. Экономит время одной команды.
В конвейере (**Pipelining**) инструкции проходят через все 5 стадий физически, даже если они не выполняют там полезной работы. Пустые операции(NOP), занимает место, чтобы соблюдался ритм. Нужно для поддержания **синхронности** и предотвращения **структурных конфликтов**. Экономит время всего потока.



### 4. Pipelineeffizienz
насколько реально ускоряется процессор при использовании конвейерной обработки по сравнению с идеальным случаем.
#### Идеальный случай
В идеале, если разделить выполнение команды на k этапов (например, 5 этапов в MIPS), то пропускная способность (**Durchsatz**) должна вырасти в k раз. В примере с «бытовой проблемой» (стиркой) это работает идеально только в том случае, если каждый шаг (стирка, сушка, глажка) длится ровно один и тот же отрезок времени (например, 1 час)


Implementiert man eine Pipelinearchitektur für eine **homogene Rechenzeit** pro Arbeitsschrit, lassen sich Speedup und Effizienz wie folgt berechnen:
![[Pasted image 20260504230613.png]]

In der Regel benötigen nicht alle Arbeitsschritte die selbe Zeit. Speicherzugriffe dauern länger als ALU Operationen, die wiederum länger dauern als einfache Registerzugriffe.
In einer Pipeline wird also die Rechenzeit für alle Phasen an die Rechenzeit der längsten Phase angeglichen. Die zusätzlich benötigte Zeit pro Pipelinezyklus nennt man Pipelineverschnitt.

Пример: 

Wir nehmen an, dass sich folgende Verzögerungszeiten im Datenpfad ergeben:

- 100 ps für alle Registerzugriffe
- 200 ps für alle anderen Pipelinestufen


