# Publicación pública en GitHub Pages

El tablero está preparado para que cualquier persona con el enlace pueda ver,
buscar, filtrar y descargar la información sin iniciar sesión. Microsoft 365 se
usa únicamente para habilitar la edición del administrador.

La información visible forma parte de `index.html`. No publiques datos que no
deban ser accesibles para cualquier visitante. El Excel original debe permanecer
en SharePoint Online o OneDrive para la Empresa.

## 1. Configuración terminada

`microsoft365.config.json` ya contiene el inquilino, la aplicación SPA, el
enlace institucional del Excel, la hoja y el correo de la cuenta administradora
(`institucional.jaac@ucacue.edu.ec`).
No es necesario cambiarlo para esta publicación.

La configuración es cerrada por defecto: una cuenta cuyo correo u Object ID no coincida
con el autorizado no puede activar la edición.

## 2. Registrar la aplicación en Microsoft Entra ID

Registra como URI de redirección de tipo SPA la dirección exacta:

`https://dac-institucional.github.io/PMCA/`

Agrega los permisos delegados de Microsoft Graph `User.Read` y
`Files.ReadWrite`. No agregues un secreto al HTML.

Si la política institucional lo permite, activa **Assignment required** en la
aplicación empresarial y asigna únicamente tu usuario. Así otra cuenta ni
siquiera podrá usar la aplicación para iniciar sesión.

## 3. Proteger realmente el Excel y el código

En SharePoint o OneDrive, solo tu cuenta debe tener **Puede editar**. Las demás
cuentas no necesitan acceso al archivo, porque consultan la copia pública
incluida en el sitio. Si el Excel hereda permisos de edición de una carpeta,
rompe la herencia o muévelo a una carpeta dedicada.

En GitHub, conserva únicamente tu cuenta con permiso de escritura sobre el
repositorio. Un repositorio público permite leer y copiar el código, pero no
modificar tu publicación sin permiso de colaborador.

La lista `adminEmails` del navegador mejora la experiencia, pero la seguridad
real depende de los permisos del Excel, la asignación de Entra ID y los permisos
del repositorio.

## 4. Publicar

Sube estos cuatro archivos a la raíz del repositorio `DAC-INSTITUCIONAL/PMCA`:

- `index.html`
- `microsoft365.config.json`
- `.nojekyll`
- `README_GITHUB.md`

En GitHub abre **Settings → Pages**, selecciona **Deploy from a branch**, la
rama `main` y la carpeta `/ (root)`. La dirección pública será:

`https://dac-institucional.github.io/PMCA/`

GitHub Pages es un alojamiento estático. Cuando cambie el Excel, la sesión del
administrador podrá leer y editar la versión vigente, pero los demás visitantes
verán la última copia publicada en `index.html`. Para que todos vean los cambios,
genera nuevamente el HTML con los datos actualizados y publícalo. Una
actualización automática requiere un flujo adicional de GitHub Actions o un
servicio intermedio con credenciales protegidas; esas credenciales nunca deben
guardarse en el HTML.
