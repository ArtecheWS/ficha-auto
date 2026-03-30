# ficha-auto

Fichaje automático en [Ficha.Work](https://app.ficha.work) mediante GitHub Actions. Se ejecuta de lunes a viernes a las 9:00 (entrada) y 17:00 (salida), **sin necesidad de tener el ordenador encendido**.

- Salta los festivos del calendario laboral de la empresa
- - Salta los días de vacaciones registrados en Ficha.Work
  - - Token de sesión renovado automáticamente en cada ejecución
    - - Logs de cada fichaje visibles en la pestaña Actions de GitHub
     
      - ---

      ## Tutorial: cómo configurarlo en tu cuenta

      Cada persona debe hacer una copia de este repositorio y configurar su propio token. Sigue los pasos:

      ### Paso 1 — Crea tu cuenta en GitHub

      Si no tienes cuenta, créala gratis en [github.com](https://github.com). Si ya tienes, inicia sesión.

      ### Paso 2 — Haz un fork de este repositorio

      1. Entra en este repositorio
      2. 2. Haz clic en el botón **Fork** (arriba a la derecha)
         3. 3. Deja las opciones por defecto y haz clic en **Create fork**
           
            4. Ahora tienes tu propia copia del repositorio en tu cuenta de GitHub.
           
            5. ### Paso 3 — Obtén tu Refresh Token de Ficha.Work
           
            6. 1. Abre [app.ficha.work](https://app.ficha.work) en tu navegador e inicia sesión
               2. 2. Pulsa **F12** para abrir las herramientas de desarrollador
                  3. 3. Ve a la pestaña **Application** (Chrome) o **Storage** (Firefox)
                     4. 4. En el panel izquierdo haz clic en **Local Storage** → `https://app.ficha.work`
                        5. 5. Busca la fila que se llama **refreshToken**
                           6. 6. Copia el valor (es un texto muy largo)
                             
                              7. > ⚠️ Este token es como una contraseña. No lo compartas con nadie ni lo pegues en ningún sitio que no sea el secret de tu repositorio privado.
                                 >
                                 > ### Paso 4 — Añade el token como secret en tu repositorio
                                 >
                                 > 1. En tu repositorio (el fork), ve a **Settings** (pestaña superior)
                                 > 2. 2. En el menú izquierdo haz clic en **Secrets and variables** → **Actions**
                                 >    3. 3. Haz clic en **New repository secret**
                                 >       4. 4. En **Name** escribe exactamente: `REFRESH_TOKEN`
                                 >          5. 5. En **Secret** pega el valor que copiaste en el paso anterior
                                 >             6. 6. Haz clic en **Add secret**
                                 >               
                                 >                7. ### Paso 5 — Activa los workflows en tu fork
                                 >               
                                 >                8. GitHub desactiva los Actions automáticamente en los forks. Para activarlos:
                                 >               
                                 >                9. 1. Ve a la pestaña **Actions** de tu repositorio
                                 >                   2. 2. Verás un aviso que dice que los workflows están desactivados
                                 >                      3. 3. Haz clic en **I understand my workflows, go ahead and enable them**
                                 >
                                 > ### Paso 6 — Prueba que funciona
                                 >
                                 > 1. Ve a la pestaña **Actions**
                                 > 2. 2. En el panel izquierdo haz clic en **Fichaje automatico Ficha.Work**
                                 >    3. 3. Haz clic en **Run workflow** → **Run workflow**
                                 >       4. 4. Espera unos segundos y recarga la página
                                 >          5. 5. Verás una ejecución en la lista. Haz clic en ella para ver el log y confirmar que el fichaje se ha realizado correctamente
                                 >            
                                 >             6. ¡Listo! A partir de ahora se fichará automáticamente cada día laborable.
                                 >            
                                 >             7. ---
                                 >            
                                 >             8. ## Ajuste de horario (cambio de hora invierno/verano)
                                 >
                                 > GitHub Actions trabaja en UTC. España usa:
                                 > - **Verano (marzo–octubre):** UTC+2 → cron `0 7` = 9:00 y `0 15` = 17:00
                                 > - - **Invierno (octubre–marzo):** UTC+1 → cron `0 8` = 9:00 y `0 16` = 17:00
                                 >  
                                 >   - Para cambiar el horario edita el archivo `.github/workflows/fichar.yml` haciendo clic en él y luego en el icono del lápiz ✏️.
                                 >  
                                 >   - ## Renovar el token si deja de funcionar
                                 >  
                                 >   - El `refreshToken` caduca si no se usa durante un periodo prolongado. Si el script empieza a fallar, repite el **Paso 3** y **Paso 4** con el nuevo token.
