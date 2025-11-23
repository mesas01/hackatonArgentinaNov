# Guía de Diagnóstico - Error AbortError

## Verificación Rápida

### 1. Verificar la URL del Backend en Vercel

En la imagen que compartiste, veo que `VITE_BACKEND_URL` está configurada pero la URL aparece truncada. Asegúrate de que:

1. **La URL esté completa** - Debe ser algo como:
   ```
   https://tu-backend-xxxxx-uc.a.run.app
   ```
   **NO debe tener barra final** (`/`)

2. **Verifica la URL completa**:
   - Haz clic en el ícono del ojo 👁️ en Vercel para ver el valor completo
   - O edita la variable para verla completa

### 2. Probar la Conexión al Backend

Abre en tu navegador la siguiente URL (reemplaza con tu URL real):
```
https://commitspre-243000873240.us-central1.run.app/health
```

**Si funciona**, deberías ver una respuesta JSON como:
```json
{"status":"ok"}
```

**Si NO funciona**, verás un error. Esto significa que:
- El backend no está desplegado
- La URL es incorrecta
- El backend no está accesible públicamente

### 3. Verificar CORS en el Backend

En Google Cloud Run, verifica que tengas configurada la variable de entorno:

```
CORS_ORIGIN=https://tu-frontend.vercel.app
```

O si quieres permitir todos los orígenes (solo para desarrollo):
```
CORS_ORIGIN=*
```

### 4. Verificar en la Consola del Navegador

1. Abre tu aplicación en Vercel
2. Abre las **Herramientas de Desarrollador** (F12)
3. Ve a la pestaña **Console**
4. Intenta crear un evento
5. Busca mensajes que empiecen con `[Backend]` - estos te mostrarán qué URL está usando

### 5. Verificar los Logs del Backend

En Google Cloud Console:
1. Ve a **Cloud Run** → Tu servicio
2. Ve a la pestaña **Logs**
3. Intenta crear un evento desde el frontend
4. Verifica si las peticiones están llegando al backend

## Soluciones Comunes

### Problema: La URL está truncada o incompleta

**Solución**: 
1. En Vercel, edita la variable `VITE_BACKEND_URL`
2. Asegúrate de copiar la URL completa desde Google Cloud Run
3. **NO incluyas barra final** (`/`)
4. Redespliega la aplicación

### Problema: El backend no responde

**Solución**:
1. Verifica que el backend esté desplegado y funcionando en Google Cloud Run
2. Prueba el endpoint `/health` directamente en el navegador
3. Verifica los logs del backend en Google Cloud

### Problema: Error de CORS

**Solución**:
1. En Google Cloud Run, configura `CORS_ORIGIN` con la URL de tu frontend
2. Ejemplo: `CORS_ORIGIN=https://tu-app.vercel.app`
3. Redespliega el backend

### Problema: Timeout

**Solución**:
1. El timeout por defecto es 15 segundos
2. Si tu backend tarda más, aumenta `VITE_BACKEND_TIMEOUT_MS` en Vercel
3. O verifica por qué el backend tarda tanto en responder

## Comandos para Probar

### Probar el Backend directamente:
```bash
curl https://tu-backend-xxxxx-uc.a.run.app/health
```

Deberías recibir:
```json
{"status":"ok"}
```

### Probar crear un evento (desde terminal):
```bash
curl -X POST https://tu-backend-xxxxx-uc.a.run.app/events/create \
  -H "Content-Type: application/json" \
  -d '{
    "creator": "GBDZQGS2ERUGP2Z4DCXUDNBTT73AH7JQ5XEF5AU4HPVY6IC4Q7VSW3B2",
    "eventName": "Test Event",
    "eventDate": 1735689600,
    "location": "Test",
    "description": "Test",
    "maxPoaps": 100,
    "claimStart": 1735689600,
    "claimEnd": 1736294400,
    "metadataUri": "https://example.com/metadata.json",
    "imageUrl": "https://example.com/image.png"
  }'
```

## Próximos Pasos

1. **Verifica la URL completa** en Vercel (haz clic en el ícono del ojo)
2. **Prueba el endpoint `/health`** en tu navegador
3. **Revisa la consola del navegador** cuando intentas crear un evento
4. **Revisa los logs del backend** en Google Cloud

Si después de estos pasos el problema persiste, comparte:
- La URL completa del backend (puedes ocultar partes sensibles)
- El mensaje de error exacto de la consola del navegador
- Si el endpoint `/health` responde correctamente

