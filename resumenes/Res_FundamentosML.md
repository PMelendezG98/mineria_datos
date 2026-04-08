# 2. Fundamentos de Machine Learning

## 1. El Cambio de Paradigma: De Reglas al Aprendizaje Inductivo
Tradicionalmente (ej. años 90), la automatización usaba **sistemas basados en reglas (programación deductiva)**. 
* *Ejemplo:* Si ingreso > $50k y antigüedad > 2 años, aprobar crédito.
* *El problema:* Es frágil. Si alguien gana $49k pero no tiene deudas, el sistema falla. Las reglas explotan exponencialmente cuando metes miles de variables.

**El Machine Learning invierte el proceso.** No le damos las reglas a la máquina; le damos los **datos (entradas)** y las **respuestas deseadas (salidas)**, y la máquina *descubre* las reglas.

**La Analogía Clave:**
* **Arquitecto (Programación Tradicional):** Diseña todo de arriba hacia abajo. Control absoluto, pero baja adaptabilidad.
* **Jardinero (Machine Learning):** Prepara el entorno y nutre el suelo (datos limpios). La planta (el modelo) crece por procesos intrínsecos.

### Definición Formal de Machine Learning (Tom Mitchell)
Un programa aprende de la experiencia **E** con respecto a una tarea **T** y una medida de rendimiento **P**, si su desempeño en la tarea T, medido por P, mejora con la experiencia E.

Para el ingeniero de negocios, descomponer esto ayuda a identificar oportunidades de ML:

| Componente | Definición | Ejemplo: Detección de Fraude | Ejemplo: Valoración Inmobiliaria |
| :--- | :--- | :--- | :--- |
| **Tarea (T)** | Labor que el sistema debe ejecutar | Clasificar una transacción como "Fraudulenta" o "Legítima" | Predecir el precio de venta de una propiedad |
| **Experiencia (E)** | Los datos históricos que el sistema utiliza para entrenarse | Millones de transacciones pasadas con sus etiquetas reales | Historial de ventas de casas con características y ubicación |
| **Rendimiento (P)** | La métrica cuantitativa que define el éxito | Precisión, Recall, o Costo Financiero del Fraude | Error Cuadrático Medio (diferencia precio predicho vs. real) |

*Implicación de negocio:* El ML es un activo que se aprecia con el uso (a más experiencia, mejor rendimiento).

---

## 2. Fundamentos Teóricos: Aproximación de Funciones
El objetivo del ML es encontrar una función estimada $\hat{f}(x)$ que imite a la realidad $f(x)$ lo suficientemente bien.
La realidad siempre tiene "ruido" o variables no medidas ($\epsilon$):
$$y = f(x) + \epsilon$$
$$y \approx \hat{f}(x)$$

**Generalización vs. Memorización:** El modelo debe aprender la *estructura subyacente* (los principios) para predecir datos nuevos, no aprenderse las respuestas del entrenamiento de memoria.

---

## 3. Paradigmas de Aprendizaje

### A. Aprendizaje Supervisado (Con Maestro)
Usa **Datos Etiquetados** (x, y). El objetivo es la Predicción. Feedback directo.
* **Regresión (Continua):** ¿Cuánto? (Ej. Predecir ventas mensuales, vida útil de una máquina).
* **Clasificación (Discreta):** ¿Cuál? (Ej. ¿El cliente comprará Sí/No?, Fraude).
* *Ejemplo de negocio (Churn):* Entrenas al modelo con 5 años de datos de clientes que cancelaron o se quedaron. Lo aplicas a clientes actuales para saber quién está en riesgo *antes* de que cancele.

### B. Aprendizaje No Supervisado (Sin Maestro)
Usa **Datos No Etiquetados** (x). El objetivo es describir y encontrar estructura.
* **Clustering:** Agrupar. (Ej. Segmentar clientes por comportamiento de compra sin saber previamente cuántos grupos hay).
* **Detección de Anomalías:** Eventos que se desvían de la norma. (Ej. Seguridad informática).
* **Reducción de Dimensionalidad:** Simplificar variables.

