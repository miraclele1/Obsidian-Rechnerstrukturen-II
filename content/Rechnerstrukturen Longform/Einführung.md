---
title: Kap. 1 - Einführung
draft: false
tags:
  -
---
**Rechnerstrukturen** (архитектура ЭВМ) — это наука о том, как спроектировать компьютер так, чтобы он эффективно выполнял софт.

#### Mikroarchitektur eines CPU-Kerns

Die **Mikroarchitektur** gliedert sich in drei Teilsysteme:

- **Front-End**: Zuständig für Befehlsholung (Instruction Fetch) und Befehlsdekodierung.
- **Execution Engine**: Der Ort der **Befehlsausführung**.
- **Memory Subsystem**: Verwaltet den Datenfluss zwischen der CPU und dem Speicher
  
  ![[Pasted image 20260409233742.png|213]]

Die **Post-PC-Ära** bezeichnet den <u>Rückgang</u> der Dominanz von Desktop-PCs zugunsten mobiler Geräte wie Smartphones und Tablets. Dieser Wandel hat auch die **Rechnerarchitektur** und den **Energieverbrauch** beeinflusst. Während PCs auf hohe Leistung und dauerhaften Netzbetrieb ausgelegt waren, setzen mobile Geräte auf energieeffiziente Prozessoren und spezialisierte Hardwarebeschleuniger zur Minimierung des Stromverbrauchs.

**Ziel** des **Rechnerarchitekten** ist in einem einyuhaltenden _Kostenrahmen_, ein Maschine möglichst hoher Leistungsfähigkeit zu konstruieren. 

**Befehlssatz(-architektur)**(isa) ist wie eine API. Sie definiert welche Maschienenbefehle, Datentype, Speicherorte zu nutzen sind. **Rechnerarchitektur**(Mikroarchitektur) ist die Umsetzung. 
ISA (Instruction Set Architecture) — это архитектура набора команд, определяющая интерфейс между программным обеспечением и аппаратной частью (процессором).

> [!info]- Нажми, чтобы развернуть
> Die **ISA** bleibt oft über Generationen gleich (z. B. x86 oder RISC-V), damit Software weiterhin läuft. Die **Mikroarchitektur** kann sich massiv verändern (mehr Pipelines oder größere L3-Caches hinzufügen), um die Performanz zu steigern, ohne dass der Programmierer seinen Code ändern muss. Sie bleibt gleich, um **Abwärtskompatibilität** über viele Rechnergenerationen hinweg zu garantieren: Einmal geschriebene Software soll ohne Neukompilierung auf immer leistungsfähigerer Hardware laufen. Während die interne **Mikroarchitektur** (das „Wie“) ständig optimiert wird, bleibt die **ISA** (das „Was“) als stabiler Standard bestehen