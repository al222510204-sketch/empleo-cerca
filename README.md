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
└── README.md           # Instrucciones y descripción del proyecto
---
## Arquitectura y flujo de funcionamiento

![Arquitectura y flujo de funcionamiento](./docs/arquitectura.png)
