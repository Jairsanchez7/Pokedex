
# Despliegue de mi Aplicación PokeDex en Azure

En este documento te voy a explicar cómo desplegué mi proyecto **PokeDex**, desarrollado en **Angular**, en la nube de **Microsoft Azure** usando **GitHub** como repositorio de origen.

---

## Requisitos previos

Antes de comenzar, necesité tener:

- Una cuenta activa en [Microsoft Azure](https://portal.azure.com/).
- Una cuenta en [GitHub](https://github.com/).
- Mi proyecto **PokeDex** desarrollado en Angular y subido a GitHub.
- Angular CLI instalado (`npm install -g @angular/cli`).

## Pasos que seguí para el despliegue

### 1. Creación de la Web App en Azure

1. Ingresé al portal de Azure.
2. Busqué **"App Services"** y seleccioné **Crear**.
3. Configuré la Web App:
   - **Nombre**: pokedex (debe ser único).
   - **Publicación**: Código.
   - **Pila de runtime**: Node.js (versión estable recomendada).
   - **Plan de App Service**: Utilicé uno gratuito.

4. Revisé todo y creé la Web App.

### 2. Configuración del despliegue continuo desde GitHub

1. Abrí el recurso creado en Azure.
2. En el menú lateral, seleccioné **Centro de implementación** (Deployment Center).
3. En **Fuente**, elegí **GitHub**.
4. Autoricé a Azure para acceder a mi cuenta de GitHub.
5. Seleccioné el repositorio donde estaba mi PokeDex y la rama `main`.
6. Configuré la construcción:
   - **Framework**: Node.js.
   - **Comando de Build**:
     ```bash
     npm install && npm run build -- --prod
     ```

7. Guardé todos los cambios.


### 5. Aumentar la seguridad de la aplicación

Para mejorar la seguridad de mi PokeDex, añadí un archivo llamado **staticwebapp.config.json** en el directorio de despliegue. Su contenido fue el siguiente:

```json
{
  "globalHeaders": {
    "Content-Security-Policy": "default-src * 'unsafe-inline' 'unsafe-eval' data: blob:;",
    "X-Frame-Options": "ALLOWALL",
    "Permissions-Policy": "geolocation=*, camera=*, microphone=*"
  }
}
```

Este archivo permite establecer políticas de seguridad importantes como:
- Controlar el contenido que puede ser cargado (CSP).
- Permitir el uso de la aplicación dentro de iframes (X-Frame-Options).
- Configurar permisos de acceso a geolocalización, cámara y micrófono (Permissions-Policy).

### 5. Validación final

- Una vez que Azure terminó el despliegue, probé mi aplicación visitando la URL pública, por ejemplo:
  ```
  (https://lemon-wave-0a0c0201e.6.azurestaticapps.net/)
  ```

---



