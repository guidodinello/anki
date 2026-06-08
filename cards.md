# MMC — Anki Cards

Tarjetas de repaso organizadas por sesión. Formato: pregunta → respuesta.

---

## Sesión 4 — Error y tamaño de muestra

**Card 1** `E2-4.1`
¿De qué teorema o resultado se deriva cada fórmula de peor caso para n, y qué supuesto exige cada uno?

> $n_C$: desigualdad de Chebyshev — vale para cualquier v.a. con varianza finita, sin asumir forma de la distribución.
> $n_H$: teorema de Hoeffding — exige que las v.a. estén acotadas en $[0,1]$; es exacto (no asintótico).
> $n_N$: Teorema Central del Límite — asintótico en $n$ y en $\varepsilon$; no garantiza cobertura para $n$ finito.

---

**Card 2** `E2-4.1`
¿Cómo dependen $n_C$, $n_N$, $n_H$ de ε?

> Los tres escalan como 1/ε². Reducir ε a la mitad cuadruplica n en los tres casos.

---

**Card 3** `E2-4.1`
¿Cómo dependen de δ?

> $n_C$ escala como 1/δ — muy sensible. $n_H$ escala como ln(1/δ) — poco sensible. $n_N$ escala como (Φ⁻¹)² — intermedio.

---

**Card 4** `E2-4.1`
¿Cuál garantiza cobertura y cuál no?

> $n_C$ y $n_H$ garantizan cobertura siempre. $n_N$ no garantiza — es asintótico en n y en ε, puede ser optimista especialmente cuando λ está cerca de 0 o 1.

---

**Card 5** `E2-4.1`
¿Qué es el nivel de cobertura empírico y cuándo se puede calcular?

> Es la proporción de experimentos en que el IC contuvo al valor exacto λ. Solo calculable cuando λ es conocido.

---

**Card 6** `E2-4.1`
¿Cuál es el paso clave en la derivación de Chebyshev para obtener la cota sobre n?

> Elegir β = ε/σ para convertir |Z|/σ < β en |λ̄ − λ| < ε, luego comparar 1 − σ²/ε² ≥ 1 − δ para despejar n.

---

**Card 6b** `E2-3.1`
¿Qué significa que $\bar{\lambda}(R)$ es un estimador fuertemente consistente de $\lambda(R)$?

> Que $\bar{\lambda}(R) \to \lambda(R)$ con probabilidad 1 cuando $n \to \infty$ (también escrito c.p.1, c.s., o "casi seguramente"). Es la forma más fuerte de convergencia probabilística. Sin embargo, no da información sobre el error para $n$ finito — que es el problema de mayor interés práctico.

---

**Card 6c** `E2-3.1`
¿Qué mide el error estándar $\sqrt{V[\bar{\lambda}(R)]}$ y por qué es solo un indicador grosero?

> Mide la desviación estándar estimada del estimador — tiene las mismas unidades que $\bar{\lambda}(R)$ y es directamente comparable con él. Es grosero porque $\bar{\lambda}(R)$ y $V[\bar{\lambda}(R)]$ están fuertemente correlacionados: si $\lambda < 1/2$, una subestimación de $\lambda$ tiende a venir acompañada de una subestimación de la varianza, con lo que el error real queda oculto. Este fenómeno no se atenúa sino que se agudiza con $n \to \infty$.

---

**Card 6d** `E2-3.1`
¿Cuál es la relación cualitativa entre $\bar{\lambda}(R)$ y $V[\bar{\lambda}(R)]$ cuando $\lambda \neq 1/2$?

> Están fuertemente correlacionados. Cuando $\lambda < 1/2$, una subestimación del estimador puntual tiende a venir acompañada de una subestimación de la varianza — el error real queda oculto. Cuando $\lambda > 1/2$, ocurre lo opuesto. Esta correlación no desaparece con $n \to \infty$, lo que hace que el error estándar sea un indicador grosero y justifica usar un IC formal en lugar de solo reportar el error estándar.

---

**Card 6e** `E2-4.1`
¿Por qué la fórmula $n_N$ de peor caso tiene $2\varepsilon$ en el denominador pero la fórmula con varianza estimada no?

> Son dos contextos distintos. **Peor caso** (Sesión 4): $n_N = \lceil (\Phi^{-1}(1-\delta/2) / 2\varepsilon)^2 \rceil$ — el $2$ viene de sustituir $\sigma^2 \leq 1/4$ (peor caso Bernoulli), entonces $\sigma \leq 1/2$. **Con varianza estimada** (Sesión 6): $\dot{n}_N = \lceil [\Phi^{-1}(1-\delta/2)]^2\, \hat\sigma^2_{n'} / \varepsilon^2 \rceil$ — acá $\hat\sigma^2_{n'}$ ya es la varianza medida, no el peor caso, así que no hay el factor $1/4$. La fórmula general es siempre $(\Phi^{-1})^2 \cdot \sigma^2 / \varepsilon^2$; la diferencia es qué valor de $\sigma^2$ se usa.

---

**Card 6f** `E2-4.1`
¿Cuándo usar $n_C$, $n_H$, $n_N$ de peor caso, y cuándo el algoritmo de dos etapas con $\hat\sigma^2$?

