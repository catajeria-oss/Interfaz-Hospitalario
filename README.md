# Sistema de Gestión de Laboratorio Clínico

Este proyecto consiste en una aplicación de escritorio profesional e interactiva diseñada para la automatización y administración de procesos hospitalarios. Desarrollada en **Python**, implementa una arquitectura robusta que conecta una interfaz gráfica avanzada en **PyQt5** con un sistema de base de datos relacional integrado en **SQLite3**.

El sistema cuenta con un control de acceso basado en roles (RBAC) que divide las funciones operativas del hospital para garantizar la seguridad y eficiencia de los datos:
* **Rol Recepcionista:** Orientado al flujo de entrada del paciente y lectura general de la analítica.
* **Rol Tecnólogo Médico:** Orientado a la gestión clínica, análisis clínico profundo y manipulación de registros médicos de laboratorio.

## Características y Funcionalidades Principales

### 1. Registro e Ingreso de Pacientes (Módulo Frontend/Recepción)
* **Formulario Informativo Completo:** Permite la inscripción de pacientes capturando identificadores únicos, nombres, apellidos, RUT, dirección, edad, fecha de ingreso y correo electrónico.
* **Generación Automática de ID:** El sistema calcula e incrementa automáticamente el ID único del paciente en formato secuencial (`0001`, `0002`, etc.) consultando el último registro real en la base de datos.
* **Validación de Datos con Regex:** Implementación de expresiones regulares (`re`) y validadores Qt para asegurar el ingreso correcto de la información antes de guardarla:
  * Verificación de formato RUT chileno (ej. `12345678-K`).
  * Validación de estructura de correos electrónicos (`ejemplo@correo.com`)[cite: 4].
  * Restricciones de edad lógicas (rango de 0 a 120 años) y límites en las componentes de fecha[cite: 4].

### 2. Gestión de Exámenes Clínicos y Diagnósticos
* **Asignación por Clave Foránea:** Los tecnólogos pueden asociar múltiples exámenes diagnósticos a un paciente existente mediante su ID único, manteniendo la integridad referencial de la clínica[cite: 4].
* **Catálogo de Exámenes:** Soporte preconfigurado para pruebas clave: *Hemograma Completo, Perfil Bioquímico, Perfil Lipídico, Urocultivo y PCR Inmunológico*[cite: 4].
* **Límite de Seguridad Clínico:** El sistema restringe de manera inteligente que un mismo paciente posea más de 5 exámenes registrados en paralelo para evitar la saturación de datos[cite: 4].

### 3. Sistema CRUD Completo (Modificar y Eliminar Registros)
* **Búsqueda Multicriterio:** Motor de búsqueda integrado mediante combinación de tablas (`INNER JOIN`) que permite localizar el historial clínico de un paciente ingresando su ID, RUT o una coincidencia parcial de su nombre[cite: 4].
* **Modificación en Tiempo Real:** Permite seleccionar cualquier examen directamente desde una tabla dinámica (`QTableWidget`) y actualizar el tipo de examen, los resultados médicos o la fecha mediante ventanas de diálogo interactivas (`QInputDialog`)[cite: 4].
* **Eliminación Segura y en Cascada:** Los tecnólogos autorizados pueden remover registros médicos individuales con ventanas de confirmación previa[cite: 4]. La base de datos está configurada con `ON DELETE CASCADE`, asegurando que si un paciente es removido, sus exámenes asociados se limpien automáticamente para evitar datos huérfanos[cite: 4].

### 4. Motor de Cálculos Estadísticos y Analítica Gráfica
* **Cálculos Clínicos Automatizados:** Procesamiento instantáneo de consultas agregadas en SQL para computar el **Total de Pacientes Registrados** y el **Promedio de Edad** de la población hospitalaria actual[cite: 4].
* **Gráficos Dinámicos con Matplotlib:** Integración de un lienzo de visualización de datos (`FigureCanvasQTAgg`) dentro de la interfaz Qt[cite: 4]. Genera automáticamente un gráfico de barras interactivo que agrupa y cuenta la cantidad de exámenes clínicos realizados por cada tipo, actualizándose inmediatamente ante cualquier inserción, edición o borrado de datos[cite: 4].

---

## Imágenes

### Sistema de Autenticación de Usuarios (Login)
![Login](./Captura%20de%20pantalla%202026-06-18%20215646.png)

### Panel de Registro y Control Clínico
![Interfaz Principal](./Captura%20de%20pantalla%202026-06-18%20215703.png)

---

## Stack Tecnológico Utilizado

* **Lenguaje de Programación:** Python 3
* **Diseño e Interfaz Gráfica (GUI):** PyQt5 & Qt Designer (`.ui` XML)[cite: 4]
* **Motor de Base de Datos:** SQLite 3 (Enfoque Relacional)[cite: 4]
* **Visualización Científica:** Matplotlib (Lienzo dinámico)[cite: 4]
* **Entorno de Desarrollo:** Jupyter Notebook (`.ipynb`)[cite: 4]

---

## Requisitos e Instalación

Para ejecutar este entorno hospitalario de forma local:

1. **Clonar el repositorio** o descargar los archivos del proyecto.
2. **Instalar las dependencias** requeridas en tu entorno de Python:
```bash
   pip install PyQt5 matplotlib
