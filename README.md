# Módulo de Clima y GPS (Kotlin)

Este repositorio se encarga de leer la ubicación real del usuario y descargar el clima actual usando la API de Open-Meteo. 

Está diseñado para que el resto del equipo solo tenga que llamar a una función y recibir los datos limpios, sin preocuparse de cómo funciona por debajo.

## ¿Qué hace cada archivo?

* **OpenMeteoApi.kt**: Es la conexión pura con internet. Aquí está la configuración para hablar con la API del tiempo y el molde para guardar la temperatura y la humedad que nos devuelven.
* **GestorClima.kt**: Es el motor principal. Cuando lo llamas, obliga a la antena GPS a encenderse y buscar tu coordenada exacta en ese momento (no usa posiciones antiguas guardadas). Luego le pasa esa coordenada a la API y te devuelve los grados y la humedad.
* **MainActivity.kt**: Es una pantalla de prueba que hemos dejado montada para que puedas comprobar que todo funciona pulsando un botón, antes de integrarlo en la interfaz definitiva del proyecto.

## ¿Cómo integrarlo en el proyecto principal?

Para que este código funcione al juntarlo con el resto de la aplicación, hay que añadir estas configuraciones:

1. **Permisos en el AndroidManifest.xml**:
Asegúrate de poner estos tres permisos antes de la etiqueta `<application>`:
`<uses-permission android:name="android.permission.INTERNET" />`
`<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />`
`<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />`

2. **Dependencias en el build.gradle.kts (Module :app)**:
Hay que añadir estas 5 herramientas para que el GPS, la conexión a internet y las tareas en segundo plano funcionen:
`implementation("com.squareup.retrofit2:retrofit:2.9.0")`
`implementation("com.squareup.retrofit2:converter-gson:2.9.0")`
`implementation("com.google.android.gms:play-services-location:21.0.1")`
`implementation("org.jetbrains.kotlinx:kotlinx-coroutines-play-services:1.7.3")`
`implementation("androidx.lifecycle:lifecycle-runtime-ktx:2.7.0")`

## ¿Cómo probarlo?

Hemos dejado todo preparado para que la prueba sea instantánea:

1. Dale al botón de **Run** (el triángulo verde) en Android Studio para instalar la app.
2. **Si usas el emulador:** Como el móvil virtual no tiene GPS real, tienes que darle una ubicación a mano. Haz clic en los tres puntos verticales (...) del menú lateral del emulador (Extended Controls). Ve a la pestaña **Location**, busca una ciudad en el mapa (por ejemplo, Madrid, España) y pulsa el botón **Set Location**. 
3. Al abrirse la app en la pantalla, acepta los permisos de ubicación que te pide.
4. Pulsa el botón **"Actualizar Clima"** que aparece en el centro.

Para comprobar la telemetría y ver exactamente qué está pasando por debajo, abre la pestaña **Logcat** (abajo en Android Studio) y escribe en el buscador del filtro: **PRUEBA_ROBERTO**

Ahí podrás ver en tiempo real:
* Si se han dado correctamente los permisos del GPS.
* Las coordenadas exactas (latitud y longitud) frescas que detecta el móvil.
* La telemetría de la API del tiempo (los datos de temperatura y humedad descargados).

## Licencia

Este repositorio se distribuye bajo la Licencia MIT. Esto significa que el código es totalmente libre: se puede usar, copiar, modificar y distribuir sin restricciones para integrarlo en la aplicación final.
