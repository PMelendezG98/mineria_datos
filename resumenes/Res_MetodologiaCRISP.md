# 3. Metodología CRISP-DM

## 1. Introducción: El Fin de la Fragmentación
Antes de finales de los 90s, la minería de datos era caótica y *ad hoc*, lo que provocaba altas tasas de fracaso por la **desconexión entre objetivos de negocio y ejecución técnica**.

Para resolverlo nace **CRISP-DM** (*Cross-Industry Standard Process for Data Mining*), diseñado bajo 4 pilares:
1. **Agnóstico a la industria:** Funciona en retail, salud, banca, etc.
2. **Independiente de herramientas:** No importa si usas Python, R o SAS.
3. **Orientado al negocio:** El "Entendimiento del Negocio" es la piedra angular.
4. **Iterativo:** No es lineal (tipo cascada), permite retroalimentación y ajustes continuos.

---

## 2. Las Seis Fases de CRISP-DM



### Fase 1: Entendimiento del Negocio (La más crítica)
Fase diferenciadora. No se toca código.
* **Actividades Principales:**
  1. **Determinar Objetivos de Negocio:** ¿Qué dolor aliviamos? (Ej. "Aumentar retención 10%").
  2. **Evaluación de la Situación:** Inventario de recursos y restricciones legales (GDPR).
  3. **Traducción a Objetivos de Minería de Datos:** (Ej. "Reducir fraude" -> "Modelo de clasificación binaria con precisión >95% y Falsos Positivos <1%").

### Fase 2: Entendimiento de los Datos (Filtro de viabilidad)
No importa la brillantez del negocio si los datos no existen o son basura.
* **Actividades Principales:**
  1. **Recolección inicial:** Identificar fuentes internas (SQL) y externas (APIs).
  2. **Análisis Exploratorio (EDA):** Estadísticas descriptivas (media, mediana) y visualizaciones (histogramas).
  3. **Verificación de Calidad:** Detectar nulos, duplicados e inconsistencias lógicas (ej. edades negativas). *Principio: Garbage In, Garbage Out.*

### Fase 3: Preparación de los Datos (60-80% del tiempo total)
La fase más costosa. Los algoritmos requieren vectores matemáticos estructurados.
* **Actividades Principales:**
  1. **Selección y Limpieza:** Eliminar/Imputar valores faltantes y manejar *outliers*.
  2. **Ingeniería de Características (Feature Engineering):** Crear variables con poder predictivo. (Ej. Transformar "fecha" en "días desde la última transacción").
  3. **Transformaciones Técnicas:** Normalización/Escalado (0-1) y Codificación de variables de texto (*One-Hot Encoding*, *Label Encoding*).
  4. **Integración:** Unir tablas (joins).

### Fase 4: Modelado
El núcleo computacional.
* **Actividades Principales:**
  1. **Selección de Técnicas:** Regresión, Clasificación o Clusterización.
  2. **Diseño de la Prueba:** Dividir en conjunto de *Entrenamiento* (70-80%) y *Prueba* (20-30%). Usar **Validación Cruzada**.
  3. **Construcción:** Ajustar un modelo base (baseline), comparar algoritmos y afinar hiperparámetros.

### Fase 5: Evaluación (Óptica del Negocio)
Se revisa el modelo desde la silla del director, no del programador.
* **Actividades Principales:**
  1. **Resultados vs Objetivos:** ¿El rendimiento justifica el costo de implementación? (ROI).
  2. **Revisión Ética y Metodológica:** ¿Hay *data leakage* (fuga de datos del futuro)? ¿El modelo perpetúa sesgos?
  3. **Decisión:** Proceder al despliegue, Iterar (regresar) o Cancelar.

### Fase 6: Despliegue (Operacionalización)
Integrar la inteligencia en los procesos diarios.
* **Actividades Principales:**
  1. **Implementación:** APIs, dashboards, integración con CRM.
  2. **Monitoreo Continuo:** Vigilar el **Data Drift** (los datos cambian) y el **Model Drift** (el rendimiento se degrada).
  3. **Mantenimiento:** Definir cada cuándo se reentrena el modelo.

