# Proyecto de Traducción — Plugins y Sitios WordPress

Archivos de traducción para los plugins y sitios WordPress de Close·technology, en español, francés, italiano, alemán e inglés.

## Estructura del repositorio

```
glossary/
  locale-es.csv                 Glosario de términos en español
  locale-fr.csv                 Glosario de términos en francés
  locale-it.csv                 Glosario de términos en italiano
  locale-de.csv                 Glosario de términos en alemán
  locale-ca.csv                 Glosario de términos en catalán

translations-xliff/
  <carpeta-job>/                Una carpeta por cada trabajo de traducción WPML
    *.xliff                     Un archivo por página/entrada

wp-plugins-*.po                 Archivos PO para traducciones de plugins en WordPress.org
```

## Formatos de archivo

### XLIFF (`.xliff`)

Exportado desde WPML. Cada `<trans-unit>` tiene un `<source>` (original) y un `<target>` (traducción).

| Estado del target | Significado |
|---|---|
| `state="translated"` | Completado — no modificar |
| `state="needs-review-translation"` | Sugerencia automática — revisar y confirmar |
| *(sin atributo state)* | Sin traducir — el texto fuente está copiado en el target |

### PO (`.po`)

Formato gettext estándar para las páginas de plugins en WordPress.org.

| Campo | Significado |
|---|---|
| `msgid` | Cadena original en inglés |
| `msgstr` | Traducción |
| `msgstr ""` (vacío) | Sin traducir |

## Reglas de traducción

Cada idioma tiene sus propias convenciones — consultar el glosario correspondiente en `glossary/`.

### Targets en inglés (ES → EN)

Se usa al traducir contenido de sitios en español al inglés.

- Usar inglés natural y profesional — evitar traducciones literales.
- Los títulos usan sentence case (solo la primera palabra y los nombres propios en mayúscula), salvo que el original use mayúsculas completas con intención estilística.

## Problemas habituales

| Problema | Qué hacer |
|---|---|
| **Unidad sin traducir** | El target es idéntico al source — traducirlo |
| **Producto incorrecto en el target** | Las sugerencias automáticas a veces toman contenido de otra página — verificar que el target corresponde al producto/tema del source |
| **Etiquetas HTML espurias** | `<br>` o `data-mce-bogus` añadidos por TinyMCE — eliminarlos |
| **Atributos inyectados** | `target="_blank"` o `rel="noopener"` a veces añadidos por la herramienta — conservarlos solo si están en el source |
| **Lorem ipsum** | Texto de relleno dejado en el target — traducir o marcar |

## Comprobar el progreso de traducción

Para contar las unidades sin traducir en una carpeta de job XLIFF:

```bash
python3 -c "
import xml.etree.ElementTree as ET, glob, os
folder = 'translations-xliff/<carpeta-job>'
ns = {'x': 'urn:oasis:names:tc:xliff:document:1.2'}
total = 0
for f in sorted(glob.glob(f'{folder}/*.xliff')):
    tree = ET.parse(f)
    root = tree.getroot()
    units = root.findall('.//x:trans-unit', ns)
    untranslated = sum(1 for u in units
        if u.find('x:target', ns) is not None
        and u.find('x:target', ns).get('state', '') != 'translated')
    if untranslated > 0:
        print(f'{os.path.basename(f)}: {untranslated} restantes')
        total += untranslated
print(f'Total: {total}')
"
```
