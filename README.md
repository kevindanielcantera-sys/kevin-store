# Kevin Store

Tienda estática, adaptable a celular y computador. Incluye catálogo, búsqueda, filtros, orden por precio, bolsa guardada en el navegador y pedidos por WhatsApp. El catálogo puede conectarse a Supabase sin servidor propio.

## Probar en el computador

Abre `index.html` en Chrome, Edge o Firefox. Verás productos de muestra. La bolsa funciona localmente. El botón `⌘` explica cómo activar el administrador; todavía no guarda productos porque eso requiere configurar Supabase y crear una cuenta protegida.

## Activar pedidos por WhatsApp

Edita `config.js` y escribe el número completo con código de país, solo dígitos. Para Colombia empieza por `57`, por ejemplo `573001234567`. No escribas `+`, espacios ni guiones. Guarda, recarga y prueba el botón de pedido.

## Conectar Supabase gratis

1. Crea un proyecto en [supabase.com](https://supabase.com/). El nivel gratuito puede ser suficiente para empezar; sus topes y condiciones pueden cambiar. En un proyecto gratuito, Supabase puede pausar proyectos con poca actividad y tiene límites de almacenamiento, tráfico y base de datos.
2. En **Project Settings → API** copia la **Project URL** y la clave pública **publishable** (o `anon` si la consola muestra el formato anterior). Pégalas en `supabaseUrl` y `supabaseAnonKey` dentro de `config.js`.
3. En **SQL Editor**, abre `supabase-schema.sql`, ejecútalo y revisa que la operación termine correctamente. El script configura el catálogo, los permisos y el bucket público `product-images` para las fotos. Si ya habías conectado Supabase, vuelve a ejecutar el script para añadir Storage.
4. En **Authentication → Users**, crea tu usuario con tu correo y una contraseña única. Desactiva el registro público de usuarios en **Authentication → Sign In / Providers** o en los ajustes de registro.
5. Copia el UUID de tu usuario. En el SQL Editor ejecuta `insert into public.store_admins (user_id) values ('TU-UUID');` reemplazando el texto por el UUID real.
6. Abre la tienda, pulsa `⌘` e ingresa con ese correo y contraseña. Ya podrás agregar, editar, ocultar y mostrar productos. Para cada producto, elige la foto en tu celular o computador (JPG, PNG, WebP o AVIF, máximo 5 MB); se subirá al almacenamiento de Supabase y aparecerá en la tienda. Las políticas RLS en la base de datos verifican el UUID; no basta con conocer la dirección de la página.

**Seguridad:** `config.js` es público porque el navegador lo descarga. Solo coloca la URL y clave pública de Supabase. Nunca pegues una clave `service_role` o `secret` en los archivos del sitio. La clave pública es segura únicamente mientras las políticas RLS estén habilitadas como en el SQL incluido. No publiques productos con datos privados.

## Publicar gratis con GitHub Pages

1. Crea o inicia sesión en [github.com](https://github.com/) y crea un repositorio público llamado `kevin-store`.
2. Sube el contenido de esta carpeta a la raíz del repositorio. Debes ver `index.html`, `styles.css`, `app.js`, `config.js` y `supabase-schema.sql` en la raíz.
3. En el repositorio abre **Settings → Pages**. En **Build and deployment**, selecciona **Deploy from a branch**, rama `main`, carpeta `/ (root)` y pulsa **Save**.
4. Espera a que GitHub Pages publique el sitio. La dirección gratuita será `https://TU-USUARIO.github.io/kevin-store/`.
5. Prueba el enlace en tu computador y en tu celular. Si cambias `config.js`, vuelve a subir el archivo para publicar la configuración.

## Costos y límites

- GitHub Pages, HTML, CSS y JavaScript: $0 para un sitio estático público dentro de las condiciones de GitHub Pages.
- Supabase: $0 mientras el proyecto se mantenga dentro del nivel gratuito; hay topes de base de datos, tráfico y almacenamiento de fotos, cambios de condiciones y posible pausa por inactividad. Optimiza las fotos y guarda una copia de los datos.
- WhatsApp: el enlace de pedido es gratuito, pero la conversación la atiendes tú. No hay pago en línea, cálculo automático de envío, inventario avanzado ni confirmación de pago.
- Dirección: se usa el subdominio gratuito de GitHub; un dominio propio normalmente cuesta dinero.
- Las fotos de demostración usan imágenes remotas de Unsplash. Reemplázalas por fotos propias y asegúrate de tener derecho a publicar cualquier imagen.

## Personalizar

Reemplaza nombre, precio, categoría y fotos de los productos de muestra en `app.js` antes de conectar Supabase. Con Supabase activo, la tabla será la fuente del catálogo. El checkout solicita disponibilidad y envío por WhatsApp, así que confirma esos detalles con cada cliente.
