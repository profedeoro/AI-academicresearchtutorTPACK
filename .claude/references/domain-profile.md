# Domain Profile

## Field

**Primary:** Innovación Educativa — Tecnología Educativa e Inteligencia Artificial en Educación Superior
**Adjacent subfields:** Educación Superior, Competencias Investigativas, Tutoría Virtual, Learning Analytics, Diseño Instruccional, Ciencias de la Computación Educativa

---

## Target Journals (ranked by tier)

| Tier | Journals |
|------|----------|
| Top | Computers & Education, Internet and Higher Education, British Journal of Educational Technology |
| Top field | Educational Technology Research and Development (ETR&D), International Journal of AI in Education (IJAIED), Journal of Computer Assisted Learning |
| Strong field | Education and Information Technologies, Interactive Learning Environments, Journal of Educational Computing Research |
| Specialty | Revista Iberoamericana de Educación Superior, RIED (Revista Iberoamericana de Educación a Distancia), Apertura, REDIE |
| Latinoamérica | Educación XX1, Pixel-Bit, Campus Virtuales, Revista de Investigación Educativa |

---

## Common Data Sources

| Dataset | Type | Access | Notes |
|---------|------|--------|-------|
| Encuestas a estudiantes de posgrado | Primaria/survey | Recolección propia | Competencias investigativas, percepción del tutor IA |
| Registros de interacción con el ecosistema IA | Log data/analytics | Interno | Frecuencia, tipo de consultas, feedback recibido |
| Bases de datos bibliográficas (Scopus, WoS, ERIC) | Bibliométrica | Institucional | Para revisiones sistemáticas y análisis bibliométrico |
| Rúbricas de evaluación de productos investigativos | Evaluación | Recolección propia | Pre-post para medir mejora en competencias |
| Datos académicos institucionales | Admin/panel | Restringido | Rendimiento, avance en tesis, tiempo de graduación |

---

## Common Identification Strategies

| Strategy | Typical Application | Key Assumption to Defend |
|----------|-------------------|------------------------|
| Diseño cuasi-experimental pre-post con grupo control | Comparar competencias investigativas antes/después del uso del tutor IA | Equivalencia inicial entre grupos; no contaminación entre grupos |
| Mixed methods (secuencial explicativo) | Cuantificar mejora + explicar experiencias con el tutor IA | Integración coherente de hallazgos cuanti-cuali |
| Análisis de contenido de interacciones | Evaluar calidad del feedback del tutor IA | Categorización confiable (inter-rater reliability) |
| Design-Based Research (DBR) | Iteración y mejora del ecosistema IA en contexto real | Documentación rigurosa de ciclos de diseño |
| Revisión sistemática / Meta-análisis | Sintetizar evidencia sobre IA como tutor en educación superior | Protocolo PRISMA, búsqueda exhaustiva |

---

## Theoretical Foundation: AI-TPACK

**El ecosistema IA se fundamenta en el modelo AI-TPACK — una reconfiguración profunda del TPACK (Mishra & Koehler, 2006) donde la IA adquiere agencia pedagógica diferenciada como tercer actor en la relación formativa.**

AI-TPACK no es simplemente "TPACK + IA como herramienta". Es una reconfiguración epistemológica donde la IA tiene rol pedagógico propio dentro de la tríada estudiante-IA-docente:

| Actor | Rol | Funciones |
|---|---|---|
| **Estudiante** | Sujeto en formación | Desarrolla competencias investigativas con apoyo del tutor IA; mantiene autonomía |
| **Tutor IA** | Tercer actor pedagógico | Orientación, retroalimentación inmediata, apoyo en escritura y estructura argumentativa |
| **Docente** | Asesor experto | Aspectos complejos y formativos; supervisión; validación de calidad |

### Dimensiones AI-TPACK aplicadas al ecosistema

| Dimensión | Aplicación al Ecosistema IA |
|---|---|
| **TK** (Technological Knowledge) | Dominio de herramientas IA, RAG, interfaces conversacionales |
| **PK** (Pedagogical Knowledge) | Estrategias de tutoría, feedback formativo, andamiaje (scaffolding) |
| **CK** (Content Knowledge) | Metodología de investigación, redacción académica, bases de datos |
| **TPK** (Tech + Pedagogy) | Diseño de interacciones IA que promuevan aprendizaje activo |
| **TCK** (Tech + Content) | RAG sobre bases rigurosas (Scopus, WoS, ERIC) para consultas de contenido |
| **PCK** (Pedagogy + Content) | Secuenciación didáctica de competencias investigativas |
| **AI-TPACK** (intersección total) | El tutor IA integra tecnología, pedagogía y contenido como actor con agencia pedagógica propia |

**Implicación para el diseño:** Toda funcionalidad del ecosistema debe justificarse en al menos una intersección AI-TPACK. El tutor no es una herramienta que el estudiante "usa" — es un actor con funciones pedagógicas diferenciadas que media la relación formativa sin sustituir el juicio experto del docente.

