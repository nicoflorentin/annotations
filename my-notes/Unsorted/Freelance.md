# Guía para Empezar como Freelance en Desarrollo Web/Móvil

## 1. Estrategia Inicial

### Nicho y Diferenciación
Dado tu stack (React, React Native, Tailwind, BD), especialízate en:
- **PWA (Progressive Web Apps)**: Aplicaciones que funcionen como web y móvil
- **Dashboards administrativos** para pequeñas empresas
- **Aplicaciones móviles híbridas** con React Native

### Presencia y Captación
- **Portafolio obligatorio**: 3-4 proyectos demostrativos (si no tienes reales, crea proyectos ficticios de calidad)
- 
- **LinkedIn optimizado**: No solo "programador", sino "solucionador de problemas web/móviles"
- **GitHub activo**: Repositorios públicos con código limpio y READMEs profesionales

### Precios y Facturación
- **Por proyecto**: Calcula horas estimadas × tu tarifa horaria + 30% imprevistos
- **Tarifa inicial recomendada**: USD 20-35/hora (ajustable según complejidad)
- **Facturación por hitos**: 30% al inicio, 40% al entregar versión funcional, 30% al final

---

## 2. Documentación Esencial para Clientes

### A. PROPUESTA TÉCNICA Y COMERCIAL
```
CONTRATO DE DESARROLLO DE SOFTWARE
CLIENTE: [Nombre]
DESARROLLADOR: [Tu nombre]
PROYECTO: [Nombre del proyecto]

1. ALCANCE DEL PROYECTO
   - Descripción funcional detallada
   - Tecnologías a utilizar: React, React Native, [Base de datos], Tailwind CSS
   - Entregables esperados
   - NO INCLUYE: Diseño gráfico profesional (solo implementación), hosting, mantenimiento post-entrega

2. CRONOGRAMA Y HITOS
   - Fecha de inicio: [Fecha]
   - Hito 1 (30%): Wireframes y arquitectura → [Fecha]
   - Hito 2 (40%): Versión funcional → [Fecha]
   - Hito 3 (30%): Entrega final → [Fecha]

3. INVERSIÓN Y FORMA DE PAGO
   - Total: [Monto]
   - 30% al inicio (USD XXX)
   - 40% al aprobar Hito 2 (USD XXX)
   - 30% al entregar proyecto (USD XXX)

4. MODIFICACIONES DE ALCANCE
   - Cambios menores: Ajustes sin costo hasta 5 horas acumuladas
   - Cambios mayores: Se cotizarán aparte y extenderán cronograma
   - "Scope creep" definido: Cualquier funcionalidad no descrita aquí se considera adicional
```

### B. ACUERDO DE CONFIDENCIALIDAD Y PROPIEDAD
```
DERECHOS DE PROPIEDAD INTELECTUAL

1. CÓDIGO FUENTE
   - El cliente recibe licencia perpetua para usar el código
   - El desarrollador retiene derecho a usar componentes genéricos en futuros proyectos
   - Exclusión: Funciones específicas del negocio del cliente no serán reutilizadas

2. TERCEROS Y LICENCIAS
   - Dependencias de código abierto mantienen sus licencias originales
   - Componentes premium serán cotizados aparte
   - API keys y credenciales: Responsabilidad del cliente

3. MANTENIMIENTO Y GARANTÍA
   - Período de garantía: 30 días post-entrega para corrección de bugs
   - Soporte post-garantía: Se cotizará por separado (USD XX/hora)
   - Hosting y deployment: No incluido (se proveerá guía de deploy)
```

### C. ESPECIFICACIÓN TÉCNICA DETALLADA
```
REQUERIMIENTOS TÉCNICOS

1. ARQUITECTURA
   - Frontend: React/React Native con hooks
   - Estilos: Tailwind CSS con configuración personalizada
   - Estado: Context API o Redux Toolkit (según complejidad)
   - Backend: [Firebase/Supabase/Node.js + PostgreSQL]
   - Autenticación: [Sistema elegido]

2. DESPLIEGUE (DEPLOYMENT)
   - Web: Vercel/Netlify (recomendado por simplicidad)
   - Móvil: Expo (desarrollo) → EAS Build (producción)
   - Base de datos: [Proveedor elegido]
   - Variables de entorno: El cliente debe proveer keys necesarias

3. PERFORMANCE Y SEO
   - Puntuación Lighthouse objetivo: >85 en performance
   - SEO básico implementado (meta tags, sitemap)
   - Web responsive: Mobile-first approach

4. LIMITACIONES TÉCNICAS
   - Compatibilidad: Últimas 2 versiones de navegadores principales
   - Dispositivos móviles: iOS 13+, Android 9+
   - No incluye: Integraciones con ERP/CRM personalizados
```

