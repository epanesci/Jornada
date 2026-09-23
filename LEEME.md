# Jornada: guía de instalación

Jornada es la app de turnos, briefing del día y mensajes de tu equipo. Esta guía explica cómo publicarla en internet con **Firebase**, que guarda los datos y los inicios de sesión, **GitHub**, que guarda los archivos, y **Netlify**, que la publica en una dirección web. Los tres son gratis para un equipo pequeño.

Tiempo aproximado: 30–40 minutos la primera vez.

---

## Paso 1: Firebase (datos e inicio de sesión)

1. Entra en **https://console.firebase.google.com** con tu cuenta de Google.
2. Pulsa **Crear un proyecto**. Ponle de nombre `jornada`. Cuando te pregunte por Google Analytics, **desactívalo**, porque no hace falta. Espera a que termine.
3. **Registra la app web:**
   - En la página principal del proyecto, pulsa el icono **`</>`** (Web).
   - Ponle de apodo `Jornada`. **No** marques "Firebase Hosting".
   - Pulsa **Registrar app**. Aparece un bloque de código con `const firebaseConfig = { apiKey: "...", ... }`.
   - Abre el archivo **`firebase-config.js`** de esta carpeta con cualquier editor de texto (el Bloc de notas sirve) y sustituye los valores de ejemplo por los tuyos: `apiKey`, `authDomain`, `projectId`, etc. Guarda el archivo.
   - Si te resulta más fácil, copia ese bloque y pásamelo en el chat: yo te devuelvo el archivo ya relleno. Estos datos no son secretos.
4. **Activa el inicio de sesión:**
   - En el menú de la izquierda: **Compilación → Authentication → Comenzar**.
   - En la pestaña **Método de acceso**, activa **Correo electrónico/contraseña** y guarda.
   - Activa también **Google**, elige tu correo como "correo de asistencia" y guarda.
5. **Crea la base de datos:**
   - Menú izquierdo: **Compilación → Firestore Database → Crear base de datos**.
   - Ubicación: elige una de Europa (por ejemplo `eur3` o `europe-west`). Esto no se puede cambiar después.
   - Elige **modo de producción** y créala.
   - Ve a la pestaña **Reglas**, borra todo lo que haya y pega el contenido completo del archivo **`firestore.rules`**. Pulsa **Publicar**.

   Las reglas son la seguridad de la app: solo entran personas con sesión iniciada, solo los gestores cambian horarios, y los mensajes directos solo los leen sus dos participantes.

---

## Paso 2: GitHub (guardar los archivos)

1. Entra en **https://github.com** y crea una cuenta si no tienes.
2. Ve a **https://github.com/new**:
   - En "Repository name" escribe `jornada`.
   - Puede ser **Private** (privado).
   - Pulsa **Create repository**.
3. En la página del repositorio vacío, pulsa el enlace **"uploading an existing file"**.
4. Arrastra **todos los archivos de esta carpeta, incluida la carpeta `icons`**. Asegúrate de que `firebase-config.js` ya tiene tus datos.
5. Abajo, pulsa **Commit changes**.

---

## Paso 3: Netlify (publicar la web)

1. Entra en **https://app.netlify.com** y pulsa **Sign up with GitHub**.
2. Pulsa **Add new site → Import an existing project → GitHub**, autoriza el acceso y elige el repositorio `jornada`.
3. Deja **Build command** vacío. En **Publish directory** escribe un punto: `.`
4. Pulsa **Deploy**. En un minuto tendrás una dirección tipo `https://algo-raro-123.netlify.app`.
5. Si quieres un nombre más bonito, ve a **Site configuration → Change site name**. Por ejemplo, `jornada-mirestaurante` da `https://jornada-mirestaurante.netlify.app`.

---

## Paso 4: autorizar tu dirección en Firebase

Sin este paso, el inicio de sesión dará error.

1. En Firebase: **Authentication → Configuración (Settings) → Dominios autorizados**.
2. Pulsa **Agregar dominio** y escribe tu dirección de Netlify **sin** `https://`, por ejemplo `jornada-mirestaurante.netlify.app`.

---

## Paso 5: primer uso (hazlo tú antes que nadie)

1. Abre tu dirección de Netlify.
2. Pulsa **Crear cuenta**, o entra con Google.
3. Arriba aparecerá **"Esta app aún no tiene administrador"**. Pulsa **Ser el administrador**.

   La primera persona que pulse ese botón queda como administrador principal para siempre, así que hazlo tú primero.
4. Ve a **Equipo → + Persona** y añade a tu gente. En tu propia ficha, en "Cuenta en la app", elige tu cuenta. Así verás tus turnos en la pantalla Hoy.

---

## Paso 6: instalar en el móvil

- **Android (Chrome):** abre la dirección. La app te ofrecerá un botón **Instalar**. Si no aparece, usa el menú ⋮ → **Instalar app**.
- **iPhone (Safari):** abre la dirección, pulsa el botón **Compartir** (el cuadrado con la flecha) y luego **Añadir a pantalla de inicio**.

Se abre a pantalla completa con su icono, como cualquier app.

En iPhone, si "Entrar con Google" falla dentro de la app instalada, usa correo y contraseña.

---

## Paso 7: invitar al equipo

1. Envía la dirección web a tus compañeros por WhatsApp o correo.
2. Cada uno crea su cuenta.
3. En **Equipo**:
   - Abre la ficha de cada persona y, en **"Cuenta en la app"**, elige su cuenta. Así cada uno ve "Tú" y sus turnos.
   - En **Accesos a la app**, pulsa **Hacer gestor** a quien deba poder cambiar horarios y el briefing. El resto solo puede verlos y usar los mensajes.

---

## Hacer cambios más adelante

Cuando cambies un archivo en GitHub (por ejemplo, si te paso una versión nueva, la subes con **Add file → Upload files**), Netlify publica la nueva versión sola en un minuto. Los datos del equipo no se pierden.

## Límites del plan gratis

- **Firebase (plan Spark):** unas 50.000 lecturas y 20.000 escrituras al día. Sobra para un equipo de 5 a 30 personas.
- **Netlify:** gratis para una web como esta.

## Qué hay en esta carpeta

| Archivo | Para qué sirve |
|---|---|
| `index.html` | La app completa |
| `firebase-config.js` | Los datos de tu proyecto de Firebase (lo rellenas tú) |
| `firestore.rules` | Las reglas de seguridad, que se pegan en Firebase |
| `manifest.webmanifest`, `sw.js`, `icons/` | Permiten instalarla en el móvil |
| `netlify.toml` | Ajustes para Netlify |