> Depende de si φ es indicatriz o no. **φ indicatriz (Bernoulli):** $\sigma^2 \leq 1/4$ está acotada, entonces podés usar peor caso — $n_C$ o $n_H$ con garantía exacta, $n_N$ sin garantía (asintótico). **φ general (integración):** $\sigma^2$ no está acotada, no hay peor caso disponible — obligatorio usar el algoritmo de dos etapas: corrida preliminar → $\hat\sigma^2_{n'}$ → $\dot{n}_N$.

---

## Sesión 5 — Intervalos de confianza

**Card 6g** `E2-4.1`
¿Cuál es la definición formal de intervalo de confianza y cuál es la trampa conceptual más común?

> $[I_1, I_2]$ es un IC de nivel $(1-\delta)$ para $\lambda$ si y solo si $I_1$ e $I_2$ son variables aleatorias tales que $\text{Prob}(I_1 \leq \lambda \leq I_2) \geq 1-\delta$. La trampa: $\lambda$ es un valor fijo desconocido — son $I_1$ e $I_2$ los que son aleatorios (dependen de la muestra). Decir "hay 95% de probabilidad de que $\lambda$ esté en el intervalo" es impreciso; lo correcto es "si repitiéramos el experimento muchas veces, al menos el 95% de los intervalos obtenidos contendría a $\lambda$".

---

**Card 6h** `E2-4.1`
¿Qué es el nivel de cobertura de un IC y en qué se diferencia del nivel de cobertura empírico?

> **Nivel de cobertura** (teórico): la probabilidad $\text{Prob}(I_1 \leq \lambda \leq I_2)$ — una propiedad del método, no de una corrida particular. Un IC de nivel $(1-\delta)$ garantiza que esta probabilidad sea $\geq 1-\delta$. **Nivel de cobertura empírico**: si se repite el experimento $K$ veces, es la proporción de intervalos que efectivamente contuvieron a $\lambda$. Solo calculable cuando $\lambda$ es conocido (por eso se usa para validar métodos en simulación). Si el IC está bien construido, el empírico debe aproximarse al teórico cuando $K$ es grande.

---

**Card 7** `E2-4.1`
¿Qué es δ y qué es (1−δ) en el contexto de un IC?

> (1−δ) es el nivel de confianza — la probabilidad de que el IC contenga al valor exacto. δ es la probabilidad de que el IC falle, es decir que el valor exacto quede fuera del intervalo.

---

**Card 8** `E2-3.1`
¿Por qué el IC exacto (binomial) garantiza cobertura ≥ 1−δ y no exactamente 1−δ?

> Porque la Binomial es discreta y no siempre es posible dar exactamente el nivel pedido. El IC es conservador por construcción.

---

**Card 9** `E2-3.1`
¿Cuáles son los supuestos para que S ~ Binomial(n, λ)?

> 1. φ es indicatriz (valores 0 o 1). 2. X^(j) uniforme en J^m (garantiza P(X^(j) ∈ R) = λ). 3. Las muestras son independientes. Con estos tres, cada φ(X^(j)) ~ Bernoulli(λ) iid, y la suma es Binomial por definición.

---

**Card 10** `E2-3.1`
¿En qué se basa el IC de Wald y qué limitación tiene?

> Se basa en la aproximación normal (TLC): el estimador $\bar\lambda$ estandarizado converge a $N(0,1)$ cuando $n \to \infty$. La limitación es que es asintótico — para $n$ finito no garantiza cobertura, especialmente cuando $\lambda$ está cerca de 0 o 1 donde la Binomial es muy asimétrica.

---

**Card 11** `E2-3.1`
¿Cuándo falla el IC de Wald y por qué?

> Cuando λ está cerca de 0 o 1. La Binomial es muy asimétrica en esos casos y la aproximación normal es mala. Puede dar extremos fuera de [0,1] y cobertura real menor a 1−δ.

---

**Card 12** `E2-3.1`
¿En qué se basa el IC de Chebyshev y qué lo diferencia del de Wald?

> Se basa directamente en la desigualdad de Chebyshev, sin aproximación normal. Garantiza cobertura $\geq 1-\delta$ para cualquier $n$ y cualquier $\lambda$ — no es asintótico. El costo es que tiende a ser más ancho (más conservador) que Wald o Agresti-Coull.

---

**Card 13** `E4`
¿Cuál es la idea del IC de Agresti-Coull y por qué mejora a Wald?

> Aplica Wald pero sobre cantidades ajustadas: agrega artificialmente algunos "éxitos" y "fracasos" extra antes de calcular. Esto empuja la estimación hacia $1/2$, mejorando la cobertura cuando $\lambda$ es cercano a 0 o 1 — exactamente donde Wald falla más. Sigue siendo aproximado (no garantiza cobertura exacta), pero es mejor en la práctica que Wald.

---

**Card 14** `E2-3.1`
¿Qué IC usarías si λ es muy chico y necesitás garantía exacta?

> Chebyshev (con β = δ^{−1/2}). Es el único que garantiza cobertura ≥ 1−δ para cualquier n y cualquier λ, sin asumir nada sobre la distribución más allá de varianza finita.

---

**Card 15** `E2-3.1`
¿Cuál IC es más ancho en general: Chebyshev o Agresti-Coull?

> Chebyshev, porque es más conservador. El cociente asintótico de anchos es δ^{−1/2} · Φ^{−1}(1−δ/2), que es siempre mayor a 1. Agresti-Coull es más ajustado pero sin garantía exacta.

---

**Card 16** `E1`
¿Por qué la linealidad de la esperanza es suficiente para mostrar que S/n es insesgado, sin necesitar independencia?

> Porque E[S/n] = (1/n)·Σ E[φ(X^(j))] = (1/n)·n·λ = λ, usando solo que cada E[φ(X^(j))] = λ (iid). La independencia no es necesaria para la esperanza — sí lo es para la varianza.

---

## Sesión 6 — Integración por Monte Carlo

**Card 17** `E3`
¿Cuál es la diferencia entre el pseudocódigo de estimación de volumen y el de integración general (Lebesgue-Stieltjes)?

> Volumen: sortea X^(j) uniforme en J^m, aplica indicatriz φ, estima varianza con fórmula Bernoulli. Integración general: sortea Z^(j) con densidad dF arbitraria, aplica función κ genérica, estima varianza con Welford. El caso de volumen es un caso particular con φ = indicatriz y dF = uniforme.

---

**Card 18** `E3`
¿Qué es la fórmula de Welford y para qué sirve?

> Es un algoritmo recursivo para calcular la varianza muestral en un solo pasaje: $T = T + (1-1/j)(\kappa(Z^{(j)}) - S/(j-1))^2$. Al final, $\hat\sigma^2_n = T/(n-1)$. Equivalente algebraicamente a la fórmula clásica pero más estable numéricamente y sin necesitar guardar todos los valores.

---

**Card 19** `E3`
¿Cuál es el orden del error de MC para integración multidimensional? ¿Por qué es ventajoso frente a métodos determinísticos?

> MC tiene error $O(n^{-1/2})$ independiente de la dimensión $m$. Los métodos de cuadratura clásicos tienen error $O(n^{-k/m})$ que se deteriora con $m$ (maldición de la dimensionalidad). MC gana cuando $m$ es grande o la función es irregular.

---

**Card 20** `E3`
¿Cuándo es preferible un método determinístico sobre Monte Carlo?

> Cuando la dimensión es baja y la función es suave y bien comportada. En esos casos los métodos de cuadratura convergen más rápido que $O(n^{-1/2})$.

---

**Card 21** `E3`
¿Cómo se determina n para integración general con precisión prefijada (ε, δ)?

> Con estimación en dos etapas: (1) correr n' muestras preliminares para estimar $\hat\sigma^2_{n'}$, (2) calcular $n_N = \lceil [\Phi^{-1}(1-\delta/2)]^2 \hat\sigma^2_{n'} / \varepsilon^2 \rceil$ y correr con semilla distinta. No se puede usar Hoeffding ni Chebyshev de peor caso porque la varianza no está acotada en general.

---

**Card 21b** `E3`
¿Por qué el paso 3 del algoritmo de determinación de n requiere semillas distintas a las de la corrida preliminar?

> Porque la estimación de $N$ se hizo con los datos de la corrida preliminar. Si usás las mismas semillas para la corrida final, los experimentos finales ya no son independientes de la estimación de $N$ — están correlacionados. Eso invalida la justificación estadística del método. Con semillas distintas, las dos corridas son independientes entre sí.

---

**Card 22** `E3`
¿Cómo generaliza Lebesgue-Stieltjes el problema de integración a dominios no acotados?

> Reescribís la integral como $\zeta = E_{dF}[\kappa(Z)]$ eligiendo una densidad $dF$ con soporte en todo el dominio. El estimador es $S/n$ acumulando $\kappa(Z^{(j)})$ con $Z^{(j)} \sim dF$. La densidad $dF$ no necesita ser uniforme ni el dominio acotado.

---

**Card 23** `E3`
¿Cuál es el IC para integración general y en qué se diferencia del de Wald?

> $I_{1,2} = \bar\zeta_n \mp \Phi^{-1}(1-\delta/2)(\hat\sigma^2_n/n)^{1/2}$. Misma estructura que Wald pero usando $\hat\sigma^2_n$ de Welford en vez de $\bar\lambda(1-\bar\lambda)$. Asintóticamente válido (TLC). Wald es el caso particular cuando φ es indicatriz.

---

## Sesión 7 — Problemas de conteo

**Card 24** `E4`
¿Qué es un problema de conteo?

> Un problema donde el espacio de dominio es discreto y se quiere estimar cuántos elementos de un conjunto base $\mathcal{X}$ cumplen una propiedad. Formalmente: estimar $\zeta = |\bigcup_{j=1}^k S_j|$ o $|\bigcap_{j=1}^k S_j|$ donde los $S_j$ son subconjuntos de $\mathcal{X}$.

---

**Card 25** `E4`
¿Por qué no siempre es aplicable un método enumerativo para un problema de conteo?

> Porque $|\mathcal{X}|$ crece exponencialmente con el tamaño del problema (e.g. $2^m$ para $m$ aristas en un grafo). Muchos de estos problemas son NP-completos, por lo que enumerar todos los elementos tiene tiempo prohibitivo cuando la dimensión crece.

---

**Card 26** `E4`
¿Cuáles son los 5 pasos para plantear un problema de conteo como Monte Carlo?

> 1. ¿Qué quiero contar? (identificar la propiedad de interés)
> 2. ¿Cuál es $\mathcal{X}$ y cuánto vale $r = |\mathcal{X}|$?
> 3. ¿Cómo sorteo uniformemente un elemento de $\mathcal{X}$?
> 4. ¿Cómo evalúo si un elemento cumple la propiedad?
> 5. Aplicar el esquema estándar: $\bar\zeta_n = rS/n$, varianza, IC.

---

**Card 27** `E4`
¿Cuál es el estimador puntual en Monte Carlo para conteo y por qué es insesgado?

> $\bar\zeta_n = rS/n$. Es insesgado porque $E[S] = n\lambda = n\zeta/r$, entonces $E[\bar\zeta_n] = r \cdot E[S]/n = r \cdot \zeta/r = \zeta$.

---

**Card 28** `E4`
¿Cuál es el estimador de varianza en Monte Carlo para conteo?

> $V(\bar\zeta_n) = \bar\zeta_n(r - \bar\zeta_n)/(n-1)$. Viene de que $S \sim \text{Bin}(n, \lambda)$ con $\lambda = \zeta/r$, y $\text{Var}(\bar\zeta_n) = \zeta(r-\zeta)/n$.

---

**Card 29** `E4`
¿Por qué el IC en conteo lleva un factor $r$?

> Porque $I_1, I_2$ son límites del IC para la proporción $\lambda = \zeta/r$. Como $\zeta = r\lambda$, se multiplica por $r$ para escalar de proporción a cantidad absoluta: IC = $(rI_1(S,n,\delta),\ rI_2(S,n,\delta))$.

---

**Card 30** `E4`
¿Qué tiene en común el esquema de conteo con el de estimación de volúmenes?

> Son formalmente idénticos. En ambos casos $S \sim \text{Bin}(n, \lambda)$, el estimador es $r \cdot S/n$, y la varianza y los ICs se calculan igual. La única diferencia es qué es $\mathcal{X}$ y cómo se sortea un elemento uniforme de él.

---

## Sesión 8 — Números aleatorios

**Card 31** `E5`
¿Cuáles son las cuatro fuentes principales de números aleatorios?

> 1. **Software (pseudo-aleatorios):** algoritmos determinísticos, rápidos y reproducibles via semilla. 2. **Hardware específico:** mide fenómenos físicos (ruido termal, decaimiento radiactivo, estática atmosférica). 3. **Mixto:** entropía del hardware estándar de la PC (teclado, mouse, disco) — base de `/dev/random`. 4. **Externas:** tablas históricas (RAND, años 50) y sitios web que sirven números generados por hardware.

---

**Card 32** `E5`
¿Cuáles son las fuentes físicas de aleatoriedad usadas en dispositivos de hardware?

> Dos familias principales: **mecánica cuántica** (decaimiento radiactivo detectable con contador Geiger, fotones en espejo semi-transparente) y **ruido termal** (ruido Johnson de una resistencia amplificado y comparado con un umbral, o estática de radio). Las fuentes cuánticas son teóricamente más "puras" porque el resultado de un evento cuántico es imprevisible según la física actual.

---

**Card 33** `E5`
¿Cómo funciona el método de Von Neumann para eliminar sesgo?

> Se toman los bits de a pares y se aplica la regla: par `00` o `11` → descartar; par `10` → emitir bit 1; par `01` → emitir bit 0. Funciona porque $P(1,0) = p(1-p) = P(0,1)$ para cualquier $p$, así que los bits emitidos son equiprobables. El costo es descartar siempre más del 50% de los bits generados.

---

**Card 34** `E5`
¿Por qué el método de Von Neumann descarta siempre más del 50% de los bits?

> La probabilidad de emitir un bit es $P(\text{emitir}) = 2p(1-p)$, que es el doble de $P(1,0) = P(0,1) = p(1-p)$. El máximo de $2p(1-p)$ es $1/2$, alcanzado cuando $p = 1/2$. Para cualquier sesgo ($p \neq 1/2$), la tasa de emisión es menor a $1/2$, es decir, se descarta más del 50%.

---

**Card 35** `E5`
¿Qué cinco tipos de problemas se han observado con generadores de hardware en la práctica?

> 1. **Sesgo:** fracción de 1s ≠ 0.5 (canadiense: ~0.498; alemán: hasta 0.623). 2. **Auto-correlación:** muestreo demasiado rápido → bits sucesivos correlacionados. 3. **Cross-correlación:** canales independientes se contaminan entre sí por falta de blindaje. 4. **Fallas físicas:** canales muertos o degradados — el dispositivo sigue produciendo números pero son malos. 5. **Errores de software:** ej. apertura de archivo en modo texto en Windows convierte bytes 10 en secuencias 13,10.

---

**Card 36** `E5`
¿Qué fuentes de números aleatorios están disponibles en Internet y cuáles son sus limitaciones?

> **random.org** (estática atmosférica): API REST gratuita con cuota ~1M enteros/día; archivo histórico requiere pago o BitTorrent. **QRNG-ANU** (óptica cuántica): cuota limitada en plan gratuito. **HotBits** (contador Geiger): dado de baja. **Tabla RAND** (años 50): solo $10^6$ dígitos, no alcanza para ejercicios con iteraciones 6D. Limitación estructural: el hardware real es lento (~20.000 bytes/s), por eso las cuotas son bajas.

---

**Card 37** `E5`
¿Por qué no es válido reutilizar valores de la tabla RAND para ampliar el tamaño muestral?

> La tabla tiene $10^6$ dígitos. Si cada iteración del ejercicio usa 6 números, con $n = 10^6$ iteraciones cada valor se reutiliza en promedio 6 veces. Eso introduce dependencia entre muestras, lo que invalida el supuesto de independencia del estimador Monte Carlo — el error real puede ser mayor que el calculado.

---

## Sesión 9 — Generadores pseudo-aleatorios

**Card 38**
¿Qué es el período de un generador pseudo-aleatorio y cuál es el máximo posible?

> El período es el largo de la secuencia antes de que los valores se repitan (largo del ciclo). El máximo es $Q^t$, donde $t$ es la cantidad de valores que el generador recibe en entrada (el tamaño del estado) y $Q$ es el rango de cada valor. Ese techo existe porque hay exactamente $Q^t$ estados posibles — cuando se repite un estado, se repite todo lo que sigue.

---

**Card 39**
¿Por qué $Q^t$ es el máximo período alcanzable?

> El estado del generador son $t$ valores entre $0$ y $Q-1$. Hay $Q^t$ estados posibles distintos. Como $f$ es determinística, cada estado tiene exactamente un sucesor — la secuencia de estados es una cadena determinística sobre un conjunto finito. El ciclo no puede ser más largo que el dominio. Período máximo = tamaño del dominio = $Q^t$.

---

**Card 40**
¿Cuáles son las propiedades deseables de un generador pseudo-aleatorio?

> 1. **Período largo:** exceder los requerimientos de la aplicación ($N \cdot M$ para $N$ replicaciones con $M$ números cada una). 2. **Eficiencia computacional:** rápido, poca memoria. 3. **Repetibilidad:** misma semilla reproduce la misma secuencia exactamente. 4. **Portabilidad:** mismo resultado en cualquier SO, hardware y lenguaje. 5. **Múltiples secuencias independientes:** poder generar subsecuencias separadas del ciclo. 6. **Uniformidad e independencia:** la secuencia debe pasar tests estadísticos de uniformidad y ausencia de correlación.

---

**Card 41**
¿Qué significa "múltiples secuencias independientes" y cómo se implementa?

> Dividir el ciclo en bloques contiguos y usar cada bloque como generador virtual independiente: $g_1 = Z_0 \ldots Z_{k-1}$, $g_2 = Z_k \ldots Z_{2k-1}$, etc. La garantía de no solapamiento es exacta. El problema práctico es llegar a $Z_k$ sin iterar $k$ pasos — algunos generadores ofrecen **jump ahead**: calcular $Z_n$ directamente para cualquier $n$ en tiempo constante.

---

**Card 42**
¿Por qué no alcanza con elegir semillas distintas para obtener secuencias independientes?

> Con semillas arbitrarias no hay garantía de que las subsecuencias no se solapan — una podría empezar en el medio del ciclo de otra. Verificarlo requeriría conocer el ciclo completo. La partición explícita del ciclo garantiza no solapamiento por construcción.

---

**Card 43**
¿Cuáles son las familias de generadores basados en recurrencias lineales?

> Todos tienen la forma $Z_i = \left(\sum_{s=1}^{p} A_s Z_{i-s}\right) \bmod Q$. Las tres subfamilias según $p$: (1) **$p=1$, recurrencias de un paso:** multiplicativos congruenciales ($Z_i = AZ_{i-1} \bmod Q$) y mixtos congruenciales ($Z_i = AZ_{i-1} + C \bmod Q$). (2) **$p>1$:** generadores recursivos múltiples (MRG). (3) **$p>1$, $Q=2$:** Feedback Shift Register generators (FSRG) y su generalización GFSRG.

---

**Card 44**
¿Cuál es la diferencia práctica entre el generador multiplicativo y el mixto congruencial?

> El mixto agrega una constante $C$: $Z_i = AZ_{i-1} + C \bmod Q$. Sin $C$, el cero es punto fijo (si $Z_i = 0$ toda la secuencia es cero), por lo que el período máximo del multiplicativo es $Q-1$. El mixto puede alcanzar período $Q$. A cambio, el multiplicativo es más rápido (una operación menos por paso).

---

**Card 45**
¿Período máximo garantiza buen comportamiento estadístico?

> No. Período máximo garantiza que no se repite ningún valor antes de agotar el ciclo, pero no dice nada sobre el orden. Ejemplo: $f(x) = (x+1) \bmod Q$ tiene período máximo pero genera $0, 1, 2, 3, \ldots$ — correlación total entre consecutivos, inútil para Monte Carlo. Las condiciones de período máximo son necesarias pero no suficientes; también se necesita uniformidad e independencia verificadas con tests estadísticos.

---

## Sesión 10 — Generadores pseudo-aleatorios (parte 3)

**Card 46**
¿Cuáles son los dos métodos de combinación de generadores lineales vistos en el curso?

> **Shuffling:** reordena la salida de un generador $X$ usando $Y$ como fuente de ruido para decidir el orden. **Merging:** combina dos generadores como $Z_i = (X_i + Y_i) \bmod M_1$. En ambos casos la nueva secuencia $Z$ tiene propiedades iguales o mejores que las originales, siempre que $X$ e $Y$ sean independientes.

---

**Card 47**
¿Cómo funciona el algoritmo de shuffling paso a paso?

> Se inicializa un buffer $T = (T_1, \ldots, T_K)$ con los primeros $K$ valores de $X$. Luego para cada $Z_i$: (1) generar $Y_i$, calcular $j = \lceil K Y_i / M_2 \rceil$; (2) emitir $Z_i = T_j$; (3) generar el siguiente valor de $X$ y reemplazar $T_j$ con él. La secuencia $Z$ es una permutación aleatoria de $X$; $Y$ solo decide el orden pero nunca aparece en la salida.

---

**Card 48**
¿Qué garantiza el método de shuffling y qué no puede garantizar?

> Garantiza que si $X$ e $Y$ son independientes, $Z$ tendrá propiedades iguales o mejores que $X$. No garantiza cuánto mejora — no es fácil cuantificar el grado de mejoría. Ventaja práctica: es conceptualmente simple, rápido de implementar y requiere poca memoria extra (solo el buffer de tamaño $K$).

---

**Card 49**
¿Cuál es el período del generador obtenido por merging y por qué?

> $\text{mcm}(d_1, d_2)$, donde $d_1$ y $d_2$ son los períodos de $X$ e $Y$ respectivamente. Si $d_1$ y $d_2$ son coprimos, el período se maximiza: $\text{mcm}(d_1, d_2) = d_1 \cdot d_2$. Esta es una ventaja importante del merging sobre usar un solo generador.

---

**Card 50**
¿Cuáles son los dos tipos de generadores no lineales vistos en el curso?

> **Cuadrático:** $Z_i = (AZ_{i-1}^2 + BZ_{i-1} + C) \bmod M$. **Inversivo:** $Z_i = (AZ_{i-1}^{-1} + C) \bmod M$, donde $Z_{i-1}^{-1}$ es el inverso multiplicativo módulo $M$ (el valor tal que $Z_{i-1} \cdot Z_{i-1}^{-1} \bmod M = 1$).

---

**Card 51**
¿Cuál es la ventaja y la desventaja de los generadores no lineales frente a los lineales?

> **Ventaja:** los lineales siempre producen valores que caen en una grilla en el espacio de dimensión $k$ — los no lineales evitan ese problema. **Desventaja:** mayor costo computacional y mayor dificultad de análisis teórico, por lo que no siempre superan en la práctica a las mejores variantes lineales.

---

**Card 52**
¿Cuáles son los dos enfoques para evaluar la bondad de un generador pseudo-aleatorio?

> **Tests teóricos:** calculan medidas sobre la estructura de la secuencia — los principales son discrepancia ($k$-equidistribución) y test espectral (distancia mínima entre hiperplanos). **Tests empíricos:** pruebas de hipótesis donde la hipótesis nula es que la secuencia generada se comporta como valores uniformes e i.i.d. Los más clásicos son Kolmogorov-Smirnov y $\chi^2$. El detalle de ambos escapa al scope del curso.

---

## Sesión 11 — Sorteo de variables aleatorias con distribución arbitraria

**Card 53**
¿Por qué es importante poder generar muestras de una distribución arbitraria?

> Dos razones: (1) evaluar $\kappa(z)$ puede ser computacionalmente más barato que evaluar $\phi(x)$ en el planteo uniforme; (2) es el mecanismo que habilita los métodos de reducción de varianza (importance sampling): si podés expresar $\zeta = \int \kappa(z)\,dF(z)$, podés cambiar $F$ por una $F^*$ más conveniente y reducir la varianza del estimador.

---

**Card 54**
¿Cuáles son los cuatro métodos generales para generar muestras de una distribución arbitraria?

> 1. Transformada inversa. 2. Composición. 3. Aceptación-rechazo. 4. Cociente de uniformes. El curso solo desarrolla el primero.

---

**Card 55**
¿Cuál es el teorema de la transformada inversa? ¿Y su prueba?

> **Teorema:** sea $U \sim U(0,1)$ y $F^{-1}(u) = \inf\{z : F(z) \geq u\}$. Entonces $Z = F^{-1}(U)$ tiene distribución $F$.
>
> **Prueba:** $\Pr(Z \leq z) = \Pr(F^{-1}(U) \leq z) = \Pr(U \leq F(z)) = F(z)$. La segunda igualdad usa la monotonía de $F$; la tercera, que $U$ es uniforme.

---

**Card 56**
¿Cómo se aplica la transformada inversa para generar una exponencial de parámetro $\lambda$?

> $F(x) = 1 - e^{-\lambda x}$, entonces $F^{-1}(u) = -\frac{1}{\lambda}\ln(1-u)$. Como $1-U \sim U(0,1)$ también, se simplifica a:
> $$X = -\frac{1}{\lambda}\ln(U)$$
> Generás $U \sim U(0,1)$ y calculás $X$.

---

**Card 57**
¿Cómo se aplica la transformada inversa para el caso discreto?

> Sea $\Pr(Z = a_k) = p_k$. Calculás las acumuladas $q_k = \sum_{l \leq k} p_l$. Generás $U \sim U(0,1)$, buscás $k$ tal que $q_{k-1} < U \leq q_k$, y devolvés $a_k$. La probabilidad de obtener $a_k$ es $q_k - q_{k-1} = p_k$. ✓

---

**Card 58**
¿Cuáles son las tres ventajas del método de la transformada inversa?

> 1. Un solo número aleatorio uniforme por muestra generada. 2. Preserva el signo de correlación: si $U_1$ y $U_2$ están correlacionados, $F^{-1}(U_1)$ y $F^{-1}(U_2)$ también — útil para variables antitéticas y secuencias comunes. 3. Permite generar muestras condicionales $Z \mid a' \leq Z \leq b'$ fácilmente.

---

**Card 59**
¿Cuándo falla la transformada inversa y cómo se maneja?

> Cuando $F^{-1}$ no tiene forma cerrada (ej: distribución normal). En ese caso hay que usar métodos numéricos para calcular la inversa, con el consiguiente error de aproximación y costo computacional. Para distribuciones específicas como la normal existen métodos alternativos más eficientes.

---

**Card 60**
¿Cuándo podés generar un vector aleatorio componente a componente independientemente, y cuándo no?

> Si las componentes son independientes, $F(z) = \prod_j F_j(z_j)$ y podés generar cada $Z_j$ por separado con su distribución marginal $F_j$. Si no son independientes, debés usar la factorización condicional: $f(z) = f_1(z_1) \cdot f_2(z_2 \mid z_1) \cdots$ y generar en orden, condicionando en los valores ya generados.

---

## Sesión 12 — IC simultáneos, estimación de cocientes, estimación secuencial

**Card 61**
¿Qué problema surge al querer hacer una afirmación simultánea sobre $L$ parámetros estimados con la misma corrida?

> Cada IC individual tiene nivel $\geq 1-\delta$, pero la probabilidad de que todos sean correctos al mismo tiempo no se puede calcular directamente porque las estimaciones están correlacionadas (se obtuvieron con los mismos datos). No se puede multiplicar las probabilidades individuales.

---

**Card 62**
¿Cuál es la desigualdad de Bonferroni y de qué se deriva?

> Para $L$ eventos $A_i$ (no necesariamente independientes):
> $$\text{Prob}\!\left(\bigcap_{i=1}^{L} A_i\right) \geq 1 - \sum_{i=1}^{L}(1 - \text{Prob}(A_i)) \geq 1 - L\delta$$
> Se deriva directamente del principio de inclusión-exclusión (también conocida como desigualdad de Boole).

---

**Card 63**
¿Cuáles son las dos formas de usar Bonferroni para ICs simultáneos?

> 1. **$\delta$ fijo por parámetro:** el nivel conjunto resultante es $\geq 1 - L\delta$. Al crecer $L$, la confianza conjunta cae.
> 2. **Nivel conjunto $1-\delta'$ predeterminado:** usás $\delta = \delta'/L$ para cada IC individual. Al crecer $L$, cada IC se vuelve más ancho (menor $\delta$ individual → IC más conservador).

---

**Card 64**
¿Qué limitación tiene el método de Bonferroni y cómo se puede paliar?

> Es conservador: la cota $1 - L\delta$ puede ser muy pesimista cuando $L$ es grande. En los dos modos de uso, crecer $L$ implica sacrificar ya sea confianza o precisión. Solo se puede paliar parcialmente aumentando $n$.

---

**Card 65**
¿Por qué no se puede usar directamente la fórmula estándar de IC para estimar un cociente $\theta = \mu_Y/\mu_X$?

> Porque $\bar{\theta}_n = \bar{Y}_n / \bar{X}_n$ es cociente de dos variables aleatorias, potencialmente correlacionadas si se calculan con las mismas replicaciones. Las fórmulas estándar asumen que el estimador es una media simple, no un cociente.

---

**Card 66**
¿Cuál es el resultado clave para la estimación de cocientes y cómo se construye el IC?

> $\bar{\theta}_n = \bar{Y}_n / \bar{X}_n$ es asintóticamente normal. Su varianza depende de las varianzas de $X$ e $Y$ y de su covarianza. En la práctica se estiman esas tres cantidades con la misma corrida de simulación (varianzas muestrales y covarianza muestral) y se construye un IC de la forma usual. Es una aproximación de orden $1/n$ — válida asintóticamente.

---

**Card 67**
¿En qué situación concreta aparece la estimación de cocientes en Monte Carlo?

> Cuando $R_1 \subseteq R_2$ y querés estimar $\theta = \lambda(R_1)/\lambda(R_2)$ (la proporción del volumen de $R_2$ que está en $R_1$). Otro caso: en problemas de conteo, estimar $|S_\alpha \cap S_\beta| / |S_\alpha|$ sin necesitar conocer $|S|$.

---

**Card 68**
¿Qué es la estimación secuencial y cuál es su ventaja conceptual?

> En vez de fijar $n$ antes de empezar, se va muestreando y se para cuando se detecta que ya se alcanzó la precisión especificada $(\varepsilon, \delta)$. La ventaja es no desperdiciar cómputo cuando ya se logró la precisión, y no parar antes de tiempo si aún no se logró.

---

**Card 69**
¿Cuál es la idea de la condición de parada en la estimación secuencial (Chow-Robbins)?

> Se para cuando la varianza estimada acumulada indica que ya se alcanzó la precisión $(\varepsilon, \delta)$ especificada. En la práctica, se compara la varianza muestral actual con un umbral que depende de $\varepsilon$ y de $\Phi^{-1}(1-\delta/2)$. No hace falta memorizar la fórmula exacta — lo importante es el concepto: el criterio de parada es dinámico y se evalúa después de cada replicación.

---

**Card 70**
¿Cuál es la limitación clave de la estimación secuencial y por qué no se usa mucho en la práctica?

> El nivel de confianza y la eficiencia del método solo convergen a los valores teóricos cuando $\varepsilon \to 0$. Para $\varepsilon$ finito hay un error de aproximación no controlado. Esta limitación hace que no sea demasiado usado en la práctica a pesar de ser conceptualmente atractivo.

---

## Sesión de repaso — Pseudocódigo genérico y muestreo antitético

**Card 71**
¿Cuál es el esquema genérico de Monte Carlo? Describí los parámetros de entrada y los 4 pasos.

> **Parámetros:** $\kappa$ (kernel, función del plan de muestreo), $n$ (tamaño de muestra), $1-\delta$ (nivel de cobertura).
>
> **Pasos:**
> 1. Inicializar $S = 0$, $T = 0$
> 2. Para $j = 1 \ldots n$: sortear $X^{(j)}$ con la distribución apropiada; calcular $W = \kappa(X^{(j)})$; si $j > 1$: $T \mathrel{+}= (1 - 1/j)(W - S/(j-1))^2$; $S \mathrel{+}= W$
> 3. Calcular estimadores puntuales: $\bar{\varphi} = S/n$, $\hat{\sigma}^2 = T/(n-1)$, $V[\bar{\varphi}] = \hat{\sigma}^2/n$
> 4. Calcular IC$(S, n, \delta)$

---

**Card 72**
¿Qué cambia y qué no cambia entre las distintas instanciaciones del esquema genérico de MC?

> **No cambia:** la estructura del loop, Welford para $T$, los estimadores puntuales $\bar{\varphi} = S/n$, $\hat{\sigma}^2 = T/(n-1)$, $V[\bar{\varphi}] = \hat{\sigma}^2/n$.
>
> **Cambia según el problema:**
>
> | Problema | Distribución de $X$ | $W = \kappa(X^{(j)})$ |
> |---|---|---|
> | Estimación $E(X)$ | $F_X$ (cualquiera) | $X^{(j)}$ |
> | Volumen | $U(J^m)$ | $\mathbf{1}[X^{(j)} \in R]$ |
> | Integración | $U(J^m)$ | $\kappa(X^{(j)})$ |
> | Conteo | Uniforme sobre subconj. de tamaño $M$ sin reemplazo | $r \cdot \mathbf{1}[a^{(j)} \text{ exitoso}]$ |
> | Antitético | $U(J^m)$ | $(\kappa(X^{(j)}) + \kappa(1-X^{(j)}))/2$ |
>
> **El IC también cambia:** TLC (Wald con $\hat{\sigma}^2$) en general; Agresti-Coull en conteo.

---

**Card 73**
¿Qué es el kernel $\kappa$ en el esquema genérico de Monte Carlo?

> Es la función que transforma cada réplica $X^{(j)}$ en el valor que se acumula. El método estima $\varphi = E[\kappa(X)]$. El nombre "kernel" es el más general — el curso también usa $\phi$ (Sesión 6) o $\kappa$ (Sesión 2) según el contexto. "Función a integrar" es incorrecto en general: solo aplica cuando el problema es explícitamente una integral.

---

**Card 74**
¿Por qué la fórmula de Welford $T \mathrel{+}= (1-1/j)(W - S/(j-1))^2$ es válida para cualquier instanciación del esquema?

> Porque es un algoritmo para calcular $\hat{\sigma}^2 = \frac{1}{n-1}\sum(W^{(j)} - \bar{W})^2$ de forma numéricamente estable y sin guardar todos los valores. El contenido de $W$ cambia según el problema, pero la fórmula acumula siempre la varianza de las réplicas individuales, independientemente de qué representen. Al final, $V[\bar{\varphi}] = \hat{\sigma}^2/n$.

---

**Card 75**
¿El IC por TLC $\bar{\varphi} \pm \Phi^{-1}(1-\delta/2)\sqrt{\hat{\sigma}^2/n}$ es válido para todas las instanciaciones?

> No siempre. Es válido para integración, volumen y estimación de $E(X)$ (asintóticamente, vía TLC). Para **conteo**, el estimador es una proporción y cuando $\hat{p}$ es extremo (cercano a 0 o 1) la aproximación normal es mala — el curso usa **Agresti-Coull** en ese caso. La estructura es siempre la misma (construir IC a partir de $\bar{\varphi}$ y $V[\bar{\varphi}]$ con nivel $1-\delta$), pero la fórmula concreta depende del problema.

---

**Card 76**
¿En qué consiste el muestreo antitético y por qué reduce la varianza?

> En lugar de generar réplicas independientes, se generan pares $(X^{(j)}, Y^{(j)})$ donde $Y^{(j)} = 1 - X^{(j)}$ (componente a componente), y se promedia el kernel: $W = (\kappa(X^{(j)}) + \kappa(Y^{(j)}))/2$.
>
> Reduce la varianza porque si $\kappa$ es monótona, $X$ e $Y$ están **negativamente correlacionados**: cuando $\kappa(X)$ es grande, $\kappa(Y)$ tiende a ser chico. La varianza del promedio es $(\sigma^2 + \sigma_{XY})/2$, y como $\sigma_{XY} < 0$, es menor que la varianza estándar $\sigma^2$.

---

**Card 77**
¿Cuál es la diferencia entre el pseudocódigo estándar y el antitético?

> El pseudocódigo es idéntico salvo dos líneas adicionales en el loop:
>
> ```
> Sortear X^(j) ~ U(J^m)
> Y^(j) = 1 − X^(j)              ← nuevo
> W = (κ(X^(j)) + κ(Y^(j))) / 2  ← nuevo (antes W = κ(X^(j)))
> Si j > 1: T += (1−1/j)(W − S/(j−1))²
> S += W
> ```
>
> Los pasos 3 y 4 (estimadores puntuales e IC) son idénticos al esquema estándar.