### Tabla Comparativa de Paradigmas (De Examen)
| Característica | Aprendizaje Supervisado | Aprendizaje No Supervisado |
| :--- | :--- | :--- |
| **Datos de Entrada** | Datos Etiquetados (x, y) | Datos No Etiquetados (x) |
| **Objetivo** | Predicción (Predecir y) | Descripción (Entender estructura de x) |
| **Feedback** | Directo (Error entre predicción y real) | Inexistente (Basado en coherencia interna) |
| **Complejidad de Evaluación** | Más fácil de evaluar (¿Acertó?) | Difícil de evaluar objetivamente |
| **Ejemplo Típico** | Predecir precio de acciones | Segmentar clientes por comportamiento |
| **Fase CRISP-DM típica** | Modelado con objetivo claro | Entendimiento de Datos / Exploración |

---

## 4. El Dilema Estratégico: Sesgo vs. Varianza (Bias-Variance Trade-off)
El error total de un modelo se descompone matemáticamente en:
$$\text{Error Total} = \text{Sesgo}^2 + \text{Varianza} + \text{Error Irreducible } (\epsilon)$$

* **Sesgo (Bias - Subajuste/Underfitting):** El modelo hace suposiciones demasiado simplistas. Es "cerrado de mente". Falla en el entrenamiento y en la prueba.
* **Varianza (Variance - Sobreajuste/Overfitting):** El modelo es hiper sensible al ruido. Es "impresionable". Le va al 100% en el entrenamiento, pero falla miserablemente con datos nuevos.

En el aprendizaje automático, existe una **tensión inevitable** para encontrar el punto óptimo (donde la suma del sesgo y varianza es mínima):
* **Modelo más complejo** $\rightarrow$ Reduce sesgo (se ajusta mejor) pero aumenta varianza (se vuelve más inestable).
* **Modelo más simple** $\rightarrow$ Reduce varianza (se vuelve más estable) pero aumenta sesgo (es demasiado simple).

**¿Cómo se logra este balance? (Técnicas de mitigación):**
* **Validación Cruzada:** Evaluar el modelo en múltiples particiones de datos (evita que el modelo se aprenda de memoria una sola muestra).
* **Regularización:** Penalizar la complejidad innecesaria (evita que el modelo se vuelva loco con tantas variables).
* **Early Stopping:** Detener el entrenamiento antes del sobreajuste.
---

## 5. Regresión Lineal: La Herramienta de Predicción Continua
Es el "caballo de batalla" de la analítica. Aunque existen cosas más complejas, se sigue usando muchísimo por su **simplicidad, velocidad y alta interpretabilidad** (es una "Caja Blanca").

**El Problema de Negocio:**
Se usa exclusivamente cuando tu variable objetivo ($y$) es un **número continuo**.
* *Ejemplos:* Proyección de ventas trimestrales ($), estimar elasticidad-precio, predecir tiempo de entrega (días), valoración inmobiliaria.

**Intuición Geométrica:**
Imagina un gráfico de dispersión (X = Gasto en Marketing, Y = Ingresos). Los puntos están regados pero con tendencia a subir. La regresión lineal busca dibujar la **única línea recta perfecta** que pase lo "más cerca" posible de todos los puntos al mismo tiempo.

### La Ecuación Desmenuzada
Para entender el modelo, hay que entender su anatomía matemática:
$$y = \beta_0 + \beta_1 x_1 + \beta_2 x_2 + ... + \beta_n x_n + \epsilon$$

* **$y$ (Target):** Lo que queremos predecir (Ej. Ventas).
* **$x_i$ (Features):** Nuestras variables de entrada (Ej. $x_1$ = Gasto en Ads, $x_2$ = Precio).
* **$\beta_0$ (Intercepto):** El valor base de $y$ si todas las $x$ fueran cero. (Ej. Las ventas orgánicas si apagáramos todo el marketing).
* **$\beta_i$ (Coeficientes/Pesos):** El impacto de cada variable. Si $\beta_1 = 0.75$, significa que por cada peso extra que meto a $x_1$, mis ventas $y$ suben 75 centavos.
* **$\epsilon$ (Error Irreducible):** El "ruido" de la realidad. Cosas que afectan las ventas pero que no medimos (clima, humor del cliente, etc.).

