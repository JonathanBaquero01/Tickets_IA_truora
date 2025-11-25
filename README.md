# AI Ticket Classifier (RAG Architecture) 

> **Desarrollado por:** Ing. Jonathan Baquero  
> **Para:** Truora.com

Este proyecto es un sistema inteligente de gestión y clasificación de tickets de soporte técnico. Utiliza **Inteligencia Artificial Generativa (Google Gemini 1.5 Flash)** y una arquitectura **RAG (Retrieval-Augmented Generation)** ejecutada del lado del cliente para analizar, priorizar y sugerir soluciones a incidentes basándose en datos históricos reales.

---

## 🚀 Características Principales

*   **Clasificación Automática:** Determina Título, Prioridad (P1-P4), Urgencia, Categoría y SLA basándose en la descripción del problema.
*   **Arquitectura RAG (Client-Side):** Consulta una base de conocimiento local (`Knowledge_base.json`) para encontrar patrones históricos y mejorar la precisión de la IA sin alucinaciones.
*   **Human-in-the-Loop (Feedback):** Permite a los ingenieros editar y corregir las predicciones de la IA antes de guardar el ticket.
*   **Sincronización de SLA:** Ajusta automáticamente los tiempos de resolución y urgencia según la prioridad seleccionada, respetando la matriz de negocio.
*   **Gestión de Ciclo de Vida:** Flujo completo desde la creación, edición en "Tickets en Proceso", hasta el marcado como "Resuelto".
*   **Zero-Build:** Funciona directamente en el navegador sin necesidad de Node.js, Webpack o servidores backend complejos.

---

## 🛠️ Stack Tecnológico

*   **Frontend:** HTML5 Semántico + Vanilla JavaScript (ES Modules).
*   **Estilos:** Tailwind CSS (vía CDN).
*   **Inteligencia Artificial:** Google Gemini 1.5 Flash (vía Google GenAI SDK).
*   **Datos:** JSON local como base de conocimiento vectorial simulada.

---

## 📋 Arquitectura RAG (Cómo funciona)

El sistema no solo pregunta a la IA, sino que sigue un flujo inteligente:

1.  **Recuperación (Retrieval):** Cuando el usuario escribe un problema, el sistema busca en el archivo `Knowledge_base.json` los 3 tickets históricos más similares mediante búsqueda léxica.
2.  **Aumentación (Augmentation):** Inyecta estos casos históricos en el *prompt* del sistema como contexto ("Few-Shot Learning").
3.  **Generación (Generation):** Gemini genera una clasificación y solución sugerida basada en cómo se resolvieron esos problemas en el pasado.

---

## 📦 Instalación y Uso

Debido a que el proyecto carga un archivo JSON externo y utiliza módulos de ES, debe ejecutarse en un servidor local (no funcionará correctamente dando doble clic al archivo HTML por políticas CORS del navegador).


---

## 📂 Estructura del Proyecto

```text
.
├── index.html            # Lógica principal, UI y controlador RAG
├── index.css             # Estilos personalizados y directivas Tailwind
├── Knowledge_base.json   # Base de datos con 50 tickets históricos (Fuente de verdad)
└── README.md             # Documentación del proyecto