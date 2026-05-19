# 📋 GUÍA PASO A PASO: IMPLEMENTAR EN VERCEL

## 🎯 Objetivo
Reemplazar tu versión actual (Opus) con la nueva versión optimizada (Haiku) sin perder datos ni funcionalidad.

---

## PASO 1: PREPARAR LOS ARCHIVOS NUEVOS

### 1.1 Obtén los archivos actualizados

Tendrás 4 archivos nuevos/modificados:
```
✓ index.html          (público/interfaz)
✓ generate.js         (API backend)
✓ package.json        (configuración)
✓ vercel.json         (timeout Vercel)
```

### 1.2 Verifica que tengas Git configurado
```bash
cd tu-proyecto-repo
git status
```

---

## PASO 2: REEMPLAZAR ARCHIVOS EN TU REPO

### 2.1 Actualiza `public/index.html`

```bash
# Opción A: Copia el archivo nuevo
cp ruta/al/nuevo/index.html public/index.html

# Opción B: O edita manualmente — requiere hacer estos cambios:
# • Línea 7: Agregar <script src="https://cdnjs.cloudflare.com/ajax/libs/docx/8.5.0/docx.min.js"></script>
# • Línea 193: Reemplazar dropdown de semestre con <input type="hidden" id="semestre" value="2°">
# • Agregar función updateSemestreAutomatico()
# • Línea 422: Cambiar botón a dos botones (downloadHTML, downloadDOCX)
# • Función buildPrompt(): Mejorar texto del prompt
```

### 2.2 Actualiza `api/generate.js`

```bash
# Opción A: Copia el archivo nuevo
cp ruta/al/nuevo/generate.js api/generate.js

# Opción B: O edita manualmente — cambios clave:
# • Línea 22: Cambiar modelo de 'claude-opus-4-5' a 'claude-haiku-4-5-20250101'
# • Línea 23: Cambiar max_tokens de 8192 a 3500
# • Agregar AbortController con timeout de 25000ms
```

### 2.3 Actualiza `vercel.json`

```bash
# Reemplaza completamente con:
cat > vercel.json << 'EOF'
{
  "version": 2,
  "functions": {
    "api/generate.js": {
      "memory": 1024,
      "maxDuration": 30
    }
  },
  "buildCommand": "npm run build",
  "outputDirectory": ".next"
}
EOF
```

### 2.4 Actualiza `package.json`

```bash
# En la sección "version", cambia a:
"version": "4.5.1"

# Y en "description":
"description": "Generador de Secuencias Didácticas para Telebachillerato Comunitario - Optimizado con Haiku 4.5"
```

---

## PASO 3: COMMIT Y PUSH

### 3.1 Agrega los cambios a Git
```bash
git add public/index.html
git add api/generate.js
git add vercel.json
git add package.json
```

### 3.2 Verifica que solo cambiaste lo necesario
```bash
git diff --cached
```

Deberías ver:
- `public/index.html`: + script docx.js, semestre automático, botones duales, prompt mejorado
- `api/generate.js`: Haiku 4.5, max_tokens 3500, AbortController
- `vercel.json`: Configuración de timeout
- `package.json`: Versión 4.5.1

### 3.3 Commit con mensaje descriptivo
```bash
git commit -m "Upgrade: Haiku 4.5, timeout control, auto-semester, dual downloads"
```

### 3.4 Push a GitHub
```bash
git push origin main
```

(Reemplaza `main` con tu rama si es diferente: `develop`, `master`, etc.)

---

## PASO 4: VERCEL REDEPLOY AUTOMÁTICO

### 4.1 Espera el redeploy automático

Vercel detecta automáticamente cambios en:
- `api/generate.js` → Redeploy de Serverless
- `vercel.json` → Redeploy de configuración

**Tiempo esperado:** 2-5 minutos

### 4.2 Verifica el deploy en dashboard Vercel

1. Ve a https://vercel.com/dashboard
2. Selecciona tu proyecto
3. Mira los Deployments recientes
4. Busca el más nuevo (debe estar "Ready" ✅)

```
Estado esperado:
┌─────────────────────────────────┐
│ ✅ Upgrade: Haiku 4.5...        │
│    Ready · 2min ago             │
│    Built with Next.js 14.0.0    │
│    3 functions · 2 static files │
└─────────────────────────────────┘
```

### 4.3 Si ves "Failed" (rojo)

1. Haz clic en el deployment fallido
2. Ve a "Logs"
3. Busca el error
4. Errores comunes:

```
❌ "module not found"
   → Verifica que package.json está bien

❌ "JSON parsing error"
   → Revisa vercel.json, debe ser JSON válido

❌ "syntax error"
   → Revisión typos en generate.js
```

---

## PASO 5: PRUEBAS EN VIVO

### 5.1 Abre tu app actualizada

```
https://tu-proyecto.vercel.app
```

### 5.2 Prueba los cambios principales

