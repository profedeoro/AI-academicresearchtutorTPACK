# Research Specification: Ecosistema IA como Tutor Virtual en Formación Investigativa

## Título Completo
Diseño y validación de un ecosistema de formación investigativa mediado por la interacción estudiante-IA-docente desde el enfoque AI-TPACK en el Programa de Maestría en Innovación Educativa del Politécnico Grancolombiano

---

## Pregunta de Investigación
¿Cómo diseñar y validar un ecosistema de formación investigativa mediado por inteligencia artificial que, fundamentado en el modelo AI-TPACK y articulado con la tríada estudiante-IA-docente, fortalezca las competencias investigativas y reduzca la sobrecarga de acompañamiento docente en la Maestría en Innovación Educativa del Politécnico Grancolombiano?

---

## Motivación

### Problema central
La masificación del posgrado ha desbordado la capacidad de asesoría personalizada. En la Maestría en Innovación Educativa del Politécnico Grancolombiano, el incremento sostenido de matrícula genera un círculo vicioso: sobrecarga docente → retroalimentación insuficiente → avances fragmentados de baja calidad → mayor carga de correcciones en etapas finales → afectación de tasas de graduación y calidad de productos investigativos.

### Factores estructurales
- **Sobrecarga docente:** La relación estudiante-asesor excede la capacidad efectiva de acompañamiento (De Kleijn et al., 2012; Lee, 2008; Pyhältö et al., 2015)
- **Baja competencia investigativa:** Dificultades en formulación de problemas, manejo de literatura y escritura académica (Carlino, 2013; Kamler & Thomson, 2014)
- **Contexto latinoamericano:** Las competencias de escritura y alfabetización académica no se desarrollan sistemáticamente en los planes de estudio (Carlino, 2013; Moreno et al., 2024)
- **Tendencia internacional:** La OCDE y UNESCO señalan la necesidad de integrar tecnologías digitales para promover autonomía investigativa (OECD, 2021; UNESCO, 2021)

### Relevancia teórica
No existe en la literatura un ecosistema articulado que integre IA como tutor con fundamentación pedagógica (AI-TPACK) dentro del proceso de formación investigativa en posgrado. Los tres elementos — pedagogía, herramientas IA, acompañamiento investigativo — existen por separado, pero no integrados ni validados como sistema.

---

## Hipótesis
Un ecosistema de formación investigativa mediado por IA, diseñado desde el enfoque AI-TPACK y articulado con la tríada estudiante-IA-docente, mejorará la calidad de los avances de trabajo de grado presentados por los estudiantes y reducirá la carga de correcciones repetitivas para los docentes asesores, comparado con el modelo de acompañamiento tradicional.

---

## Marco Teórico: AI-TPACK

### Reconfiguración del modelo TPACK
El enfoque AI-TPACK no es una extensión superficial del TPACK (Mishra & Koehler, 2006) donde la IA simplemente reemplaza el componente tecnológico. Es una **reconfiguración profunda** donde la IA adquiere agencia pedagógica diferenciada como tercer actor en la relación formativa:

| Actor | Rol en la tríada | Funciones diferenciadas |
|-------|------------------|------------------------|
| **Estudiante** | Sujeto en formación | Desarrolla competencias investigativas con apoyo del tutor IA; mantiene autonomía y responsabilidad sobre su proceso |
| **Tutor IA** | Tercer actor pedagógico | Orientación metodológica, retroalimentación inmediata, apoyo en escritura y estructura argumentativa; no sustituye al docente |
| **Docente** | Asesor experto | Se concentra en aspectos complejos y formativos; supervisión del proceso; validación de calidad; reducción de carga rutinaria |

### Principio fundamental
La IA no es una herramienta que el estudiante "usa" — es un actor con funciones pedagógicas propias, fundamentadas en las intersecciones del modelo TPACK, que media y enriquece la relación formativa sin sustituir el juicio experto del docente.

---

## Estrategia Empírica

### Tipo de estudio
**Diseño y validación** — no cuasiexperimental. El estudio se centra en diseñar el ecosistema con fundamentación pedagógica y validar su pertinencia y funcionalidad.

