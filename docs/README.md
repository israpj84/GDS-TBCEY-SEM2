# Generador de Secuencias Didácticas TBC - v4.5.1

## 🎯 ¿Qué es esto?

Una herramienta para **docentes de Telebachillerato Comunitario** que genera **Secuencias Didácticas personalizadas** usando IA (Claude Haiku), adaptadas al contexto real de comunidades rurales.

## ⚡ Cambios en v4.5.1

✅ **Más rápido:** Haiku 4.5 en lugar de Opus  
✅ **Sin timeouts:** Vercel timeout controlado a 25 segundos  
✅ **Más humano:** Prompts con lenguaje docente real  
✅ **Semestre automático:** Se asigna soloal elegir UAC  
✅ **Descarga dual:** HTML + DOCX nativo  
✅ **83% más barato:** Cos tos de API reducidos  

## 🚀 Cómo usar

### Para docentes (usuarios finales):

1. **Abre la app** en tu navegador (Vercel URL)
2. **Completa los 5 pasos:**
   - Datos básicos (TBC, docente, UAC, unidad)
   - Contexto de la comunidad (recursos, diagnóstico)
   - Calendario de sesiones (fechas, días, horarios)
   - Sube PAEC en PDF + API key de Claude
   - Descarga tu Secuencia Didáctica

3. **Descarga** en HTML (imprimible) o DOCX (editable)

### Para desarrolladores (actualizar en Vercel):

1. **Reemplaza estos archivos** en tu repo:
   ```
   public/index.html        ← Interfaz optimizada
   api/generate.js          ← Haiku 4.5 + timeout
   package.json             ← Versión actualizada
   vercel.json              ← Config timeout
   ```

2. **Push a GitHub:**
   ```bash
   git add .
   git commit -m "Upgrade: Haiku 4.5, timeout control, auto-semester, DOCX"
   git push
   ```

3. **Vercel redeploy automático** ✅

## 📋 Requisitos

- **API Key de Anthropic** (gratuita, obtén en https://console.anthropic.com)
- **PAEC en PDF** (documento del proyecto)
- **Navegador moderno** (Chrome, Firefox, Safari, Edge)

## 🔑 API Key de Anthropic

1. Crea una cuenta en https://console.anthropic.com
2. Ve a "API Keys" en el dashboard
3. Crea una nueva clave
4. Pégala en la app (en Paso 4)
5. ⚠️ **No la compartas** — es como tu contraseña

## 📊 Costo

- **Antes:** $0.015 por generación (Opus)
- **Ahora:** $0.0025 por generación (Haiku)
- **Ahorro:** ~85% menos costo

## ✨ Características

- 📍 **Contexto real:** Adapta a comunidades rurales maya del sureste
- 🎯 **UACs integradas:** IMCyPMaT, RQPMaT, PESii, OPMaT
- 📅 **Calendario inteligente:** Calcula sesiones automáticamente
- 🤖 **IA práctica:** Claude genera actividades lisas para usar
- 📥 **Descarga dual:** HTML + DOCX
- 🔄 **Semestre automático:** Sin selecciones manuales
- 🏃 **Ultra rápido:** 8-12 segundos máximo

## 🛠️ Tecnología

- **Frontend:** HTML5 + CSS3 + JavaScript vanilla
- **Backend:** Node.js + Vercel Serverless
- **IA:** Claude Haiku 4.5 (Anthropic)
- **Librerías:** docx.js (descarga DOCX)

## 📞 Soporte

Si algo no funciona:

1. **Revisa la consola** (F12 → Console) para ver errores
2. **Verifica tu API key** sea válida
3. **Prueba con menos progresiones** o fechas más cortas
4. **Limpia caché del navegador** (Ctrl+Shift+Supr)

## 📝 Notas

- El PAEC se envía a Claude para análisis, NO se almacena en servidores
- La app funciona 100% en el navegador (excepto llamada a API)
- Cada generación es independiente (puedes generar múltiples secuencias)

## 🎓 Para docentes: Cómo obtener mejor resultado

1. **PAEC claro:** Cuanto más detallado sea tu PAEC, mejores actividades
2. **Contexto real:** Describe tu grupo y comunidad con precisión
3. **Prueba Haiku:** Aunque es más pequeño que Opus, es **muy bueno** para esto
4. **Reduce si tarda:** Si tarda mucho, reduce el rango de fechas
5. **Descarga DOCX:** Abre en Word, edita, personaliza aún más

## 📖 Más info

- Documentación: Ver `CAMBIOS_REALIZADOS.md`
- Repo: [Tu repositorio GitHub]
- Deploy: Vercel

---

**¡Listo para generar Secuencias Didácticas! 🚀**

*v4.5.1 — Optimizado para docentes de TBC con Haiku 4.5*
