# Fondeos — Estructura de la capacitación

Orden propuesto de cards del deck. Cada card = una pantalla completa (100dvh), navegable con wheel/touch/rail. Texto mínimo, nivel explicado para alguien que no sabe nada de cuentas de fondeo.

---

## Fase 0 — Apertura

**Card 0 — Portada**
- Título + branding (equivalente a `#card-0` de Luis).
- Sin slideshow salvo que se quiera agregar.

**Card 1 — Qué es una cuenta de fondeo**
- Concepto: apalancar capital ajeno para operar, a cambio de un fee de acceso + disciplina.
- Mensaje: es una oportunidad, no un atajo — exige cumplir reglas.

---

## Fase 1 — Con quién trabajamos

**Card 2 — Empresas con las que confiamos**
- FTMO, 5ERS, Alpha Capital, FundingPips, Atmos, Breakout — como recomendación positiva, sin mencionar categorías de riesgo ni nombrar otras firms.
- Tono: "estas son las que usamos nosotros", no "cuidado con las demás".

**Card 3 — Cómo leer las reglas de cada una**
- Las reglas viven en la FAQ de cada empresa.
- Importante: cambiar el idioma nativo de la página, no usar Google Translate (riesgo de imprecisión).
- Grid de links directos a las 6 FAQ (pendiente: Johnny los pega).

---

## Fase 2 — Tipos de programa (conocimiento compuesto: de más simple/barato a más exigente)

**Card 4 — Mapa de tipos de prueba**
- 2 fases, 1 fase, instantánea, pasa-primero-paga-después (NOVA).
- Presentados como espectro: costo de entrada ↔ velocidad de cobro ↔ margen de error permitido.

**Card 5 — 2 fases: la cuenta para quedarte**
- Uso: cuando vas a tomarte el tiempo de probar consistencia, para una cuenta de largo plazo.
- Menor fee, más pasos.

**Card 6 — 1 fase: el punto medio**
- Uso: menos pasos que 2 fases, todavía con evaluación previa.
- Fee más alto que 2 fases a cambio de velocidad.

**Card 7 — Instantánea: dinero rápido**
- Uso: liquidez rápida, ya fondeada desde el día uno, cobrás al cumplir consistencia.
- Fee más caro, exige más disciplina (sin fase de práctica protegida).
- Nota: al retirar el 100%, la cuenta resetea al capital inicial (no se pierde, se reinicia).

**Card 8 — NOVA (Atmos): pasa primero, paga después**
- Mecánica: $5 de entrada a la evaluación (fase única, 5% total), luego $184 (ejemplo cuenta $25k) al pasar, para activar el capital real.
- Particularidad de riesgo: 1% diario **por activo** (flotante + cerrado), no agregado — distinto a como se calcula en otras cuentas.
- Mecánica de recompra: al cobrar, la cuenta se cierra, pero se puede volver a pagar el fee de esa prueba para reabrir sobre el mismo capital ya validado (sin volver a pasar la evaluación).
- Esta card es explicación en texto — no entra en la calculadora genérica (reglas propias, ver nota en spec técnica).

---

## Fase 3 — Reglas comunes (glosario transferible — genérico + caso Atmos)

Cada card de esta fase sigue el mismo patrón: **concepto general → cómo se ve en Atmos (ejemplo concreto) → qué revisar en la FAQ de otra firm**. Esto es intencional: el objetivo es que después de la capacitación, cualquiera pueda leer una FAQ distinta y reconocer el mismo concepto aunque el número cambie.

**Card 9 — Riesgo diario**
- Concepto: % máximo que podés perder en un día antes de romper la cuenta.
- Ejemplo Atmos Instant: 3% de $10k = $300/día.

**Card 10 — Riesgo total (con y sin trailing)**
- Concepto: % máximo de pérdida acumulada permitida sobre el capital.
- Diferencia entre estático (fijo desde el inicio) y trailing (se mueve con el equity).

