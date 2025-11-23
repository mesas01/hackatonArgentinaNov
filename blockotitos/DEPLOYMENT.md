# Guía de Despliegue

Esta guía explica cómo desplegar la aplicación frontend en Vercel y el backend en Google Cloud Run, y cómo conectarlos correctamente.

## Problema Común: Error "AbortError: signal is aborted without reason"

Este error generalmente ocurre cuando:
1. El frontend no puede conectarse al backend (URL incorrecta o no configurada)
2. El backend no está accesible desde internet
3. Hay problemas de CORS entre frontend y backend

## Configuración del Frontend en Vercel

### 1. Variables de Entorno Requeridas

En el panel de Vercel, ve a **Settings > Environment Variables** y configura:

#### Variable: `VITE_BACKEND_URL`
- **Valor**: La URL completa de tu backend en Google Cloud Run
- **Ejemplo**: `https://tu-backend-xxxxx-uc.a.run.app`
- **Importante**: No incluyas la barra final (`/`) al final de la URL

#### Variables Opcionales (con valores por defecto):
- `VITE_BACKEND_TIMEOUT_MS`: Timeout en milisegundos (default: 15000)
- `VITE_BACKEND_MAX_ATTEMPTS`: Número máximo de reintentos (default: 3)
- `VITE_BACKEND_RETRY_BACKOFF_MS`: Tiempo entre reintentos en ms (default: 400)

### 2. Obtener la URL del Backend

1. Ve a [Google Cloud Console](https://console.cloud.google.com/)
2. Navega a **Cloud Run**
3. Selecciona tu servicio de backend
4. Copia la URL que aparece en la parte superior (algo como `https://tu-backend-xxxxx-uc.a.run.app`)

### 3. Configurar en Vercel

1. Ve a tu proyecto en Vercel
2. Ve a **Settings > Environment Variables**
3. Agrega la variable `VITE_BACKEND_URL` con la URL de tu backend
4. Asegúrate de que esté configurada para **Production**, **Preview** y **Development** según necesites
5. **Redespliega** tu aplicación después de agregar las variables

## Configuración del Backend en Google Cloud Run

### 1. Variables de Entorno Requeridas

En Google Cloud Run, configura las siguientes variables de entorno:

```
PORT=8080
RPC_URL=https://soroban-testnet.stellar.org
NETWORK_PASSPHRASE="Test SDF Network ; September 2015"
ADMIN_SECRET=tu_secret_key_aqui
CLAIM_PAYER_SECRET=tu_secret_key_aqui
SPOT_CONTRACT_ID=tu_contract_id_aqui
MOCK_MODE=false
CORS_ORIGIN=https://tu-frontend.vercel.app
ASSET_BASE_URL=https://tu-backend-xxxxx-uc.a.run.app
```

### 2. Configurar CORS

La variable `CORS_ORIGIN` debe contener la URL de tu frontend en Vercel. Si quieres permitir múltiples orígenes, puedes usar:

```
CORS_ORIGIN=https://tu-frontend.vercel.app,https://tu-frontend-preview.vercel.app
```

O usa `*` para permitir todos los orígenes (solo para desarrollo):

```
CORS_ORIGIN=*
```

### 3. Configurar ASSET_BASE_URL

La variable `ASSET_BASE_URL` debe ser la URL completa de tu backend en Cloud Run. Esto se usa para generar URLs de imágenes subidas.

## Verificación de la Conexión

### 1. Verificar que el Backend esté Accesible

Abre en tu navegador:
```
https://tu-backend-xxxxx-uc.a.run.app/events/onchain
```

Deberías ver una respuesta JSON (puede estar vacía si no hay eventos).

### 2. Verificar CORS

Abre la consola del navegador en tu frontend y verifica que no haya errores de CORS. Si ves errores como:

```
Access to fetch at 'https://...' from origin 'https://...' has been blocked by CORS policy
```

Entonces necesitas configurar correctamente `CORS_ORIGIN` en el backend.

### 3. Verificar Variables de Entorno en Vercel

En el build log de Vercel, verifica que las variables de entorno estén siendo leídas correctamente. Si ves que `backendBaseUrl` es `http://localhost:4000` en producción, significa que `VITE_BACKEND_URL` no está configurada.

## Solución de Problemas

### Error: "No se pudo conectar al backend"

1. Verifica que `VITE_BACKEND_URL` esté configurada en Vercel
2. Verifica que la URL del backend sea correcta y accesible
3. Verifica que el backend esté funcionando en Google Cloud Run
4. Redespliega el frontend después de cambiar las variables de entorno

### Error: "La petición fue cancelada por timeout"

1. Verifica que el backend esté respondiendo (prueba la URL directamente)
2. Aumenta `VITE_BACKEND_TIMEOUT_MS` si el backend tarda mucho en responder
3. Verifica los logs del backend en Google Cloud para ver si hay errores

### Error: "CORS policy"

1. Verifica que `CORS_ORIGIN` en el backend incluya la URL de tu frontend
2. Asegúrate de que la URL del frontend sea exacta (incluyendo `https://`)
3. Redespliega el backend después de cambiar `CORS_ORIGIN`

## Comandos Útiles

### Probar el Backend Localmente

```bash
cd blockotitos/backend
npm install
npm run dev
```

El backend estará disponible en `http://localhost:4000`

### Probar el Frontend Localmente

```bash
cd blockotitos
npm install
# Crea un archivo .env.local con:
# VITE_BACKEND_URL=http://localhost:4000
npm run dev
```

## Notas Importantes

- **Siempre redespliega** después de cambiar variables de entorno
- Las variables de entorno que empiezan con `VITE_` son expuestas al cliente
- No pongas secrets sensibles en variables `VITE_*`
- El backend en Cloud Run debe estar configurado para aceptar tráfico sin autenticación (o configurar autenticación según necesites)

