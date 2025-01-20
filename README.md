Framework de Automatización de Pruebas API: Postman-Newman-Docker-Allure
Este framework proporciona una solución completa y robusta para la automatización de pruebas de API, integrando las mejores prácticas de la industria y herramientas modernas de testing.
📋 Tabla de Contenidos

Descripción General
Prerequisitos
Configuración Inicial
Creación de Pruebas
Configuración del Entorno
Ejecución de Pruebas
Pipeline y CI/CD
Reportes
Solución de Problemas
Conclusiones

🌟 Descripción General
Este framework integra:

Postman: Desarrollo de pruebas API
Newman: Ejecución de pruebas desde CLI
Docker: Contenedorización del entorno de pruebas
Allure: Reportes detallados y visuales
GitHub Actions: Automatización de CI/CD

🔧 Prerequisitos

Node.js (v14 o superior)
Docker Desktop
Git
Postman
Visual Studio Code
Cuenta de GitHub

🚀 Configuración Inicial
1. Instalación de Dependencias Globales
bashCopy# Instalar Newman y reporter de Allure
npm install -g newman newman-reporter-allure allure-commandline

# Verificar instalaciones
newman --version
allure --version
2. Configuración del Proyecto
bashCopy# Crear directorio del proyecto
mkdir api-testing-framework
cd api-testing-framework

# Inicializar proyecto Node.js
npm init -y

# Instalar dependencias del proyecto
npm install newman newman-reporter-allure allure-commandline --save-dev
📝 Creación de Pruebas
1. Desarrollo en Postman

Crear una Nueva Colección en Postman:

Nombre: "JSONPlaceholder CRUD Tests"
Descripción: "Pruebas CRUD para API JSONPlaceholder"


Configurar Requests:

javascriptCopy// GET - Listar Posts
GET https://jsonplaceholder.typicode.com/posts
Tests:
pm.test("Status Code is 200", () => {
    pm.response.to.have.status(200);
});
pm.test("Response is an array", () => {
    pm.expect(pm.response.json()).to.be.an("array");
});

// POST - Crear Post
POST https://jsonplaceholder.typicode.com/posts
Body:
{
    "title": "Test Post",
    "body": "Test Body",
    "userId": 1
}
Tests:
pm.test("Status Code is 201", () => {
    pm.response.to.have.status(201);
});

// GET - Obtener Post
GET https://jsonplaceholder.typicode.com/posts/1
Tests:
pm.test("Status Code is 200", () => {
    pm.response.to.have.status(200);
});

// DELETE - Eliminar Post
DELETE https://jsonplaceholder.typicode.com/posts/1
Tests:
pm.test("Status Code is 200", () => {
    pm.response.to.have.status(200);
});
2. Exportar Colección

Click derecho en la colección
Export > Collection v2.1
Guardar como JSONPlaceholder-CRUD.postman_collection.json
Mover al directorio del proyecto

⚙️ Configuración del Entorno
1. Configurar package.json
jsonCopy{
  "name": "api-testing-framework",
  "version": "1.0.0",
  "scripts": {
    "test": "newman run JSONPlaceholder-CRUD.postman_collection.json -r cli,allure --reporter-allure-export=allure-results",
    "report:generate": "allure generate --clean allure-results -o allure-report",
    "report:open": "allure open allure-report"
  }
}
2. Crear Dockerfile
dockerfileCopyFROM node:16-alpine

# Instalar Newman y reporter Allure
RUN npm install -g newman newman-reporter-allure

WORKDIR /app

COPY package*.json ./
COPY JSONPlaceholder-CRUD.postman_collection.json ./

RUN npm install
RUN mkdir allure-results

CMD ["npm", "test"]
3. Configurar GitHub Actions
Crear .github/workflows/main.yml:
[Contenido del main.yml como se mostró anteriormente]
🔄 Control de Versiones
bashCopy# Inicializar repositorio
git init

# Agregar archivos
git add .

# Crear commit inicial
git commit -m "feat: configuración inicial del framework"

# Conectar con repositorio remoto
git remote add origin https://github.com/username/api-testing-framework.git

# Subir cambios
git push -u origin main
▶️ Ejecución de Pruebas
Local sin Docker
bashCopy# Ejecutar pruebas
npm test

# Generar reporte
npm run report:generate

# Abrir reporte
npm run report:open
Con Docker
bashCopy# Construir imagen
docker build -t api-tests .

# Ejecutar contenedor
docker run --name test-container api-tests

# Copiar resultados
docker cp test-container:/app/allure-results ./allure-results
[Resto del contenido como se mostró anteriormente]
🎯 Conclusiones
Este framework representa un enfoque moderno y robusto para la automatización de pruebas API, ofreciendo múltiples ventajas críticas:
Ventajas de la Dockerización:

Consistencia Garantizada:

Elimina el "funciona en mi máquina"
Asegura que las pruebas se ejecuten en un entorno idéntico
Reduce falsos positivos por diferencias de ambiente


Portabilidad:

Facilita la adopción por nuevos miembros del equipo
Permite ejecución en cualquier sistema con Docker
Simplifica la integración con CI/CD


Aislamiento:

Previene conflictos con dependencias locales
Permite múltiples versiones de herramientas
Facilita la limpieza y reset del ambiente



Beneficios del Framework:

Eficiencia Operativa:

Reduce tiempo de configuración
Automatiza procesos repetitivos
Facilita la escalabilidad de pruebas


Calidad Mejorada:

Asegura consistencia en la ejecución
Proporciona reportes detallados
Facilita la identificación de problemas


Colaboración Efectiva:

Estandariza procesos de prueba
Mejora la visibilidad del estado de pruebas
Facilita la integración con flujos de trabajo existentes



Este framework no solo automatiza pruebas, sino que establece un estándar de calidad y eficiencia en el proceso de testing, fundamental para equipos que buscan excelencia en el desarrollo de software.

Desarrollado con ❤️ por el equipo de QA
