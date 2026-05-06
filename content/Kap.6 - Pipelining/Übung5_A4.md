![[Pasted image 20260501000249.png]]


```
import numpy as np
import matplotlib.pyplot as plt

T = 5.5  # ns
C = 1.0  # ns
k = 1
b = 0.016

S_values = np.arange(1, 36)
G_values = 1 / ((T / S_values + C) * (1 + b * k * S_values))

S_opt_continuous = np.sqrt(T / (C * b * k))
print(f"Continuous S_opt: {S_opt_continuous}")

S_opt_int = S_values[np.argmax(G_values)]
print(f"Integer S_opt: {S_opt_int}")

plt.figure(figsize=(10, 6))
plt.plot(S_values, G_values * 1000, marker='o', linestyle='-', color='b') # G in MIPS/GIPS? 1/ns = 10^9/s = 1 GIPS. Let's just plot 1/ns.
plt.title("Pipeline-Durchsatz nach Flynn")
plt.xlabel("Stufenzahl $S$")
plt.ylabel("Durchsatz $G$ (1/ns)")
plt.grid(True)
plt.axvline(x=S_opt_int, color='r', linestyle='--', label=f'Optimales $S = {S_opt_int}$')
plt.legend()
plt.savefig("throughput_plot.png")
plt.close()

```

Результат выполнения кода

```
Continuous S_opt: 18.540496217739157
Integer S_opt: 19

```

(a) Расчет оптимального количества стадий ($S_{opt}$)**

Согласно аналитической модели пропускной способности конвейера Флинна, оптимальное количество стадий рассчитывается по формуле:

$$S_{opt} = \sqrt{\frac{T}{C \cdot b \cdot k}}$$

Подставляем заданные параметры:

$$S_{opt} = \sqrt{\frac{5.5}{1.0 \cdot 0.016 \cdot 1}} = \sqrt{343.75} \approx 18.54$$

Так как количество стадий должно быть целым числом, проверяем соседние значения (18 и 19). Максимальная пропускная способность достигается при **$S = 19$**.

**(b) График пропускной способности в зависимости от количества стадий $S$**

График построен на основе формулы пропускной способности:

$$G(S) = \frac{1}{\left(\frac{T}{S} + C\right) \cdot (1 + b \cdot k \cdot S)}$$

для $S \in \{1, \dots, 35\}$.