# Portal Estudiantil SIGPS

Portal de apoyo para estudiantes que realizan su **Servicio Social en la Facultad Multidisciplinaria Oriental de la Universidad de El Salvador (FMO–UES)**. Reúne guías, modelos descargables y asistentes para preparar documentos de inscripción, proyecto, memoria y cartas.

El portal es un sitio estático: funciona en el navegador y no requiere un backend propio. Su contenido orienta y ayuda a preparar borradores; no sustituye la revisión, aprobación ni emisión de documentos por parte de la institución.

## Funciones

- Guías y modelos originales en PDF y Word para las etapas del Servicio Social.
- Asistentes para preparar documentos editables de inscripción, proyecto y memoria.
- Organización de cronogramas y distribución de horas por alumno.
- Generación de cartas de solicitud, prórroga, ampliación y retiro.
- Checklist interactivo para dar seguimiento a los pasos del proceso.
- Interfaz adaptable a dispositivos móviles.

Los documentos Word se generan en el navegador con plantillas locales y las bibliotecas **Docxtemplater** y **PizZip**. No se cargan desde CDN.

## Vista previa local

Se requiere **Node.js**. Desde la raíz del repositorio, ejecuta:

```sh
npm start
```

Abre [http://127.0.0.1:8765](http://127.0.0.1:8765). El servidor solo entrega archivos estáticos para la vista previa; no instala dependencias ni levanta una API. Para probar la generación de documentos, usa HTTP en lugar de abrir las páginas directamente con `file://`.

## Publicación

El portal puede alojarse en GitHub Pages o en cualquier servicio de hosting estático. Para preparar los archivos públicos localmente:

```sh
npm run export:pages
```

El comando copia el sitio a `dist/`; no compila ni instala paquetes. Para GitHub Pages, configura **Settings → Pages → Source: GitHub Actions** y ejecuta manualmente el workflow **Publicar portal estático** desde la pestaña **Actions**. El workflow publica el contenido de `dist/`.

Consulta la [guía de publicación estática](docs/publicacion-estatica.md) para los pasos completos.

## Privacidad y alcance

- Los datos de los formularios se procesan en el navegador. Los borradores de inscripción, proyecto y memoria permanecen en memoria mientras la página está abierta; no se envían a un servidor ni se conservan al recargarla.
- El checklist conserva su estado en `sessionStorage` durante la sesión del navegador.
- La configuración activa es estática: no consulta una API ni servicios locales. La integración futura con el backoffice SIGPS no está habilitada.
- El catálogo académico incluido es de demostración, no oficial. Debe validarse con coordinación antes de usarse para trámites reales.
- Las guías y plantillas disponibles no indican una versión institucional confirmada. Verifica su vigencia con la UPS o coordinación.
- Los documentos generados son editables y requieren revisión. El portal no crea contenido académico, no incorpora automáticamente anexos externos y no aplica firmas, sellos ni aprobaciones.

## Documentación del proyecto

| Documento | Descripción |
| --- | --- |
| [`docs/procesos.md`](docs/procesos.md) | Recorridos, relación con las guías y alcance funcional |
| [`docs/inscripcion-word.md`](docs/inscripcion-word.md) | Plantilla y generación del documento de inscripción |
| [`docs/proyecto-word.md`](docs/proyecto-word.md) | Estructura y formato del documento de proyecto |
| [`docs/cronograma-memoria.md`](docs/cronograma-memoria.md) | Cronogramas y generación del documento de memoria |
| [`docs/publicacion-estatica.md`](docs/publicacion-estatica.md) | Despliegue estático y recursos incluidos |

## Desarrollo y pruebas

Las páginas se implementan con **HTML, CSS y JavaScript nativo**. No se utiliza un framework de interfaz ni un proceso de compilación.

Para instalar las dependencias de desarrollo y ejecutar las pruebas:

```sh
npm ci --ignore-scripts
npm test
```

`npm ci` instala las dependencias fijadas en `package-lock.json`. Las copias locales de Docxtemplater y PizZip ya están incluidas en `js/vendor/`.

## Estructura principal

| Ruta | Contenido |
| --- | --- |
| `index.html` | Página principal y acceso a las etapas |
| `procesos.html` | Guías y asistentes para inscripción, proyecto y memoria |
| `cartas.html` | Generación de cartas de solicitud y procesos extraordinarios |
| `checklist.html` | Lista interactiva de seguimiento |
| `css/` y `js/` | Estilos, lógica y bibliotecas locales |
| `documentos/` | Guías originales, modelos y plantillas |
| `docs/` | Documentación técnica y funcional |

## Recursos institucionales

Los archivos originales se conservan como referencia y no se modifican. La procedencia de las guías está registrada en [`documentos/procesos/fuentes.json`](documentos/procesos/fuentes.json). Consulta a la UPS o coordinación sobre requisitos, plazos y versiones vigentes antes de presentar documentos.
