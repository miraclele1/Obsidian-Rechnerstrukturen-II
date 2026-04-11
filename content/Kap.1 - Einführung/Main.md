**Rechnerstrukturen** (архитектура ЭВМ) — это наука о том, как спроектировать компьютер так, чтобы он эффективно выполнял софт.

#### Mikroarchitektur eines CPU-Kerns

Die **Mikroarchitektur** gliedert sich in drei Teilsysteme:

- **Front-End**: Zuständig für Befehlsholung (Instruction Fetch) und Befehlsdekodierung.
- **Execution Engine**: Der Ort der **Befehlsausführung**.
- **Memory Subsystem**: Verwaltet den Datenfluss zwischen der CPU und dem Speicher
  
  ![[Pasted image 20260409233742.png|213]]

Die **Post-PC-Ära** bezeichnet den <u>Rückgang</u> der Dominanz von Desktop-PCs zugunsten mobiler Geräte wie Smartphones und Tablets. Dieser Wandel hat auch die **Rechnerarchitektur** und den **Energieverbrauch** beeinflusst. Während PCs auf hohe Leistung und dauerhaften Netzbetrieb ausgelegt waren, setzen mobile Geräte auf energieeffiziente Prozessoren und spezialisierte Hardwarebeschleuniger zur Minimierung des Stromverbrauchs.

**Ziel** des **Rechnerarchitekten** ist in einem einyuhaltenden _Kostenrahmen_, ein Maschine möglichst hoher Leistungsfähigkeit zu konstruieren. 

**Befehlssatz** — это просто набор конкретных команд.
**Befehlssatzarchitektur**(ISA) ist wie eine API. Sie definiert welche Maschienenbefehle, Datentype, Speicherorte zu nutzen sind. **Rechnerarchitektur**(Mikroarchitektur) ist die Umsetzung. 
ISA (Instruction Set Architecture) — это архитектура набора команд, определяющая интерфейс между программным обеспечением и аппаратной частью (процессором) которая будет кормить на протяжении генераций. 
Помимо самих команд, она определяет:

- **Maschinenbefehle**
- **Registersatz** (доступные регистры).
- **Datenformate** (типы данных).
- **Adressierungsmodi** (способы обращения к памяти).

![[Pasted image 20260410140755.png|197]]

> [!info]- Нажми, чтобы развернуть
> Die **ISA** bleibt oft über Generationen gleich (z. B. x86 oder RISC-V), damit Software weiterhin läuft. Die **Mikroarchitektur** kann sich massiv verändern (mehr Pipelines oder größere L3-Caches hinzufügen), um die Performanz zu steigern, ohne dass der Programmierer seinen Code ändern muss. Sie bleibt gleich, um **Abwärtskompatibilität** über viele Rechnergenerationen hinweg zu garantieren: Einmal geschriebene Software soll ohne Neukompilierung auf immer leistungsfähigerer Hardware laufen. Während die interne Mikroarchitektur (das „Wie“) ständig optimiert wird, bleibt die ISA (das „Was“) als stabiler Standard bestehen


**RISC** и **CISC** — это две разные философии проектирования этого интерфейса.

|                | RISC                                                        | CISC                                                                                 |
| -------------- | ----------------------------------------------------------- | ------------------------------------------------------------------------------------ |
| Примеры        | ARM, RISC-V                                                 | x86                                                                                  |
| Работа         | фикс. длина команд, <br>предсказуемое время                 | варьируется                                                                          |
| Speichermodell | работа только через<br>регистры Load/Store                  | команды напрямую<br>с процом                                                         |
| Цель           | Минимизировать кол-во тактов<br>Cycles Per Instruction, CPI | Минимизировать кол-во <br>инструкций в программе <br>(**Instruction Count**, **IC**) |
|                |                                                             |                                                                                      |
> [!info]- Нажми, чтобы развернуть
> **Регистр** — это сверхбыстрая  <u>ячейка памяти</u> внутри проца для врем. хранения команд, адресов в текущий момент. Быстрее RAM
> **Taktzyklus** - это единица времени работы проца. За такт выполняется один Maschienenbefehl или этап в Pipeline. Оно не фиксированное - зависит от тактовой частоты GHz. Его длительность - Zyklyszeit.
> **Цикл команды**(Befehlzyklus) - это процесс выполнения одной инструкции, там много стадий.
> **Инструкция** - это команда из набора команд процессора (Befehlssatz), которая приказывает выполнить конкретное действие - напр.  арифметическую операцию (ADD)
> **CPI**(Cycles Per Instuction) - среднее кол-во тактов процессора для одной инструкции. Если стадий  5 -> CPI = 5
> $$T_{CLK} = \frac{1}{f_{CLK}}$$
> $$t_{ex} = IC \cdot CPI \cdot T_{CLK}$$
> T_{ex} - CPU Zeit - чтобы расчитать новое время выполнения после оптимизации(уменьшить IC, снизить CPI )
> T_{CLK} - Zykluszeit
>

Бесконечно увеличивать тактовую частоту (**Taktfrequenz**) невозможно из-за **Power Wall** (энергетический барьер). Больше частоты -> перегрев(power wall) -> предел охлождения -> снижение напряжения -> лимит тока. Именно из-за  него перестали наращивать частоту и перешли к Multicore и параллелизму. 

[[3.3 Anforderungen]]
[[3.5. Steigern der Perfomanz (Power Wall)]]
