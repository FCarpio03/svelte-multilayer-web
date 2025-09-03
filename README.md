# Svelte Multilayer Web Application

Este repositorio contiene un **sitio web multicapas** desarrollado con **Svelte** y **Vite**. El proyecto demuestra cómo estructurar una aplicación web utilizando múltiples capas, separando la presentación, la lógica y la gestión de datos, siguiendo buenas prácticas de desarrollo web moderno.

## Tecnologías utilizadas

- **Svelte** – Framework de frontend para interfaces reactivas  
- **Vite** – Bundler y herramienta de desarrollo rápida  
- **HTML, CSS y JavaScript** – Para la estructura y estilos del sitio  

## Características

- Formulario multicapas con validaciones  
- Navegación fluida entre secciones  
- Código modular y organizado por capas  
- Base para aplicaciones web escalables y mantenibles  

## Instalación y uso

1. Clona el repositorio:
```bash
git clone https://github.com/FCarpio03/svelte-multilayer-web.git
cd svelte-multilayer-web

2. Instala dependencias:
npm install

3. Ejecuta la aplicación en modo desarrollo:
npm run dev

Abre tu navegador en la URL que indique Vite (por defecto http://localhost:5173)

Estructura del proyecto:

.
├── public/           ← Archivos estáticos
├── src/
│   ├── components/   ← Componentes reutilizables
│   ├── routes/       ← Páginas o secciones del sitio
│   ├── stores/       ← Estado global
│   └── main.js       ← Entrada principal
├── package.json
├── vite.config.js
└── README.md

Propósito del proyecto

Este proyecto es ideal para:

Aprender a estructurar aplicaciones Svelte por capas

Mostrar buenas prácticas de frontend moderno

Servir como base para aplicaciones web más complejas
