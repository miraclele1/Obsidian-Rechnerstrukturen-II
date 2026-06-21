## Aufgabe 5
**Цепочка рассуждений (Chain-of-Thought):**

1. **Правила архитектуры:** * **Issue / Commit:** Архитектура 2-скалярная, значит за один такт могут быть выданы (Issue) и зафиксированы (Commit) максимум 2 инструкции (строго по порядку).
    - **Begin EX:** Начинается, когда готовы операнды и свободна нужная FU (Functional Unit), но не раньше следующего такта после Issue.
    - **On CDB:** Результат доступен через `Begin_EX + Latenz`. Латентности: Int/Branch = 1, LSU = 2, FP = 3.
    - **MEM read:** Выполняется на втором такте работы LSU (для загрузок). Store-инструкции (`sw.f`) вычисляют адрес, но ничего не читают из памяти (ставим прочерк).
2. **Анализ 1-й итерации:** * `mul.f` ждет данные от обеих `lw.f` (появятся на CDB в 4-м такте, значит EX начнется в 5-м)
    - `bne` ждет обновления адреса от `addi r1` (на CDB в 5-м такте, EX начнется в 6-м).
3. **Анализ 2-й итерации (Спекулятивной):** * Благодаря идеальному предсказанию, 2-я итерация начинает Issue сразу после `bne` (в 4-м такте).
    - Так как результат `bne` 1-й итерации становится известен только в 7-м такте, **все** инструкции 2-й итерации являются спекулятивными.
    - Инструкции загрузки 2-й итерации зависят от `addi` из 1-й итерации (адреса готовы в 5-м такте, поэтому EX начинается в 6-м).

### (a) Scheduling

|**Iter.**|**Instruction**|**Issue**|**Begin EX**|**MEM read**|**On CDB**|**Commit**|**Spekulativ?**|
|---|---|---|---|---|---|---|---|
|1|`1 lw.f f0, 0(r1)`|1|2|3|4|5|Nein|
|1|`1 lw.f f1, 0(r2)`|1|2|3|4|5|Nein|
|1|`1 mul.f f2, f0, f1`|2|5|-|8|9|Nein|
|1|`1 sw.f f2, 0(r1)`|2|3|-|-|10|Nein|
|1|`1 addi r1, r1, #4`|3|4|-|5|10|Nein|
|1|`1 addi r2, r2, #4`|3|4|-|5|11|Nein|
|1|`1 bne r1, r3, for`|4|6|-|7|11|Nein|
|2|`2 lw.f f0, 0(r1)`|4|6|7|8|12|Ja|
|2|`2 lw.f f1, 0(r2)`|5|6|7|8|12|Ja|
|2|`2 mul.f f2, f0, f1`|5|9|-|12|13|Ja|
|2|`2 sw.f f2, 0(r1)`|6|7|-|-|14|Ja|
|2|`2 addi r1, r1, #4`|6|7|-|8|14|Ja|
|2|`2 addi r2, r2, #4`|7|8|-|9|15|Ja|
|2|`2 bne r1, r3, for`|7|9|-|10|15|Ja|

### (b) Performanz

1. **CPI для первых двух итераций:**
    
    - Всего инструкций: $7 \times 2 = 14$
        
    - Последний Commit завершается на 15-м такте.
        
    - **$CPI_{2 \text{ iter}} = \frac{15}{14} \approx 1,07$**
        
2. **Значение CPI при бесконечном числе итераций ($N \to \infty$):**
    
    - В цикле 7 инструкций. Пропускная способность процессора — выдача (Issue) 2 инструкций в такт.
        
    - Конфликтов по функциональным блокам (FU), которые могли бы затормозить конвейер больше, чем стадия Issue, нет.
        
    - Следовательно, на одну итерацию требуется минимум 3,5 такта.
        
    - **CPI будет стремиться к $3,5 / 7 = 0,5$.**
        
3. **Идеальный ожидаемый CPI:**
    
    - Для 2-скалярной архитектуры (максимум 2 выполняемые инструкции за такт) теоретический максимум IPC = 2.
        
    - **$CPI_{ideal} = \frac{1}{IPC_{max}} = \frac{1}{2} = 0,5$.**

