Para llevar este proyecto al siguiente nivel, es fundamental preparar tu entorno de desarrollo. La herramienta **Firebase CLI** es el puente que conecta tu código en Flutter con los servicios en la nube de Google.

Aquí tienes la guía técnica paso a paso para configurar tu estación de trabajo.

---

## 🟢 1. Software necesario: Node.js y NPM
Para usar Firebase CLI, necesitas **Node.js**, un entorno de ejecución que incluye **NPM** (Node Package Manager), el cual permite instalar herramientas de forma global en tu sistema.

### Cómo verificar si ya los tienes:
Abre tu terminal (PowerShell o CMD) y escribe:
* `node -v`
* `npm -v`

Si ves un número de versión (ej. `v20.10.0`), ¡ya estás listo! Si aparece un error, sigue el proceso de instalación.

### Instalación paso a paso en Windows:
1.  **Descarga:** Ve al sitio oficial [nodejs.org](https://nodejs.org/) y elige la versión **LTS** (es la más estable para estudiantes).
2.  **Instalación:** Ejecuta el archivo `.msi` descargado.
3.  **Configuración:** Dale "Next" a todo, pero asegúrate de que la casilla **"Add to PATH"** esté marcada (esto es lo que permite usar los comandos de manera global).
4.  **Reinicio:** Es vital cerrar y volver a abrir tu terminal para que reconozca los nuevos comandos.

---

## 🛠️ 2. Instalación de Firebase CLI (Global)
Una vez que NPM funciona, instalaremos las herramientas de Firebase para que estén disponibles en cualquier carpeta de tu computadora.

### El comando mágico:
En tu terminal, escribe el siguiente comando:
```bash
npm install -g firebase-tools
```
> **Nota:** El parámetro `-g` significa **Global**. Esto permite que el comando `firebase` funcione tanto en tu carpeta `crudoxxo` como en cualquier otro proyecto futuro.



---

## 🔑 3. Acceso y Comandos de Firebase

### Cómo acceder con tu Cuenta de Google
Para que Firebase sepa quién eres y te permita modificar tus bases de datos, debes autenticarte:

1.  En la terminal escribe: `firebase login`
2.  Se abrirá automáticamente una ventana en tu navegador.
3.  Selecciona tu cuenta de Google (la misma que usaste en la Consola de Firebase).
4.  Haz clic en "Permitir". 
5.  ¡Listo! En la terminal verás un mensaje de éxito: *Success! Logged in as usuario@gmail.com*.

### Cómo usar firebase-tools en tu proyecto
Una vez logueado, estos son los comandos que más usarás como "Software Creator":

* **`firebase projects:list`**: Muestra todos tus proyectos creados en la consola (aquí deberías ver tu proyecto `crudoxxo`).
* **`firebase init`**: Este comando inicia un asistente dentro de tu carpeta `crudoxxo` para conectar las funciones de Firestore.
* **`firebase deploy`**: Envía tus reglas de seguridad o configuraciones de hosting a la nube.

---

## 🚀 4. Integración Específica con Flutter (FlutterFire CLI)
Aunque ya tienes Firebase CLI, Flutter requiere una herramienta adicional para configurar automáticamente los archivos de Android e iOS:

1.  **Instalar FlutterFire CLI:**
    ```bash
    dart pub global activate flutterfire_cli
    ```
2.  **Configurar el proyecto:**
    Dentro de tu carpeta `xflutternava1777/crudoxxo`, ejecuta:
    ```bash
    flutterfire configure
    ```
    Este comando te pedirá seleccionar tu proyecto de la lista y **generará automáticamente** el archivo `firebase_options.dart`, ahorrándote horas de configuración manual.



---

### Flujo de trabajo para el estudiante:
1.  **Instalas Node.js** (El motor).
2.  **Instalas Firebase Tools** con NPM (La herramienta).
3.  **Te logueas** con Google (La llave).
4.  **Configuras con FlutterFire** (El puente).

¿Lograste visualizar el número de versión de NPM en tu terminal o necesitas que revisemos algún error específico del instalador?