**Card 11 — Trailing risk a fondo** *(ejercicio aleatorio aplica aquí)*
- Concepto: el máximo de pérdida "sigue" a las ganancias hasta cierto punto, luego se congela.
- Ejemplo Atmos Instant/NOVA: trailing 6-8%, se bloquea en el valor inicial de la cuenta una vez alcanzado el umbral (ej. +10% → el piso de $10k queda fijo).

**Card 12 — Riesgo por operación (a partir del riesgo diario)**
- Concepto: dividir el riesgo diario máximo en porciones por operación.
- Ejemplo: $300/día ÷ 6 = $50/operación, o ÷ 8 = $37.5/operación.

**Card 13 — Regla de consistencia** *(card ancla — lleva a la Calculadora)*
- Concepto: ninguna firm la calcula igual — distintas fórmulas, mismo nombre.
- Ejemplo Atmos Instant Funding (20%): mejor día define el piso del objetivo de cobro, no un techo sobre el total.
- Aviso explícito: en otras firms (FTMO Best Day Rule, FundingPips On-Demand, The5%ers) la misma palabra significa un cálculo distinto — "revisa la fórmula exacta en la FAQ de tu firm".

**Card 14 — Calculadora de riesgo diario y consistencia** *(herramienta interactiva)*
- Inputs: 1) % de consistencia a aplicar, 2) riesgo máximo diario, 3) cantidad de porciones, 4) selector de RR (1:2 a 1:6).
- Output: riesgo por operación, ganancia en día perfecto, objetivo de cobro resultante según el % de consistencia.
- Nota aclaratoria: el RR no tiene que ser el mismo todos los días — lo que importa es acercarse a la meta acumulada.

**Card 15 — Ventana de noticias fundamentales**
- Concepto: restricción de operar X minutos antes/después de noticias de alto impacto — varía si aplica en evaluación, en fondeada, o en ambas.
- Dónde revisarlas: calendario económico (ForexFactory u equivalente — a confirmar cuál usa Johnny).

**Card 16 — Ganancia requerida para aprobar**
- Concepto: % objetivo de ganancia por fase para pasar la evaluación.

**Card 17 — Mínimo de días operados**
- Concepto: algunas firms exigen un número mínimo de días con operación, aunque ya hayas alcanzado el objetivo de ganancia antes.

**Card 18 — Otras reglas a vigilar (mención breve, sin profundizar)**
- EAs/bots, copy trading, hedging entre cuentas — nombradas como "otra categoría a revisar en la FAQ", sin desarrollo extenso.

---

## Fase 4 — Práctica

**Card 19+ — Ejercicios aleatorios** *(aplican en los conceptos marcados arriba)*
- Patrón: "Tu cuenta es de $X, el riesgo máximo es Y%, ¿cuál es el valor máximo de pérdida en dólares?"
- Parámetros (tamaño de cuenta, %) se randomizan cada vez que el deck llega a esa card — no en cada carga de página, sino en cada tránsito del `goTo()` hacia esa posición.
- Candidatas confirmadas para llevar ejercicio: riesgo diario (Card 9), trailing risk (Card 11), riesgo por operación (Card 12). Las demás quedan como explicación sin ejercicio — a confirmar si Johnny quiere sumar alguna más.

---

## Fase 5 — Cierre

**Card final — Cierre**
- Mensaje de cierre, sin botón de WhatsApp con número embebido.

---

## Pendientes antes de construir

1. Links de FAQ de las 6 empresas (Johnny los va a pegar).
2. Confirmar fuente de calendario de noticias fundamentales que recomienda Johnny.
3. Confirmar si alguna card adicional de la Fase 3 amerita ejercicio aleatorio.

## Decisión cerrada: sin card de "pregunta + reveal por WhatsApp"

El tipo de card "pregunta conceptual + reveal de respuesta" definido en la spec original queda **descartado**. La única interactividad real de la página son los Ejercicios aleatorios (Card 9, 11, 12) y la Calculadora (Card 14) — ambos con inputs y cálculo en vivo dentro de la página. Las preguntas por WhatsApp en vivo siguen siendo parte de la dinámica de la capacitación tal como la da Johnny, pero no requieren ninguna card ni mecanismo dedicado dentro del HTML.
