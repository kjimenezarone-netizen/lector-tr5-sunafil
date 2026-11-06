# TR5-V2 — Proyecto revisado y corregido (v3.1)

Este paquete contiene el **código completo** extraído del RAR proporcionado por el usuario, con las mejoras implementadas en TR5/TR6 y RUC Masivo. No es un aplicador ni requiere descargar otro kit.

## Qué se cambió

1. Orden TR: **Carga → Registros originales → Trabajadores/cruce → Exportación Excel**.
2. Se eliminó de la **interfaz TR** el panel de columnas visibles; las columnas originales NO se borran del TXT, de la tabla ni de Excel.
3. Se centralizó Excel en un único panel con alcance, resumen de hojas, previsualización y descarga; el botón antiguo de descarga rápida se convirtió en acceso al centro.
4. La zona de carga se limpia automáticamente al finalizar con éxito, sin borrar los resultados procesados.
5. Se añadió **Finalizar consulta y limpiar todo**, con confirmación explícita, para TR y RUC. Descargar Excel NO limpia la consulta.
6. Los filtros secundarios y gráficos se consultan en paneles desplegables; las tarjetas de hallazgos rápidos TR reemplazan opciones duplicadas.
7. Se corrigió la cancelación real del RUC, se mejoró el aislamiento de tareas y se protegió la presentación HTML de valores importados.
8. La ficha TR6 diferencia las dos columnas de régimen (salud y pensión). Los textos laborales expresan *indicadores a verificar*, no conclusiones de incumplimiento.
9. Se quitaron funciones JavaScript sin referencias y se incorporaron pruebas de regresión.

## Requisitos

- Navegador moderno (Chrome/Edge/Firefox).
- Para pruebas automatizadas: **Node.js 18 o posterior** (validado con Node.js 22).
- Para servir la aplicación en local: **Python 3** o extensión **Live Server** de VS Code.
- Conexión a Internet si se usan Chart.js, Tailwind y html2pdf desde sus CDN.

## Uso local

Abra esta carpeta en Visual Studio Code y, desde su terminal:

```powershell
node --test
py -m http.server 8000
```

Visite `http://localhost:8000`, seleccione intendencia y pruebe los lectores. No ejecute el `index.html` desde `file://` si puede usar un servidor local, ya que el Worker puede necesitar HTTP.

## Publicar en GitHub sin tocar `main` directamente

1. Haga una copia de seguridad o clone el repositorio:

```powershell
git clone https://github.com/kjimenezarone-netizen/tr5-v2.git
cd tr5-v2
git switch -c mejora/reorganizacion-lectores-v3-1
```

2. Copie **el contenido** de esta carpeta corregida a la raíz del clon. Mantenga la carpeta `.git` del clon (no sustituir). Revise `git status` y los archivos afectados.
3. Verifique y publique:

```powershell
node --test
git diff --check
git add -A
git commit -m "feat: reorganizar lectores TR5 TR6 y RUC masivo"
git push -u origin mejora/reorganizacion-lectores-v3-1
```

4. En GitHub cree el Pull Request y revise los archivos antes de fusionarlo en `main`.

## Comprobación técnica de esta entrega

- **21 pruebas automáticas pasadas**, sintaxis de JS correcta.
- **127 registros** de las muestras: **6 TR5 + 121 TR6**, agrupados en **121 identidades** sin pérdida de filas; **4 identidades** en ambos reportes.
- HTML: **4 pasos**, **151 IDs únicos** y ningún control de selección de columnas TR.
- **Pendiente:** prueba visual y de clics en navegador real. Chromium no pudo navegar en este entorno por una restricción administrativa.

## Archivos de documentación

- `DOCUMENTACION_CAMBIOS.xml`: especificación técnica, matriz de 21 cambios, pruebas, instrucciones y limitaciones.
- `CAMBIOS_APLICADOS.patch`: diferencia detallada entre el RAR original y el código corregido.

## Advertencias

- RUC soporta **TXT y ZIP**. No se implementaron lectores RAR ni TAR.
- El repositorio público puede contener datos en `muestras/`; verifique si esas muestras requieren anonimización antes de publicarlas.
- Los controles de limpieza no modifican originales ni los Excel ya descargados. Solo descartan datos temporales en memoria y vistas.
