# Retrostuary

Skin estilo **Windows 95** para **Kodi 21 Omega**, basada en Estuary (phil65 y
Piers, equipo de Kodi). Mod de RubénSDFA1laberot — EspaKodi.

Este repositorio es el punto de entrada para instalar y actualizar la skin: lo
instalas una vez y a partir de ahí Kodi se encarga.

## Instalar desde el repositorio (recomendado)

1. En Kodi: **Ajustes** → **Interfaz** → **Explorador de archivos** →
   **Añadir fuente**.
2. En `<Ninguno>` pega `https://espakodi.github.io/retrostuary/` y ponle el nombre `retrostuary`.
3. **Add-ons** → icono de paquete (arriba a la izquierda) →
   **Instalar desde archivo zip** → elige la fuente `retrostuary` →
   `repository.retrostuary-1.0.0.zip`.
4. **Instalar desde repositorio** → **Retrostuary Repository** → **Aspecto** →
   **Retrostuary** → **Instalar**.

> **Si ya tienes la skin instalada a mano, Kodi no la actualizará sola.** Las
> instalaciones manuales se marcan como tales y se saltan la comprobación de
> actualizaciones, así que la skin se quedaría en la versión con la que la
> instalaste. Desinstala el ZIP antiguo y repite los pasos. Al instalar desde el
> repositorio, Kodi sustituye la copia anterior sin preguntar.

Si aparece un aviso de seguridad: **Ajustes** → **Sistema** → **Add-ons** →
activa *Orígenes desconocidos*.

## Instalar sin el repositorio

Descarga `skin.retrostuary/skin.retrostuary-1.5.4.zip` y usa **Add-ons** → icono de paquete → **Instalar
desde archivo zip**. Esta vía **no** recibe actualizaciones.

## Qué hay en este repositorio

| Ruta | Qué es |
|---|---|
| `addons.xml` | el catálogo que Kodi lee; declara `repository.retrostuary` y `skin.retrostuary` |
| `addons.xml.md5` | checksum del catálogo. Tiene que existir: si da 404, Kodi descarta el repositorio entero |
| `index.html` | la página que sirve la raíz del sitio, con los pasos de instalación |
| `.nojekyll` | GitHub Pages sirve el repo **sin** pasar por Jekyll. Sin esto, Jekyll ignora cualquier carpeta que empiece por `_` |
| `.gitattributes` | fija los fines de línea en LF para que el `addons.xml` que se sube sea el mismo que se hashea |
| `repository.retrostuary/repository.retrostuary-1.0.0.zip` | el addon de repositorio, en la ruta que Kodi construye (`<datadir>/<id>/<id>-<ver>.zip`) |
| `repository.retrostuary-1.0.0.zip` | el mismo zip en la raíz, que es lo que se pincha en *Instalar desde archivo zip* |
| `skin.retrostuary/` | la skin: zip, manifest, recursos y ficheros sueltos |

`index.html` y los `.md` de la raíz **no los pide Kodi**; están para quien abre
la URL o el repo en un navegador. Los ficheros sueltos de cada carpeta
(`addon.xml`, `icon.png`, `LICENSE.txt`) los produce `create_repository.py`, el
generador oficial de la wiki de Kodi, y tampoco los lee el motor: los usa el
generador y hacen la carpeta autodescriptiva.

## Verificación de integridad

| Fichero | Tamaño | SHA-256 | MD5 |
|---|---|---|---|
| `repository.retrostuary-1.0.0.zip` | 40.127 | `77c5f62b3f8206643be3de9cb63890112bec04500aa241a2ad828811b057135e` | `8b52353251e2befb88fda4d67901b071` |
| `skin.retrostuary-1.5.4.zip` | 4.484.502 | `a1d097bda273fcc898e7762e03db74efabbe850570ede3178dfc369ced7df4b0` | `018d3f83836c798fc9715ba03f1a8ba9` |

Si descargas un ZIP a mano, comprobar el hash te dice si llegó íntegro:

```
Get-FileHash .\skin.retrostuary-1.5.4.zip -Algorithm SHA256
```

## Licencia y créditos

El código y los assets propios se publican bajo **CC BY-SA 4.0**. Al derivarse
de Estuary (CC BY-SA 4.0) y de Chicago95 (GPL-3.0-or-later) de grassmunk, la
skin completa se distribuye bajo **CC BY-SA 4.0** por la cláusula de
compatibilidad de licencias copyleft; los ficheros heredados de Chicago95
conservan su GPL-3.0-or-later. El `LICENSE.txt` completo viaja dentro de cada
ZIP.

- **Estuary** — phil65 y Piers, equipo de Kodi · CC BY-SA 4.0
- **Chicago95** — grassmunk y colaboradores · GPL-3.0-or-later
- **Flaticon** — `media/icons/settings.png`, por atribución

Esta skin es de terceros y se puede desinstalar sin riesgo. No forma parte de
Kodi ni del equipo de Kodi.

## Cómo se genera

Casi nada de esto se escribe a mano. `build_repo.py` (en el repo del proyecto,
fuera de este sitio) lee el `addon.xml` de la skin, fusiona los dos addons en
el catálogo, calcula el md5 de los bytes exactos que se sirven, copia los zips
y los ficheros sueltos, genera este README con los hashes del momento, poda lo
que sobra y verifica antes de dejar nada escrito. Si algo no cuadra, se niega
a publicar y dice qué.

La excepción es `index.html`: la landing está escrita a mano y el script solo
actualiza en ella los nombres de zip (`<id>-<versión>.zip`) cuando cambia una
versión. El texto, el orden y el estilo son decisiones editoriales, no
generadas.

```powershell
python build_zip.py skin.retrostuary   # empaqueta la skin (con sus 4 guardas)
python build_repo.py                   # genera este repositorio y lo verifica
python check_published.py              # comprueba que lo publicado sirve bien
```

---

Telegram: t.me/espakodi
