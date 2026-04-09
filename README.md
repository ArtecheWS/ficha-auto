# 🕒 Ficha-Auto

Fichaje automático en [Ficha.Work](https://app.ficha.work) mediante **GitHub Actions**. El sistema se ejecuta automáticamente de lunes a viernes a las **09:00** (entrada) y **17:00** (salida), sin necesidad de que tu ordenador esté encendido.

## ✨ Características
* 🚫 **Inteligente:** Salta automáticamente los días festivos de tu empresa.
* 🌴 **Vacaciones:** Respeta los días de vacaciones registrados en Ficha.Work.
* 🔄 **Autosuficiente:** El token de sesión se renueva automáticamente en cada ejecución.
* 📋 **Transparente:** Logs detallados de cada fichaje en la pestaña *Actions*.

---

## 🚀 Tutorial: Cómo configurarlo en tu cuenta

Sigue estos pasos para tener tu propio sistema de fichaje en menos de 5 minutos:

### Paso 1: Preparar tu repositorio
1. Inicia sesión en tu cuenta de [GitHub](https://github.com).
2. Haz un **Fork** de este repositorio (botón arriba a la derecha).
3. Deja las opciones por defecto y haz clic en **Create fork**. Ahora tienes una copia privada en tu cuenta.

### Paso 2: Obtener tu Refresh Token
1. Abre [app.ficha.work](https://app.ficha.work) e inicia sesión.
2. Pulsa **F12** para abrir las herramientas de desarrollador.
3. Ve a la pestaña **Application** (Chrome/Edge) o **Storage** (Firefox).
4. En el panel izquierdo, despliega **Local Storage** y selecciona `https://app.ficha.work`.
5. Busca la clave llamada `refreshToken` y copia su valor (un texto muy largo).

> [!CAUTION]
> Este token es como tu contraseña. **No lo compartas**. Guárdalo solo en los secretos de GitHub para que permanezca oculto.

### Paso 3: Configurar el Secret en GitHub
1. En **tu** repositorio (el fork), ve a la pestaña **Settings**.
2. En el menú izquierdo, ve a **Secrets and variables** → **Actions**.
3. Haz clic en **New repository secret**.
4. **Name:** `REFRESH_TOKEN`
5. **Secret:** Pega el valor que copiaste en el paso anterior.
6. Haz clic en **Add secret**.

### Paso 4: Activar los Workflows
GitHub desactiva las acciones por defecto al hacer un fork. Para activarlas:
1. Ve a la pestaña **Actions** de tu repositorio.
2. Haz clic en el botón verde: **"I understand my workflows, go ahead and enable them"**.

### Paso 5: Prueba de funcionamiento
1. Dentro de la pestaña **Actions**, selecciona el flujo **Fichaje automático** en la lista de la izquierda.
2. Haz clic en el desplegable **Run workflow** → botón **Run workflow**.
3. Espera unos segundos, recarga la página y haz clic en la ejecución para ver los logs y confirmar que ha funcionado.

---

## ⏰ Ajuste de Horario (UTC)

GitHub Actions trabaja siempre con la hora **UTC**. Para que fiche a las 09:00 y 17:00 de Madrid, el archivo `.github/workflows/fichar.yml` debe configurarse según la época del año:

| Época | Diferencia Madrid | Configuración Cron |
| :--- | :--- | :--- |
| **Verano** (Marzo-Octubre) | UTC+2 | `0 7` (9:00) y `0 15` (17:00) |
| **Invierno** (Octubre-Marzo) | UTC+1 | `0 8` (9:00) y `0 16` (17:00) |

> [!TIP]
> Para editarlo, abre el archivo `.yml`, pulsa el icono del lápiz ✏️, cambia las horas y haz clic en **Commit changes**.

---

## 🛠️ Mantenimiento
* **Si deja de funcionar:** Lo más probable es que el `refreshToken` haya caducado por falta de uso prolongado. Repite los **Pasos 2 y 3** con un token nuevo.
* **Logs:** Siempre puedes revisar la pestaña **Actions** para verificar si el fichaje de hoy ha sido exitoso.