### Fases completadas
1. **Encuesta de percepción docente** (realizada): Encuesta a docentes de pregrado y posgrado sobre la percepción del ecosistema IA como herramienta de apoyo. Resultados alentadores y positivos.
2. **Validación por juicio de expertos** (realizada): Instrumento tipo Likert evaluado por expertos.

### Fase pendiente
3. **Prueba piloto**: Implementación del ecosistema con estudiantes y docentes de la Maestría en Innovación Educativa.

#### Diseño de la prueba piloto

**Muestra:** 15-20 estudiantes de la Maestría en Innovación Educativa en proceso de trabajo de grado. Tamaño consistente con estándares de pruebas piloto en Design-Based Research y validación de tecnología educativa (Reeves, 2006; McKenney & Reeves, 2012).

**Duración total del proyecto:** 1 año

| Fase | Meses | Actividades |
|------|-------|-------------|
| Preparación | 1-3 | Protocolos, instrumentos, onboarding de estudiantes y docentes |
| Implementación | 4-8 | Uso del ecosistema durante 1 semestre académico |
| Análisis y redacción | 9-12 | Análisis de datos, redacción de resultados |

#### Tareas del ecosistema mapeadas a AI-TPACK

El ecosistema clo-author es el artefacto tecnopedagógico. Sus comandos constituyen las funcionalidades que se validan, cada una con justificación pedagógica en el modelo AI-TPACK:

| Fase investigativa | Comando | Dimensión AI-TPACK | Función del tutor IA |
|---|---|---|---|
| Definición del problema | `/discover interview` | **PCK** (Pedagogía + Contenido) | Guiar al estudiante a formalizar su idea de investigación mediante entrevista estructurada |
| Revisión de literatura | `/discover lit` | **TCK** (Tecnología + Contenido) | Búsqueda y síntesis bibliográfica sobre bases rigurosas (Scopus, WoS, ERIC, Redalyc, SciELO) mediante sistema RAG. Incluye 11 submodos estructurados (ver detalle abajo) |
| Exploración de datos | `/discover data` | **TCK** | Identificar y evaluar fuentes de datos pertinentes con criterios de factibilidad |
| Estrategia empírica | `/strategize` | **AI-TPACK** (intersección total) | Diseño metodológico con validación integrada por agente crítico |
| Análisis de datos | `/analyze` | **TPK** (Tecnología + Pedagogía) | Ejecución guiada de análisis con retroalimentación formativa |
| Escritura académica | `/write` | **PCK** (Pedagogía + Contenido) | Redacción con protocolo anti-hedging, humanización y estándares de escritura científica |
| Revisión por pares simulada | `/review` | **AI-TPACK** (intersección total) | Simulación de proceso editorial como formación en estándares de publicación académica |
| Presentación académica | `/talk` | **TPK** (Tecnología + Pedagogía) | Estructuración de comunicación académica para seminarios y defensas |

**Principio:** Cada comando tiene una justificación pedagógica dentro del modelo AI-TPACK — no es "el estudiante usa IA", es "el tutor IA ejerce una función formativa específica en cada fase del proceso investigativo".

#### Submodos de `/discover lit` — Revisión de literatura estructurada

El comando `/discover lit` se enriquece con 11 submodos que guían al estudiante a través de una revisión bibliográfica integral, cada uno con fundamentación pedagógica en el modelo AI-TPACK.

**Infraestructura base: Sistema RAG sobre bases académicas rigurosas**

Todos los submodos se alimentan de un sistema de Retrieval-Augmented Generation (RAG) que consulta exclusivamente fuentes académicas verificadas. Esta es la capa tecnológica esencial sin la cual los submodos no pueden operar:

| Base de datos | Cobertura | Prioridad | Función en el ecosistema |
|---|---|---|---|
| **Scopus** (Elsevier) | Multidisciplinar, 27k+ journals | Alta | Búsqueda de literatura, bibliometría, factor de impacto |
| **Web of Science** (Clarivate) | Multidisciplinar, alto impacto | Alta | Validación de calidad, redes de citación |
| **ERIC** (US Dept. of Education) | Educación especializada | Alta | Fuente primaria para temas educativos |
| **Redalyc** | Latinoamérica, ciencias sociales | Alta | Investigación regional en español/portugués |
| **SciELO** | Latinoamérica, acceso abierto | Alta | Contexto latinoamericano, acceso a texto completo |
| **Semantic Scholar** (AI2) | IA-powered, open access | Media | API para RAG automatizado, extracción de metadatos |
| **OpenAlex** | Open scholarly metadata | Media | API libre para metadatos bibliográficos |
| **Google Scholar** | Amplia cobertura | Media | Búsqueda complementaria, grey literature |
| **Dialnet** | España e Iberoamérica | Media | Revistas en español |
| **DOAJ** | Open access verificado | Media | Acceso a texto completo verificado |

**Principio fundamental:** El tutor IA nunca genera referencias inventadas. Todo resultado bibliográfico debe ser trazable a una fuente verificable en estas bases. Las APIs de estas bases constituyen la columna vertebral tecnológica del ecosistema para la obtención de manuscritos académicos rigurosos.

**Dimensión AI-TPACK:** TCK (Tecnología + Contenido) — la tecnología RAG al servicio del acceso a contenido investigativo de calidad.

---

**Submodos centrales:**

| Submodo | Qué entrega al estudiante | Dimensión AI-TPACK |
|---|---|---|
| `/discover lit estado` | Síntesis del estado del arte: qué se ha investigado, autores clave, hallazgos principales, métodos utilizados | **TCK** (Tecnología + Contenido) |
| `/discover lit oportunidad` | Oportunidades de investigación identificadas a partir de tendencias y limitaciones del campo | **PCK** (Pedagogía + Contenido) |
| `/discover lit riesgo` | Riesgos principales del tema: amenazas a la viabilidad, limitaciones metodológicas recurrentes, controversias no resueltas | **PCK** (Pedagogía + Contenido) |
| `/discover lit vacio` | Vacíos de investigación documentados: qué falta, qué no se ha estudiado, qué poblaciones/contextos están sub-representados | **TCK** (Tecnología + Contenido) |
| `/discover lit etica` | Consideraciones éticas específicas del tema investigado: dilemas, marcos normativos, antecedentes de controversias éticas en el campo | **PCK** (Pedagogía + Contenido) |

**Submodos complementarios:**

| Submodo | Qué entrega al estudiante | Dimensión AI-TPACK | Justificación pedagógica |
|---|---|---|---|
| `/discover lit marco` | Mapeo de teorías y modelos teóricos relevantes: cuáles se han usado, cómo se relacionan, cuál es el más pertinente | **CK** (Contenido) | Los estudiantes de maestría frecuentemente tienen dificultad para identificar y articular su marco teórico (Kamler & Thomson, 2014) |
| `/discover lit debates` | Controversias y tensiones activas: posturas enfrentadas, autores en cada posición, argumentos centrales | **PCK** (Pedagogía + Contenido) | Posicionar la investigación dentro de un debate fortalece la contribución y demuestra dominio del campo |
| `/discover lit metodologia` | Tendencias metodológicas: qué métodos se han usado, cuáles dominan, cuáles emergen, limitaciones reportadas | **TCK** (Tecnología + Contenido) | Ayuda al estudiante a justificar su elección metodológica con evidencia del campo |
| `/discover lit bibliometria` | Análisis bibliométrico: volumen de publicaciones por año, revistas más productivas, redes de coautoría, palabras clave emergentes | **TK** (Tecnología) | Visión cuantitativa del campo que complementa la lectura cualitativa |
| `/discover lit contexto` | Contextualización regional: qué se ha investigado en Latinoamérica vs. contexto global, brechas de representación geográfica | **PCK** (Pedagogía + Contenido) | Fundamental para investigadores en contexto latinoamericano — posiciona la contribución regionalmente |

**Submodo integrador:**

