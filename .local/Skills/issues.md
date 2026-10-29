# Issues: Guía de Manejo de Issues

## Propósito
Plantilla genérica para el manejo, clasificación y resolución de issues en proyectos C++. Sirve como referencia para cualquier repositorio que utilice sistemas de issue tracking.

## Tipos de Issues Soportados

### Bug Reports
- **Descripción**: Errores o comportamiento inesperado en el código
- **Campos obligatorios**: Título, descripción, pasos para reproducir, entorno
- **Etiqueta sugerida**: `bug`

### Feature Requests
- **Descripción**: Nuevas funcionalidades o mejoras propuestas
- **Campos obligatorios**: Título, descripción, caso de uso, beneficio esperado
- **Etiqueta sugerida**: `feature`

### Documentation
- **Descripción**: Mejoras o correcciones en la documentación
- **Campos obligatorios**: Título, sección afectada, tipo de mejora
- **Etiqueta sugerida**: `doc`

### Build/CI Issues
- **Descripción**: Problemas con la compilación, builds o integración continua
- **Campos obligatorios**: Título, comando/build que falla, mensaje de error
- **Etiqueta sugerida**: `build` o `ci`

### Performance
- **Descripción**: Problemas de rendimiento, FPS bajo, memory leaks
- **Campos obligatorios**: Título, métricas afectadas, condiciones de reproducción
- **Etiqueta sugerida**: `performance`

## Etiquetas y Categorías Recomendadas

| Categoría | Etiquetas | Cuando Usar |
|-----------|-----------|-------------|
| Errores | `bug` | Fallo en la ejecución o lógica incorrecta |
| Mejoras | `feature` | Nuevas funcionalidades solicitadas |
| Documentación | `doc` | Mejoras o correcciones en docs |
| Build | `build` | Fallos en compilación o cmake |
| CI | `ci` | Fracaso en integración continua |
| Performance | `performance` | Problemas de FPS, memory, etc. |
| Question | `question` | Dudas o aclaraciones necesarias |
| Area | `area` | Problemas en un módulo específico |

## Flujo de Trabajo de Resolución

### 1. Creación de Issue
- Usar template apropiado según el tipo
- Llenar todos los campos obligatorios
- Incluir versión del build y plataforma
- Agregar logs relevantes si aplica

### 2. Triage y Clasificación
- Revisar por un mantenedor o agente asignado
- Clasificar tipo y etiquetas
- Asignar a versión o milestone si corresponde
- Determinar prioridad (P0/P1/P2/P3)

### 3. Trabajo en el Issue
- Comentar con hallazgos mientras se investiga
- Crear branches `issue/#` para work
- Vincular commits con `closes #NN`
- Mantener issue actualizado con progreso

### 4. Validación y Cierre
- Probar fix en build limpio
- Verificar que no haya regressions
- Mover a `Done` cuando criteria de aceptación cumplan
- Cerrar con descripción breve de solución

## Plantillas Recomendadas

```yaml
# Bug Report Template
title: Bug report - <descripción corta>
labels: [bug]
body:
  - type: description
    id: description
    attributes:
      description: "Describe el bug aquí"
      required: true
  - type: steps-to-reproduce
    id: steps
    attributes:
      description: "Pasos para reproducir el error"
      required: true
  - type: environment
    id: environment
    attributes:
      description: "Versión, plataforma, build"
      required: true
```

## Integración con Otras Skills

### Con `code.md`
- Revisar convenciones de código antes de cerrar issues de tipo bug
- Seguir formato de commit para fixes

### Con `fix.md`
- Aplicar procedimiento formal de corrección para issues de bug
- Documentar solución en `fix.md` sección Bugs Resueltos

### Con `log.md`
- Generar log en `logs/` para issues que requieran builds largos
- Capturar timestamps y errores en log correspondiente

### Con `repo.md`
- Ver comandos de Git para cerrar issues
- `git commit -m "fix: describir solución"`
- `git push origin branch`