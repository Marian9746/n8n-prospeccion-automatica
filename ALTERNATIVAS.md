# Alternativas y Opciones de APIs

## Búsqueda de Negocios en Google Maps

### Opción 1: SerpAPI (Recomendado para principiantes)
- **Web**: https://serpapi.com
- **Gratis**: 100 búsquedas/mes
- **Pago**: $50/mes = 5,000 búsquedas
- **Ventajas**: Fácil de usar, documentación clara
- **Configuración**: API Key simple

### Opción 2: Outscraper
- **Web**: https://outscraper.com
- **Gratis**: 1,000 créditos al mes
- **Pago**: Desde $10/mes
- **Ventajas**: Más económico, más datos por negocio
- **Configuración**: API Key + endpoint diferente

```javascript
// Cambio en el nodo "Buscar en Google Maps"
// URL para Outscraper:
https://api.outscraper.com/maps/search-v2
// Query params:
{
  "query": "restaurantes Madrid",
  "limit": 20,
  "language": "es"
}
```

### Opción 3: Google Places API (Directamente)
- **Web**: https://console.cloud.google.com
- **Gratis**: $200 crédito mensual
- **Ventajas**: Oficial de Google, confiable
- **Desventajas**: Más complejo de configurar

### Opción 4: Apify (Scraping avanzado)
- **Web**: https://apify.com
- **Gratis**: Prueba limitada
- **Ventajas**: Scraping sin límites de API
- **Desventajas**: Más lento, puede violar ToS de Google

---

## Búsqueda de Emails

### Opción 1: Scraping directo (Actual - Gratis)
- Incluido en el workflow
- Busca emails en el HTML de la web
- Gratis pero menos efectivo (~30-40% de éxito)

### Opción 2: Hunter.io
- **Web**: https://hunter.io
- **Gratis**: 25 búsquedas/mes
- **Pago**: $49/mes = 500 búsquedas
- **Efectividad**: ~70-80%
- **n8n Node**: Sí (oficial)

```javascript
// Añadir nodo Hunter.io después de "Obtener Detalles"
{
  "operation": "domainSearch",
  "domain": "={{ $json.website }}"
}
```

### Opción 3: RocketReach
- **Web**: https://rocketreach.co
- **Gratis**: 5 búsquedas/mes
- **Pago**: $39/mes = 80 búsquedas
- **Efectividad**: ~85%
- **n8n**: Requiere HTTP Request

### Opción 4: Snov.io
- **Web**: https://snov.io
- **Gratis**: 50 créditos/mes
- **Pago**: $39/mes = 1,000 créditos
- **n8n**: Integración via API

---

## Generación de Emails (IA)

### Opción 1: OpenAI GPT-4 (Actual - Recomendado)
- **Costo**: $0.03/email (~3 centavos)
- **Calidad**: Excelente
- **Personalización**: Muy alta

### Opción 2: Claude (Anthropic)
- **Web**: https://anthropic.com
- **Costo**: Similar a GPT-4
- **Calidad**: Excelente, más "humano"
- **n8n**: Requiere HTTP Request custom

```javascript
// Cambiar nodo OpenAI por HTTP Request a Claude
{
  "url": "https://api.anthropic.com/v1/messages",
  "method": "POST",
  "headers": {
    "anthropic-api-key": "tu-api-key",
    "anthropic-version": "2023-06-01"
  },
  "body": {
    "model": "claude-3-sonnet-20240229",
    "messages": [...]
  }
}
```

### Opción 3: Llama 2 (Local/Gratis)
- **Costo**: Gratis (self-hosted)
- **Requisitos**: GPU potente o Ollama
- **Calidad**: Buena pero inferior a GPT-4
- **Configuración**: Compleja

### Opción 4: Gemini (Google)
- **Web**: https://ai.google.dev
- **Gratis**: 60 requests/minuto
- **Calidad**: Muy buena
- **n8n**: Requiere HTTP Request

