ALU берет 2 числа и сохраняет результат. 
![[Pasted image 20260520222829.png]]
В **Stack** - Одно число из Top Of the Stack и следущее. 
В **Akku** - одно число из Akku, второе из Speicher 
В **Reg-Speicher** - одно число из Register другой из Speicher. (забей что в регистре берется послдений) x86 архитектура (Intel/AMD) 
В **Reg-Reg** - берется из Reg и сохраняется туда же. RISC архитектура (Apple) Speicher-Speicher - забей никто не использует. 

Данные разного размера(8 бит и 8 байт) должны лежать в разных адресах.

## 3.2 Speicherausrichtung
**Надо учить что сколько байт и битов!!!**

Стандарт для современных систем, так как железо для него проще и быстрее. Mit Speicherausrichtung называется Aligned Access.

все энтити должны цельно лежать, не дробиться.

![[Pasted image 20260520223516.png]]
- **Padding** — это вынужденная жертва памятью ради скорости. Мы тратим лишние байты, чтобы процессору было легче и быстрее читать данные.
- Если в адресе ещё есть место чтобы поместить цельные данные , в этом адресе могут хранится несколько энтити. (char C & short D)
#### Ohne Speicherausrichtung (без выравнивания, Misaliged Access)
Padding нету.
![[Pasted image 20260520223601.png]]


## 3.1 Byte-Reihenfolge (Endianness)
![[Pasted image 20260520223638.png]]
Это правило вступает в силу только для данных, размер которых больше 1 байта. Одиночные символы (**`char`**) всегда выглядят одинаково



-------------------------------------------------------------------
Wegen der Vorteile bei der Übersetzung von Hochsprachen haben sich _Registermaschinen_ allgemein _durchgesetzt_. Man favorisiert dabei Maschinen mit möglichst vielen allgemein nutzbaren Registern (general purpose Register - **GPR**).