# ficha-auto

Fichaje automático en [Ficha.Work](https://app.ficha.work) mediante GitHub Actions. Se ejecuta de lunes a viernes a las 9:00 (entrada) y 17:00 (salida), sin necesidad de tener el ordenador encendido.

## Características

- Ficha entrada a las 9:00 y salida a las 17:00 automáticamente
- Salta los **festivos** del calendario laboral de la empresa
- Salta los días de **vacaciones** registrados en Ficha.Work
- No ficha en fin de semana
- Token de sesión renovado automáticamente en cada ejecución
- Logs de cada fichaje visibles en la pestaña Actions de GitHub

## Configuración

### 1. Añadir el secret REFRESH_TOKEN

Ve a **Settings → Secrets and variables → Actions → New repository secret** y crea un secret con:

- **Name:** `REFRESH_TOKEN`
- **Secret:** el valor de `refreshToken` de Ficha.Work

Para obtener el `refreshToken`:
1. Abre [app.ficha.work](https://app.ficha.work) en el navegador
2. Pulsa `F12` → pestaña **Application** → **Local Storage** → `app.ficha.work`
3. Copia el valor de `refreshToken`

> El `refreshToken` caduca si no se usa durante semanas. Si el script empieza a fallar, repite este paso.

### 2. Horario

El workflow está configurado en UTC. España está en **UTC+2** en verano y **UTC+1** en invierno.

| Hora Madrid | Cron (UTC verano) | Cron (UTC invierno) |
|-------------|-------------------|---------------------|
| 09:00       | `0 7 * * 1-5`     | `0 8 * * 1-5`       |
| 17:00       | `0 15 * * 1-5`    | `0 16 * * 1-5`      |

Si necesitas ajustar el horario en invierno, edita `.github/workflows/fichar.yml` y cambia los valores del cron.

## Ejecución manual

En la pestaña **Actions** de GitHub puedes ejecutar el workflow manualmente con el botón **Run workflow**. Útil para probar que funciona correctamente.

## Archivos

| Archivo | Descripción |
|---------|-------------|
| `fichawork.js` | Script principal de fichaje |
| `.github/workflows/fichar.yml` | Workflow de GitHub Actions con el cron |