### El Método de Mínimos Cuadrados (OLS)
¿Cómo sabe la computadora cuál es la "mejor" línea? Usando el método OLS (Ordinary Least Squares). 
Mide la distancia vertical (el error o "residuo") entre cada punto real y la línea que propuso. Su objetivo es que la suma de esos errores sea la más pequeña posible.

$$\text{Minimizar: } \sum_{i=1}^{n} (y_{\text{real}}^{(i)} - y_{\text{predicho}}^{(i)})^2$$

**¿Por qué se eleva al cuadrado?** Por dos razones de examen:
1. Para quitar los signos negativos (un error de -5 y uno de +5 se cancelarían si no los cuadras).
2. Para **penalizar fuertemente los errores grandes**. Un error de 2 se vuelve 4, pero un error de 10 se vuelve 100. *Esto hace que la regresión lineal sea extremadamente sensible a los Outliers (valores atípicos).*

### Métricas de Evaluación
* **$R^2$ (Coeficiente de Determinación):** Va de 0 a 1. Te dice qué porcentaje de la realidad logra explicar tu modelo. (Ej. $R^2 = 0.85$ significa que tu modelo explica el 85% del comportamiento de las ventas, el otro 15% es incertidumbre).
* **RMSE (Raíz del Error Cuadrático Medio):** Te da el error promedio en las mismas unidades de tu negocio, pero penalizando errores graves. (Ej. "Nos equivocamos en promedio por ±$500 pesos").
* **MAE (Error Absoluto Medio):** Promedio de los errores absolutos. Es mucho más "relajado" y robusto contra *outliers* que el RMSE.

### Limitaciones
1. **Asume Linealidad:** Si en la vida real tus datos hacen una curva (exponencial), la línea recta va a predecir basura.
2. **Sensibilidad a Outliers:** Un solo punto atípico gigantesco puede "jalar" y torcer toda la línea por culpa de elevar los errores al cuadrado en OLS.
3. **Multicolinealidad:** Si dos variables de entrada miden casi lo mismo (Ej. "Sueldo Anual" y "Sueldo Mensual"), la ecuación se vuelve inestable y los coeficientes $\beta$ pierden sentido lógico.

---

### Regularización: Combatiendo el Sobreajuste (Overfitting)
Cuando le metes demasiadas variables a una Regresión Lineal, o hay multicolinealidad, el modelo sufre **Overfitting (Alta Varianza)**. Empieza a crear coeficientes $\beta$ gigantes y erráticos para intentar "tocar" cada punto del entrenamiento, fracasando en la vida real.

Para curar esto, usamos la **Regularización**, que no es más que agregarle un "castigo" matemático a la función de costo si el modelo se pone muy complejo:

#### 1. Regresión Ridge (Penalización L2)
Castiga elevando al **cuadrado** los coeficientes.
$$\text{Minimizar: } \text{SSE} + \lambda \sum_{j=1}^{p} \beta_j^2$$
* **Efecto:** Reduce el tamaño de los coeficientes gigantes y reparte el peso entre variables correlacionadas. 
* **Regla de oro:** Ridge "encoge" todas las variables, pero **nunca elimina ninguna (no llega a cero exacto)**. Úsala cuando crees que *todas* tus variables aportan algo al negocio.

#### 2. Regresión Lasso (Penalización L1)
Castiga usando el **valor absoluto** de los coeficientes.
$$\text{Minimizar: } \text{SSE} + \lambda \sum_{j=1}^{p} |\beta_j|$$
* **Efecto:** Es un asesino de variables. Literalmente puede forzar el peso de una variable a **cero exacto**.
* **Regla de oro:** Lasso funciona como un selector automático de características (*Feature Engineering* automático). Úsala cuando tienes 100 variables y quieres que el modelo te diga cuáles 10 son las únicas que realmente importan.

#### Elastic Net (Lo mejor de ambos mundos)
Si tienes cientos de variables y muchas están correlacionadas, Lasso podría volverse loco eliminando demasiadas. Elastic Net combina ambos castigos:
$$\text{Minimizar: } \text{SSE} + \lambda_1 \sum |\beta_j| + \lambda_2 \sum \beta_j^2$$

