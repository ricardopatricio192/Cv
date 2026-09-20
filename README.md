# CV Web - Ricardo Patricio Cid

Sitio estático de currículum (HTML + CSS + JavaScript) listo para publicarse gratis con **GitHub Pages**.

## Estructura del proyecto

```
cv/
├── index.html            ← Página principal (CV completo)
├── style.css             ← Estilos (tema oscuro, animaciones, modal de zoom)
├── img/                  ← Imágenes: perfil.png + certificado-01.png ... certificado-20.png
├── .nojekyll             ← Desactiva Jekyll (OBLIGATORIO para que GitHub Pages sirva todo)
├── .gitattributes        ← Trata los .png como binarios y normaliza fin de línea
└── README.md
```

> La carpeta se llamaba antes `certificados` y fue renombrada a `img`.
> Todas las rutas del `index.html` ya apuntan a `./img/certificado-XX.png` (42 referencias, 0 faltantes).

## ¿Por qué `.nojekyll`? (carpeta legible por GitHub Pages)

GitHub Pages procesa por defecto el sitio con **Jekyll**. Ese proceso:

- Ignora archivos y carpetas que empiezan con `_` o `.`.
- Puede tardar/fallar al procesar carpetas de imágenes grandes.

Al agregar un archivo vacío llamado `.nojekyll` en la **raíz** del repositorio, GitHub Pages
sirve todos los archivos tal cual están en el repositorio, sin procesamiento previo. Así
`https://usuario.github.io/repositorio/img/certificado-01.png` responde directamente.

## Publicar el sitio en GitHub Pages (paso a paso)

### 1. Crear el repositorio en GitHub

1. Entrar a <https://github.com/new>.
2. **Repository name**: por ejemplo `cv`.
3. Visibilidad: **Public** (necesario para Pages gratis).
4. **NO** marcar "Add a README file" (ya existe uno local).
5. Crear el repositorio.

### 2. Subir los archivos (desde esta carpeta, en PowerShell)

```powershell
cd "C:\Users\RICKY\OneDrive\Documentos\cv"
git init -b main
git add .
git commit -m "CV web con certificados en img/"
git remote add origin https://github.com/TU-USUARIO/cv.git
git branch -M main
git push -u origin main
```

### 3. Activar GitHub Pages

1. En el repositorio: **Settings** → **Pages**.
2. En *Build and deployment* → **Source**: `Deploy from a branch`.
3. **Branch**: `main` y carpeta `/ (root)` → **Save**.
4. Esperar 1-2 minutos y abrir:

```
https://TU-USUARIO.github.io/cv/
```

Los certificados quedarán disponibles (y compartibles) en:

```
https://TU-USUARIO.github.io/cv/img/certificado-01.png
```

### 4. Para actualizar el contenido más adelante

```powershell
git add .
git commit -m "Actualizo contenido"
git push
```

GitHub Pages se regenera automáticamente en 1-2 minutos.

## Prueba local (opcional)

Con Python instalado:

```powershell
cd "C:\Users\RICKY\OneDrive\Documentos\cv"
python -m http.server 8000
```

Luego abrir <http://localhost:8000> (no abrir `index.html` con doble clic: algunas
imágenes y estilos se comportan distinto bajo `file://`).

## Notas y recomendaciones

- `img/certificado-14.png` existe en la carpeta pero hoy no se muestra en el CV.
  Si querés agregarlo, copiá el bloque de otro certificado en `index.html`
  y usá `./img/certificado-14.png`.
- La foto de perfil es **local**: `./img/perfil.png` (820x820 px, PNG RGB opaco, ~547 KB).
  Reemplazó al enlace externo de Microsoft Sway, así el sitio no depende de ningún servicio
  de terceros para mostrar la foto.
  La imagen se editó con segmentación por IA (modelo ISNet sobre ONNX Runtime): se recortó
  el fondo original (muro y árbol de Navidad) y se compuso la silueta sobre un degradado
  oscuro con los colores del sitio (`#071116` → `#12222b`, halos menta `#7ff2c3` y cian
  `#00b4dc`), luz de contorno suave y vineteado. **Los rasgos del rostro no se retocaron**:
  los píxeles del sujeto son los originales.
  Como el recorte circular lo hace el CSS (`border-radius: 50%` + `object-fit: cover`),
  la imagen ya no necesita transparencia: es un cuadrado opaco centrado en el rostro.
  Si querés cambiar la foto, guardá el nuevo archivo como `img/perfil.png` (ideal: cuadrada,
  rostro centrado y ~800 px de lado).
- No hay datos sensibles: el sitio es 100% estático y público. El teléfono,
  mail y localidad que figuran en el encabezado quedan visibles para cualquiera
  que entre al link.
