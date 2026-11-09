# 📱 App con Tareas en Segundo Plano y Notificaciones

Ejercicio práctico en **Flutter (Android)** que muestra cómo ejecutar tareas en segundo plano y programar notificaciones locales, con una interfaz moderna en Material 3.

## 🎯 Objetivos de aprendizaje

- Crear una app en Flutter desde cero
- Ejecutar tareas en segundo plano
- Programar notificaciones locales
- Diseñar una interfaz moderna

## 🧰 Tecnologías

- Flutter / Dart (SDK ^3.7.0)
- `workmanager` ^0.9.0+3
- `flutter_local_notifications` ^17.2.2
- `timezone` ^0.9.4

## ✨ Funcionalidades

- **Sync periódico:** tarea automática cada 15 minutos (mínimo en Android).
- **Ejecutar ahora:** lanza la tarea de sincronización de inmediato para pruebas.
- **Notificaciones programadas:** recordatorio a los 10 segundos o a 1 minuto.
- **Navegación desde notificación:** al tocarla se abre la pantalla *Detalle*.
- **Log de actividad:** registro en pantalla de las acciones de la app.

## 📂 Contenido del repositorio

Este repositorio contiene el archivo principal de la aplicación:

- `main.dart`: interfaz, notificaciones y navegación de la app.

## 🚀 Cómo usarlo

1. Crea un proyecto Flutter:
   ```bash
   flutter create background_app
   cd background_app
   ```
2. Agrega las dependencias en `pubspec.yaml` y ejecuta `flutter pub get`.
3. Reemplaza `lib/main.dart` por el archivo de este repositorio.
4. Conecta un dispositivo Android o emulador y ejecuta:
   ```bash
   flutter run
   ```

> En Android 13+ acepta el permiso de notificaciones cuando el sistema lo solicite.

## 🧪 Cómo probar

1. **Ejecutar Ahora (prueba):** aparece una notificación con la hora actual y se registra en el log.
2. **Notificar en 10 segundos / 1 minuto:** aparece la notificación programada.
3. **Tocar la notificación:** se abre la pantalla *Detalle*.
4. **Activar Sync Periódico:** el botón cambia a *Detener Sync* y el estado se actualiza.

## 🧠 Análisis

1. **Tarea en segundo plano:** trabajo que la app realiza sin estar abierta (sincronizar datos, avisos); mantiene la información actualizada.
2. **`registerOneOffTask` vs `Future.delayed`:** el primero lo ejecuta el sistema (WorkManager) aunque la app se cierre; `Future.delayed` solo funciona mientras la app está en ejecución.
3. **`Future.delayed` en lugar de un bucle:** es asíncrono y no bloquea la interfaz ni gasta CPU.
4. **WorkManager vs `Timer`:** respeta restricciones (red, batería) y sobrevive al cierre de la app y reinicios; un `Timer` muere con el proceso.
5. **App cerrada con tarea periódica:** Android sigue ejecutándola y corre el `callbackDispatcher` según el intervalo y restricciones.