*(El valor de lambda $\lambda$, que decide qué tan duro es el castigo, siempre se encuentra haciendo Validación Cruzada).*

#### Tabla Comparativa: Ridge vs. Lasso

| Característica | Ridge (L2) | Lasso (L1) |
| :--- | :--- | :--- |
| **Penalización** | Suma de cuadrados ($\beta_j^2$) | Suma de absolutos ($\|\beta_j\|$) |
| **Selección de Variables** | No (las encoge pero las conserva todas) | Sí (puede forzar coeficientes a CERO) |
| **Interpretabilidad** | Media (mantienes un modelo grande) | Alta (te deja un modelo simple) |
| **Multicolinealidad** | La maneja excelente (reparte pesos) | Selecciona una variable al azar y mata al resto |
| **Conexión Sesgo-Varianza** | Aumenta el sesgo, reduce la varianza | Aumenta el sesgo, reduce la varianza |

---

## 6. Regresión Logística: Clasificación y Probabilidad
A diferencia de la Regresión Lineal (que predice "cuánto"), la Regresión Logística predice **"cuál"** (clasificación binaria: 1 o 0).
* *Ejemplos:* ¿Es fraude o no? (1/0), ¿El cliente cancelará? (1/0), ¿Es spam? (1/0).

### ¿Por qué falla la Regresión Lineal aquí?
Si intentas usar una línea recta para predecir si alguien va a comprar (1) o no (0), la línea se va a ir al infinito. Para un cliente con ingresos altísimos, la recta podría predecir un "1.5" (¡un 150% de probabilidad de compra!), lo cual es matemáticamente absurdo.

### La Función Sigmoide (La magia matemática)
Para arreglar eso, la Regresión Logística toma el resultado de la línea recta y lo pasa por la **Función Sigmoide**. Esta función tiene forma de "S" y su único trabajo es "aplastar" cualquier número para que a fuerza caiga en un rango entre **0 y 1**.
$$P(y=1) = \frac{1}{1 + e^{-(\beta_0 + \beta_1 x)}}$$

### El Verdadero Valor: Probabilidades vs. Etiquetas
El modelo no te escupe un "Sí" o un "No" a secas. Te da el **riesgo exacto** (una probabilidad). Esto es oro puro para el negocio porque te permite hacer estrategias distintas:
* Cliente A (Probabilidad 51%): Salvable. Mándale un correo amistoso.
* Cliente B (Probabilidad 99%): Causa perdida. No gastes presupuesto en él.

### El Umbral de Decisión (Thresholding)
Para que la máquina tome una decisión final, usamos un umbral (por defecto es 0.5: arriba de 0.5 es "Sí", abajo es "No"). 
* **El truco de negocio:** Tú puedes mover esa perilla dependiendo del **Costo del Error**. Si detectar fraude es vital porque un fraude te cuesta $5,000 y molestar al cliente solo $10, puedes bajar el umbral a **0.20** ("Si hay un 20% de riesgo, bloquéalo"). Vas a tener muchas falsas alarmas, pero protegerás el dinero del banco.

### La Matriz de Confusión (El corazón de la evaluación)
Es la tabla que cruza lo que el modelo **predijo** vs. lo que **realmente pasó**. 

|                | Predicho: Negativo (0) | Predicho: Positivo (1) |
|----------------|------------------------|------------------------|
| **Real: Negativo (0)** | **Verdadero Negativo (TN)** | **Falso Positivo (FP)** |
| **Real: Positivo (1)** | **Falso Negativo (FN)** | **Verdadero Positivo (TP)** |

* **TP (True Positive):** Predijiste fraude y SÍ era. (Éxito).
* **TN (True Negative):** Predijiste legítimo y SÍ era. (Éxito).
* **FP (Falso Positivo - Falsa Alarma):** Predijiste fraude, pero era legítimo. (Costo: Enojo del cliente).
* **FN (Falso Negativo - El Peor Error):** Predijiste legítimo, pero ERA FRAUDE. (Costo: Pierdes miles de pesos).

