# 🚗 Garatge · Els meus vehicles

Seguimiento de vehículos (mantenimientos, reparaciones, ITV, seguro, facturas…).

- **Frontend:** `index.html` → publicado en GitHub Pages.
- **Backend:** `apps-script/` → Google Apps Script (Google Sheets como base de datos y Drive para las facturas).

```
index.html               ← la app (GitHub Pages)
apps-script/Codigo.gs    ← API en Apps Script (doPost)
apps-script/appsscript.json
```

## 1. Apps Script (backend)

1. Abre tu proyecto **Garatge** en script.google.com.
2. Sustituye el contenido de `Código.gs` por el de [`apps-script/Codigo.gs`](apps-script/Codigo.gs).
3. Borra el archivo `Index` del proyecto (la interfaz ahora vive en GitHub).
4. **Clave de acceso** (recomendado): ⚙️ *Configuración del proyecto* → *Propiedades del script* → añade
   `CLAU` = la clave que quieras. Sin ella, cualquiera con la URL podría leer/modificar los datos.
5. *Implementar* → *Gestionar implementaciones* → ✏️ editar la implementación existente →
   *Versión: Nueva versión* → *Implementar*. (Así se mantiene la misma URL `/exec`.)
   - Ejecutar como: **Yo** · Quién tiene acceso: **Cualquier persona**.
   - Si no tenías implementación: *Nueva implementación* → tipo *Aplicación web*.
6. Copia la URL que acaba en `/exec`.

## 2. GitHub Pages (frontend)

1. En GitHub: *Settings* → *Pages* → *Source: Deploy from a branch* → rama `main`, carpeta `/ (root)`.
2. La app quedará en: **https://katwolo.github.io/garatge/**
3. La primera vez que la abras te pedirá (⚙️) la **URL del Apps Script** y la **clave**. Se guardan en el navegador.
   - Opcional: pon la URL fija en `GAS_URL_PER_DEFECTE` dentro de `index.html` para no tener que introducirla en cada dispositivo.

## Cómo funciona la conexión

`index.html` hace `fetch(POST)` a la URL `/exec` con `{ clau, fn, args }` y el Apps Script responde
`{ ok, data | error }`. Funciones disponibles: `getData`, `saveVehicle`, `deleteVehicle`,
`saveRecord`, `deleteRecord`, `getFitxer`.
