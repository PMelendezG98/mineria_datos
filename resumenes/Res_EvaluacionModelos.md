# 4. Evaluación de Modelos como Herramienta Financiera

## 1. La Ilusión de la Exactitud (Accuracy Paradox)
En el mundo de los negocios, la pregunta no es *"¿Qué tan preciso es el modelo?"*, sino **"¿Cuánto dinero genera o ahorra?"**.

**El problema con la Exactitud (Accuracy):**
En contextos donde un evento es muy raro (ej. Fraude que es solo el 0.1%), un modelo "tonto" que siempre prediga "No es fraude" tendrá un **99.9% de Accuracy**, pero será un fracaso rotundo porque no detectará un solo fraude real.
* *Regla de examen:* Nunca uses Accuracy si las clases están muy desbalanceadas o si los costos de equivocarte son asimétricos.

---

## 2. Los Costos Asimétricos del Error (FP vs. FN)
Dependiendo del problema, un error cuesta mucho más que el otro.

**A) ¿Cuándo es más caro el Falso Negativo (FN)?**
Cuando NO detectar el evento tiene consecuencias graves.
* *Ejemplos:* Fraude bancario (pierdes la transacción), Diagnóstico de cáncer (riesgo de muerte), Fallas en maquinaria.
* *Solución:* Prefieres tener falsas alarmas (Falsos Positivos) con tal de no perderte los eventos reales.

**B) ¿Cuándo es más caro el Falso Positivo (FP)?**
Cuando intervenir/actuar te cuesta mucho dinero o daña la marca.
* *Ejemplos:* Mandar folletos carísimos de tarjetas Platinum a gente que no califica, Filtrar correos importantes como Spam, Hacer una cirugía innecesaria.

---

## 3. Repaso de Métricas y la Matriz como Estado de Resultados

### La Tabla de Valor Financiero (El corazón del tema)
Imagina un caso de Retención de Clientes (Churn).
* **LTV (Lifetime Value):** Lo que vale el cliente (Ej. $5,000).
* **Costo de Retención (C):** Lo que te cuesta llamarlo o darle un descuento (Ej. $200).

|                     | Realidad: Se va (1) | Realidad: Se queda (0) |
|---------------------|-----------------------------------|-----------------------------|
| **Predice: Se va (1)**| **TP:** Ganamos $(LTV - C)$ | **FP:** Perdemos $(-C)$ |
| **Predice: Se queda (0)**| **FN:** Perdemos todo $(-LTV)$ | **TN:** No hacemos nada $(\$0)$ |

**La Fórmula de Beneficio Esperado:**
$$Beneficio = TP \times (LTV - C) + FP \times (-C) + FN \times (-LTV)$$
*Nota de examen:* Siempre haz este cálculo. Un modelo con menos *Accuracy* puede generar mucho más dinero si se equivoca en las cosas "baratas" (Falsos Positivos) y acierta en las "caras" (Verdaderos Positivos).

---

## 4. Priorización y Eficiencia de Campañas

Cuando no tienes presupuesto para llamar al 100% de tus clientes, usas el modelo para **priorizar**.

### A) La Curva de Ganancia Acumulada (Cumulative Gain)

Grafica qué porcentaje total de "churners" capturas si vas contactando a tu base en orden de riesgo.
* *Lectura práctica:* "Si contactamos solo al 30% más riesgoso de nuestra base, capturamos el 80% de las fugas totales".

### B) El Gráfico de Elevación (Lift)
Mide cuántas veces **mejor** es tu modelo comparado con elegir clientes al azar.
* *Fórmula:* $Lift = (\% \text{ de churners en el decil}) / (\% \text{ de churners en toda la base})$
* *Lectura práctica:* "Un Lift de 4.0x significa que si usamos el modelo en nuestro top 10% de clientes, encontraremos 4 veces más fugas que si lo hiciéramos a ciegas".

---

## 5. La Curva de Beneficio (Profit Curve) y el Umbral Óptimo

¿A partir de qué porcentaje de riesgo debo contactar a un cliente? La **Curva de Beneficio** grafica todos los umbrales posibles (de 0 a 1) contra el dinero total que generan.

Tiene forma de montaña:
* **Umbral muy bajo (Ej. 0.01):** Contactas a casi todos. Gastas demasiado en Falsos Positivos (llamar a los que no se iban). Pierdes dinero.
* **Umbral muy alto (Ej. 0.99):** Solo contactas a los súper seguros. Tienes muchos Falsos Negativos (se te escapan los que se querían ir). Pierdes dinero.
* **El Umbral Óptimo ($t^*$):** La cima de la montaña. Es el punto exacto donde la campaña da su máxima ganancia.

**La Fórmula del Umbral Óptimo (Si los costos son constantes):**
$$t^* = \frac{Costo\_Intervencion}{LTV}$$
*Ejemplo:* Si retener cuesta $200 y el cliente vale $5,000, $t^* = 200 / 5000 = 0.04$.
*Conclusión de negocio:* Debes intervenir con cualquier cliente que tenga más del **4% de probabilidad de fuga**, ya que matemáticamente el beneficio justifica el riesgo.

---

## 6. Curva ROC vs. Precision-Recall (PR)
A nivel directivo, la curva ROC puede engañar cuando hay clases muy desbalanceadas (como en Fraude).
* **ROC-AUC:** Mide qué tan bien *rankea* el modelo. Falla en fraude porque su cálculo incluye los Verdaderos Negativos (TN), que son millones, diluyendo el error de las falsas alarmas.
* **PR-AUC (Precision-Recall):** Mide la confiabilidad ("Cuando el modelo dice fraude, ¿qué tanto puedo creerle?"). Ignora los TN, enfocándose solo en lo que predijo como positivo.
* *Regla:* Usa PR-AUC siempre que estés lidiando con Fraude, Churn o Enfermedades Raras.