### Métricas Derivadas
* **Accuracy (Exactitud):** ¿En qué porcentaje le atinamos a todo? $(TP+TN) / \text{Total}$. *(Inútil si las clases están muy desbalanceadas).*
* **Precision (Precisión):** De todas las alarmas que sonaron, ¿cuántas eran reales? $TP / (TP + FP)$.
* **Recall (Sensibilidad):** De todos los criminales que había en la calle, ¿a cuántos logramos atrapar? $TP / (TP + FN)$.
* **F1-Score:** La media armónica entre Precision y Recall. Te da un balance justo cuando tienes datos muy asimétricos.
  $$F1 = 2 \cdot \frac{Precision \cdot Recall}{Precision + Recall}$$

### Curva ROC y AUC (Evaluación Global)
* **Curva ROC:** Gráfica que muestra cómo se comporta el modelo en todos los umbrales posibles (Sensibilidad vs. Tasa de Falsos Positivos).
* **AUC (Área Bajo la Curva):** Es la calificación del modelo (de 0 a 1). 
  * **0.5:** El modelo es inútil (es como lanzar una moneda).
  * **1.0:** El modelo es perfecto.
  * *Interpretación real:* Un AUC de 0.85 significa que, si agarras a un cliente que se fue y a uno que se quedó, hay un 85% de probabilidad de que el modelo haya rankeado con mayor riesgo al que realmente se fue.

---

## 7. Clusterización con K-Means: Estructurando el Caos (No Supervisado)
Aquí no predecimos el futuro, aquí **descubrimos grupos ocultos** (segmentación de clientes). Es un algoritmo No Supervisado porque no le damos etiquetas ("respuestas") a la máquina.

### Intuición del Algoritmo (Los 4 Pasos)
Es un algoritmo geométrico iterativo que busca "centros de gravedad":
1. **Inicialización:** Decides cuántos grupos quieres ($K$) y la máquina tira $K$ puntos al azar (centroides).
2. **Asignación:** Cada cliente (punto) se afilia al centroide que le quede más cerca.
3. **Actualización:** El centroide se mueve al centro exacto (al promedio) de todos los clientes que se le afiliarán.
4. **Iteración:** Se repiten los pasos 2 y 3 hasta que los centroides dejan de moverse (convergencia).

### La Regla de Oro Técnica: ¡Estandarizar los Datos!
*Pregunta segura de examen:* K-Means usa distancias geométricas. Si no **normalizas/estandarizas** los datos antes (ponerlos en la misma escala, ej. de 0 a 1), el algoritmo va a colapsar.
* *Ejemplo:* Si tienes la variable "Edad" (de 18 a 65) y la variable "Ingreso" ($20,000 a $100,000), una simple diferencia de 5,000 pesos va a eclipsar por completo una diferencia de 40 años. El modelo solo agrupará por dinero ignorando la edad.

### ¿Cómo elegir el número óptimo de clusters ($K$)?
Como no hay "respuestas correctas", usamos métricas matemáticas y de negocio:
1. **Método del Codo (Elbow Method):** Graficas la *Inercia* (suma de distancias al centro) probando de 1 a 10 clusters. Buscas el "codo" de la gráfica, donde meter más clusters ya no reduce significativamente la inercia.
2. **Índice de Silueta:** Mide la cohesión (qué tan pegados están los de un grupo) vs. la separación (qué tan lejos están del grupo vecino). Un valor cercano a **1** es excelente; un **0** significa que se están empalmando.

### Profiling (La traducción al Negocio)
El algoritmo solo te escupe etiquetas (ej. "Cluster A", "Cluster B"). El trabajo del Ingeniero en Negocios es calcular los promedios de cada grupo para darles una "personalidad" y justificar las decisiones corporativas:

| Cluster | Edad Prom. | Gasto Prom. | Interpretación de Negocio |
| :--- | :--- | :--- | :--- |
| **A** | 22 años | $150 | "Estudiantes Digitales" |
| **B** | 45 años | $800 | "Profesionales Ocupados" |
| **C** | 35 años | $300 | "Familias Ahorradoras" |

Estos perfiles se traducen directamente en **estrategias de marketing diferenciadas**:
* **Cluster A:** Descuentos estudiantiles, experiencia mobile-first, redes sociales.
* **Cluster B:** Servicio premium, conveniencia, compra rápida.
* **Cluster C:** Valor por dinero, bundles familiares, programas de lealtad.
