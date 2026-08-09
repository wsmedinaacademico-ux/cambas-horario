# Horario de Monitorías — sitio público

Publica el Horario de Monitorías del CAMBAS como una página web estática en
GitHub Pages. Este repositorio contiene **solo la página publicada**: ni datos
de origen, ni código, ni resultados de corridas.

## Qué hay aquí

| Archivo      | Para qué |
|--------------|----------|
| `index.html` | La página completa. Autocontenida: tipografía, logo y datos van embebidos en base64, sin una sola petición externa. |
| `.nojekyll`  | Le dice a GitHub Pages que sirva los archivos tal cual, sin pasarlos por Jekyll. |

## Por qué es un repositorio aparte

El generador vive en `Programas/CAMBAS_AsignacionCentro/`, cuyo directorio
`salidas/` guarda `.xlsx` y `.pkl` con datos reales de monitores. Un sitio de
GitHub Pages gratuito es público, así que ese repositorio **no debe publicarse**.
Aquí solo llega el HTML final.

## Cómo se genera `index.html`

1. Ejecutar el programa generador:

   ```
   cd Programas/CAMBAS_AsignacionCentro
   python main.py
   ```

   Produce `salidas/horario_<propuesta>_<fecha>.html`.

2. Copiar ese archivo a este repositorio con el nombre `index.html`
   (GitHub Pages sirve `index.html` como raíz del sitio).

3. Publicar:

   ```
   git add index.html
   git commit -m "Actualizar horario"
   git push
   ```

   GitHub Pages redespliega solo, en menos de un minuto.

## Privacidad

La página lista nombres de monitores. Por eso `index.html` incluye:

```html
<meta name="robots" content="noindex, nofollow">
```

La URL queda abierta para que los estudiantes la consulten, pero los buscadores
no la indexan. La etiqueta la emite el generador
(`src/horario_web.py`), así que sobrevive a cada regeneración — **no la quites
al actualizar el archivo**.

Se usa la etiqueta `meta` y no un `robots.txt` con `Disallow` a propósito: un
`Disallow` impide que el rastreador lea la página, y por tanto que vea la propia
instrucción de no indexar; la URL puede terminar indexada igual si alguien la
enlaza.

## Pendiente conocido

El `index.html` publicado hoy **no lleva la tipografía Plus Jakarta Sans ni el
logo de Icesi**: `src/marca.py` los busca en `Documentación/`, pero los archivos
están en `Marca/`, y el cargador devuelve una cadena vacía sin avisar. La página
cae a Segoe UI y sin logo. Al corregirlo hay que regenerar y volver a publicar.