| Submodo | Qué entrega al estudiante | Dimensión AI-TPACK |
|---|---|---|
| `/discover lit sintesis` | Documento integrador que articula todos los submodos en una narrativa coherente: estado del arte → vacíos → oportunidad → marco teórico → posicionamiento de la investigación del estudiante | **AI-TPACK** (intersección total) |

**Secuencia recomendada para el estudiante:**
1. `estado` → entender qué existe
2. `marco` → identificar fundamentos teóricos
3. `metodologia` → conocer cómo se ha investigado el tema
4. `bibliometria` → ver el panorama cuantitativo del campo
5. `contexto` → situar en Latinoamérica
6. `vacio` → identificar qué falta
7. `oportunidad` → encontrar dónde contribuir
8. `riesgo` → anticipar amenazas
9. `debates` → posicionarse en controversias
10. `etica` → evaluar implicaciones éticas del tema
11. `sintesis` → integrar todo en narrativa coherente

**Nota:** El tutor IA guía al estudiante a través de esta secuencia de manera progresiva. Cada submodo construye sobre los anteriores, generando una revisión bibliográfica estructurada y fundamentada que eleva la calidad del trabajo antes de llegar al docente asesor.

#### Versiones diferenciadas del ecosistema por rol

El ecosistema tiene dos versiones con funcionalidades diferenciadas según el rol en la tríada AI-TPACK:

**Versión Estudiante — Tutor IA como acompañante investigativo**

| Comando | Disponible | Función formativa |
|---|---|---|
| `/discover interview` | Si | Formalizar idea de investigación |
| `/discover lit` | Si | Búsqueda y síntesis bibliográfica |
| `/discover data` | Si | Exploración de fuentes de datos |
| `/strategize` | Si | Diseño metodológico guiado |
| `/analyze` | Si | Análisis de datos con retroalimentación |
| `/write` | Si | Escritura académica con estándares |
| `/talk` | Si | Preparación de presentaciones |
| `/review` | No | Exclusiva docente |
| `/review --peer` | No | Exclusiva docente |
| `/submit` | No | Exclusiva docente |

**Versión Docente — Ecosistema completo + funcionalidades de supervisión**

Incluye todos los comandos del estudiante más las funcionalidades exclusivas de supervisión, cada una con fundamentación científica:

**1. Dashboard de seguimiento**
- **Base teórica:** Learning Analytics (Siemens & Long, 2011; Ferguson, 2012) — uso de datos sobre el aprendiz para optimizar el proceso formativo
- **Complemento:** La frecuencia y calidad del monitoreo predice el éxito del estudiante en supervisión de tesis (De Kleijn et al., 2012; Pyhältö et al., 2015)
- **Qué muestra:** Progreso por fase investigativa, frecuencia de uso, alertas de inactividad, hitos completados
- **Dimensión AI-TPACK:** TPK — monitoreo pedagógico mediado por tecnología

**2. Comparación de versiones**
- **Base teórica:** Evaluación formativa y feedback progresivo (Black & Wiliam, 1998; Hattie & Timperley, 2007) — el aprendizaje se evidencia en la trayectoria, no en un producto aislado
- **Complemento:** Escritura como proceso — la revisión iterativa como mecanismo de aprendizaje (Flower & Hayes, 1981; Carlino, 2013)
- **Qué muestra:** Cambios entre versiones de cada sección, mejoras en estructura argumentativa, evolución de la formulación del problema
- **Dimensión AI-TPACK:** PCK — evaluar progreso en competencias investigativas

**3. Retroalimentación asistida por IA**
- **Base teórica:** Modelo de feedback efectivo de Hattie & Timperley (2007) — el feedback debe responder: ¿hacia dónde voy? (feed up), ¿cómo voy? (feed back), ¿qué sigue? (feed forward)
- **Complemento:** Scaffolding (Vygotsky, 1978; Wood, Bruner & Ross, 1976) — andamiaje adaptativo que el docente puede refinar
- **Complemento:** Tutoría inteligente (VanLehn, 2011) — tutores que combinan retroalimentación inmediata con supervisión humana logran efectos cercanos a la tutoría 1:1
- **Qué sugiere al docente:** Puntos críticos del trabajo, debilidades metodológicas, inconsistencias argumentativas, sugerencias priorizadas por severidad
- **Dimensión AI-TPACK:** AI-TPACK (intersección total) — la IA asiste al docente, no solo al estudiante