---

## RAG — Bases de Datos Rigurosas

**El sistema RAG del ecosistema debe alimentarse exclusivamente de fuentes académicas verificadas:**

| Base de Datos | Cobertura | Prioridad | Uso en el Ecosistema |
|---|---|---|---|
| **Scopus** (Elsevier) | Multidisciplinar, 27k+ journals | Alta | Búsqueda de literatura, bibliometría |
| **Web of Science** (Clarivate) | Multidisciplinar, alto impacto | Alta | Validación de calidad, factor de impacto |
| **ERIC** (US Dept. of Education) | Educación especializada | Alta | Fuente primaria para temas educativos |
| **Google Scholar** | Amplia cobertura, incluye grey literature | Media | Búsqueda complementaria, citas |
| **Semantic Scholar** (AI2) | IA-powered, open access | Media | API para RAG automatizado |
| **DOAJ** | Open access verificado | Media | Acceso a texto completo |
| **Redalyc** | Latinoamérica, ciencias sociales | Alta | Investigación regional, español/portugués |
| **SciELO** | Latinoamérica, acceso abierto | Alta | Contexto latinoamericano |
| **Dialnet** | España e Iberoamérica | Media | Revistas en español |
| **OpenAlex** | Open scholarly metadata | Media | API libre para metadatos bibliográficos |

**Principio:** El tutor IA nunca debe generar referencias inventadas. Todo feedback bibliográfico debe ser trazable a una fuente verificable en estas bases.

---

## Field Conventions

- Reportar tamaños de efecto (Cohen's d, eta cuadrado) junto con significancia estadística
- **TPACK como marco teórico central** — toda intervención tecnológica debe articularse en sus dimensiones
- Triangulación de datos como criterio de rigor en investigación cualitativa
- Considerar aspectos éticos del uso de IA en educación (sesgo, privacidad, dependencia)
- Discutir implicaciones para la práctica docente y el diseño curricular
- En estudios con tecnología, describir detalladamente la intervención/herramienta
- Reportar reliability (Cronbach's alpha, ICC) de todos los instrumentos
- Marcos complementarios a TPACK: TAM (adopción), SAMR (niveles de integración), ZDP (andamiaje)

---

## Notation Conventions

| Symbol | Meaning | Anti-pattern |
|--------|---------|-------------|
| $n$ | Tamaño de muestra | No usar $N$ para subgrupos |
| $M$ ($SD$) | Media (desviación estándar) | No reportar solo la media sin dispersión |
| $d$ | Tamaño de efecto Cohen | Siempre acompañar con IC 95% |
| $\alpha$ | Nivel de significancia / Cronbach's alpha | Especificar cuál de los dos en cada contexto |

---

## Seminal References

| Paper | Why It Matters |
|-------|---------------|
| **Mishra & Koehler (2006)** | **TPACK — marco teórico central del proyecto** |
| Koehler & Mishra (2009) | Evolución y aplicación del TPACK en formación docente |
| Zawacki-Richter et al. (2019) | Revisión sistemática de IA en educación superior — mapa del campo |
| Crompton & Burke (2023) | Meta-análisis de IA en educación — efectos y tendencias |
| Luckin et al. (2016) | Intelligence Unleashed — marco para IA como tutor |
| VanLehn (2011) | Comparación tutores humanos vs. inteligentes — benchmark del campo |
| Hattie & Timperley (2007) | Marco de feedback efectivo — base para diseño del tutor |
| Bandura (1997) | Autoeficacia — marco para competencias investigativas |
| Healey & Jenkins (2009) | Research-based learning en educación superior |
| UNESCO (2023) | Guía para IA en educación — marco ético y de política |

---

## Field-Specific Referee Concerns

- "¿Qué valor agrega la IA sobre un tutor humano?" — siempre justificar la ventaja diferencial
- "¿No genera dependencia tecnológica?" — abordar riesgos de sobre-dependencia del tutor IA
- "¿Cómo se controla el sesgo de la IA en el feedback?" — discutir validación del contenido generado
- "¿Qué pasa con la equidad de acceso?" — brecha digital y acceso diferencial a tecnología
- "¿Cuál es el marco teórico?" — los revisores esperan fundamentación pedagógica sólida, no solo tecnológica
- "¿Generalización?" — resultados de un programa de posgrado no generalizan automáticamente
- "¿Efecto Hawthorne?" — estudiantes pueden mejorar por la novedad, no por la herramienta

---

## Quality Tolerance Thresholds

| Quantity | Tolerance | Rationale |
|----------|-----------|-----------|
| Tamaños de efecto | d ± 0.05 | Variabilidad entre muestras educativas |
| Reliability (α) | ≥ 0.70 | Estándar Nunnally para investigación educativa |
| Inter-rater reliability (κ) | ≥ 0.80 | Acuerdo sustancial para análisis de contenido |
| Tasas de respuesta | ≥ 60% | Umbral aceptable para encuestas educativas |
