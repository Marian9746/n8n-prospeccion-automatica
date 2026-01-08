# 🚀 n8n - Prospección Automatizada de Negocios en Instagram

Sistema de automatización completo para recopilar datos de negocios en Instagram y enviar emails personalizados usando IA.

## 📋 ¿Qué hace este sistema?

### Parte 1: Recopilación de Datos de Instagram
- 📸 Lee usernames de Instagram que tú agregas manualmente a un Google Sheet
- 📊 Extrae información automáticamente: nombre, bio, website, email, seguidores
- ✉️ Encuentra emails en la bio y en sus websites
- 📝 Guarda todo en Google Sheets automáticamente

### Parte 2: Análisis y Envío de Emails
- 🤖 Lee los negocios de Google Sheets
- 🌐 Analiza el contenido de cada website
- 💬 Genera emails personalizados con ChatGPT
- 📧 Envía los emails automáticamente por Gmail
- ✅ Actualiza el estado en Google Sheets

---

## 🛠️ Requisitos Previos

### 1. Cuentas y API Keys Necesarias

#### Google Cloud (para Sheets y Gmail)
1. Ve a [Google Cloud Console](https://console.cloud.google.com)
2. Crea un nuevo proyecto
3. Activa estas APIs:
   - Google Sheets API
   - Gmail API
4. Crea credenciales OAuth 2.0

#### OpenAI (para ChatGPT)
1. Regístrate en [OpenAI](https://platform.openai.com)
2. Crea una API Key en la sección API Keys
3. Asegúrate de tener créditos disponibles

#### Instagram (para obtener datos de negocios)
- **No necesitas API key** - El workflow extrae datos de perfiles públicos
- Solo necesitas buscar manualmente los usernames en Instagram
- **Opcional - Apify**: [apify.com](https://apify.com) - Para búsqueda automatizada por hashtags ($10-20/mes)

### 2. Software Necesario
- Docker Desktop (ya instalado en tu sistema)
- Un navegador web

---

## 🚀 Instalación y Configuración

### Paso 1: Levantar n8n con Docker

1. Abre PowerShell en la carpeta del proyecto:
```powershell
cd C:\Users\maria\n8n-prospeccion-automatica
```

2. Inicia n8n:
```powershell
docker-compose up -d
```

3. Espera 30 segundos y accede a n8n:
```
http://localhost:5678
```

4. Login inicial:
   - Usuario: `themode`
   - Contraseña: `jnRdx3F4`
   - **¡Cámbiala después por seguridad!**

### Paso 2: Configurar Credenciales en n8n

#### A) Google Sheets y Gmail (OAuth2)

1. En n8n, ve a **Settings** → **Credentials** → **New**
2. Busca "Google" y selecciona:
   - **Google Sheets OAuth2 API**
   - **Gmail OAuth2**
3. Completa:
   - **Client ID**: De Google Cloud Console
   - **Client Secret**: De Google Cloud Console
   - **OAuth Callback URL**: `http://localhost:5678/rest/oauth2-credential/callback`
4. Haz clic en **Connect** y autoriza el acceso
5. Repite para Gmail

#### B) OpenAI API

1. **Settings** → **Credentials** → **New**
2. Busca "OpenAI"
3. Pega tu API Key
4. Guarda

#### C) SerpAPI (o Outscraper)

1. **Settings** → **Credentials** → **New**
2. Selecciona **HTTP Query Auth**
3. Configura:
   - **Name**: `api_key`
   - **Value**: Tu API key de SerpAPI
4. Guarda

### Paso 3: Crear Google Sheets

1. Ve a [Google Sheets](https://sheets.google.com)
2. Crea una nueva hoja llamada **"Prospección Instagram"**
3. Crea **2 pestañas** con estos encabezados:

#### Pestaña 1: "Instagram Input"
```
Username | Estado
```

#### Pestaña 2: "Negocios Instagram"
```
nombre | username | url_instagram | website | email | bio | seguidores | posts | es_negocio | categoria | fecha_recopilacion | estado
```

4. Copia el ID del Spreadsheet (está en la URL):
   ```
   https://docs.google.com/spreadsheets/d/ESTE_ES_EL_ID/edit
   ```

5. **Agrega usernames** en "Instagram Input":
   - Busca negocios en Instagram (por hashtags, ubicación, etc.)
   - Copia los usernames (ej: @negociomoda, @marketingpro)
   - Pégalos en la columna "Username"
   - Deja "Estado" vacío

📸 **Ver guía completa:** [INSTAGRAM-SETUP.md](INSTAGRAM-SETUP.md)

### Paso 4: Importar Workflows

1. En n8n, haz clic en **"+"** → **Import from File**
2. Importa los dos archivos:
   - `workflows/parte1-busqueda-recopilacion.json`
   - `workflows/parte2-analisis-emails.json`

### Paso 5: Configurar los Workflows

#### En Workflow Parte 1:

1. Abre el nodo **"Leer Usernames de Instagram"**
   - Selecciona tu Google Sheets credential
   - Pega el Spreadsheet ID
   - Verifica que Sheet Name sea: `Instagram Input`

2. Abre el nodo **"Guardar en Google Sheets"**
   - Selecciona tu Google Sheets credential
   - Pega el Spreadsheet ID
   - Verifica que Sheet Name sea: `Negocios Instagram`

3. Abre el nodo **"Marcar como Procesado"**
   - Selecciona tu Google Sheets credential
   - Pega el Spreadsheet ID
   - Verifica que Sheet Name sea: `Instagram Input`

#### En Workflow Parte 2:

1. Abre **"Leer Negocios de Google Sheets"**
   - Asigna credenciales de Google Sheets
   - Pega el Spreadsheet ID

2. Abre **"ChatGPT - Generar Email Personalizado"**
   - Asigna credenciales de OpenAI
   - **PERSONALIZA EL PROMPT** con info de tu negocio:
     ```
     Servicios de marketing digital especializado en marcas de moda.
     Ayudamos a pequeñas marcas a crecer en redes sociales...
     ```

3. Abre **"Enviar Email por Gmail"**
   - Asigna credenciales de Gmail

4. Abre **"Actualizar Estado en Sheets"**
   - Asigna credenciales y Spreadsheet ID

---

## ▶️ Cómo Usar

### Primera Ejecución: Buscar Negocios

1. Abre el workflow **"Parte 1: Búsqueda y Recopilación"**
2. Haz clic en **"Execute Workflow"**
3. Revisa que los datos se guarden en Google Sheets
4. Verifica los emails encontrados

### Segunda Parte: Enviar Emails Automáticos

**Opción A - Ejecución Manual:**
1. Abre el workflow **"Parte 2: Análisis Web y Envío"**
2. Cambia el trigger a "Manual Trigger" temporalmente
3. Haz clic en **"Execute Workflow"**
4. Revisa los primeros emails generados

**Opción B - Automática (Recomendado):**
1. El workflow se ejecuta automáticamente cada 24 horas
2. Solo procesa negocios con estado "Pendiente"
3. Envía 5 emails por ejecución (ajustable)
4. Actualiza el estado a "Email Enviado"

---

## 🎯 Personalización

### Ajustar el Prompt de ChatGPT

Edita el nodo **"ChatGPT - Generar Email Personalizado"** con tu propuesta de valor:

```
Somos [TU NOMBRE/EMPRESA], especialistas en marketing digital para marcas de moda.

Nuestros servicios:
- Gestión de redes sociales (Instagram, TikTok)
- Creación de contenido visual
- Estrategias de crecimiento orgánico
- Campañas de influencers

[Añade tu experiencia, casos de éxito, etc.]
```

### Cambiar Zona de Búsqueda

En el nodo **"Buscar en Google Maps"**, modifica las coordenadas:

```javascript
// Madrid centro
"ll": "@40.4168,-3.7038,15z"

// Barcelona
"ll": "@41.3851,2.1734,15z"

// Otra ciudad: busca en Google Maps y copia las coordenadas
```

### Ajustar Cantidad de Emails por Día

En el nodo **"Procesar en Lotes de 5"**:
- Cambia `batchSize` de 5 a 10, 20, etc.
- **Cuidado**: No envíes demasiados emails o Gmail puede bloquearte

---

## 📊 Interpretación de Resultados

### Columnas en Google Sheets

- **nombre**: Nombre del negocio
- **website**: URL de su página web
- **telefono**: Número de contacto
- **email**: Email encontrado (o "No encontrado")
- **rating**: Calificación en Google (0-5)
- **total_reviews**: Cantidad de reseñas
- **fecha_recopilacion**: Cuándo se recopiló
- **estado**: Pendiente / Email Enviado / Sin Email
- **fecha_email**: Cuándo se envió el email
- **asunto_enviado**: Asunto del email enviado

### Seguimiento de Respuestas

Para saber si alguien respondió:
1. Revisa tu bandeja de entrada de Gmail
2. Usa filtros: `to:me subject:"Re:"`
3. Considera usar etiquetas en Gmail para organizarlas

---

## ⚠️ Buenas Prácticas y Límites

### Para Evitar Ser Bloqueado

1. **Gmail**: Máximo 500 emails/día (cuenta gratuita)
2. **OpenAI**: Controla tu gasto (cada email ~$0.01-0.03)
3. **Google Maps API**: 100 búsquedas gratis/mes
4. **SerpAPI**: 100 búsquedas gratis/mes

### Recomendaciones

✅ **SÍ hacer:**
- Empieza con 5-10 emails/día
- Personaliza bien el prompt de ChatGPT
- Revisa los primeros emails generados manualmente
- Usa un email profesional (@tudominio.com mejor que @gmail.com)
- Incluye opción de "unsubscribe" en tus emails

❌ **NO hacer:**
- Enviar cientos de emails el primer día
- Usar lenguaje spam ("GRATIS", "OFERTA", etc.)
- Mentir o exagerar en los emails
- Ignorar las respuestas negativas

---

## 🔧 Solución de Problemas

### n8n no arranca

```powershell
# Ver logs
docker-compose logs -f

# Reiniciar contenedor
docker-compose restart

# Borrar y recrear
docker-compose down
docker-compose up -d
```

### No encuentra emails en websites

- Algunos sitios no publican emails públicamente
- Considera usar herramientas como Hunter.io
- Añade nodo para buscar en redes sociales

### ChatGPT genera emails genéricos

- Mejora el prompt con más contexto de tu negocio
- Aumenta la temperatura (0.8 → 0.9)
- Añade ejemplos de buenos emails en el prompt

### Gmail no envía emails

- Verifica que has autorizado OAuth correctamente
- Activa "Aplicaciones menos seguras" si es necesario
- Considera usar Gmail para negocios (Google Workspace)

---

## 📈 Próximos Pasos y Mejoras

### Ideas para Ampliar

1. **Añadir análisis de Instagram/TikTok**
   - Buscar el perfil social del negocio
   - Analizar engagement y followers
   - Personalizar email según su presencia social

2. **Follow-up automático**
   - Si no responden en 7 días, enviar recordatorio
   - Máximo 2 follow-ups

3. **Sistema de scoring**
   - Calcular "potencial" del cliente según:
     - Rating de Google
     - Cantidad de reviews
     - Calidad del website
     - Presencia en redes

4. **Integración con CRM**
   - Enviar leads a HubSpot, Pipedrive, etc.
   - Trackear conversaciones

5. **Dashboard de métricas**
   - Tasa de apertura (requiere herramientas adicionales)
   - Tasa de respuesta
   - ROI del sistema

---

## 📞 Soporte

### Recursos Útiles

- [Documentación de n8n](https://docs.n8n.io)
- [Comunidad de n8n](https://community.n8n.io)
- [Ejemplos de workflows](https://n8n.io/workflows)

### Estructura del Proyecto

```
n8n-prospeccion-automatica/
├── docker-compose.yml          # Configuración de Docker
├── .env.example               # Variables de entorno
├── workflows/
│   ├── parte1-busqueda-recopilacion.json
│   └── parte2-analisis-emails.json
├── backups/                   # Backups automáticos
└── README.md                  # Esta guía
```

---

## 📝 Notas Finales

- **Legalidad**: Asegúrate de cumplir con GDPR/LOPD si operas en Europa
- **Ética**: No hagas spam. Ofrece valor real en tus emails
- **Pruebas**: Siempre prueba con tu propio email primero
- **Costos**: Monitorea el gasto en OpenAI y otras APIs

---

## 🎉 ¡Listo!

Ya tienes todo configurado. Empieza con búsquedas pequeñas, revisa los resultados, y escala gradualmente.

**¡Mucha suerte con la prospección automatizada!** 🚀
