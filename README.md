# 🛠️ Modelado de un Proceso de Software con SPEM 2.0: Gestión de Defectos

Este repositorio contiene la especificación, modelado formal y documentación del proceso de **Gestión de Defectos**, desarrollado con el metamodelo **SPEM 2.0** (*Software & Systems Process Engineering Metamodel*) utilizando la herramienta **EPF Composer**.

## 📌 Información del Proyecto

* **Autor:** Everson Leandro Restrepo Gaviria

## 📖 Tabla de Contenidos

* [Introducción](#-introducción)

* [Descripción del Proceso](#-descripción-del-proceso)

  * [Propósito y Contexto](#propósito-y-contexto)

  * [Fases del Proceso](#fases-del-proceso)

  * [Matriz de Tareas, Entradas y Salidas](#matriz-de-tareas-entradas-y-salidas)

  * [Roles y Responsabilidades](#roles-y-responsabilidades)

* [Principales Desafíos](#-principales-desafíos)

* [Modelo SPEM 2.0 y EPF Composer](#-modelo-spem-20-y-epf-composer)

  * [Estructura del Método](#estructura-del-método)

  * [Delivery Process](#delivery-process)

* [Conclusiones](#-conclusiones)

* [Bibliografía](#-bibliografía)

## 🚀 Introducción

La ingeniería de procesos de software busca describir, analizar y mejorar la forma en que los equipos construyen software. Un proceso que solo existe en la práctica y en la memoria de quienes lo ejecutan es difícil de comunicar, evaluar y mejorar.

Este proyecto formaliza el proceso de **Gestión de Defectos** (desde el reporte inicial hasta la verificación y cierre definitivo) usando el estándar **SPEM 2.0** de la OMG. El modelo se construyó en **Eclipse Process Framework (EPF) Composer**, separando el contenido del método (*Method Content*) del proceso (*Process*).

## 🔄 Descripción del Proceso

### Propósito y Contexto

El propósito fundamental es garantizar que:

1. Ningún defecto se pierda o quede sin asignación clara.

2. Se atiendan prioritariamente los defectos más críticos.

3. Ningún defecto se cierre sin verificar objetivamente que la corrección funciona y no genera regresiones.

Aplica a equipos de desarrollo pequeños o medianos que mantienen productos en evolución constante.

### Fases del Proceso

El ciclo se organiza en tres fases secuenciales con un **bucle de retroalimentación** en la fase de verificación:

```
graph TD
    A[Inicio: Defecto Detectado] --> Phase1[Fase 1: Registro y Triage]
    Phase1 --> M1((Hito: Defecto Asignado))
    M1 --> Phase2[Fase 2: Resolución]
    Phase2 --> Phase3[Fase 3: Verificación y Cierre]
    
    Phase3 -->|Verificación Fallida / Regresión| Phase2
    Phase3 -->|Verificación Exitosa| M2((Hito: Defecto Verificado))
    M2 --> B[Defecto Cerrado]

```

1. **Fase 1: Registro y triage**

   * **Objetivo:** Documentar el defecto, asignarle prioridad, severidad y un responsable.

   * **Tareas:** *Reportar defecto*, *Priorizar y asignar defecto*.

   * **Hito:** `Defecto asignado`.

2. **Fase 2: Resolución**

   * **Objetivo:** Comprender el origen del problema y eliminarlo.

   * **Tareas:** *Analizar causa raíz*, *Corregir defecto*.

3. **Fase 3: Verificación y cierre**

   * **Objetivo:** Confirmar que el defecto se resolvió adecuadamente sin efectos colaterales.

   * **Tareas:** *Verificar corrección*, *Cerrar defecto*.

   * **Hito:** `Defecto verificado`.

### Matriz de Tareas, Entradas y Salidas

| Tarea | Rol Principal | Entradas (Input Work Products) | Salida (Output Work Product) | 
 | ----- | ----- | ----- | ----- | 
| **Reportar defecto** | Reportante | — | Reporte de defecto | 
| **Priorizar y asignar defecto** | Líder Técnico | Reporte de defecto | Reporte de defecto (actualizado) | 
| **Analizar causa raíz** | Desarrollador | Reporte de defecto | Análisis de causa raíz | 
| **Corregir defecto** | Desarrollador | Reporte de defecto, Análisis de causa raíz | Corrección | 
| **Verificar corrección** | Tester *(Apoyo: Reportante)* | Reporte de defecto, Corrección, Checklist de verificación | Evidencia de prueba | 
| **Cerrar defecto** | Líder Técnico | Evidencia de prueba, Reporte de defecto | Defecto cerrado | 

### Roles y Responsabilidades

| Rol | Responsabilidad Principal | Artefactos a Cargo (Work Products) | 
 | ----- | ----- | ----- | 
| **Reportante** | Detectar y describir el defecto con pasos reproducibles y evidencia. Apoyar en la verificación si se requiere. | Plantilla de reporte de defecto, Reporte de defecto | 
| **Líder Técnico** | Tomar decisiones sobre el flujo del defecto, asignar severidad/prioridad, asignar desarrollador y realizar el cierre formal. | Defecto cerrado | 
| **Desarrollador** | Reproducir el error, identificar causa raíz, implementar la solución y validarla localmente. | Análisis de causa raíz, Corrección | 
| **Tester** | Ejecutar pruebas independientes de la corrección y pruebas de regresión. | Checklist de verificación, Evidencia de prueba | 

> 💡 **Nota de Diseño:** La separación entre el Desarrollador (quien corrige) y el Tester (quien verifica) es deliberada para garantizar objetividad en el control de calidad.

## ⚡ Principales Desafíos

* **Calidad de los reportes:** Evitar reportes vagos (ej. *"no funciona"*) mediante el uso obligatorio de una plantilla de reporte estandarizada.

* **Cuellos de botella en el triage:** Prevenir la sobresaturación del Líder Técnico mediante criterios claros y objetivos para clasificar severidad vs. prioridad.

* **Soluciones superficiales:** Exigir la tarea *Analizar causa raíz* para evitar corregir únicamente el síntoma.

* **Equilibrio de formalidad:** Mantener el nivel de rigurosidad necesario sin sobrecargar al equipo con burocracia excesiva.

## 🏗️ Modelo SPEM 2.0 y EPF Composer

### Estructura del Método

El contenido del método (*Method Content*) se definió de manera independiente a la estructura del proceso para favorecer la reutilización:

* **Roles:** Reportante, Líder Técnico, Desarrollador, Tester.

* **Work Products:** Reporte de defecto, Análisis de causa raíz, Corrección, Evidencia de prueba, Defecto cerrado, Checklist de verificación, Plantilla de reporte.

* **Tasks:** Reportar, Priorizar/Asignar, Analizar causa raíz, Corregir, Verificar, Cerrar.

* **Guidance:** Plantillas y checklists.

### Delivery Process

El proceso principal (*Delivery Process*) ensambla tres **Capability Patterns**:

1. `Registro y triage`

2. `Resolución`

3. `Verificación y cierre`

```
[Registro y triage] ──> [Resolución] ──> [Verificación y cierre]

```

## 📝 Conclusiones

* **Explicitación del Proceso:** El uso de SPEM 2.0 permitió transformar un flujo informal en un modelo estructurado, claro y reutilizable.

* **Visibilidad de Inconsistencias:** El proceso de modelado formal sacó a la luz ambigüedades sobre responsabilidades de roles y criterios de cierre que pasaban desapercibidos en la práctica diaria.

* **Equilibrio Agilidad / Disciplina:** Es crucial adaptar la formalidad del proceso al tamaño y contexto del equipo de desarrollo.

* **Herramientas:** EPF Composer ofrece una plataforma potente para la publicación de sitios web con la documentación de procesos, aunque requiere superar su curva de aprendizaje inicial respecto al metamodelo SPEM 2.0.

## 📚 Bibliografía

1. **Eclipse Foundation.** (s. f.). *Eclipse Process Framework (EPF) Project*. [https://www.eclipse.org/epf/](https://www.eclipse.org/epf/?utm_source=gemini)

2. **Object Management Group (OMG).** (2008). *Software & Systems Process Engineering Metamodel Specification (SPEM)*, Version 2.0 (formal/2008-04-01). [https://www.omg.org/spec/SPEM/2.0/](https://www.omg.org/spec/SPEM/2.0/?utm_source=gemini)