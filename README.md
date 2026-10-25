# ⎈ Kubernetes Cheatsheets

Cheatsheets visuales de Kubernetes en español: diagramas, `kubectl` con buscador, manifiestos listos para copiar, botón copiar y tema claro/oscuro.
Sitio 100 % estático (HTML + CSS + JS, sin build ni dependencias).

| Hoja | Contenido |
|---|---|
| `index.html` | Portada, buscador “Quiero…” y descargas en PNG |
| `01-conceptos.html` | Arquitectura del cluster, estado deseado, Deployment → Pods, glosario, equivalencias con Docker |
| `02-kubectl.html` | Cluster local, contextos, `get`/`describe`, `apply`, logs, `exec`, `port-forward`, rollouts, Helm |
| `03-manifiestos.html` | Anatomía, labels y selectors, Deployment, Service, ConfigMap, Secret, PVC, Ingress, probes |
| `04-red-config-datos.html` | Tipos de Service y puertos, DNS, Ingress, inyección de config, PVC/PV, StatefulSet |
| `05-de-compose-a-k8s.html` | Migración de una app Node + Mongo de Docker Compose a Kubernetes |
| `06-problemas.html` | Diagnóstico y errores comunes con causa y solución |

## Estructura

```
kubernetes-cheatsheets/
├── index.html, 01-…06-*.html   # páginas
├── 404.html                    # página de error (Netlify la usa sola)
├── assets/
│   ├── style.css               # estilos y temas
│   └── app.js                  # navegación, buscador, copiar, resaltado
├── img/                        # cada hoja exportada a PNG (oscuro y claro)
└── netlify.toml                # config de deploy
```

## Verlo en local

Doble clic en `index.html` funciona. Para probarlo igual que en Netlify (rutas absolutas del 404, portapapeles):

```bash
python -m http.server 8080
```

y abrí <http://localhost:8080>.

## Subir a GitHub

1. Creá un repositorio **vacío** en <https://github.com/new> (sin README ni .gitignore), por ejemplo `kubernetes-cheatsheets`.
2. Desde esta carpeta:

```bash
git remote add origin https://github.com/<tu-usuario>/kubernetes-cheatsheets.git
git push -u origin main
```

## Publicar en Netlify

1. <https://app.netlify.com> → **Add new site → Import an existing project → GitHub**.
2. Elegí el repo `kubernetes-cheatsheets`.
3. Dejá **Build command** vacío y **Publish directory** en `.` (ya lo define `netlify.toml`).
4. **Deploy**. Cada `git push` a `main` vuelve a publicar solo.
5. Opcional: **Site configuration → Change site name** para tener `kubernetes-cheatsheets.netlify.app` (si está libre).

## Enlazar con las cheatsheets de Docker

En `assets/app.js`, completá la URL del sitio hermano y aparece el botón en la barra:

```js
other: { label: "Docker", href: "https://<tu-sitio-docker>.netlify.app/", icon: "whale" },
```

## Editar contenido

- Cada página es HTML plano: agregá tarjetas copiando una existente (`<div class="card t-cont">…</div>`).
- Los bloques `<pre><code>` se resaltan y reciben el botón copiar solos. `data-lang="yaml"`, `"dockerfile"` o `"plain"` cambia el resaltado (por defecto, shell).
- Los valores a reemplazar se escriben como `&lt;nombre&gt;` y se ven en rosa.
- Las imágenes de `img/` **no se regeneran solas**: si cambiás una hoja, volvé a exportarla (por ejemplo, con la captura de página completa de las DevTools del navegador, abriendo la hoja con `?theme=dark` o `?theme=light`).
