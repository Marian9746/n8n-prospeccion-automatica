# Guía Rápida de Inicio

## Pasos para Empezar en 10 minutos

### 1. Iniciar n8n
```powershell
cd C:\Users\maria\n8n-prospeccion-automatica
docker-compose up -d
```

Accede a: http://localhost:5678
- Usuario: `marian`
- Password: `jnRdx3F4`

### 2. APIs Necesarias

Crea cuentas gratuitas en:
- ✅ [OpenAI](https://platform.openai.com) - Para ChatGPT
- ✅ [Google Cloud](https://console.cloud.google.com) - Para Sheets y Gmail
- ❓ [Apify](https://apify.com) - OPCIONAL, para búsqueda automatizada en Instagram

### 3. Configurar Credenciales

En n8n → Settings → Credentials, añade:
1. **Google Sheets OAuth2**
2. **Gmail OAuth2**
3. **OpenAI API**

### 4. Crear Google Sheet

1. Crea una hoja llamada: **"Prospección Instagram"**
2. Crea **2 pestañas** con estos encabezados:

   **Pestaña "Instagram Input":**
   ```
   Username | Estado
   ```

   **Pestaña "Negocios Instagram":**
   ```
   nombre | username | url_instagram | website | email | bio | seguidores | posts | es_negocio | categoria | fecha_recopilacion | estado
   ```

3. Copia el ID del Sheet (de la URL)
4. **Busca en Instagram** y pega usernames en "Instagram Input"

### 5. Importar Workflows

En n8n:
1. Click en **"+"** → **Import from File**
2. Importa:
   - `workflows/parte1-busqueda-recopilacion.json`
   - `workflows/parte2-analisis-emails.json`

### 6. Configurar Workflows

#### Workflow Parte 1:
- Nodo "Leer Usernames de Instagram": Pega tu Spreadsheet ID
- Nodo "Guardar en Google Sheets": Pega tu Spreadsheet ID
- Asigna todas las credenciales

#### Workflow Parte 2:
- Nodo "ChatGPT": **¡IMPORTANTE!** Personaliza el prompt con tu negocio
- Nodo "Leer Google Sheets": Pega tu Spreadsheet ID (pestaña "Negocios Instagram")
- Asigna todas las credenciales

### 7. Primera Prueba

1. Ejecuta **Workflow Parte 1** manualmente
2. Revisa que los negocios aparezcan en Google Sheets
3. Si todo OK, ejecuta **Workflow Parte 2** con 1-2 negocios de prueba

### 8. ¡A Prospectar!

- Workflow Parte 1: Ejecuta cuando quieras buscar negocios nuevos
- Workflow Parte 2: Se ejecuta automáticamente cada 24h

---

## Costos Aproximados

Para 100 negocios:
- **Instagram (manual)**: Gratis
- **Apify (opcional)**: $10-20/mes para búsqueda automática
- **OpenAI (ChatGPT)**: $2-5 (100 emails personalizados)
- **Gmail**: Gratis
- **Google Sheets**: Gratis

**Total**: ~$2-5 por 100 negocios (o gratis si buscas manualmente)

---

## Checklist de Configuración

- [ ] Docker corriendo y n8n accesible
- [ ] API Keys obtenidas (OpenAI, Google Cloud)
- [ ] Credenciales configuradas en n8n
- [ ] Google Sheet creada con 2 pestañas y encabezados correctos
- [ ] Usernames de Instagram agregados a "Instagram Input"
- [ ] Workflows importados
- [ ] Spreadsheet ID actualizado en ambos workflows
- [ ] Prompt de ChatGPT personalizado
- [ ] Prueba con 1 negocio completada

---

## Comandos Útiles

```powershell
# Ver si n8n está corriendo
docker ps

# Ver logs de n8n
docker-compose logs -f

# Reiniciar n8n
docker-compose restart

# Detener n8n
docker-compose down

# Actualizar n8n a última versión
docker-compose pull
docker-compose up -d
```

---

## Preguntas Frecuentes

**Q: ¿Puedo usar Outlook en lugar de Gmail?**
A: Sí, n8n tiene integración con Microsoft 365. Cambia el nodo Gmail por Outlook.

**Q: ¿Cómo encuentro emails si no están en el website?**
A: Considera usar Hunter.io o RocketReach. Ambos tienen integraciones con n8n.

**Q: ¿Cuántos emails puedo enviar por día?**
A: Gmail gratuito: 500/día. Gmail Workspace: 2000/día. Empieza con 5-10.

**Q: ¿El email se envía desde mi cuenta personal?**
A: Sí. Te recomiendo crear una cuenta específica para esto (ej: hola@tumarca.com)

**Q: ¿Necesito saber programar?**
A: No. Los workflows están listos. Solo necesitas configurar las credenciales y personalizar el prompt.

---

Para más detalles, consulta el [README.md](README.md) completo.
