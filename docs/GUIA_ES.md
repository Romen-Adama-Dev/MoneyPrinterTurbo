# Guía en español: vídeos para promocionar una app

Esta edición de MoneyPrinterTurbo está preparada para abrir la interfaz en español. Su función es convertir un tema o guion en vídeos cortos: genera el texto con un modelo de IA, crea una locución, añade subtítulos y música, combina material visual y renderiza el resultado.

## ¿Sirve para promocionar una app?

Sí, como herramienta de producción. No sustituye la estrategia de marketing, la medición de conversiones ni la gestión de campañas. Funciona mejor si subes capturas, grabaciones verticales y demostraciones reales de tu app como **material local**. Pexels, Pixabay y Coverr son útiles como apoyo, pero no pueden mostrar tu producto.

El flujo recomendado para cada anuncio es:

1. Define una sola idea: problema, beneficio o caso de uso.
2. Prepara entre 3 y 8 clips o imágenes de la app, sin datos privados.
3. Genera o pega un guion breve con gancho, demostración y llamada a la acción.
4. Usa formato vertical 9:16, material local y concatenación secuencial.
5. Revisa el resultado antes de publicarlo. Empieza con publicación manual.

## Puesta en marcha con Docker

Docker es la opción más reproducible y ya incluye Python y FFmpeg.

```bash
cp config.example.toml config.toml
docker compose up --build webui
```

Abre <http://127.0.0.1:8501>. Para detenerlo, pulsa `Ctrl+C` y ejecuta:

```bash
docker compose down
```

`config.toml`, `storage/` y las claves están ignorados por Git. No añadas credenciales a `config.example.toml` ni a capturas del panel.

## Configuración mínima

En **Ajustes → Configuración LLM**, elige un proveedor, introduce su clave y pulsa **Probar conexión del modelo**. El LLM solo hace falta para redactar el guion, obtener términos de búsqueda y crear metadatos sociales. Puedes evitar ese coste pegando tu propio guion y usando material local.

La voz predeterminada, **Azure TTS V1 / Edge TTS**, no necesita clave. Para subtítulos sincronizados con esa voz, conserva el proveedor `edge`. Si subes una locución ya grabada, usa `whisper`; la primera ejecución descarga un modelo grande.

Para imágenes de stock necesitas una clave de Pexels, Pixabay o Coverr. Para una promoción centrada en tu producto, elige **Archivo local** y no necesitas ninguna de esas claves.

## Primera prueba recomendada

En el formulario principal usa:

- **Tema**: `Una forma rápida de [beneficio principal] con [nombre de la app]`.
- **Idioma del guion**: `es-ES`.
- **Requisitos del guion**: `Vídeo de 20 segundos. Abre con un problema concreto, muestra tres pasos reales de la app y termina con una llamada a probarla. Sin afirmaciones exageradas.`
- **Fuente de vídeo**: `Archivo local`.
- **Concatenación**: `Secuencial`.
- **Relación**: `Vertical 9:16`.
- **Duración por clip**: entre 3 y 5 segundos.
- **Vídeos por ejecución**: 1 durante las pruebas.
- **Voz**: una voz `es-ES` o `es-MX` que encaje con tu público.
- **Música**: ninguna al principio, para validar antes la narración.

Sube los clips en el orden narrativo. Las imágenes fijas también funcionan, pero una grabación de pantalla suele comunicar mejor cómo se usa el producto.

## Plantilla de guion

```text
[0–3 s] ¿Te cuesta [problema específico]?
[3–7 s] Con [app] puedes [beneficio principal].
[7–15 s] Abre [pantalla], pulsa [acción] y obtén [resultado].
[15–20 s] Prueba [app] y [llamada a la acción verificable].
```

No dependas de que la IA conozca una app que aún no es pública. Incluye siempre el nombre exacto, público, problema, funciones reales, tono, duración, plataforma y llamada a la acción. Revisa cifras, precios y promesas antes de renderizar.

## Dónde quedan los resultados

Cada ejecución crea una carpeta en `storage/tasks/<id-de-tarea>/`. La interfaz permite reproducir, descargar, abrir y reutilizar la configuración de tareas anteriores. Los materiales descargados se guardan en `storage/cache_videos/` y pueden limpiarse desde el panel de caché.

## Publicación: empieza de forma segura

La publicación automática mediante Upload-Post viene desactivada. Déjala así hasta que hayas generado y revisado varios vídeos. Primero descarga el MP4 y publícalo manualmente; así puedes comprobar encuadre, subtítulos, derechos musicales, enlaces y metadatos.

Cuando quieras automatizar TikTok, Instagram o YouTube Shorts, configura Upload-Post en tu `config.toml` y prueba inicialmente con YouTube en modo `private` o `unlisted`. Nunca confirmes una publicación automática con claves de producción durante una prueba.

## Cómo mantener este fork actualizado

En esta copia, `origin` apunta a `Romen-Adama-Dev/MoneyPrinterTurbo` y `upstream` al proyecto original. Para consultar e integrar futuras versiones:

```bash
git fetch upstream
git switch main
git merge upstream/main
git push origin main
```

Antes del `merge`, comprueba `git status`. Si este fork evoluciona mucho, integra las actualizaciones en una rama y pruébalas antes de llevarlas a `main`.

## Límites que conviene tener presentes

- La calidad del anuncio depende más del guion y de tus clips que del renderizador.
- Los proveedores de IA, voz, música, stock y publicación pueden tener costes y condiciones propias.
- Comprueba las licencias del material y de la música para uso comercial.
- La herramienta no mide instalaciones, atribución, retención ni retorno publicitario.
- No expongas la WebUI o la API a Internet sin autenticación, HTTPS y una revisión de seguridad.

