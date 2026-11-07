GUARDIA PBA · PAQUETE PWA

CONTENIDO
- index.html: aplicación basada en el HTML original, conservando sus seis pestañas.
- manifest.webmanifest: datos de instalación PWA.
- service-worker.js: caché del shell para apertura sin conexión y actualización versionada.
- assets/: iconos de la aplicación.

INSTALACIÓN
1. Publicar TODO el contenido de esta carpeta en un hosting HTTPS, manteniendo la estructura.
2. Abrir la URL en Chrome para Android.
3. Menú ⋮ > Instalar aplicación (o Agregar a pantalla principal, según la versión).
4. Abrir Guardia PBA desde el icono. La primera apertura debe hacerse con internet para descargar el shell.

DATOS Y RESPALDOS
- Los datos de la app siguen guardándose localmente en el navegador (localStorage) y las fotos en IndexedDB.
- En Registro > Respaldo de datos se puede descargar un JSON con los registros y las fotos y luego importarlo.
- La importación reemplaza los datos locales; exportá una copia antes de restaurar.
- El archivo de respaldo NO está cifrado. Protegelo como información sensible.

LIMITACIONES IMPORTANTES
- Esta versión no incorpora bloqueo por PIN ni cifrado integral del almacenamiento local. El cifrado protege los archivos de respaldo, no los datos mientras permanecen dentro del navegador.
- No hay sincronización en nube ni acceso multiusuario.
- El modo offline cubre la interfaz y recursos locales; enlaces externos y WhatsApp requieren internet.
- No cargar información policial, personal o sensible real hasta completar una revisión de seguridad y validar el uso autorizado.
- La PWA requiere hosting HTTPS. Abrir index.html directamente como archivo no habilita instalación ni service worker.


SEGURIDAD LOCAL (v2)
- Al primer inicio se crea una contraseña de al menos 10 caracteres, con letras y números.
- Los datos de la aplicación se cifran con AES-256-GCM; la clave se deriva mediante PBKDF2-SHA-256 (310.000 iteraciones).
- Las fotografías de IndexedDB también se cifran individualmente con AES-256-GCM.
- La app se bloquea tras 5 minutos sin actividad y al volver de segundo plano aplica un bloqueo diferido.
- Los datos antiguos guardados sin cifrar se migran al crear el PIN; las fotos antiguas se migran al desbloquear.
- Los respaldos exportados se cifran aparte con una contraseña elegida al exportar. La contraseña del respaldo puede ser distinta de la contraseña de la app.
- No existe recuperación de la contraseña. Si se pierde, los datos locales cifrados no se pueden recuperar. Guardá un respaldo cifrado y conservá su contraseña.
- El cifrado requiere HTTPS y un navegador compatible con Web Crypto. No abrir index.html directamente como archivo.
- La app no cifra datos que el usuario copie a WhatsApp, comparta o exporte fuera de ella.
- Esto es protección local del navegador, no una certificación institucional ni una auditoría de seguridad. Validar autorización y política de datos antes de cargar información real.


HUELLA Y CAMBIOS (v3)
- Desbloqueo con huella: Más > Mis datos > Huella > Activar huella. Se crea una llave de acceso (passkey) del teléfono.
- La huella no reemplaza el cifrado: la llave de acceso (extensión PRF de WebAuthn) protege una copia de la clave de datos. Sin huella ni contraseña, los datos siguen ilegibles.
- La contraseña sigue funcionando siempre y es la única forma de recuperar el acceso si la huella falla o cambiás de teléfono.
- Quien conozca el PIN de desbloqueo del teléfono puede usarlo en lugar de la huella. Usá un bloqueo de pantalla seguro.
- La llave de acceso puede sincronizarse con tu cuenta de Google: otro teléfono con esa cuenta también podría desbloquear.
- Requiere HTTPS, bloqueo de pantalla con huella y Chrome actualizado. Si el teléfono no admite huella para cifrar, la app lo avisa y se sigue usando la contraseña.
- Si se crea una contraseña nueva desde cero, la huella anterior se desactiva y hay que volver a activarla.
- Corregido: teclado de texto para la contraseña, ajustes de datos viejos que no se aplicaban, diálogos propios en lugar de los avisos del navegador, y el bloqueo automático ya no se duplica.
- Probado con una huella simulada en Chrome. Falta la prueba en un teléfono real.
