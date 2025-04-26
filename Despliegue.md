
# Despliegue de la Aplicación PokeDex a Azure

Este documento describe de manera clara y directa cómo desplegar o publicar el proyecto **PokeDex** desarrollado en **Angular** en la nube de **Microsoft Azure** utilizando **GitHub** como repositorio fuente.

---

## Requisitos previos

Antes de iniciar, asegúrate de tener:

- Una cuenta activa en [Microsoft Azure](https://portal.azure.com/).
- Una cuenta en [GitHub](https://github.com/).
- El proyecto **PokeDex** ya desarrollado en Angular y subido a GitHub.
- Angular CLI instalado en tu máquina (`npm install -g @angular/cli`).

## Pasos para el despliegue

### 1. Crear una Web App en Azure

1. Ingresa al portal de Azure.
2. En el panel de búsqueda, escribe **"App Services"** y selecciona **Crear**.
3. Configura la Web App:
   - **Nombre**: pokedex-{loquesea} (debe ser único).
   - **Publicación**: Código.
   - **Pila de runtime**: Node.js (versión estable recomendada).
   - **Región**: Selecciona la más cercana a tu público objetivo.
   - **Plan de App Service**: Puedes usar uno gratuito (F1) para pruebas.

4. Haz clic en **Revisar y Crear**, luego en **Crear**.

### 2. Configurar despliegue continuo desde GitHub

1. Una vez creada la Web App, abre el recurso.
2. En el menú izquierdo, busca **Centro de implementación** o **Deployment Center**.
3. En **Fuente**, selecciona **GitHub**.
4. Autoriza a Azure para acceder a tu cuenta de GitHub si es necesario.
5. Escoge el repositorio donde está tu PokeDex y selecciona la rama que quieres desplegar (generalmente `main` o `master`).
6. Configura la construcción:
   - **Framework**: Selecciona **Node.js**.
   - **Comando de Build**: Usa el comando de Angular para compilar la app:
     ```bash
     npm install && npm run build -- --prod
     ```
   - **Página de inicio**: Azure necesita saber qué carpeta usar, por lo que debes indicar que el `outputPath` está en `dist/`.

7. Termina la configuración y guarda los cambios.

### 3. Ajustes adicionales (opcional pero recomendable)

- En la configuración de la App Service, establece las **Variables de entorno** para definir `NODE_ENV=production`.
- Puedes activar **Always On** si tu plan lo permite, para que la app no entre en "reposo".

### 4. Validación del despliegue

- Una vez que Azure termine de hacer el deploy, recibirás una notificación.
- Ve a la URL de tu Web App (ejemplo: `https://pokedex-loquesea.azurewebsites.net`) y verifica que tu PokeDex esté funcionando.

---

## Notas importantes

- **Errores comunes**: Si ves errores 404 o que la página no carga bien, revisa que tu Angular esté construyendo con `base-href` correcto.
  - Puedes ajustar en tu `angular.json` o construir así:
    ```bash
    ng build --prod --base-href /
    ```

- **Cambios futuros**: Cada vez que hagas "push" a la rama configurada en GitHub, Azure detecta los cambios y vuelve a desplegar automáticamente.

---

# Fin

✨ Ahora tienes tu proyecto **PokeDex** de Angular en la nube, disponible para todo el mundo.

¡Entrenadores, a capturar se ha dicho! 🌟🌊
