# Feat: Guía de Nuevas Funcionalidades

## Propósito
Esta plantilla sirve como referencia para implementar nuevas funcionalidades en proyectos C++ que sigan la arquitectura definida. Proporciona una estructura estandarizada para propuestas, implementación y validación de features.

## Estructura Obligatoria para un Feature

Todo feature debe seguir estas fases:

### 1. Propuesta del Feature
```
# Feature: <Nombre de la funcionalidad>

## Descripción
Breve descripción de qué hace y por qué es necesario.

## Justificación
- Beneficio principal para el proyecto
- Casos de uso principales
- Dependencias requeridas

## Alcance
- ¿Qué incluye este feature?
- ¿Qué está fuera del alcance?
- Posibles extensiones futuras
```

### 2. Checklist de Implementación
- [ ] Análisis arquitectónico previo
- [ ] Modificación de código necesario
- [ ] Actualización de CMakeLists.txt (si aplica)
- [ ] Nuevas dependencias (bibliotecas, herramientas)
- [ ] Pruebas unitarias/headless
- [ ] Actualización de documentación
- [ ] Pruebas manuales en el editor
- [ ] Validación en CI (GitHub Actions)

### 3. Criterios de Aceptación
- **Funcionalidad**: La feature funciona según su descripción
- **Compilación**: `cmake --build build -j$(nproc)` exitoso
- **Tests**: Las suites de tests relevantes pasan (`ctest --output-on-failure`)
- **Sin regressions**: No rompe funcionalidad existente
- **Documentación**: Docs actualizados si es necesario

## 4. Proceso de trabajo
- **Documentecion**: Antes de proceder se debe analizar la arquitectura asociada a la nueva funcionalidad.
- **Analisis**: Se debe plantear un analisis de la arquitectura relacionada a la nueva funcionalidad.
- **Verificacion**: Aprovechando la lectura se debe revisar la consistencia de la arquitectura revisada.
- **Sanitizacion**: En caso de encontrar problemas de arquitectura, bugs o inconsistencias. Se debe realizar una refactorizacion del codigo para resolver la problematica y segun el caso leer las  Skills necesarias.
- **Planificacion**: Una vez todo este preparado, realizamos el plan de integracion asociado a la nueva funcionalidad.

.agentes/(
(Informacion para trabajar)
PLAN-FIX/<TIPO_DE_PLAN>.md
PLAN-FEAT/<TIPO_DE_PLAN>.md
PLAN-REFACTOR/<TIPO_DE_PLAN>.md
PLAN-DOC/<TIPO_DE_PLAN>.md
)

- **Tests**: Una vez terminada la implementacion se deben realizar test que permitan validar la correctitud del codigo generado y de la funcionalidad.
- **Documentación**: Si se logra verificar la consistencia del codigo producido, se debe proceder con la documentacion del nuevo codigo y de los cambios realizados (en caso de ser necesario).