**4. Rúbrica automatizada**
- **Base teórica:** Evaluación criterial y rúbricas analíticas (Jonsson & Svingby, 2007; Panadero & Jonsson, 2013) — mejoran consistencia y transparencia de la evaluación
- **Complemento:** Alineamiento constructivo (Biggs & Tang, 2011) — criterios de evaluación alineados con resultados de aprendizaje esperados
- **Referente tecnológico:** Automated Essay Scoring (Shermis & Burstein, 2013), adaptado a evaluación de competencias investigativas
- **Qué evalúa:** Coherencia metodológica, calidad de revisión de literatura, solidez de formulación del problema, calidad de escritura académica
- **Dimensión AI-TPACK:** TCK — tecnología al servicio de la evaluación de contenido
- **Principio:** La rúbrica automatizada es una evaluación preliminar que el docente valida, modifica o rechaza — nunca es la evaluación final

**5. Reporte de uso del ecosistema**
- **Base teórica:** Learning Analytics y analítica académica (Siemens & Long, 2011; Gašević, Dawson & Siemens, 2015) — patrones de interacción como indicadores de engagement y autorregulación
- **Complemento:** Autorregulación del aprendizaje (Zimmerman, 2002; Pintrich, 2000) — frecuencia y tipo de uso refleja estrategias de autorregulación
- **Qué reporta:** Frecuencia por comando, patrones temporales (uso constante vs. concentrado antes de entregas), evolución del uso a lo largo del semestre
- **Dimensión AI-TPACK:** TPK — analytics para decisiones pedagógicas
- **Aplicación:** Identificar estudiantes en riesgo (baja interacción) y patrones de uso superficial vs. profundo para intervención diferenciada

#### Indicadores de éxito y medición

| Indicador | Tipo | Instrumento | Rol en el estudio |
|---|---|---|---|
| **Percepción docente** sobre reducción de carga | Cualitativo + Likert | Encuesta + entrevista semi-estructurada | **Principal** — más viable y más rico para validación |
| **Percepción estudiantil** sobre mejora de competencias | Cualitativo + Likert | Encuesta + entrevista semi-estructurada | **Principal** — evidencia desde el usuario directo |
| **Número de ciclos de corrección** por entrega | Cuantitativo descriptivo | Registro por el docente (antes/después de cada avance) | **Secundario** — evidencia complementaria observable |
| **Tiempo de retroalimentación** por revisión | Cuantitativo descriptivo | Auto-registro docente (minutos por revisión) | **Terciario** — útil pero difícil de controlar con rigor |

**Nota metodológica:** En un estudio de diseño y validación, la percepción es el indicador más fuerte. Los indicadores cuantitativos son complementarios y descriptivos — no se busca inferencia estadística, sino evidencia de que el ecosistema funciona según su diseño.

---

## Datos

### Fuentes de datos contempladas
| Fuente | Tipo | Fase | Estado |
|--------|------|------|--------|
| Encuesta de percepción docente (pregrado y posgrado) | Survey / Likert | Diagnóstico | Completada — resultados positivos |
| Instrumento de validación por juicio de expertos | Likert | Validación | Completada |
| Percepción de estudiantes (prueba piloto) | Encuesta Likert + entrevista semi-estructurada | Piloto | Pendiente |
| Percepción de docentes (prueba piloto) | Encuesta Likert + entrevista semi-estructurada | Piloto | Pendiente |
| Registro de ciclos de corrección por entrega | Cuantitativo descriptivo (registro docente) | Piloto | Pendiente |
| Tiempo de retroalimentación por revisión | Cuantitativo descriptivo (auto-registro docente) | Piloto | Pendiente |

