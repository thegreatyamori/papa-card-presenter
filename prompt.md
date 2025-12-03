## SISTEMA DE GENERACIÓN DE PREGUNTAS P.A.P.A.

### CONTEXTO DEL JUEGO

El juego **P.A.P.A. (Preguntas Absurdas Para hacer a tus Amigos)** es un party game para grupos donde:

- El grupo responde EN SECRETO una pregunta absurda
- Una persona adivina CUÁL fue la pregunta que respondieron los demas
- El desafío es que varias preguntas elicitan respuestas SIMILARES pero sobre temas distintos

### OBJETIVO DE ESTE PROMPT

Generar **100 preguntas** absurdas pero realizables que generen respuestas concretas y específicas. Las preguntas de una misma categoría deben provocar respuestas similares en naturaleza, pero sobre temáticas diferentes para crear ambigüedad.

### CRITERIOS ESENCIALES PARA LAS PREGUNTAS

**✓ CORRECTO:**

- Preguntas que generan respuestas ESPECÍFICAS y CONCRETAS (números, objetos, situaciones reales)
- Varias preguntas con respuestas que se superponen (ej: "¿Qué haces en un atasco?" → "Dormir" / "¿Qué haces en una reunión aburrida?" → "Dormir")
- Tono absurdo pero sensato (alguien realmente podría responder eso)
- Preguntas abiertas que permiten múltiples respuestas válidas
- Las respuestas a las preguntas podrian provocar risas

**✗ EVITAR:**

- Preguntas cerradas (Sí/No)
- Humor ofensivo, burlarse de grupos, contenido inapropiado
- Respuestas genéricas o abstractas sin soporte real
- Preguntas donde todos darían la misma respuesta
- Preguntas que nadie podría responder realistamente

### CATEGORÍAS Y ENFOQUE

1. **Superpoderes ridículos**: Habilidades mágicas/imposibles aplicadas a situaciones cotidianas
2. **Viajes en el tiempo**: Interacciones anacrónistas con momentos/épocas
3. **Habilidades inútiles**: Destrezas sin valor práctico pero realizables
4. **Supermercado**: Situaciones y decisiones específicas de compras/compra
5. **Animales**: Interacciones o atributos de animales en contextos humanos
6. **Supervivencia**: Situaciones, objetos, animales en lugares como bosques, islas, desiertos, mar abierto

### EJEMPLOS DE REFERENCIA (MODELO A SEGUIR)

**BUENOS EJEMPLOS:**

- ¿Qué objeto cotidiano detestas que haga ruido? → Respuestas concretas: timador, aspiradora, grifo, despertador
- ¿Qué le preguntarías a tu yo de hace veinte años? → Respuestas específicas: sobre carreras, relaciones, dinero
- ¿Qué haces cuando esperas en una cola larga? → Respuestas similares entre preguntas distintas

**PATRÓN DESEADO:**

- Pregunta A (Categoría 1) → Respuesta: "El televisor"
- Pregunta B (Categoría 2) → Respuesta: "El televisor" (pero el contexto de la pregunta es totalmente diferente)

### FORMATO DE SALIDA

Cada pregunta debe tener:

- `id`: número secuencial (1-100)
- `categoria`: una de las 5 categorías listadas
- `pregunta`: texto de la pregunta dentro de comillas dobles (máx 100 caracteres, específica y concreta)
