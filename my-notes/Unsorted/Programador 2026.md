Este video ofrece un panorama de cómo ha evolucionado la programación con la integración de la **Inteligencia Artificial (IA)** hasta 2026, destacando que el uso de solo _VS Code_ y _ChatGPT_ ya es obsoleto (0:00). El creador del contenido proporciona un mapa de herramientas y conceptos esenciales para los programadores modernos, diferenciando claramente el desarrollo profesional de la IA del "vibe coding" o desarrollo sin conocimientos técnicos (0:46).

Aquí tienes un resumen detallado de los puntos clave del video:

**1. Evolución del Entorno de Desarrollo (2:11-4:29)**

- **Desarrollo típico tradicional:** Se basaba en editores de código como _Visual Studio Code_, donde el programador escribía, ejecutaba y generaba aplicaciones manualmente (2:20).
- **Autocompletado inteligente:** La primera gran innovación, ejemplificada por _GitHub Copilot_, que permitía autocompletar bloques de código (2:57). Otras alternativas incluyeron _Tabnine_, _AWS CodeWhisperer_ y _Supermaven_ (3:23). Aunque útil, ya no es la característica principal (3:45).
- **Integración de Chats (ChatGPT):** La llegada de _ChatGPT_ permitió a los programadores copiar y pegar código, lo que se consideraba moderno en su momento. Inicialmente, se usaba de forma separada de _VS Code_, pero luego surgieron plugins que lo integraban al editor (3:50).

**2. Editores de Código con IA (4:31-12:22)** La evolución real comenzó con los _forks_ (versiones derivadas) de _VS Code_ que integraban IA de forma nativa:

- _**Cursor:**_ Un editor popular que controla completamente el editor, ejecutando comandos, reescribiendo, editando y eliminando archivos (4:50).
- _**Winsor:**_ Competidor directo de _Cursor_, también un _fork_ privativo de _VS Code_ con ideas similares de agentes inteligentes (6:33).
- _**Trae:**_ Desarrollado por _ByteDance_ (creadores de TikTok), permite a la IA hacer todo el trabajo mientras el programador solo observa (modo "solo") (7:17).
- _**Kiro:**_ De _AWS_ (Amazon), enfocado en la planificación extensa del proyecto por parte de la IA antes de la codificación (7:37).
- _**Zed:**_ Un editor creado desde cero en _Rust_, conocido por su velocidad y eficiencia, sin ser un _fork_ de _VS Code_, pero con funciones de IA similares (8:17).
- _**Antigravity:**_ Desarrollado por _Google_, utiliza sus modelos _Gemini_ y es un competidor directo de _Cursor_, ofreciendo un plan gratuito con muchos tokens (11:15). Este editor surgió de la contratación del equipo principal de _Winsor_ por parte de _Google_ (12:02).

**3. Modelos de IA Subyacentes (9:11-13:07)** Estos editores dependen de modelos de IA robustos:

- _**GPT Codex:**_ Modelo de _OpenAI_ utilizado por _GitHub Copilot_ (9:32).
- _**Claude Sonnet:**_ Modelo de _Anthropic_, considerado el mejor para escribir código en cualquier lenguaje (10:14, 13:30).
- _**Gemini:**_ Modelo de _Google_, con variaciones específicas para código (10:32).
- _**Grok:**_ Modelo de _X_ (10:38).

**4. Herramientas de Terminal con IA (TUI) (13:08-19:59)** Más allá de las interfaces gráficas (GUI), existen herramientas de línea de comandos (TUI):

- _**Claude Code:**_ Herramienta de consola de _Anthropic_ que interactúa directamente con el modelo _Claude Sonnet_, permitiendo a la IA acceder a programas, escribir y generar código (14:44).
- _**Gemini CLI:**_ La herramienta TUI de _Google_ que utiliza _Gemini_ (15:19).
- _**Codex (herramienta de terminal):**_ La herramienta de terminal de _OpenAI_ que compite con _Claude Code_ (15:33).
- _**Open Code:**_ Proyecto abierto alternativo a las herramientas de terminal empresariales (15:54).

**5. Terminales Modernas con IA (17:12-19:59)** Para ejecutar estos programas de terminal, existen terminales avanzadas:

- _**Warp:**_ Terminal desarrollada con código nativo que integra modelos de IA, permite múltiples sesiones y es muy rápida (17:29).
- _**Kitty, Alacrity, WezTerm:**_ Emuladores de terminal _open source_, altamente configurables y con soporte para GPU (18:40).
- _**Ghostty:**_ Proyecto _open source_ escrito en C, altamente configurable y con excelente rendimiento (19:06).

**6. Protocolos y Estándares (20:10-28:22)** Más allá de las herramientas específicas, hay técnicas y protocolos compartidos:

- _**MCP (Model Context Protocol):**_ Permite a la IA comunicarse con servicios externos como bases de datos (_PostgreSQL_), _Google Drive_, _Slack_, _Gmail_, _Notion_ y cualquier servicio con API (20:30-22:18). Existen MCPs para _Stripe_, _Vercel_, _Sentry_, _N8N_, entre otros (22:45).
    - _**Context.js:**_ Un MCP que ayuda a la IA a obtener código moderno, evitando que la IA tenga que buscar e interpretar documentación por sí misma (23:26).
    - _**Playwright / Chrome DevTools:**_ MCPs que permiten a la IA manipular el navegador automáticamente (24:34).
- **Extensión de Agentes (Skills, Plugins, Hooks):** Permiten añadir más funcionalidades a los agentes de IA.
    - **Skills (en _Claude Code_):** Son _mark downs_ que agrupan instrucciones específicas para que la IA genere respuestas o código en un formato deseado (26:12). Un ejemplo es _Cloud Design Engineer_, que ayuda a la IA a generar mejores interfaces (26:50).

**7. Convenciones y Archivos de Configuración (28:23-32:27)** Para que los agentes de IA funcionen de manera óptima, leen archivos de configuración:

- _**cloud.md / gemini.md / agent.md:**_ Archivos específicos de cada agente (o editor) que proporcionan contexto e instrucciones iniciales para la IA, como reglas para crear rutas _backend_ o _frontend_ (28:47).
- _**agents.md:**_ Una propuesta de estándar para tener un único archivo que múltiples editores y herramientas de IA puedan leer, simplificando la configuración entre diferentes herramientas (30:27).
- _**lls.txt:**_ Una propuesta de archivo _txt_ similar a _robots.txt_ o _sitemap_, que resume lo que hace cada página web en un formato amigable para que las IAs entiendan el contenido sin tener que leer el HTML (31:27).