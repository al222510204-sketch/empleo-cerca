# Empleo Cerca

Aplicación web diseñada para ayudar a los usuarios a localizar negocios cercanos y explorar oportunidades laborales estimadas según una ciudad o colonia, un radio de distancia y un puesto de interés.

## Integrantes
- **Amado Olivera Heriberto**
- **Galván Gutiérrez Brenda**
- **Jimenez Villalva Jeshua Ariel**
- **Montes de Oca Albarrán Eduardo**

**Institución:** Universidad Tecnológica del Valle de Toluca (UTVT)  
**Programa / Grupo:** Ingeniería en Tecnologías de la Información e Innovación Digital — TSU en Infraestructura de Redes Digitales (`IRD-42`)  
**Asignatura:** Programación de Redes  

---

## Tecnologías y APIs utilizadas

### Frontend (Cliente)
- **HTML5, CSS3 y JavaScript (ES6+):** Arquitectura completa ejecutada en el navegador (`index.html`, `style.css`, `app.js`).
- **Fetch API + `async/await` + `AbortController`:** Consumo asíncrono de servicios web con cancelación por tiempo límite (`7000 ms`).
- **Leaflet:** Visualización cartográfica interactiva con marcadores y radio de búsqueda.
- **`localStorage`:** Persistencia local de puestos guardados, seguimiento, lista de verificación y caché de consultas por 24 horas.

### Servicios Web / APIs consumidas
| Servicio | Método | Uso en el proyecto |
| :--- | :---: | :--- |
| **Photon API** (`photon.komoot.io`) | `GET` | Geocodificación principal (texto a coordenadas en formato GeoJSON). |
| **Nominatim API** (`nominatim.openstreetmap.org`) | `GET` | Geocodificación secundaria de respaldo. |
| **Overpass API** (`overpass-api.de` y servidores espejo) | `POST` | Consulta espacial de comercios, oficinas y establecimientos en OpenStreetMap. |
| **JSONPlaceholder** (`jsonplaceholder.typicode.com`) | `POST` / `PUT` | Pruebas complementarias de envío y actualización de recursos en formato JSON. |

---

## Estructura del repositorio

```text
empleo-cerca/
├── index.html          # Estructura principal y vistas (Buscar, Cerca de ti, Puestos, Mi lista, Consejos)
├── style.css           # Estilos y diseño de la interfaz
├── app.js              # Lógica de geocodificación, consultas HTTP, caché, filtros y mapa
├── .gitignore          # Archivos y carpetas excluidos del repositorio
└── README.md           # Instrucciones y descripción del proyecto
```

---

## Arquitectura y flujo de funcionamiento

![Arquitectura y flujo de funcionamiento](https://github.com/user-attachments/assets/7f035d09-befd-4e5f-af6a-4e70ca94d6e8)

---

## Instalación y ejecución en local

1. **Clonar el repositorio**
   ```bash
   git clone https://github.com/al222510204-sketch/empleo-cerca.git
   cd empleo-cerca
   ```

2. **Ejecutar la aplicación**
   Al ser una aplicación web del lado del cliente sin dependencias de servidor, abre `index.html` directamente en tu navegador o levanta un servidor local estático:
   ```bash
   python -m http.server 5500
   ```
   Después abre `http://localhost:5500` en tu navegador.

---

## Pruebas y validación de API (Postman)

Las pruebas funcionales y de rendimiento de las APIs se documentaron y ejecutaron en **Postman** utilizando la colección **Empleo Cerca API** y el entorno **Empleo Cerca - Local** (`photon_url`, `nominatim_url`, `overpass_url`, `ciudad`, `lat`, `lon`, `radio`):

- **Geocodificación (`GET`):** 6 de 6 aserciones aprobadas (`200 OK`, estructura de respuesta y validación de coordenadas dentro de México).
- **Consulta de negocios (`POST` a Overpass):** Validación de código de estado, estructura JSON (`elements`), campos requeridos y análisis de tiempos de respuesta (justificando el *timeout* de `7000 ms`, los 3 servidores espejo y el uso de caché local).
- **Operaciones de escritura (`POST` / `PUT`):** Validación con cuerpo `raw/JSON` mediante JSONPlaceholder (`201 Created` / `200 OK`).

*(El detalle completo de peticiones, scripts `pm.test`, tiempos de respuesta y capturas de ejecución se encuentra en la documentación técnica entregada del proyecto).*

---

## Secciones principales de la interfaz

1. **Buscar:** Permite ingresar la ciudad o colonia, escribir un puesto opcional, seleccionar el radio de búsqueda y utilizar accesos rápidos (Toluca, Lerma, Monterrey, Guadalajara).
2. **Cerca de ti:** Muestra en un mapa interactivo (Leaflet + OpenStreetMap) los negocios detectados dentro del radio seleccionado.
3. **Puestos:** Presenta los perfiles laborales generados por sector con filtros por palabra clave, modalidad, turno, sueldo mínimo y ordenamiento.
4. **Mi lista:** Almacena en el navegador los puestos guardados y su estado de seguimiento.
5. **Consejos:** Incluye recomendaciones prácticas y una lista de verificación interactiva previa a la postulación.
