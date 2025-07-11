## 🔍 ¿Por qué algunos links muestran imagen y otros no?

### 🧠 Depende de las **meta etiquetas HTML** del sitio. Las claves son:

```html
<meta property="og:image" content="URL-de-la-imagen.jpg" />
<meta property="og:title" content="Título de la página" />
<meta property="og:description" content="Descripción corta" />
```

Estas son parte del protocolo **Open Graph**, que usan Facebook, Twitter, Notion, Discord, etc.

---

### 🔎 En tu caso:

- ✅ `https://github.com/nicoflorentin` **sí tiene imagen**, porque GitHub tiene etiquetas `og:image`.
    
- ❌ `https://auadestudiojuridico.com` **no tiene imagen**, por eso se ve con el icono de advertencia y sin preview.
    

Podés comprobarlo con esta herramienta:  
🔗 [https://ogp.me](https://ogp.me/) o  
🔍 [https://metatags.io](https://metatags.io/)

---

## 🛠 ¿Cómo solucionarlo?

Si manejás vos la página (como con Vercel), agregá estas etiquetas en el `<head>` de tu HTML o layout de tu framework (Next.js, Astro, etc):

```html
<meta property="og:title" content="Auad & Asociados - Estudio Jurídico" />
<meta property="og:description" content="Derecho laboral, familia y sucesiones. Soluciones legales a medida." />
<meta property="og:image" content="https://auadestudiojuridico.com/preview.jpg" />
<meta property="og:url" content="https://auadestudiojuridico.com/" />
<meta name="twitter:card" content="summary_large_image" />
```

> Asegurate que la imagen sea pública, preferentemente de 1200×630 px y en formato JPG o PNG.