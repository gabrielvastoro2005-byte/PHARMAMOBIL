# Guía de entrega — Actividad Autónoma N.º 09

## Producto 1 — Inventario
Registrar Formato de moneda, Compartidor, platformModule e InfoDispositivo. En cada fila colocar firma/contrato, API Android, API iOS y rutas exactas de `commonMain`, `androidMain`, `iosMain`.

## Producto 2 — Informe comparativo (600–900 palabras)
Responder con el código y resultados reales:
1. Por qué el formato monetario difiere entre JVM y Foundation aun usando es-PE.
2. Por qué CompartidorAndroid necesita Context y CompartidorIos no.
3. Qué cambiaría usando interfaz + DI en vez de expect/actual.
4. Qué ocurre cuando falta un actual. Incluir error literal y captura.
5. Qué capacidad de PharmaMobil debe permanecer en commonMain y por qué.

## Producto 3 — Tercera capacidad
InfoDispositivo:
- expect en commonMain.
- actual Android con Build.VERSION.RELEASE.
- actual iOS con UIDevice.
- interfaz: pestaña Acerca de.

## Producto 4 — Evidencias
1. Precio Android/iOS lado a lado.
2. Compartir Android/iOS.
3. InfoDispositivo Android/iOS.
4. Error literal de compilación.
5. Rama + commits.
6. README con “Código específico de plataforma”.

## Commits sugeridos
- `docs: inventario de capacidades nativas sesion 09`
- `docs: informe comparativo android ios`
- `feat: agregar informacion de dispositivo con expect actual`
- `docs: agregar evidencias y actualizar README`
