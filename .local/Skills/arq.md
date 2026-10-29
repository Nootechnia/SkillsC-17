# Arq: Estructura y Convenciones de Arquitectura

## Propósito
Plantilla genérica de convenciones de arquitectura para proyectos C++. Sirve como referencia para diseñar, documentar y mantener la estructura de cualquier repositorio de código C++.

## Directrices Generales de Arquitectura

### 1. Módulos y Componentes
- Los proyectos deben estar divididos en módulos lógicos con responsabilidades bien definidas
- Cada módulo debe tener un propósito claro y acotado
- Las dependencias entre módulos deben ser mínimas y explícitas
- No crear ciclos de dependencia entre módulos principales

### 3. Patrones de Diseño Recomendados
- Aplicar patrones que favorezcan la mantenibilidad a largo plazo
- Evitar acoplamiento innecesario entre componentes
- Usar inyección de dependencias cuando sea apropiado
- Preferir composición sobre herencia cuando la lógica lo permita

### 4. Serialización y Almacenamiento
- Los formatos de serialización deben ser versionables o diseñarse para compatibilidad hacia atrás
- Los cambios en el formato de datos deben manejarse con cuidado para no romper lecturas antiguas
- Acotar lecturas con límites superiores cuando se procesen datos estructurados

### 5. Pruebas y Validación
- La arquitectura debe facilitar tests unitarios e integración
- Los targets headless deben poder validar la lógica sin dependencias de GPU
- Los tests deben ser autónomos y no depender del orden de ejecución

### 5. Compatibilidad Multiplataforma
- Considerar Linux y Windows como plataformas objetivo principales
- Las APIs nativas del SO deben estar aisladas en capas de abstracción
- No asumir que headers o comportamientos existen en ambas plataformas
- Probar compilación cruzada regularmente

## Convenciones de Nomenclatura

### Nombres de Archivos y Carpetas
- Usar minúsculas con guiones bajos o camelCase de manera consistente
- Evitar espacios y caracteres especiales en nombres de archivos
- Los headers de API pública deben ir en include/ o directorio similar

### Nombres de Funciones y Métodos
- Convenios de nombre (PascalCase, camelCase, snake_case) deben definirse al inicio del proyecto
- Ser consistentes en todo el código base
- Los nombres deben describir la funcionalidad, no la implementación

## Directrices de Documentación

### Lo Que Debe Documentarse
- Estructura general del proyecto
- API pública y cómo usarla
- Patrones de diseño empleados
- Cómo compilar y ejecutar el proyecto
- Cómo ejecutar los tests

### Lo Que No Debe Documentarse en el Repo
- Contexto de tareas individuales
- Decisiones temporales sin documentación posterior
- Historias de por qué se tomó una decisión si ya no aplica

## Malas Prácticas Comunes a Evitar

| Práctica | Consecuencia | Recomendación |
|----------|-------------|---------------|
| Ciclos de dependencia | Código difícil de mantener y compilar | Revisar gráfico de dependencias regularmente |
| API pública inestable | Código que rompe con pequeños cambios | Congelar API antes de releases y documentar cambios |
| Falta de modularidad | Módulos que hacen demasiado | Refactorizar para separar responsabilidades |
| Dependencias ocultas | Código que rompe en diferentes plataformas | Aislar código dependiente de plataforma |
| Sin versionado de formato | Datos que dejan de leerse en nuevas versiones | Diseñar formatos versionables o de retrocompatibilidad |

## Buenas Prácticas

1. Mantener la documentación actualizada: La documentación debe reflejar el estado actual, no el pasado
2. Revisar arquitectura en cada cambio mayor: Antes de refactorizaciones significativas
3. Probar en todas las plataformas objetivo: Antes de considerar una tarea completada
4. Usar convenios de nombre consistentes: Definirlos al inicio y hacer cumplir
5. Documentar decisiones arquitectónicas: Las decisiones importantes deben tener registro

## Ejemplo de Uso

Al iniciar un nuevo proyecto o unirse a uno existente:

1. Revisar esta plantilla y adaptar las categorías al dominio del proyecto
2. Definir la estructura de carpetos y convenios de nombre
3. Establecer qué compone la API pública vs implementación interna
4. Documentar la estructura en docs/arquitectura.md (o equivalente)
5. Verificar que los patterns de diseño aplican al dominio del proyecto
6. Compilar y testear en las plataformas objetivo antes de considerar la base funcional

Este documento sirve como base que cada proyecto puede adaptar.
