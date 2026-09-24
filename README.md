# Guía de Instalación Entorno Flutter

---

## Requisitos 

- Windows 10/11 (64 bits)
- [Git para Windows](https://git-scm.com/download/win) 
- Un teléfono Android (o emulador)
- Espacio en disco: ~5 GB entre SDK de Flutter, Android Studio y componentes

---

## Paso 1 — Instalar el SDK de Flutter

1. Descargar el SDK desde la página oficial: <https://docs.flutter.dev/get-started/install/windows>

2. **IMPORTANTE:** extraer el ZIP en una ruta **sin espacios** y **fuera de OneDrive**. Ubicación recomendada:

   ```
   C:\flutter
   ```
   
---

## Paso 2 — Agregar Flutter al PATH

1. Menú Inicio → buscar **"Variables de entorno"** → *"Editar las variables de entorno del sistema"*
2. Botón **Variables de entorno**
3. En **Variables de usuario**, seleccionar la variable **`Path`** → **Editar**
4. Clic en **Nuevo** y agregar:

   ```
   C:\flutter\bin
   ```

5. Aceptar todo.
6. Abrir una ventana CMD y probar:

   ```bash
   flutter --version
   ```

---

## Paso 3 — Instalar Android Studio

1. Descargar e instalar desde: <https://developer.android.com/studio>
2. Al abrirlo por primera vez, el asistente instala automáticamente:
   - Android SDK
   - SDK Platform-Tools
   - Android Emulator

---

## Paso 4 — Configurar componentes del SDK de Android

En **Android Studio → Settings → Languages & Frameworks → Android SDK**
(o en pantalla de bienvenida: **More Actions → SDK Manager**)

**Pestaña "SDK Platforms":**
- Marcar **Android API 36** (Android 16 "Baklava", versión 36.0). Flutter 3.47.5 lo requiere específicamente.

**Pestaña "SDK Tools"** (activar *"Show Package Details"* abajo a la derecha):
- **Android SDK Build-Tools 28.0.3** (Flutter la pide explícitamente)
- **Android SDK Command-line Tools** → instalar la versión **20.0**, **NO** la 23.0 "(latest)".
  > La 23.0 tiene un bug de incompatibilidad con Flutter que deja el estado de licencias como "unknown" y no permite aceptarlas.
- **Google USB Driver** (necesario para que Windows reconozca el teléfono)

Aplicar (**Apply**) y dejar descargar.

---

## Paso 5 — Aceptar licencias de Android

En CMD:

```bash
flutter doctor --android-licenses
```

Responder `y` a todas.

---

## Paso 6 — Verificar el entorno

```bash
flutter doctor
```

**Objetivo mínimo para desarrollar Android:**

```
[√] Flutter
[√] Android toolchain
[√] Connected device
```

**Se pueden IGNORAR** (no aplican para apps Android):

```
[X] Chrome           -> solo para desarrollo web
[X] Visual Studio    -> solo para apps de escritorio Windows
```

> **Advertencia `[!]` de espacios en la ruta del SDK de Android:**
> Para apps normales en Dart se puede ignorar. 

---

## Paso 7 — Conectar el teléfono Android físico

### En el teléfono

1. **Activar Opciones de desarrollador:** Ajustes → Acerca del teléfono → tocar **"Número de compilación" 7 veces**.
2. **Activar en Opciones de desarrollador:**
   - Depuración USB
3. Conectar por cable USB.
4. Al conectar, bajar la barra de notificaciones y cambiar el modo USB a **"Transferir archivos (MTP)"** o **"PTP"**.
5. Aceptar el popup **"¿Permitir depuración USB?"** → marcar **"Siempre permitir"**.


### En el PC — verificar la conexión

```bash
flutter devices
```

Debe listar el teléfono.

---

## Paso 8 — Crear y correr el primer proyecto

2. Crear el proyecto:

   ```bash
   cd C:\dev
   flutter create mi_app
   cd mi_app
   ```

3. Correr la app en el teléfono:

   ```bash
   flutter run
   ```

   Si hay varios dispositivos, elegir el del teléfono, o indicarlo por ID:

   ```bash
   flutter run -d <ID_DEL_DISPOSITIVO>
   ```

   > **NOTA:** la primera compilación tarda varios minutos (Gradle descarga dependencias). Las siguientes son mucho más rápidas.

4. **Teclas útiles** mientras corre:

   | Tecla | Acción |
   |---|---|
   | `r` | Hot reload (aplica cambios al instante) |
   | `R` | Hot restart (reinicia la app) |
   | `q` | Salir |

5. El código de la app está en: `lib/main.dart`

---


## Notas finales

- El **editor** puede ser VS Code, Windsurf o Antigravity (todos son forks de VS Code). Instalar las extensiones **"Flutter"** y **"Dart"** en el editor elegido.
- **NO** es necesario tener Android Studio **abierto** para desarrollar. Solo se usa para lanzar emuladores o gestionar el SDK (esporádico). Con teléfono físico NO hace falta abrirlo.
- **Estructura final recomendada:**

  ```
  C:\flutter          -> SDK de Flutter (binarios)
  C:\dev\mi_app       -> proyectos
  ```

  ```bash
  flutter doctor
  ```