## Aufgabe 6
**Allgemeine Vorüberlegungen (Chain-of-Thought):**
- Es steht eine 64-Bit-Prozessoradresse zur Verfügung, von der jedoch nur 48 Bit für die physikalische Adressierung genutzt werden. Bit 48 bis 63 werden folglich ignoriert.
    
- Alle Caches des Systems sind byteadressierbar.
- ![[Pasted image 20260617123309.png]]
- ![[Pasted image 20260617123012.png]]

### (a) L1D-Cache

- **Gegeben:** Größe = 48 kiB, Assoziativität = 12-fach, Cachezeile = 64 Byte.
- **Offset:** Um jeden Byte innerhalb der 64-Byte-Cachezeile zu adressieren, werden $\log_2(64) = 6$ Bit benötigt.
- **Index:**
    - Gesamte Anzahl an Sets = $\frac{\text{Cache-Größe}}{\text{Cachezeile} \times \text{Assoziativität}}$
    - Sets = $\frac{48 \times 1024}{64 \times 12} = \frac{49152}{768} = 64$ Sets.
    - Zur Adressierung von 64 Sets werden $\log_2(64) = 6$ Bit benötigt.
- **Tag:** Restliche Bits der physikalischen Adresse = $48 - 6 \text{ (Offset)} - 6 \text{ (Index)} = 36$ Bit.
    

### (b) L1I-Cache

- **Gegeben:** Größe = 32 kiB, Assoziativität = 8-fach, Cachezeile = acht 64-bit Wörter.
    
- **Offset:** Ein 64-Bit-Wort entspricht 8 Byte. Acht Wörter sind $8 \times 8 = 64$ Byte pro Cachezeile. Benötigt werden $\log_2(64) = 6$ Bit.
    
- **Index:**
    
    - Sets = $\frac{32 \times 1024}{64 \times 8} = \frac{32768}{512} = 64$ Sets.
        
    - Zur Adressierung von 64 Sets werden $\log_2(64) = 6$ Bit benötigt.
        
- **Tag:** Restliche Bits = $48 - 6 \text{ (Offset)} - 6 \text{ (Index)} = 36$ Bit.
    

### (c) L2-Cache

- **Gegeben:** Größe = 2 MiB, Assoziativität = 32-fach, Cachezeile = 64 Byte.
    
- **Offset:** $\log_2(64) = 6$ Bit.
    
- **Index:**
    
    - Größe in Byte = $2 \times 1024 \times 1024 = 2097152$ Byte.
        
    - Sets = $\frac{2097152}{64 \times 32} = \frac{2097152}{2048} = 1024$ Sets.
        
    - Zur Adressierung von 1024 Sets werden $\log_2(1024) = 10$ Bit benötigt.
        
- **Tag:** Restliche Bits = $48 - 10 \text{ (Index)} - 6 \text{ (Offset)} = 32$ Bit.


### d)
![[Pasted image 20260617121317.png]]

4Ghz => 1/4 => **0,25ns Dauer von 1 Takt**
**Gegebene Werte:**

- Taktfrequenz: 4 GHz $\rightarrow$ 1 Takt = 0,25 ns
    
- **L1-Zugriffszeit** ($T_{L1}$): 3 Takte = 0,75 ns
    
- **L2-Zugriffszeit** ($T_{L2}$): 12 Takte = 3,0 ns
    
- **L3-Zugriffszeit** ($T_{L3}$): 36 Takte = 9,0 ns
    
- **Hauptspeicher** ($T_{Mem}$): 65 ns
    
- **Missrate** ($MR$): 10% -> 0,1
    

**Berechnung der mittleren Speicherzugriffszeit (AMAT):**

$$AMAT = T_{L1} + MR \cdot (T_{L2} + MR \cdot (T_{L3} + MR \cdot T_{Mem}))$$

$$AMAT = 0,75 + 0,1 \cdot (3,0 + 0,1 \cdot (9,0 + 0,1 \cdot 65))$$

$$AMAT = 0,75 + 0,1 \cdot (3,0 + 0,1 \cdot 15,5)$$

$$AMAT = 0,75 + 0,1 \cdot (3,0 + 1,55)$$

$$AMAT = 0,75 + 0,1 \cdot 4,55$$

$$AMAT = 0,75 + 0,455 = 1,205$$

**Ergebnis:** 1,205 ns
