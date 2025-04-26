
# Despliegue de mi Aplicación PokeDex en Azure

En este documento te voy a explicar cómo desplegué mi proyecto PokeDex, desarrollado en Angular, en la nube de Microsoft Azure usando GitHub* como repositorio de origen.

---

Pasos que seguí para el despliegue

1. Creación de la Web App en Azure

* Ingresé al portal de Azure.
*  Busqué "App Services" y seleccioné Crear.
*   Configuré la Web App:
   - Nombre: pokedex.
   - Publicación: Código.
   - Pila de runtime: Node.js
   - Plan de App Service: Utilicé uno gratuito.
   - Revisé todo y creé la Web App.

2. Configuración del despliegue continuo desde GitHub

   * Abrí el recurso creado en Azure.
   * En el menú lateral, seleccioné Centro de implementación (Deployment Center).
   *  En Fuente, elegí GitHub.
   *   Autoricé a Azure para acceder a mi cuenta de GitHub.
   *   Seleccioné el repositorio donde estaba mi PokeDex y la rama `main`.
*  Configuré la construcción:
   - Framework: Node.js.
   - Comando de Build;
     ```bash
     npm install && npm run build -- --prod
     ```
   - Output Path: Especifiqué la carpeta `dist/`.

3. Guardé todos los cambios.

1. Ajustes adicionales que realicé

- Configuré variables de entorno, como `NODE_ENV=production`.
- Activé la opción Always On para mantener la aplicación siempre activa (si el plan lo permite).

4. Validación final

- Una vez que Azure terminó el despliegue, probé mi aplicación visitando la URL pública, por ejemplo:
  ```
  https://pokedex-loquesea.azurewebsites.net
  ```

---

 Cosas que tuve en cuenta

- Si la página no cargaba bien (errores 404), revisé que el `base-href` estuviera configurado correctamente:
  ```bash
  ng build --prod --base-href /
  ```

- Cada vez que hacía un `push` en GitHub, Azure automáticamente detectaba los cambios y actualizaba la app.


