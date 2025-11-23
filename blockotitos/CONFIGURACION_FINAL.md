# Configuración Final - Frontend Vercel + Backend Google Cloud

## ✅ Estado Actual

- **Backend URL**: `https://commitspre-243000873240.us-central1.run.app` ✅ Funcionando
- **Frontend**: Desplegado en Vercel
- **Problema**: Error "AbortError: signal is aborted without reason"

## 🔧 Configuración Requerida

### 1. Variables de Entorno en Vercel

Ve a **Vercel → Tu Proyecto → Settings → Environment Variables** y verifica/agrega:

#### Variable: `VITE_BACKEND_URL`
- **Valor**: `https://commitspre-243000873240.us-central1.run.app`
- **IMPORTANTE**: 
  - ✅ Sin barra final (`/`)
  - ✅ Con `https://`
  - ✅ URL completa

#### Verificar otras variables (ya las tienes configuradas):
- ✅ `PUBLIC_STELLAR_NETWORK` = `TESTNET`
- ✅ `PUBLIC_STELLAR_NETWORK_PASSPHRASE` = `Test SDF Network ; September 2015`
- ✅ `PUBLIC_STELLAR_RPC_URL` = `https://soroban-testnet.stellar.org`
- ✅ `PUBLIC_STELLAR_HORIZON_URL` = `https://horizon-testnet.stellar.org`
- ✅ `VITE_SPOT_CONTRACT_ID` = `CC3XATHZKTV7WGEBR337JAH3UTAMQTK7VPPSDSAKHA4KGVOCJPF6P3VF`

### 2. Variables de Entorno en Google Cloud Run

Ve a **Google Cloud Console → Cloud Run → Tu Servicio → Variables y Secretos** y verifica/agrega:

#### Variables Requeridas:
```
PORT=8080
RPC_URL=https://soroban-testnet.stellar.org
NETWORK_PASSPHRASE="Test SDF Network ; September 2015"
ADMIN_SECRET=tu_secret_key_aqui
CLAIM_PAYER_SECRET=tu_secret_key_aqui
SPOT_CONTRACT_ID=CC3XATHZKTV7WGEBR337JAH3UTAMQTK7VPPSDSAKHA4KGVOCJPF6P3VF
MOCK_MODE=false
```

#### Variable Importante para CORS:
```
CORS_ORIGIN=*
```

O si quieres ser más específico (reemplaza con tu URL de Vercel):
```
CORS_ORIGIN=https://tu-frontend.vercel.app
```

#### Variable Opcional para Imágenes:
```
ASSET_BASE_URL=https://commitspre-243000873240.us-central1.run.app
```

## 🧪 Pruebas de Verificación

### 1. Probar el Backend
Abre en tu navegador:
```
https://commitspre-243000873240.us-central1.run.app/health
```

**Deberías ver**: `{"status":"ok"}` ✅

### 2. Probar desde el Frontend

1. Abre tu aplicación en Vercel
2. Abre las **Herramientas de Desarrollador** (F12)
3. Ve a la pestaña **Console**
4. Intenta crear un evento
5. Busca mensajes que empiecen con `[Backend]` - te mostrarán la URL que está usando

### 3. Verificar CORS

En la consola del navegador, si ves errores como:
```
Access to fetch at 'https://commitspre-243000873240.us-central1.run.app/...' 
from origin 'https://tu-frontend.vercel.app' has been blocked by CORS policy
```

Entonces necesitas configurar `CORS_ORIGIN` en Google Cloud Run.

## 🔄 Pasos para Aplicar los Cambios

### En Vercel:
1. Ve a **Settings → Environment Variables**
2. Verifica que `VITE_BACKEND_URL` tenga el valor exacto: `https://commitspre-243000873240.us-central1.run.app`
3. Si necesitas cambiarla, edítala y **redespliega** la aplicación

### En Google Cloud Run:
1. Ve a **Cloud Run → Tu Servicio**
2. Haz clic en **EDITAR Y DESPLEGAR NUEVA REVISIÓN**
3. Ve a la pestaña **Variables y Secretos**
4. Agrega o verifica `CORS_ORIGIN` con el valor `*` (o tu URL específica de Vercel)
5. Agrega `ASSET_BASE_URL` con el valor `https://commitspre-243000873240.us-central1.run.app`
6. Haz clic en **DESPLEGAR**

## 🐛 Solución de Problemas

### Si el error persiste después de configurar todo:

1. **Verifica la URL en Vercel**:
   - Abre la consola del navegador
   - Busca mensajes `[Backend] URL configurada:`
   - Verifica que sea exactamente `https://commitspre-243000873240.us-central1.run.app`

2. **Verifica CORS**:
   - En Google Cloud Run, asegúrate de que `CORS_ORIGIN=*` esté configurado
   - Redespliega el backend después de cambiar esta variable

3. **Verifica el Timeout**:
   - El timeout por defecto es 15 segundos
   - Si tu backend tarda más, puedes aumentar `VITE_BACKEND_TIMEOUT_MS` en Vercel

4. **Revisa los Logs**:
   - En Google Cloud Run → Logs, verifica si las peticiones están llegando
   - En Vercel → Deployments → Logs, verifica si hay errores de build

## 📝 Checklist Final

- [ ] `VITE_BACKEND_URL` configurada en Vercel con la URL correcta (sin barra final)
- [ ] `CORS_ORIGIN` configurado en Google Cloud Run (puede ser `*` para desarrollo)
- [ ] `ASSET_BASE_URL` configurado en Google Cloud Run (opcional pero recomendado)
- [ ] Frontend redesplegado en Vercel después de cambiar variables
- [ ] Backend redesplegado en Google Cloud Run después de cambiar variables
- [ ] Endpoint `/health` responde correctamente
- [ ] Consola del navegador muestra la URL correcta del backend

## 🎯 Resultado Esperado

Después de aplicar estos cambios:
- ✅ El frontend debería poder conectarse al backend
- ✅ Los errores de AbortError deberían desaparecer
- ✅ Deberías poder crear eventos sin problemas
- ✅ Los mensajes de error serán más claros si hay algún problema

