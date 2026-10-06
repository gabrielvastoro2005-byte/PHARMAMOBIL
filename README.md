# PharmaMobil — Sesión 09

Proyecto Kotlin Multiplatform de **Desarrollo de Aplicaciones Móviles**. Esta versión conserva una estructura por capas y añade el trabajo de la Actividad Autónoma N.º 09: diferencias por plataforma mediante `expect/actual`.

## Abrir en Android Studio
1. Descomprime el ZIP.
2. Android Studio → **Open** → selecciona la carpeta raíz.
3. Espera el Gradle Sync.
4. Selecciona `androidApp` y un emulador.
5. Run ▶.

## Estructura
- `androidApp`: entrada Android.
- `shared/src/commonMain`: dominio, datos, casos de uso, presentación y contratos multiplataforma.
- `shared/src/androidMain`: implementaciones nativas Android.
- `shared/src/iosMain`: implementaciones nativas iOS.
- `iosApp`: proyecto Xcode para ejecutar el framework compartido en macOS.

## Funcionalidad de PharmaMobil
La pantalla Productos permite listar, buscar, registrar, editar y eliminar productos. Cada producto muestra código, laboratorio, stock y precio. El precio se obtiene mediante la capacidad nativa de formato de moneda y el botón Compartir usa la implementación nativa de cada plataforma.

## Código específico de plataforma

### 1. Formato de moneda
**expect:** `shared/src/commonMain/.../platform/FormatoMoneda.kt`
`expect fun formatearSoles(valor: Double): String`

- Android: `FormatoMoneda.android.kt` → `NumberFormat` + `Locale("es","PE")`.
- iOS: `FormatoMoneda.ios.kt` → `NSNumberFormatter` + `NSLocale("es_PE")`.

### 2. Compartir producto
**contrato común:** `shared/src/commonMain/.../platform/Compartidor.kt`

- Android: `CompartidorAndroid.kt` → `Intent.ACTION_SEND`; requiere `Context`.
- iOS: `CompartidorIos.kt` → `UIActivityViewController`.

### 3. Módulo de inyección
**expect:** `shared/src/commonMain/.../di/AppModule.kt`
`expect val platformModule: Module`

- Android: módulo Koin con `androidContext()`.
- iOS: módulo Koin sin contexto Android.

### 4. Información del dispositivo — Producto 3
**expect:** `shared/src/commonMain/.../platform/InfoDispositivo.kt`

```kotlin
expect class InfoDispositivo() {
    val sistema: String
    val version: String
}
```

- Android: `Build.VERSION.RELEASE`.
- iOS: `UIDevice.currentDevice.systemName/systemVersion`.
- Está conectada a la interfaz en la pestaña **Acerca de**.

## Aislamiento
`commonMain` no importa `android.*` ni `platform.*`. Las APIs nativas permanecen en sus source sets.

## Evidencias requeridas por la actividad
Se deben obtener de ejecuciones reales:
- Precio del mismo producto en Android e iOS.
- Selector/hoja Compartir en Android e iOS con el texto visible.
- Pantalla Acerca de en Android e iOS.
- Error literal del compilador al retirar temporalmente un `actual`.
- Enlace a la rama y commits.

La compilación iOS requiere macOS + Xcode.
