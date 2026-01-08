# 📸 Guía de Configuración para Instagram

## 🎯 Cómo Funciona Ahora

En lugar de buscar negocios en Google Maps, ahora el sistema trabaja con cuentas de Instagram:

1. **Tú buscas manualmente** en Instagram los negocios que te interesan
2. **Copias los usernames** y los pegas en un Google Sheet
3. **El workflow automáticamente** extrae los datos de cada perfil
4. **Guarda todo** en otro Google Sheet listo para enviar emails

---

## 📋 Paso 1: Crear tus Google Sheets

Necesitas crear **1 hoja de cálculo** con **2 pestañas**:

### Pestaña 1: "Instagram Input" (donde pones los usernames)

Encabezados en la primera fila:
```
Username | Estado
```

Ejemplo:
```
Username              | Estado
@negociomoda         | 
@marketingpro        |
@tiendaboutique      |
```

**Nota:** Deja la columna "Estado" vacía. El workflow la llenará automáticamente.

### Pestaña 2: "Negocios Instagram" (donde se guardan los resultados)

Encabezados en la primera fila:
```
nombre | username | url_instagram | website | email | bio | seguidores | posts | es_negocio | categoria | fecha_recopilacion | estado
```

---

## 🔍 Paso 2: Buscar Negocios en Instagram

### Estrategias de Búsqueda:

#### A) Por Hashtags:
Busca en Instagram:
- `#marketingdigitalmadrid`
- `#modamadrid`
- `#pequeñonegocio`
- `#emprendedores`
- `#tiendaonline`

#### B) Por Ubicación:
1. Ve a Instagram y busca una ubicación: "Madrid, Spain"
2. Filtra por "Recientes" o "Populares"
3. Encuentra cuentas de negocios

#### C) Por Explorar:
1. Sigue a algunos negocios similares a tu objetivo
2. Instagram te recomendará cuentas similares
3. Revisa "Cuentas sugeridas"

### ¿Qué Buscar?
Cuentas que tengan:
- ✅ Foto de perfil profesional
- ✅ Bio completa con descripción del negocio
- ✅ Posts regulares
- ✅ Idealmente: link en la bio
- ✅ Idealmente: cuenta de "Empresa" o "Creador"

---

## ✍️ Paso 3: Copiar Usernames al Google Sheet

1. Abre tu Google Sheet "Instagram Input"
2. Copia los usernames uno por uno:
   - Puedes poner con @ o sin @: `@negociomoda` o `negociomoda`
   - El workflow limpia automáticamente el @
3. Deja la columna "Estado" vacía

Ejemplo:
```
@negociomoda
marketingpro
@tiendaboutique
fashionstoremd
```

**Consejo:** Empieza con 5-10 cuentas para hacer pruebas.

---

## ⚙️ Paso 4: Configurar el Workflow en n8n

1. Abre n8n: `http://localhost:5678`
2. Importa el workflow actualizado: `workflows/parte1-busqueda-recopilacion.json`
3. Configura estos nodos:

### Nodo "Leer Usernames de Instagram":
- Credential: Tu cuenta de Google
- Spreadsheet ID: Copia el ID de tu Google Sheet
- Sheet Name: `Instagram Input`

### Nodo "Guardar en Google Sheets":
- Credential: Tu cuenta de Google
- Spreadsheet ID: El mismo ID
- Sheet Name: `Negocios Instagram`

### Nodo "Marcar como Procesado":
- Credential: Tu cuenta de Google
- Spreadsheet ID: El mismo ID
- Sheet Name: `Instagram Input`

---

## 🚀 Paso 5: Ejecutar el Workflow

1. Haz clic en **"Execute Workflow"** en n8n
2. El workflow:
   - Lee los usernames de "Instagram Input"
   - Extrae datos de cada perfil
   - Intenta encontrar email en bio o website
   - Guarda en "Negocios Instagram"
   - Marca como "Procesado" en "Instagram Input"

3. Revisa los resultados en tu Google Sheet

---

## 📊 ¿Qué Datos Obtienes?

Para cada cuenta de Instagram, el workflow extrae:

- ✅ **Nombre completo** del negocio
- ✅ **Username** (@usuario)
- ✅ **URL del perfil** (instagram.com/usuario)
- ✅ **Bio** (descripción completa)
- ✅ **Website** (si tienen link en bio)
- ✅ **Email** (si está en la bio o en el website)
- ✅ **Seguidores** (cantidad)
- ✅ **Posts** (cantidad de publicaciones)
- ✅ **Es negocio** (true/false)
- ✅ **Categoría** (si es cuenta business)

---

## ⚠️ Limitaciones y Consideraciones

### 1. Perfiles Privados
- ❌ No se pueden extraer datos de cuentas privadas
- El workflow lo marcará como "No disponible - perfil privado"

### 2. Rate Limiting
- Instagram puede bloquear temporalmente si haces muchas peticiones
- **Recomendación:** Procesa máximo 20-30 cuentas por ejecución
- Espera 1-2 horas entre ejecuciones grandes

### 3. Email
- Solo ~30-40% de cuentas tienen email visible
- Si tienen website, hay más probabilidades de encontrar email ahí

### 4. API de Instagram
- Este método usa scraping "básico" de perfiles públicos
- Si Instagram cambia su estructura, puede dejar de funcionar
- En ese caso, necesitarás usar Apify (de pago)

---

## 💡 Consejos para Mejores Resultados

1. **Calidad sobre cantidad:** Mejor 50 cuentas relevantes que 200 aleatorias
2. **Diversifica fuentes:** Busca en varios hashtags y ubicaciones
3. **Revisa manualmente:** Antes de enviar emails, revisa que sean negocios reales
4. **Actualiza regularmente:** Instagram crece, siempre hay nuevos negocios
5. **Combina con otras fuentes:** Usa también LinkedIn, Facebook, directorios

---

## 🔄 Próximo Paso: Enviar Emails

Una vez que tengas negocios en "Negocios Instagram" con emails:

1. El **Workflow Parte 2** leerá esa hoja
2. Analizará sus perfiles y websites
3. Generará emails personalizados con ChatGPT
4. Los enviará automáticamente

**¡Ya estás listo para prospectar en Instagram! 🎉**