#### ✅ Semestre automático:
1. Ve a Paso 1 (Datos básicos)
2. Cambia el dropdown de UAC entre opciones
3. El campo "Semestre" (oculto) debe cambiar automáticamente
   - IMCyPMaT → 2°
   - RQPMaT → 4°
   - PESii → 6°
   - OPMaT → 6°

#### ✅ Generación rápida:
1. Completa todos los pasos
2. En Paso 4, copia una API key de Claude (temporal para prueba)
3. Sube un PAEC PDF ejemplo
4. Haz clic en "Generar Secuencia"
5. Observa:
   - Debe terminar en 8-12 segundos (NO 70+)
   - Sin mensaje de timeout

#### ✅ Descargas duales:
1. Una vez generada la secuencia, ve a "Resultado"
2. Verás DOS botones:
   - 📄 Descargar HTML (imprimible)
   - 📋 Descargar DOCX (editable)
3. Prueba ambos:
   - HTML: Abre en navegador, imprime
   - DOCX: Abre en Word/LibreOffice

### 5.3 Revisa la consola del navegador

```
Presiona: F12 (o Ctrl+Shift+I)
Pestaña: Console
```

No debe haber errores rojos. Puedes ignorar warnings naranjas.

---

## PASO 6: ROLLBACK (SI ALGO SALE MAL)

Si necesitas volver a la versión anterior:

### 6.1 Opción rápida: Revert en Git
```bash
git revert HEAD
git push origin main
```

Vercel redeploy automático en 2-5 min.

### 6.2 Opción desde Vercel dashboard
1. Ve a tu proyecto en Vercel
2. "Deployments" → Busca deployment anterior (marcado ✅)
3. Haz clic en el menú (⋮)
4. "Redeploy"

---

## CHECKLIST FINAL

- [ ] Archivos copiados correctamente (index.html, generate.js, vercel.json, package.json)
- [ ] `git add` de todos los cambios
- [ ] `git commit` con mensaje descriptivo
- [ ] `git push` exitoso (sin errores)
- [ ] Vercel dashboard muestra nuevo deployment en "Ready" ✅
- [ ] Semestre automático funciona (cambia al seleccionar UAC)
- [ ] Generación tarda 8-12 segundos (NO 70+)
- [ ] Botones de descarga HTML y DOCX aparecen
- [ ] HTML descarga y abre en navegador
- [ ] DOCX descarga y abre en Word
- [ ] Consola del navegador sin errores rojos
- [ ] API key de Anthropic funciona correctamente

---

## ❓ TROUBLESHOOTING

### Problema: "Timeout sigue ocurriendo"
**Solución:**
1. Verifica que `api/generate.js` tiene `claude-haiku-4-5-20250101`
2. Verifica que `max_tokens` es 3500
3. Verifica que `vercel.json` tiene `"maxDuration": 30`
4. Intenta reducir número de progresiones (4 en lugar de 6)

### Problema: "DOCX no descarga"
**Solución:**
1. Verifica que `index.html` tiene el script de docx.js (línea 7)
2. Recarga la página (Ctrl+F5)
3. Abre consola (F12) y busca errores
4. Si dice "docx is not defined", espera que docx.js cargue

### Problema: "Semestre sigue siendo dropdown"
**Solución:**
1. Verifica que línea 193 tiene: `<input type="hidden" id="semestre" value="2°">`
2. Recarga la página completamente
3. Verifica que función `updateSemestreAutomatico()` existe
4. Abre consola y ejecuta: `document.getElementById('semestre').value`

### Problema: "Deploy falla en Vercel"
**Solución:**
1. Ve a Vercel dashboard → tu proyecto → Deployments
2. Haz clic en deployment rojo → "Logs"
3. Busca la línea roja con el error
4. Errores comunes:
   - JSON inválido en `vercel.json` → Valida en jsonlint.com
   - Typo en `api/generate.js` → Revisa sintaxis
   - Rama incorrecta → Verifica `git branch`

### Problema: "Cambios no aparecen después de push"
**Solución:**
1. En Vercel: Ve a Settings → Git → verifica rama correcta
2. Fuerza actualización: Vercel Dashboard → Redeploy último deployment
3. En tu navegador: Ctrl+Shift+Supr (limpiar caché) y recarga

---

## 📞 SOPORTE

Si nada de esto funciona:

1. **Copia este info:**
   - Link de tu repo GitHub
   - Última línea de output de `git push`
   - Error en consola del navegador (F12 → Console)
   - Error en Vercel Logs

2. **Contacta:** Abre issue en tu repo o pregunta en el Discord de Vercel

---

## 🎉 ¡ÉXITO!

Una vez que veas:
```
✅ Semestre automático
✅ Generación en 8-12 segundos (SIN TIMEOUT)
✅ Descargas HTML + DOCX
```

**Tu app está 100% actualizada y lista para docentes. ¡Felicidades!** 🚀

---

**v4.5.1 DEPLOYMENT GUIDE**
*Optimizado para comunidades rurales con Haiku 4.5*