---

## 3. Casos de Estudio Reales (CRISP-DM en Acción)

### A. Walmart (Regresión - Predicción de Ventas)
* **Negocio:** Minimizar WMAE (Error Medio Absoluto Ponderado) dando peso a semanas festivas para optimizar inventario (evitar sub-stock y sobre-stock).
* **Preparación:** Manejo de devoluciones (valores negativos) y transformar días festivos en categorías.
* **Evaluación:** ¿La función de ganancias mejora respecto a usar simples promedios históricos?

### B. Fraude de Tarjetas (Clasificación binaria)
* **Negocio:** Datos súper desbalanceados (solo 0.17% es fraude). Hay **costos asimétricos**: un Falso Negativo (dejar pasar el fraude) cuesta miles de dólares; un Falso Positivo (falsa alarma) solo cuesta la frustración del cliente.
* **Despliegue:** Requiere latencia <100ms (tiempo real) y uso de SHAP para explicabilidad ante analistas.

### C. Bank Rakyat Indonesia (Clusterización - K-Means)
* **Negocio:** Segmentar 2,727 empresas usuarias del CMS para dar soporte diferenciado.
* **Modelado:** Se usó el Método del Codo, dando $K=3$.
* **Despliegue (Perfiles):** Cluster Élite (soporte 24/7), Masivo (autoservicio) e Intermedio (Upselling).

---

## 4. La Naturaleza Iterativa (Por qué no es lineal)
Fallar rápido y regresar es parte del proceso. Ejemplos de iteración:
* **De Modelado a Preparación:** Si el modelo rinde mal, regresas a crear nuevas variables (*Feature Engineering*).
* **De Evaluación a Negocio:** Si el modelo predice bien pero es inútil comercialmente, regresas a redefinir el dolor de la empresa.
* **De Despliegue a Modelado:** Si hay *Data Drift* en producción, regresas a reentrenar.

---

## 5. Desafíos Contemporáneos
1. **Integración Ágil:** Adaptar CRISP-DM a Sprints de 2 semanas. Lanzar un MVP rápido y luego iterar, en lugar de esperar el "modelo perfecto".
2. **Gobernanza y Ética:** Exigir auditorías de *Fairness* para evitar racismo algorítmico o sexismo en las variables.
3. **Explicabilidad (XAI):** En sectores regulados, las cajas negras son inaceptables. Se usa **SHAP** y **LIME** para cumplir con el "Derecho a la Explicación".
4. **MLOps:** DevOps aplicado al Machine Learning. Implica CI/CD para modelos, A/B testing en producción y monitoreo automatizado.

---

## 6. Comparación de Metodologías
* **CRISP-DM (Líder ~43%):** Negocio primero, agnóstico e iterativo. Su fase distintiva es el Entendimiento del Negocio.
* **KDD:** Enfoque más académico y técnico (proceso lineal).
* **SEMMA:** Específico para el ecosistema SAS.

---

## 7. Mejores Prácticas (Checklist de Examen)

### Entendimiento del Negocio
* **Hacer:** Definir criterios de éxito cuantitativos e involucrar a stakeholders reales.
* **Evitar:** Definir objetivos técnicos sin conexión con KPIs de negocio.

### Preparación de Datos
* **Hacer:** Documentar cada transformación para que sea reproducible.
* **Evitar:** Eliminar datos sin entenderlos o crear *Data Leakage*.

### Modelado
* **Hacer:** Comenzar con un modelo simple (baseline) y usar validación cruzada SIEMPRE.
* **Evitar:** Elegir un algoritmo complejo solo "porque está de moda" o sobreajustar en el test.

### Despliegue
* **Hacer:** Diseñar asumiendo la degradación del modelo y planificar reentrenamientos.
* **Evitar:** "Lanzar y olvidar" sin monitoreo.
