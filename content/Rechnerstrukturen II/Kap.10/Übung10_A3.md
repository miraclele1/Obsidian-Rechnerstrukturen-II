![[Pasted image 20260604005931.png]]
#### Gegeben:

- Adressierung: byte-adressierbar.
- Wortbreite: 64 Bit = 8 Byte.
- Adresse: 48 Bit.

### Teilaufgabe a)

- **Gegeben: Kapazität** = 32 kiB = 32.768 Byte, **Blockgröße** = 2 Worte = 16 Byte.
- **Anzahl der Cache-Zeilen:** 32.768 / 16 = 2048 Zeilen.
- **Adressaufteilung:**
    - Offset: log_2(16) = 4 Bit.
    - Index: log_2(2048) = 11 Bit.
    - Tag: 48 - 11 - 4 = 33 Bit.
- **Größe einer Cache-Zeile:**
    - **Größe der reinen Daten pro Cache-Zeile:** Block besteht aus 2 Worten, Wort ist 64 Bit(8 Byte).
        - Datenmenge pro Block: 2*8 = 16 Byte
    - Daten: 16 byte * 8 = 128 Bit.
    - Metadaten: 33 Bit (Tag) + 1 Bit (Validität) = 34 Bit.
    - Gesamt pro Zeile: 128 + 34 = 162 Bit.
- **Gesamte SRAM-Größe:** 2048 * 162 = 331.776 Bit.

### Teilaufgabe (b)

- **Gegeben:** Kapazität = 64 kiB = 65.536 Byte, Blockgröße = 16 Worte = 128 Byte.
- **Anzahl der Cache-Zeilen:** 65.536 / 128 = 512 Zeilen.
- **Adressaufteilung:**
    - Offset: log2(128) = 7 Bit.
    - Index: log2(512) = 9 Bit.
    - Tag: 48 - 9 - 7 = 32 Bit.
- **Größe einer Cache-Zeile:**
    - **Größe der reinen Daten pro Cache-Zeile:** Block besteht aus 16 Wort, Wort ist 64 Bit(8 Byte).
        - Datenmenge pro Block: 16*8 = 128 Byte
    - Daten: 128 Byte * 8 = 1024 Bit.
    - Metadaten: 32 Bit (Tag) + 1 Bit (Validität) = 33 Bit.
    - Gesamt pro Zeile: 1024 + 33 = 1057 Bit.
- **Gesamte SRAM-Größe:** 512 Zeilen * 1057 Bit = 541.184 Bit.
- **Größenunterschied:** 541.184 Bit - 331.776 Bit = 209.408 Bit.

### c) weniger indexes → höhere Wahrscheinlichkeit für probleme, höhere Misspenalty