---

## 3. Flujo de Trabajo Profesional

### Fase 1: Descubrimiento (Sin costo, 1-2 horas)
- Reunión para entender necesidades reales
- Documento de requisitos inicial
- Propuesta preliminar

### Fase 2: Wireframes y Arquitectura
- Wireframes en Figma (gratis) o papel
- Diagrama de base de datos
- Stack tecnológico confirmado

### Fase 3: Desarrollo Iterativo
- Comunicación semanal con avances
- Repositorio Git privado (GitHub/GitLab)
- Deploy de staging para revisión

### Fase 4: Entrega y Capacitación
- Documentación técnica básica
- Video de 15 minutos explicando funcionalidades
- Guía de deploy para el cliente

---

## 4. Herramientas Gratuitas Esenciales

### Gestión de Proyectos
- **Trello**: Para roadmap visual con el cliente
- **Google Drive**: Documentación compartida
- **GitHub Projects**: Seguimiento técnico

### Desarrollo
- **Figma Community**: Plantillas gratuitas para UI
- **Vercel/Netlify**: Hosting gratuito para demos
- **Supabase**: Backend gratuito hasta cierto límite
- **Expo**: Desarrollo móvil sin costos iniciales

### Legal y Administrativo
- **Plantillas legales**: [TermsFeed](https://www.termsfeed.com/) tiene generadores básicos gratuitos
- **Facturación**: Plantillas en Google Sheets o [InvoiceSimple](https://invoicesimple.com/)

---

## 5. Preguntas Clave para el Cliente (Antes de Cotizar)

### Sobre el Proyecto
1. "¿Cuál es el objetivo principal de negocio de este proyecto?"
2. "¿Tienes ejemplos de sitios/aplicaciones que te gusten?"
3. "¿Quién será el usuario final y qué necesita hacer?"

### Sobre Contenidos
4. "¿Tienes todos los textos, imágenes y logos listos?"
5. "¿Necesitas que cree contenido o solo desarrolles lo que me proveas?"

### Técnicas
6. "¿Necesitas integración con alguna API o servicio existente?"
7. "¿Quién manejará el hosting y dominio?"
8. "¿Necesitas panel administrativo para gestionar contenido?"

---

## 6. Cómo Manejar Situaciones Comunes

### "¿Puedes hacerlo más barato?"
Respuesta: "Mi precio refleja mi expertise en [tecnología]. Puedo reducir alcance: ¿qué funcionalidades podemos postergar para una fase 2?"

### "Mi [familiar] dice que debería tener [feature compleja]"
Respuesta: "Esa funcionalidad es interesante. Según nuestra especificación, sería un adicional de [horas] horas, aproximadamente [monto extra]. ¿Quieres que la agreguemos?"

### Cliente que no provee contenido a tiempo
Documentar: "Por acuerdo, el cronograma se extiende un día por cada día de demora en recibir contenido. Actualmente, llevamos X días de retraso."

### Cambios constantes
"Este cambio está fuera del alcance original. Tengo dos opciones: 1) Lo hacemos como adicional por [monto], o 2) Cambiamos [funcionalidad existente] por esta nueva."

---

## 7. Checklist de Entrega Final

- [ ] Código en repositorio Git (acceso al cliente)
- [ ] Variables de entorno documentadas (.env.example)
- [ ] Scripts de build y deploy documentados
- [ ] Pruebas en dispositivos reales (móvil)
- [ ] Performance auditada (Lighthouse)
- [ ] Documentación básica de mantenimiento
- [ ] Factura final emitida
- [ ] Accesos transferidos (hosting, DNS si aplica)
- [ ] Período de garantía iniciado

---

## Recomendación Final

**Empieza con proyectos pequeños** (landing pages, sitios informativos) para ganar confianza y referencias. Cada proyecto exitoso te dará:
1. Caso de estudio para portafolio
2. Posible testimonio
3. Experiencia en gestión de cliente

**Invierte en tu marca personal**: Un sitio propio simple pero profesional, aunque sea con plantilla. Demuestra lo que puedes hacer para otros.

**No subestimes tu valor**: Como autodidacta con stack moderno, tienes ventaja sobre desarrolladores que solo conocen tecnologías antiguas.

Los primeros clientes serán los más difíciles, pero cada uno te preparará mejor para el siguiente. Documenta TODO, incluso las conversaciones informales por WhatsApp (guarda capturas).

¿Necesitas que profundice en algún aspecto específico?


# Respuesta de Claude

Voy a analizar la respuesta de DeepSeek y proponer mejoras significativas basándome en tu contexto específico:

## Mejoras Críticas Necesarias

### 1. **Documentos Legales Más Robustos**

La respuesta tiene plantillas básicas, pero faltan cláusulas críticas que te protegen:

**Agregar a los contratos:**

- **Cláusula de terminación anticipada**: Qué pasa si el cliente cancela a mitad de proyecto (debes retener pagos ya efectuados + compensación)
- **Límite de revisiones**: "Se incluyen hasta 3 rondas de revisión por hito. Revisiones adicionales: USD X/hora"
- **Jurisdicción y ley aplicable**: Fundamental para disputas legales
- **Penalidades por mora en pagos**: "Demoras mayores a 7 días pausan el desarrollo"
- **Backup y recuperación de datos**: Especificar responsabilidades (el cliente debe hacer sus propios backups post-entrega)

### 2. **Gestión de Expectativas sobre IA Generativa**

Dado tu requisito de **no gastar en servicios de IA**, esto es crítico:

**Agregar sección explícita:**

```
INTEGRACIÓN DE IA Y SERVICIOS EXTERNOS

1. SERVICIOS GRATUITOS vs PAGOS
   - NO INCLUYE: Integración con GPT-4, Claude API, servicios premium de IA
   - SÍ INCLUYE: IA generativa gratuita básica si es esencial (con límites)
   - Modelos self-hosted: Cotización adicional por complejidad

2. RESPONSABILIDAD DE COSTOS
   - Si el cliente requiere servicios pagos (Stripe, Twilio, OpenAI), 
     el cliente paga licencias + mi implementación
```

### 3. **Stack Técnico Más Específico para tu Caso**

La respuesta es genérica. Deberías especificar:

**Stack gratuito recomendado:**

- **Frontend**: React + Vite (más rápido que Create React App)
- **Backend sin costo**:
    - Supabase (PostgreSQL gratis hasta 500MB, auth incluida)
    - Firebase (Firestore gratis hasta 1GB)
    - Appwrite (self-hosted, 100% gratis)
- **Despliegue**:
    - Vercel/Netlify (frontend)
    - Railway/Render.com free tier (backend si es Node.js)
    - Expo EAS Build (móvil, con plan gratuito)

### 4. **Gestión de Cambios (Change Management) Más Estricta**

Esto es donde la mayoría de freelancers pierden dinero:

**Documento de Control de Cambios (obligatorio):**

```
FORMULARIO DE SOLICITUD DE CAMBIO

Cliente: [Nombre]
Fecha: [Fecha]
Cambio solicitado: [Descripción detallada]

ANÁLISIS DE IMPACTO:
- Horas adicionales estimadas: X horas
- Costo adicional: USD XXX
- Extensión de cronograma: X días
- Funcionalidades afectadas: [Lista]

□ Aprobado por cliente (firma + fecha)
□ Pago adicional del 50% antes de iniciar cambio
□ Pago del 50% restante al completar cambio
```

**Sin este documento firmado, NO hagas el cambio.** Es tu protección legal.

### 5. **Proceso de Onboarding del Cliente**

Falta un flujo claro para el primer contacto:

**Secuencia mejorada:**

1. **Primer contacto (email/WhatsApp)**: "Gracias por contactarme. Para darte una cotización precisa, necesito que completes este brief: [link a Google Form]"
    
2. **Brief obligatorio** (Google Forms gratuito):
    
    - ¿Qué problema resuelve tu proyecto?
    - ¿Usuarios estimados? (afecta base de datos)
    - ¿Presupuesto aproximado? (filtra clientes)
    - ¿Timeline esperado?
    - ¿Tienes contenido listo? (textos, imágenes)
3. **Reunión de descubrimiento** (solo si el brief tiene sentido)
    
4. **Propuesta técnica + comercial** con opción de firma digital (DocuSign tiene plan gratuito limitado, o usa PDF + firma escaneada)
    

### 6. **Manejo de la Falta de Experiencia en Ventas**

DeepSeek no aborda esto suficientemente:

**Script de venta técnica** (tu ventaja como programador):

```
"No soy diseñador gráfico, soy ingeniero de software especializado 
en aplicaciones web/móviles funcionales y rápidas.

Mi valor está en:
- Código limpio y mantenible (no código espagueti)
- Aplicaciones que escalan (si mañana tienes 1000 usuarios, funcionará)
- Stack moderno (React/React Native, no tecnología obsoleta)

¿Qué NO hago?
- Diseño visual desde cero (necesitas traer diseño o usar plantillas premium)
- Contenido copywriting
- SEO avanzado (solo implemento lo básico técnico)

Esto me permite mantener costos competitivos y entregar rápido."
```

**Esto convierte tu "debilidad" en fortaleza**: Los clientes aprecian la honestidad y saber exactamente qué recibirán.

### 7. **Portafolio sin Proyectos Reales**

DeepSeek sugiere "proyectos ficticios" pero no da detalles:

**Proyectos demostrativos específicos** (crea estos 3):

1. **Dashboard administrativo**:
    
    - Panel con gráficos (Recharts)
    - CRUD de productos/usuarios
    - Autenticación con Supabase
    - **Deploy en Vercel + GitHub público**
2. **E-commerce básico**:
    
    - Catálogo de productos
    - Carrito de compras (sin pasarela real)
    - Checkout simulado
    - Responsive con Tailwind
3. **App móvil React Native**:
    
    - To-do list con backend
    - Sincronización offline (AsyncStorage)
    - Publicada en Expo (https://expo.dev/@tuusuario/proyecto)

**Cada uno debe tener:**

- README profesional con screenshots
- Tecnologías usadas claramente listadas
- Demo funcional online

### 8. **Gestión de Código y Entrega**

Agregar cláusula sobre el código fuente:

```
ENTREGA DE CÓDIGO FUENTE

1. REPOSITORIO
   - Código entregado en repositorio Git (GitHub/GitLab)
   - Acceso completo al cliente al pagar último hito
   - Historial de commits incluido

2. DEPENDENCIAS Y LICENCIAS
   - Todas las dependencias son de código abierto (MIT/Apache 2.0)
   - Lista completa en package.json
   - Si se requieren librerías premium, se cotiza aparte

3. NO INCLUYE
   - Refactorización futura (el código funciona, pero no garantizo 
     que futuros desarrolladores lo encuentren perfecto)
   - Migración a otras tecnologías
   - Optimizaciones no especificadas en alcance original
```

### 9. **Facturación para Argentina**

DeepSeek ignora que eres de Argentina:

**Consideraciones locales:**

- **Monotributo**: Probablemente necesites inscribirte (categorías bajas son baratas)
- **Facturación electrónica AFIP**: Si facturás localmente
- **Cobro internacional**:
    - PayPal (retiene comisión pero es lo más común)
    - Wise (menor comisión)
    - Crypto (USDT) si el cliente acepta
    - Western Union (para montos grandes)
- **Precios en USD pero cobro en ARS**: Especificar cotización del día del pago

### 10. **Documento de Cierre de Proyecto**

Falta esto completamente:

```
ACTA DE CIERRE DE PROYECTO

Proyecto: [Nombre]
Fecha de cierre: [Fecha]
Cliente: [Nombre] - Firma: _____________
Desarrollador: [Tu nombre] - Firma: _____________

CONFIRMACIONES:
□ Cliente recibió acceso a repositorio de código
□ Cliente recibió documentación técnica
□ Cliente confirmó funcionamiento en entorno de producción
□ Variables de entorno y credenciales transferidas
□ Período de garantía iniciado: [Fecha] a [Fecha + 30 días]
□ Pago final recibido

POST-GARANTÍA:
- Soporte adicional: USD X/hora o paquetes mensuales
- Nuevas funcionalidades: Cotización por separado

Ambas partes acuerdan que el proyecto se considera completado 
según especificaciones originales. Modificaciones futuras 
requerirán nuevo acuerdo comercial.
```

---

## Resumen de Mejoras Prioritarias

1. ✅ **Contratos más defensivos** (protección legal)
2. ✅ **Control de cambios estricto** (evitar scope creep)
3. ✅ **Brief obligatorio pre-cotización** (calificar clientes)
4. ✅ **Stack técnico gratuito específico** (sin costos ocultos)
5. ✅ **Script de venta técnica** (compensar falta de experiencia)
6. ✅ **Portafolio demostrativo claro** (3 proyectos específicos)
7. ✅ **Facturación Argentina** (monotributo + cobro internacional)
8. ✅ **Acta de cierre** (evitar soporte eterno gratis)

¿Querés que desarrolle alguno de estos puntos en un documento listo para usar?