---

## Envío de Emails

### Opción 1: Gmail (Actual)
- **Gratis**: 500 emails/día
- **Gmail Workspace**: 2,000 emails/día ($6/mes)
- **Ventajas**: Fácil configuración OAuth

### Opción 2: SendGrid
- **Web**: https://sendgrid.com
- **Gratis**: 100 emails/día
- **Pago**: $19.95/mes = 50,000 emails/mes
- **Ventajas**: Mejor deliverability, analytics
- **n8n Node**: Sí (oficial)

### Opción 3: Mailgun
- **Web**: https://mailgun.com
- **Gratis**: 5,000 emails/mes (3 meses)
- **Pago**: $35/mes = 50,000 emails
- **n8n Node**: Vía HTTP Request

### Opción 4: Outlook/Microsoft 365
- **Gratis**: 300 emails/día
- **Business**: 10,000 emails/día
- **n8n Node**: Sí (Microsoft 365)

---

## Base de Datos (Alternativas a Google Sheets)

### Opción 1: Google Sheets (Actual - Recomendado)
- Gratis, fácil de usar
- Bueno para <10,000 registros

### Opción 2: Airtable
- **Web**: https://airtable.com
- **Gratis**: 1,200 registros
- **Ventajas**: Más potente que Sheets, mejor UI
- **n8n Node**: Sí (oficial)

### Opción 3: PostgreSQL
- Self-hosted o PlanetScale gratis
- **Ventajas**: Ilimitado, más rápido
- **Desventajas**: Requiere setup técnico
- **n8n Node**: Sí (Postgres)

### Opción 4: Notion
- **Gratis**: Personal ilimitado
- **Ventajas**: Bonito, fácil de compartir
- **n8n Node**: Sí

---

## Paquetes Recomendados por Presupuesto

### Plan GRATIS (0€/mes)
- SerpAPI: 100 búsquedas/mes
- Scraping de emails: Manual
- OpenAI: ~$5 = 150-200 emails
- Gmail: Gratis
- **Total**: ~100 prospectos/mes

### Plan STARTER ($50/mes)
- Outscraper: $10/mes (más búsquedas)
- Hunter.io: $49/mes (500 emails verificados)
- OpenAI: ~$20 = 600-800 emails
- Gmail: Gratis
- **Total**: ~500-800 prospectos/mes

### Plan PRO ($150/mes)
- Outscraper: $30/mes (masivo)
- Hunter.io: $149/mes (2,500 emails)
- OpenAI: ~$50 = 1,500-2,000 emails
- SendGrid: $19.95/mes (mejor deliverability)
- **Total**: ~2,000-2,500 prospectos/mes

---

## Herramientas Adicionales Útiles

### Para Mejorar Deliverability
- **Warmup Tool**: Mailwarm, Lemwarm (calentar cuenta de email)
- **SPF/DKIM**: Configurar en tu dominio
- **Email Validation**: NeverBounce, ZeroBounce

### Para Tracking
- **Mailtrack**: Ver si abrieron el email
- **HubSpot**: CRM gratis con tracking
- **Pipedrive**: Gestión de leads

### Para Enriquecer Datos
- **Clearbit**: Datos de empresas
- **FullContact**: Información de contactos
- **LinkedIn Sales Navigator**: Búsqueda avanzada

---

## Recomendación Final

**Para empezar (Presupuesto bajo)**:
- SerpAPI (gratis)
- Scraping emails + Hunter.io (25 gratis)
- OpenAI GPT-4
- Gmail

**Para escalar (Presupuesto medio)**:
- Outscraper ($10-30/mes)
- Hunter.io ($49/mes)
- OpenAI GPT-4 ($50/mes)
- SendGrid ($20/mes)

**Profesional (Alto volumen)**:
- Outscraper o Apify
- Hunter.io Pro
- Claude o GPT-4
- SendGrid o Mailgun
- Airtable + CRM integrado