### Contexto institucional
- **Institución:** Politécnico Grancolombiano
- **Programa:** Maestría en Innovación Educativa (3 semestres, modalidad virtual)
- **Muestra piloto:** 15-20 estudiantes de semestre 1 + sus docentes asesores
- **Duración:** 1 año (preparación 3 meses + implementación 5 meses + análisis 4 meses)

### Criterios de selección de participantes

**Estudiantes — criterios de inclusión:**
- Matriculados en semestre 1 de la Maestría en Innovación Educativa
- Cursando las materias Investigación de la Innovación Educativa y/o Seminario 1
- Consentimiento informado firmado

**Docentes — criterios de inclusión:**
- Asesores de trabajo de grado asignados a los estudiantes participantes
- Disposición a recibir capacitación completa del ecosistema (versión docente)

### Protocolo de onboarding

**Modalidad:** Virtual (consistente con la modalidad de la maestría)

**Estudiantes:**
- Capacitación pedagógica del ecosistema IA (versión estudiante)
- Énfasis en el fundamento AI-TPACK: el tutor IA como actor pedagógico, no como generador de contenido
- Acceso restringido a la versión para estudiantes

**Docentes:**
- Capacitación completa del ecosistema (versión docente con todas las funcionalidades)
- Formación en el marco AI-TPACK como fundamento de la integración tecnológica
- Capacitación en las 5 funcionalidades exclusivas de supervisión (dashboard, comparación de versiones, retroalimentación asistida, rúbrica automatizada, reporte de uso)

---

## Resultados Esperados
1. Los avances de trabajo de grado presentados por estudiantes que usan el ecosistema IA llegarán con mayor calidad al docente, reduciendo ciclos de correcciones repetitivas
2. Los docentes percibirán una reducción significativa en la carga de acompañamiento rutinario
3. Los estudiantes reportarán mejora en sus habilidades investigativas (formulación de problemas, revisión de literatura, escritura académica)
4. El ecosistema será valorado positivamente como herramienta con integración pedagógica fundamentada en AI-TPACK

---

## Contribución
La investigación llena un vacío identificado en la revisión bibliográfica: **la integración articulada entre pedagogía, herramientas de IA y procesos de acompañamiento investigativo como ecosistema**. Mientras existen estudios sobre cada componente por separado, no se ha documentado ni validado un sistema que los integre bajo un marco teórico coherente (AI-TPACK) en el contexto de formación investigativa en posgrado, particularmente en Latinoamérica.

---

## Preguntas Abiertas (resueltas y pendientes)

### Resueltas en esta sesión
- ~~Escala de la prueba piloto~~ → 15-20 estudiantes de semestre 1, 1 año de duración
- ~~Tareas específicas del ecosistema~~ → Comandos clo-author mapeados a dimensiones AI-TPACK
- ~~Métricas de reducción de carga~~ → Percepción (principal) + ciclos de corrección + tiempo de retroalimentación
- ~~Componentes del ecosistema IA~~ → 8 comandos estudiantiles + 5 funcionalidades exclusivas docentes
- ~~Versiones diferenciadas~~ → Versión estudiante (7 comandos) + versión docente (completa + supervisión)
- ~~Funcionalidades docentes con fundamento científico~~ → Dashboard, comparación de versiones, retroalimentación asistida, rúbrica automatizada, reporte de uso
- ~~Criterios de selección~~ → Semestre 1, materias Investigación de la Innovación Educativa y Seminario 1
- ~~Protocolo de onboarding~~ → Virtual, diferenciado por rol, fundamentado en AI-TPACK

### Pendientes
1. **Instrumentos de la prueba piloto:** Diseñar/adaptar encuestas Likert y guiones de entrevista semi-estructurada para estudiantes y docentes (se parte del instrumento de percepción docente ya existente)
2. **Protocolo de registro docente:** Diseñar formato para registro de ciclos de corrección y tiempo de retroalimentación
3. **Consideraciones éticas:** Protocolo de consentimiento informado, manejo de datos, integridad académica
