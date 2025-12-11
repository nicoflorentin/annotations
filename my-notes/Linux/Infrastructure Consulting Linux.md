# 📋 **Requisitos para el puesto de Infrastructure Consulting Linux en Accenture**

---

## 🐧 **1. LINUX (Fundamental)**

### **Nivel Básico-Intermedio:**

- ✅ Administración de usuarios y permisos (`useradd`, `chmod`, `chown`, `sudo`)
- ✅ Gestión de servicios (`systemctl`, `service`)
- ✅ Configuración de red básica (`ip`, `netstat`, `nmcli`)
- ✅ Gestión de paquetes (apt, yum, dnf)
- ✅ Logs del sistema (`journalctl`, `/var/log/`)
- ✅ Bash scripting básico

### **Nivel Avanzado (Deseable):**

- ⚡ **Automatización** (Ansible, scripts complejos)
- ⚡ **Hardening** (SELinux, AppArmor, firewalls)
- ⚡ **Monitoreo avanzado** (Prometheus, Grafana, Zabbix)
- ⚡ **Tuning y benchmarking** (optimización de CPU, memoria, I/O)

**📚 Qué estudiar:**

- Linux Foundation Certified SysAdmin (LFCS)
- Red Hat Certified System Administrator (RHCSA)

---

## ☁️ **2. GOOGLE CLOUD PLATFORM (GCP)**

### **Nivel Básico:**

- ✅ Compute Engine (crear/gestionar VMs)
- ✅ Cloud Storage (buckets, objetos)
- ✅ Redes VPC básicas
- ✅ IAM (gestión de permisos y roles)
- ✅ Cloud Console y gcloud CLI

### **Nivel Avanzado (Deseable):**

- ⚡ Arquitecturas híbridas (cloud + on-premise)
- ⚡ Kubernetes Engine (GKE)
- ⚡ Políticas de seguridad avanzadas
- ⚡ Optimización de costos (billing alerts, rightsizing)
- ⚡ Load Balancing y Cloud CDN

**📚 Qué estudiar:**

- Google Cloud Associate Cloud Engineer
- Qwiklabs (labs prácticos gratuitos)

---

## 📊 **3. ANÁLISIS DE RENDIMIENTO**

### **Conocimientos clave:**

- ✅ Identificar cuellos de botella (CPU, RAM, disco, red)
- ✅ Interpretar métricas (`top`, `htop`, `iostat`, `vmstat`, `sar`)
- ✅ Análisis de logs de performance
- ✅ Proponer mejoras de configuración

### **Nivel Avanzado:**

- ⚡ Benchmarking (Apache Bench, sysbench, fio)
- ⚡ Tuning de kernel (sysctl, /proc)
- ⚡ Profiling de aplicaciones

**📚 Qué estudiar:**

- Linux Performance Tools (libro de Brendan Gregg)
- `man perf`, `man strace`

---

## 🏗️ **4. DISEÑO DE INFRAESTRUCTURA**

### **Conceptos importantes:**

- ✅ Alta disponibilidad (HA)
- ✅ Escalabilidad horizontal/vertical
- ✅ Disaster Recovery (DR)
- ✅ Infraestructura como código (IaC)
- ✅ Estándares y buenas prácticas (ITIL, ISO)

### **Nivel Avanzado:**

- ⚡ Arquitecturas multi-región
- ⚡ Terraform/Ansible para IaC
- ⚡ Contenedores (Docker, Kubernetes)
- ⚡ Microservicios

---

## 🤖 **5. INFRAESTRUCTURA INTELIGENTE (Plus)**

### **Conceptos deseables:**

- 🧠 Automatización con IA/ML (AIOps)
- 🧠 Monitoreo predictivo
- 🧠 Eficiencia energética en data centers
- 🧠 Observabilidad (traces, metrics, logs)

**No es obligatorio, pero suma mucho.**

---

## 🌐 **6. INGLÉS (B1 mínimo)**

### **Lo que necesitas:**

- ✅ Leer documentación técnica en inglés
- ✅ Participar en reuniones con clientes/equipos globales
- ✅ Escribir emails técnicos
- ✅ Entender términos técnicos (no hace falta inglés fluido)

**📚 Cómo mejorar:**

- Lee documentación oficial (Linux, GCP)
- Ve videos técnicos en inglés (YouTube)
- Practica con ChatGPT/Claude

---

## 🎯 **RESUMEN: ¿Qué priorizan?**

|Requisito|Importancia|Tu nivel actual (estimado)|
|---|---|---|
|**Linux admin**|🔴 CRÍTICO|✅ **TIENES** (sos sysadmin)|
|**GCP**|🟠 MUY IMPORTANTE|⚠️ **FALTA** (aprende básico)|
|**Performance tuning**|🟡 IMPORTANTE|✅ **TIENES** (nvtop, btop, etc.)|
|**Diseño infra**|🟡 IMPORTANTE|🟢 **BÁSICO** (Docker, compose)|
|**Inglés B1**|🟠 MUY IMPORTANTE|⚠️ **VERIFICA**|

---

## 📚 **PLAN DE ESTUDIO (2-4 semanas)**

### **Semana 1-2: GCP Básico**

