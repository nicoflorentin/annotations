# 🚀 **ROADMAP NGINX 2026 (De NOOB a PRO)**

---

## 📊 **OVERVIEW DEL ROADMAP**

```
Mes 1: Fundamentos + HTTP Basics
Mes 2: Reverse Proxy + Load Balancing
Mes 3: SSL/TLS + Security
Mes 4: Performance + Caching
Mes 5: Avanzado (Lua, Modules, Kubernetes)
Mes 6: Proyecto Real + Certificación
```

**Tiempo total:** 6 meses (dedicando 1-2 horas/día)  
**Costo:** $0 (todo gratis)

---

## 🎯 **MES 1: FUNDAMENTOS + HTTP BASICS**

### **Semana 1: Instalación y Conceptos Básicos**

#### **Día 1-2: ¿Qué es Nginx?**

```bash
# Conceptos clave:
- Web server vs Application server
- Event-driven architecture
- Nginx vs Apache (cuándo usar cada uno)
- Master process vs Worker process

# Práctica:
sudo apt update
sudo apt install nginx
systemctl status nginx
curl localhost  # Ver la página default
```

**📚 Recursos:**

- [Nginx Beginner's Guide](https://nginx.org/en/docs/beginners_guide.html) (oficial)
- Video: "What is Nginx?" (YouTube - TechWorld with Nana)

---

#### **Día 3-4: Estructura de Archivos**

```bash
# Entender la estructura:
/etc/nginx/
  ├── nginx.conf          # Configuración principal
  ├── sites-available/    # Configs disponibles
  ├── sites-enabled/      # Configs activas (symlinks)
  ├── conf.d/            # Configs adicionales
  └── snippets/          # Fragmentos reutilizables

# Práctica:
cat /etc/nginx/nginx.conf
ls -la /etc/nginx/sites-enabled/
nginx -t  # Test de sintaxis
nginx -T  # Ver config completa
```

**📝 Ejercicio:**

```nginx
# Crear tu primer server block
server {
    listen 80;
    server_name localhost;
    
    location / {
        root /var/www/html;
        index index.html;
    }
}
```

---

#### **Día 5-7: HTTP Básico**

```bash
# Conceptos:
- Request/Response cycle
- HTTP methods (GET, POST, PUT, DELETE)
- Status codes (200, 301, 404, 500)
- Headers

# Práctica:
# Crear sitio estático simple
mkdir -p /var/www/mi-sitio
echo "<h1>Mi primer sitio Nginx</h1>" > /var/www/mi-sitio/index.html

# Configurar Nginx
sudo nano /etc/nginx/sites-available/mi-sitio
```

**Config completa:**

```nginx
server {
    listen 80;
    server_name mi-sitio.local;
    
    root /var/www/mi-sitio;
    index index.html;
    
    location / {
        try_files $uri $uri/ =404;
    }
    
    # Log files
    access_log /var/log/nginx/mi-sitio.access.log;
    error_log /var/log/nginx/mi-sitio.error.log;
}
```

**📚 Recursos:**

- MDN Web Docs: HTTP
- Nginx: HTTP Core Module Docs

---

### **Semana 2: Locations y Rewrites**

#### **Día 8-10: Location Blocks**

```nginx
# Tipos de location matching
server {
    # Exact match (más prioritario)
    location = /exacto {
        return 200 "Match exacto\n";
    }
    
    # Preferential prefix
    location ^~ /static/ {
        root /var/www;
    }
    
    # Regex case-sensitive
    location ~ \.php$ {
        fastcgi_pass unix:/run/php/php8.1-fpm.sock;
    }
    
    # Regex case-insensitive
    location ~* \.(jpg|jpeg|png|gif)$ {
        expires 30d;
    }
    
    # Prefix match (menos prioritario)
    location /api/ {
        proxy_pass http://backend:3000;
    }
}
```

**🎯 Ejercicio Práctico:**

```bash
# Crear estructura:
/var/www/test/
  ├── index.html
  ├── static/
  │   └── style.css
  ├── images/
  │   └── logo.png
  └── api/
      └── test.json

# Configurar Nginx para servir cada sección correctamente
```

---

#### **Día 11-14: Rewrites y Redirects**

```nginx
# Redirects (301/302)
server {
    # Redirect simple
    location /viejo {
        return 301 /nuevo;
    }
    
    # Redirect con dominio
    server_name old-domain.com;
    return 301 https://new-domain.com$request_uri;
}

# Rewrites (interno)
server {
    # Rewrite básico
    rewrite ^/productos/(.*)$ /items/$1 last;
    
    # Rewrite con condición
    if ($request_uri ~* "^/blog/(.*)") {
        rewrite ^/blog/(.*)$ /articles/$1 last;
    }
    
    # Try files pattern (común en SPAs)
    location / {
        try_files $uri $uri/ /index.html;
    }
}
```

**🎯 Proyecto Semana 2:**

```
Crear un sitio con:
- Homepage (/)
- Blog (/blog)
- Imágenes en /static/images
- Redirect de /old a /new
- Página 404 personalizada
```

---

### **Semana 3: Variables y Logs**

#### **Día 15-17: Variables de Nginx**

```nginx
# Variables built-in importantes
server {
    location /debug {
        return 200 "
            Request URI: $request_uri
            Args: $args
            Host: $host
            Remote Addr: $remote_addr
            Scheme: $scheme
            Request Method: $request_method
            HTTP User Agent: $http_user_agent
        ";
    }
    
    # Usar variables en configuración
    location /api {
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Host $host;
    }
}

# Variables custom
map $http_user_agent $is_mobile {
    default 0;
    ~*mobile 1;
}

server {
    if ($is_mobile) {
        rewrite ^ /mobile break;
    }
}
```

**📚 Recursos:**

- Nginx Variables Documentation
- Nginx Map Module

---

#### **Día 18-21: Logging y Monitoring**

```nginx
# Custom log format
http {
    log_format main '$remote_addr - $remote_user [$time_local] '
                    '"$request" $status $body_bytes_sent '
                    '"$http_referer" "$http_user_agent"';
    
    log_format json escape=json '{'
        '"time": "$time_iso8601",'
        '"remote_addr": "$remote_addr",'
        '"request": "$request",'
        '"status": $status,'
        '"bytes": $body_bytes_sent,'
        '"referer": "$http_referer",'
        '"user_agent": "$http_user_agent"'
    '}';
    
    access_log /var/log/nginx/access.log main;
    access_log /var/log/nginx/access.json.log json;
}

# Logs por virtualhost
server {
    access_log /var/log/nginx/site1.access.log;
    error_log /var/log/nginx/site1.error.log warn;
}
```

**🔍 Análisis de logs:**

```bash
# Ver requests en tiempo real
tail -f /var/log/nginx/access.log

# Top 10 IPs
awk '{print $1}' /var/log/nginx/access.log | sort | uniq -c | sort -rn | head -10

# Top 10 URLs
awk '{print $7}' /var/log/nginx/access.log | sort | uniq -c | sort -rn | head -10

# Status codes
awk '{print $9}' /var/log/nginx/access.log | sort | uniq -c | sort -rn

# Instalar GoAccess (analizador visual)
sudo apt install goaccess
goaccess /var/log/nginx/access.log --log-format=COMBINED
```

---

### **Semana 4: Testing y Troubleshooting**

#### **Día 22-24: Testing de Configs**

```bash
# Test de sintaxis
nginx -t

# Test con config específica
nginx -t -c /path/to/nginx.conf

# Ver config completa (incluye includes)
nginx -T

# Reload sin downtime
sudo systemctl reload nginx

# Restart completo
sudo systemctl restart nginx

# Validar SSL
openssl s_client -connect localhost:443 -servername ejemplo.com
```

**🛠️ Debugging:**

```nginx
# Activar debug log
error_log /var/log/nginx/debug.log debug;

# Debug específico
server {
    error_log /var/log/nginx/site-debug.log debug;
    
    location / {
        # Ver qué archivo se está sirviendo
        add_header X-Debug-File $uri;
        add_header X-Debug-Root $document_root;
    }
}
```

---

#### **Día 25-28: Errores Comunes**

```bash
# Error: "address already in use"
sudo lsof -i :80
sudo kill -9 <PID>

# Error: "permission denied"
# Verificar permisos:
ls -la /var/www/mi-sitio
sudo chown -R www-data:www-data /var/www/mi-sitio

# Error: "connect() failed (111: Connection refused)"
# Backend no está corriendo
systemctl status backend-service

# Error: "nginx: [emerg] bind() to 0.0.0.0:80 failed"
# Ya hay algo en el puerto
sudo netstat -tlnp | grep :80
```

**🎯 Proyecto Mes 1:**

```
Crear un sitio web completo con:
✅ Multiple server blocks (varios dominios)
✅ Static files + SPA routing
✅ Custom 404/500 pages
✅ Redirects y rewrites
✅ Logging configurado
✅ Debug habilitado
```

---

## 🔄 **MES 2: REVERSE PROXY + LOAD BALANCING**

### **Semana 5: Reverse Proxy Basics**

#### **Día 29-31: Conceptos de Reverse Proxy**

```nginx
# Proxy simple a backend Node.js
upstream backend {
    server localhost:3000;
}

server {
    listen 80;
    server_name api.ejemplo.com;
    
    location / {
        proxy_pass http://backend;
        
        # Headers esenciales
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        
        # Timeouts
        proxy_connect_timeout 60s;
        proxy_send_timeout 60s;
        proxy_read_timeout 60s;
    }
}
```

**🎯 Práctica:**

```bash
# 1. Crear backend simple (Node.js)
mkdir ~/backend-test && cd ~/backend-test
npm init -y
npm install express

# server.js
const express = require('express');
const app = express();

app.get('/', (req, res) => {
    res.json({
        message: 'Backend funcionando',
        headers: req.headers
    });
});

app.listen(3000);

# 2. Configurar Nginx como proxy
# 3. Verificar headers en el backend
```

---

#### **Día 32-35: WebSockets y Streaming**

```nginx
# Proxy WebSocket
map $http_upgrade $connection_upgrade {
    default upgrade;
    '' close;
}

server {
    location /ws {
        proxy_pass http://websocket-backend;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection $connection_upgrade;
        proxy_set_header Host $host;
        
        # Timeouts largos para WS
        proxy_read_timeout 86400;
    }
}

# Proxy para streaming (video/audio)
location /stream {
    proxy_pass http://streaming-server;
    proxy_buffering off;  # Importante para streaming
    proxy_http_version 1.1;
    chunked_transfer_encoding on;
}
```

---

### **Semana 6: Load Balancing**

#### **Día 36-38: Algoritmos de Balanceo**

```nginx
# Round Robin (default)
upstream backend_rr {
    server backend1.example.com;
    server backend2.example.com;
    server backend3.example.com;
}

# Least Connections
upstream backend_lc {
    least_conn;
    server backend1.example.com;
    server backend2.example.com;
}

# IP Hash (sticky sessions)
upstream backend_ip {
    ip_hash;
    server backend1.example.com;
    server backend2.example.com;
}

# Weighted
upstream backend_weighted {
    server backend1.example.com weight=3;
    server backend2.example.com weight=2;
    server backend3.example.com weight=1;
}

# Con health checks (Nginx Plus / Open Source con módulo)
upstream backend_health {
    server backend1.example.com max_fails=3 fail_timeout=30s;
    server backend2.example.com max_fails=3 fail_timeout=30s;
    server backup.example.com backup;
}
```

**🎯 Lab Práctico:**

```bash
# Crear 3 backends con Docker
docker run -d -p 3001:80 --name backend1 nginx
docker run -d -p 3002:80 --name backend2 nginx
docker run -d -p 3003:80 --name backend3 nginx

# Modificar index.html de cada uno para identificarlos
docker exec backend1 sh -c 'echo "Backend 1" > /usr/share/nginx/html/index.html'
docker exec backend2 sh -c 'echo "Backend 2" > /usr/share/nginx/html/index.html'
docker exec backend3 sh -c 'echo "Backend 3" > /usr/share/nginx/html/index.html'

# Configurar Nginx load balancer
upstream backends {
    server localhost:3001;
    server localhost:3002;
    server localhost:3003;
}

server {
    listen 80;
    
    location / {
        proxy_pass http://backends;
    }
}

# Testear con curl en loop
for i in {1..10}; do curl localhost; done
```

---

#### **Día 39-42: Session Persistence**

```nginx
# Sticky sessions con cookies
upstream backend {
    server backend1.example.com;
    server backend2.example.com;
    
    sticky cookie srv_id expires=1h domain=.example.com path=/;
}

# Alternativa con map
map $cookie_backend $backend_server {
    default backend1.example.com;
    "backend2" backend2.example.com;
}

server {
    location / {
        proxy_pass http://$backend_server;
        
        # Setear cookie en la respuesta
        add_header Set-Cookie "backend=$backend_server; Path=/; HttpOnly";
    }
}
```

---

### **Semana 7: API Gateway Pattern**

#### **Día 43-45: Microservices Routing**

```nginx
# Rutear a diferentes microservicios
upstream users_service {
    server users-api:3001;
}

upstream products_service {
    server products-api:3002;
}

upstream orders_service {
    server orders-api:3003;
}

server {
    listen 80;
    server_name api.ejemplo.com;
    
    # Users API
    location /api/users {
        rewrite ^/api/users/(.*)$ /$1 break;
        proxy_pass http://users_service;
    }
    
    # Products API
    location /api/products {
        rewrite ^/api/products/(.*)$ /$1 break;
        proxy_pass http://products_service;
    }
    
    # Orders API
    location /api/orders {
        rewrite ^/api/orders/(.*)$ /$1 break;
        proxy_pass http://orders_service;
    }
    
    # Health check
    location /health {
        access_log off;
        return 200 "OK\n";
    }
}
```

---

#### **Día 46-49: Rate Limiting**

```nginx
# Definir zonas de rate limiting
http {
    # 10MB de memoria, llave por IP
    limit_req_zone $binary_remote_addr zone=api_limit:10m rate=10r/s;
    
    # Por API key
    limit_req_zone $http_x_api_key zone=apikey_limit:10m rate=100r/s;
    
    server {
        # Limitar requests generales
        location /api {
            limit_req zone=api_limit burst=20 nodelay;
            proxy_pass http://backend;
        }
        
        # Limitar por API key
        location /api/premium {
            limit_req zone=apikey_limit burst=50;
            proxy_pass http://backend;
        }
    }
}
```

---

### **Semana 8: Proyecto Mes 2**

**🎯 Construir API Gateway completo:**

```
Requisitos:
✅ 3+ microservicios backend (puedes usar Docker)
✅ Load balancing con health checks
✅ Rate limiting por endpoint
✅ WebSocket support
✅ Logging estructurado (JSON)
✅ Métricas básicas (/metrics endpoint)
```

**Arquitectura sugerida:**

```
Internet → Nginx (80/443)
            ↓
    ┌───────┼───────┐
    ↓       ↓       ↓
  Users  Products Orders
  :3001   :3002   :3003
```

---

## 🔒 **MES 3: SSL/TLS + SECURITY**

### **Semana 9: HTTPS Básico**

#### **Día 50-52: SSL/TLS Fundamentals**

```bash
# Generar certificado self-signed (desarrollo)
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
    -keyout /etc/nginx/ssl/selfsigned.key \
    -out /etc/nginx/ssl/selfsigned.crt
```

```nginx
server {
    listen 443 ssl http2;
    server_name ejemplo.com;
    
    ssl_certificate /etc/nginx/ssl/selfsigned.crt;
    ssl_certificate_key /etc/nginx/ssl/selfsigned.key;
    
    # Configuración SSL básica
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers HIGH:!aNULL:!MD5;
    ssl_prefer_server_ciphers on;
    
    # HSTS
    add_header Strict-Transport-Security "max-age=31536000" always;
}

# Redirect HTTP → HTTPS
server {
    listen 80;
    server_name ejemplo.com;
    return 301 https://$server_name$request_uri;
}
```

---

#### **Día 53-56: Let's Encrypt + Certbot**

```bash
# Instalar Certbot
sudo apt install certbot python3-certbot-nginx

# Obtener certificado automático
sudo certbot --nginx -d ejemplo.com -d www.ejemplo.com

# Renovación automática (ya viene configurado)
sudo certbot renew --dry-run

# Ver certificados instalados
sudo certbot certificates
```

**Config automática de Certbot:**

```nginx
# Certbot agrega esto automáticamente
server {
    listen 443 ssl http2;
    server_name ejemplo.com;
    
    ssl_certificate /etc/letsencrypt/live/ejemplo.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/ejemplo.com/privkey.pem;
    include /etc/letsencrypt/options-ssl-nginx.conf;
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem;
}
```

---

### **Semana 10: Security Headers**

#### **Día 57-59: Headers de Seguridad**

```nginx
# Configuración de seguridad completa
server {
    # Security headers
    add_header X-Frame-Options "SAMEORIGIN" always;
    add_header X-Content-Type-Options "nosniff" always;
    add_header X-XSS-Protection "1; mode=block" always;
    add_header Referrer-Policy "no-referrer-when-downgrade" always;
    
    # CSP (Content Security Policy)
    add_header Content-Security-Policy "default-src 'self' http: https: data: blob: 'unsafe-inline'" always;
    
    # Permissions Policy
    add_header Permissions-Policy "geolocation=(), microphone=(), camera=()" always;
    
    # HSTS
    add_header Strict-Transport-Security "max-age=31536000; includeSubDomains; preload" always;
}
```

**🔍 Testear seguridad:**

- https://securityheaders.com
- https://www.ssllabs.com/ssltest/

---

#### **Día 60-63: Access Control**

```nginx
# Whitelist de IPs
location /admin {
    allow 192.168.1.0/24;
    allow 10.0.0.1;
    deny all;
    
    proxy_pass http://admin-backend;
}

# Basic Auth
location /private {
    auth_basic "Área Restringida";
    auth_basic_user_file /etc/nginx/.htpasswd;
    
    proxy_pass http://backend;
}

# Crear archivo .htpasswd
# sudo apt install apache2-utils
# sudo htpasswd -c /etc/nginx/.htpasswd usuario1
```

---

### **Semana 11: WAF y Bot Protection**

#### **Día 64-66: ModSecurity (WAF)**

```bash
# Instalar ModSecurity
sudo apt install libnginx-mod-security

# Habilitar ModSecurity
sudo nano /etc/nginx/modsec/modsecurity.conf
# SecRuleEngine On

# Cargar reglas OWASP
cd /etc/nginx/modsec
sudo git clone https://github.com/coreruleset/coreruleset
sudo cp coreruleset/crs-setup.conf.example crs-setup.conf
```

```nginx
server {
    modsecurity on;
    modsecurity_rules_file /etc/nginx/modsec/main.conf;
    
    location / {
        proxy_pass http://backend;
    }
}
```

---

#### **Día 67-70: Bot Detection**

```nginx
# Detectar bots maliciosos
map $http_user_agent $is_bot {
    default 0;
    ~*bot 1;
    ~*spider 1;
    ~*crawler 1;
}

server {
    if ($is_bot) {
        return 403;
    }
    
    # Rate limiting más agresivo para bots
    location / {
        limit_req zone=bot_limit burst=5;
        proxy_pass http://backend;
    }
}

# Bloquear por referrer sospechoso
map $http_referer $bad_referer {
    default 0;
    "~*malicious-site.com" 1;
}

server {
    if ($bad_referer) {
        return 444;  # Cerrar conexión sin respuesta
    }
}
```

---

### **Semana 12: Proyecto Mes 3**

**🎯 Construir sitio production-ready:**

```
Requisitos:
✅ HTTPS con Let's Encrypt
✅ Score A+ en SSL Labs
✅ Todos los security headers
✅ Rate limiting configurado
✅ Basic auth en /admin
✅ IP whitelist para ciertas rutas
✅ Bot protection básico
✅ Logs de seguridad
```

---

## ⚡ **MES 4: PERFORMANCE + CACHING**

### **Semana 13: Static Content Optimization**

#### **Día 71-73: Compresión**

```nginx
# Gzip compression
gzip on;
gzip_vary on;
gzip_proxied any;
gzip_comp_level 6;
gzip_types
    text/plain
    text/css
    text/xml
    text/javascript
    application/json
    application/javascript
    application/xml+rss
    application/rss+xml
    font/truetype
    font/opentype
    application/vnd.ms-fontobject
    image/svg+xml;

# Brotli (mejor que gzip, requiere módulo)
brotli on;
brotli_comp_level 6;
brotli_types text/plain text/css application/json application/javascript text/xml application/xml;
```

**📊 Benchmark:**

```bash
# Sin compresión
curl -o /dev/null -s -w "%{size_download}\n" http://localhost/style.css

# Con compresión
curl -H "Accept-Encoding: gzip" -o /dev/null -s -w "%{size_download}\n" http://localhost/style.css
```

---

#### **Día 74-77: Browser Caching**

```nginx
# Cache por tipo de archivo
location ~* \.(jpg|jpeg|png|gif|ico|svg)$ {
    expires 1y;
    add_header Cache-Control "public, immutable";
}

location ~* \.(css|js)$ {
    expires 1M;
    add_header Cache-Control "public";
}

location ~* \.(woff|woff2|ttf|otf)$ {
    expires 1y;
    add_header Cache-Control "public, immutable";
    add_header Access-Control-Allow-Origin "*";
}

# No cache para HTML
location ~* \.html$ {
    expires -1;
    add_header Cache-Control "no-store, no-cache, must-revalidate";
}
```

---

### **Semana 14: Nginx Caching**

#### **Día 78-80: FastCGI Cache (PHP)**

```nginx
# Definir zona de cache
fastcgi_cache_path /var/cache/nginx levels=1:2 keys_zone=php_cache:10m max_size=1g inactive=60m;

server {
    location ~ \.php$ {
        fastcgi_cache php_cache;
        fastcgi_cache_valid 200 60m;
        fastcgi_cache_methods GET HEAD;
        fastcgi_cache_key "$scheme$request_method$host$request_uri";
        
        # Bypass cache
        fastcgi_cache_bypass $http_pragma $http_authorization;
        fastcgi_no_cache $http_pragma $http_authorization;
        
        # Headers de debug
        add_header X-Cache-Status $upstream_cache_status;
        
        fastcgi_pass unix:/run/php/php8.1-fpm.sock;
    }
}
```

---

#### **Día 81-84: Proxy Cache**

```nginx
# Cache para contenido dinámico
proxy_cache_path /var/cache/nginx/proxy levels=1:2 keys_zone=api_cache:10m max_size=1g inactive=60m use_temp_path=off;

upstream backend {
    server backend1:3000;
}

server {
    location /api {
        proxy_cache api_cache;
        proxy_cache_valid 200 10m;
        proxy_cache_valid 404 1m;
        
        # Cache key
        proxy_cache_key "$scheme$request_method$host$request_uri$is_args$args";
        
        # Cache bypass
        proxy_cache_bypass $http_pragma;
        proxy_no_cache $http_pragma;
        
        # Headers
        add_header X-Cache-Status $upstream_cache_status;
        add_header X-Cache-Key "$scheme$request_method$host$request_uri";
        
        proxy_pass http://backend;
    }
    
    # Purge cache (requiere módulo)
    location ~ /purge(/.*) {
        allow 127.0.0.1;
        deny all;
        proxy_cache_purge api_cache "$scheme$request_method$host$1";
    }
}
```

**🧪 Testear cache:**

```bash
# Primera request (MISS)
curl -I http://localhost/api/users | grep X-Cache-Status

# Segunda request (HIT)
curl -I http://localhost/api/users | grep X-Cache-Status

# Purge cache
curl -X PURGE http://localhost/purge/api/users
```

---

### **Semana 15: HTTP/2 y HTTP/3**

#### **Día 85-87: HTTP/2 Optimization**

```nginx
server {
    listen 443 ssl http2;
    
    # Server push (obsoleto en HTTP/3)
    http2_push_preload on;
    
    location / {
        # Push recursos críticos
        add_header Link "</style.css>; rel=preload; as=style" always;
        add_header Link "</script.js>; rel=preload; as=script" always;
        
        root /var/www/html;
    }
}
```

**📊 Verificar HTTP/2:**

```bash
curl -I --http2 https://localhost
```

---

#### **Día 88-91: HTTP/3 (QUIC)**

```bash
# Compilar Nginx con soporte HTTP/3 (requiere compilación custom)
# O usar imagen Docker con HTTP/3
docker pull macbre/nginx-http3
```

```nginx
server {
    listen 443 ssl http2;
    listen 443 quic reuseport;  # HTTP/3
    
    # Advertise HTTP/3
    add_header Alt-Svc 'h3=":443"; ma=86400';
    
    ssl_protocols TLSv1.3;
}
```

---

### **Semana 16: Proyecto Mes 4**

**🎯 Optimizar sitio existente:**

```
Benchmarks antes/después:
✅ PageSpeed Score > 90
✅ GTmetrix Grade A
✅ Lighthouse Performance > 90

Implementar:
✅ Gzip/Brotli compression
✅ Browser caching
✅ Proxy cache para API
✅ HTTP/2 habilitado
✅ Recursos optimizados (minify, image
```