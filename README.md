# Marco de Pruebas de API con Postman, Newman, Docker y Allure

Este proyecto proporciona un marco completo para realizar pruebas automatizadas de API. Utiliza herramientas como Postman/Newman para ejecutar pruebas, Docker para un entorno de pruebas aislado, GitHub Actions para integración continua y Allure para generar reportes visuales y detallados.

🌟 Descripción General
El marco combina varias tecnologías para garantizar un flujo de pruebas eficiente:

Postman/Newman: Creación y ejecución de pruebas de API.
Docker: Entorno de pruebas contenedorizado.
GitHub Actions: Ejecución de pruebas automatizadas y despliegue continuo.
Allure: Reportes visuales y detallados de las pruebas.
🏗️ Estructura del Proyecto
plaintext
Copy
Edit
API-TestFramework-GitActions-Docker-Allure/
├── .github/                 # Configuración de flujos de trabajo de GitHub Actions
│   └── workflows/
│       └── main.yml         # Configuración del pipeline
├── JSONPlaceholder-CRUD.postman_collection.json  # Colección de pruebas de Postman
├── allure-report/           # Reportes generados por Allure
├── allure-results/          # Resultados de las pruebas en formato Allure
├── Dockerfile               # Configuración de Docker
├── package.json             # Dependencias del proyecto y scripts
├── package-lock.json        # Bloqueo de dependencias
└── README.md                # Documentación
🔄 Flujo de Trabajo

1. Creación de Pruebas

Crea tus pruebas de API en Postman.
Exporta la colección en formato JSON desde Postman.
En Postman:
Ve a la colección.
Haz clic en "Exportar".
Coloca el archivo JSON exportado en el directorio raíz del proyecto.

2. Ejecución Local
Construir la Imagen de Docker
bash
Copy
Edit
docker build -t api-tests .
Ejecutar las Pruebas
bash
Copy
Edit
docker run --name test-container api-tests
Generar Reporte de Allure
bash
Copy
Edit
## Exportar resultados al directorio allure-results/

docker cp test-container:/app/allure-results ./allure-results

# Generar el reporte HTML
npm run report:generate

# Abrir el reporte en el navegador
npm run report:open
3. Pipeline Automatizado (GitHub Actions)
El pipeline de GitHub Actions se ejecuta automáticamente en los siguientes casos:

Pushed a las ramas main, master o develop.
Al abrir una Pull Request.
Ejecución programada diaria a medianoche.
Ejecución manual desde la interfaz de GitHub.
Pasos del Pipeline
Clona el repositorio y verifica el código.
Construye la imagen de Docker.
Ejecuta las pruebas en un contenedor Docker.
Genera los resultados de Allure y el historial de reportes.
Publica el reporte en GitHub Pages.
El reporte se encuentra disponible en:
Reporte Allure.

🚀 Configuración Inicial
1. Clonar el Repositorio
bash
Copy
Edit
git clone https://github.com/E-Gregorio/API-TestFramework-GitActions-Docker-Allure.git
cd API-TestFramework-GitActions-Docker-Allure

# Instalar dependencias
npm install
2. Configurar el Repositorio en GitHub
Activa GitHub Actions en la pestaña "Actions".
Habilita GitHub Pages en la pestaña "Settings".
En "Branch", selecciona gh-pages.
Configura los permisos necesarios para Actions:
contents: write
pages: write
id-token: write
📊 Reportes con Allure
El reporte de Allure incluye:

Resumen de ejecución de pruebas.
Detalle de casos de prueba ejecutados.
Tendencias históricas de las ejecuciones.
Análisis detallado de fallos.
Información del entorno.
Para acceder al reporte de Allure:

Ve a la configuración del repositorio en GitHub (Settings).
Busca la sección Pages.
Encuentra la URL publicada, por ejemplo:
Reporte Allure.
🤝 Contribuir
Haz un fork del repositorio.
Crea una rama para tus cambios.
Realiza los cambios necesarios y haz commit.
Envía un Pull Request para revisión.
📝 Mejores Prácticas
Organiza las pruebas en colecciones bien definidas.
Utiliza variables de entorno para pruebas dinámicas.
Separa los datos de prueba de la lógica del caso de prueba.
Incluye aserciones detalladas para validar respuestas.
Mantén el proyecto actualizado y bien documentado.
Último consejo:
¡Automatiza, documenta y comparte el conocimiento! Este marco está diseñado para escalar y adaptarse a proyectos de cualquier tamaño. Si encuentras un problema o tienes sugerencias, no dudes en contribuir al repositorio.