```bash
# Objetivos:
1. Crear cuenta GCP (free tier $300 USD)
2. Completar Qwiklabs:
   - "GCP Essentials"
   - "Baseline: Infrastructure"
3. Crear una VM, configurar firewall, conectar por SSH
4. Crear un bucket de Cloud Storage
5. Configurar IAM (crear service accounts)
```

**Recursos:**

- [Qwiklabs](https://www.qwiklabs.com/) (gratis con cuenta Google)
- [Google Cloud Skills Boost](https://www.cloudskillsboost.google/)

---

### **Semana 2-3: Linux Avanzado**

```bash
# Objetivos:
1. Automatización con Ansible:
   - Instalar Ansible
   - Crear playbook para configurar servidor
2. Hardening:
   - Configurar firewall (ufw/iptables)
   - Deshabilitar servicios innecesarios
3. Monitoreo:
   - Instalar Prometheus + Grafana
   - Configurar dashboards
```

**Recursos:**

- [Ansible for DevOps](https://www.ansiblefordevops.com/) (libro gratis)
- [Linux Hardening Guide](https://github.com/trimstray/linux-hardening-checklist)

---

### **Semana 3-4: Proyectos Prácticos**

**Proyecto 1: Infraestructura híbrida**

```bash
# Desplegar aplicación en GCP + local
1. VM en GCP con Nginx
2. Base de datos local (MySQL en Docker)
3. Conectar ambos con VPN/túnel
```

**Proyecto 2: Monitoreo end-to-end**

```bash
1. Servidor Linux con servicios (Apache, MySQL, Docker)
2. Prometheus scraping métricas
3. Grafana con alertas
4. Logs centralizados (ELK stack o similar)
```

---

## 💼 **TIPS PARA LA ENTREVISTA**

### **Prepará respuestas para:**

1️⃣ **"Contame de un problema complejo que resolviste en Linux"**

- Usa ejemplos de tu `.bash_history` (recuperación de SD, Docker, etc.)

2️⃣ **"¿Cómo debuggearías un servidor lento?"**

- Respuesta modelo:
    
    ```
    1. Verifico métricas: top, iostat, netstat2. Reviso logs: journalctl, /var/log/3. Identifico proceso problemático4. Analizo con strace/perf si es necesario5. Aplico fix y monitoreo
    ```
    

3️⃣ **"¿Qué experiencia tenés con cloud?"**

- Si no tenés GCP, decí:
    
    > "Tengo experiencia con Docker y virtualización local. Estoy haciendo labs de GCP y me certifiqué/estoy certificándome en [curso]."
    

4️⃣ **"¿Cómo automatizarías el deployment de 100 servidores?"**

- Respuesta: Ansible/Terraform + scripts + CI/CD

---

## 🎯 **TU VENTAJA COMPETITIVA**

**Tenés experiencia con:**

- ✅ Linux diario (tu `.bash_history` lo demuestra)
- ✅ Docker/Docker Compose
- ✅ Troubleshooting (recuperación de datos, debugging de packages)
- ✅ Scripting (bash, npm, git)
- ✅ Monitoreo (nvtop, btop)

**Solo te falta:**

- ⚠️ GCP (aprende básico en 2 semanas)
- ⚠️ Inglés técnico (practica leyendo docs)

---

## 📝 **CHECKLIST PRE-ENTREVISTA**

```
□ Crear cuenta GCP y hacer 3-5 labs
□ Instalar gcloud CLI y crear una VM
□ Repasar comandos Linux (systemctl, journalctl, iptables)
□ Leer sobre IaC (Terraform/Ansible conceptos básicos)
□ Practicar inglés: leer docs de GCP en inglés
□ Preparar 3 ejemplos de problemas técnicos resueltos
□ Actualizar CV con skills: Linux, Docker, GCP (labs), Git
□ Linkedin: agregar certificaciones/labs de GCP
```

---

## 🚀 **CERTIFICACIONES QUE SUMAN (Opcional)**

|Certificación|Dificultad|Costo|Tiempo|
|---|---|---|---|
|**Google Cloud Associate**|🟢 Media|USD 125|2-4 semanas|
|**Linux Foundation LFCS**|🟡 Media-Alta|USD 375|4-8 semanas|
|**Red Hat RHCSA**|🔴 Alta|USD 400|8-12 semanas|

**Recomendación:** Empezá por **Google Cloud Associate** (es la más relevante para el puesto).

---

## 💡 **RECURSOS GRATIS**

```bash
# GCP
- Qwiklabs (labs gratis con cuenta trial)
- Google Cloud Skills Boost
- YouTube: "Google Cloud Tech" channel

# Linux
- Linux Journey (interactive)
- OverTheWire (wargames para aprender bash)
- man pages (RTFM siempre)

# Inglés técnico
- Read The Docs (cualquier proyecto open source)
- Stack Overflow (leer preguntas/respuestas)
- ChatGPT: "Explain [concepto] in English"
```

---

## 🎯 **CONCLUSIÓN**

**¿Estás listo para aplicar?**

- ✅ **Linux:** SÍ (tenés experiencia)
- ⚠️ **GCP:** NO (aprende básico en 2 semanas)
- ✅ **Performance:** SÍ (usas nvtop, btop, docker stats)
- ⚠️ **Inglés:** VERIFICA (practica)

**Tiempo estimado para estar listo:** **2-4 semanas de estudio intensivo.**

---

¿Querés que te arme un **plan de estudio diario** detallado? 📅