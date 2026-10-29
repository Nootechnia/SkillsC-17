# Code: Convenciones de Código y Estilo

## Propósito
Esta plantilla sirve como referencia para las convenciones de código en proyectos C++ que sigan la arquitectura definida. Define estándares de estilo, nombres, copyright y flujo de trabajo para mantener consistencia en todo el proyecto.

## Idioma y Nombres
- **Idioma**: C++17. Identificadores, comentarios y logs en español
  (`fijarPosicion`, `AudioEngine::reproducir`). Nombres de tipo en PascalCase,
  métodos en camelCase.
- **Copyright**: TODO archivo fuente nuevo del motor debe llevar el header
  Apache 2.0 (ver cabecera de cualquier `.h`/`.cpp` existente como modelo) o
  al menos `SPDX-License-Identifier: Apache-2.0`.

## Estilo de Código
- **Indentación**: 4 espacios (no tabs)
- **Llaves**: Estilo K&R - apertura en misma línea, cierre en línea siguiente para clases/funciones
- **Longitud de línea**: Máximo 120 caracteres
- **Espacios en blanco**: Ninguna línea al final de archivo, un espacio después de ``, `;`, en operadores binarios

## Documentación en el Código y Sanitizador de Comentarios
### Normas Generales de Comentarios
- **Prohibido**: Uso de emojis, caracteres raros o símbolos no ASCII en comentarios
- **Excepción**: Solo caracteres ASCII estándar, salvo situaciones técnicas inevitables de implementación
- **Enfoque**: Comentarios precisos, centrados en código existente o arquitectura
- **Rol necesario**: Los comentarios deben cumplir una función técnica, no son redundantes o triviales
- **Ubicación**: Colocarse en lugares donde no interrumpan la lectura del código (margen, antes de bloques significativos, no dentro de líneas lógicas continuas)

## Archivos Relacionados en el Sistema de Skills

Esta plantilla forma parte de un conjunto más amplio de habilidades definidas en la carpeta `Skills/`. Los siguientes archivos están relacionados y pueden consultarse para una visión completa del procedimiento de trabajo:

- **`readme.md`**: Plantilla genérica para generar README.md en cualquier proyecto C++
- **`code.md`**: Convenciones de código y estilo (este documento)
- **`feat.md`**: Guía para implementar nuevas funcionalidades (features)
- **`refactor.md`**: Guía para refactorizar código existente
- **`fix.md`**: Guía para solucionar problemas y bugs comunes
- **`arq.md`**: Reglas y restricciones de arquitectura del proyecto
- **`doc.md`**: Guía de documentación y manuales de usuario
- **`license.md`**: Información sobre licencias y terceros
- **`ci.md`**: Configuración de integración continua y flujos de trabajo
- **`git.md`**: Flujo de trabajo y ramas del repositorio Git
- **`repo.md`**: Comandos esenciales para build y tests
- **`test.md`**: Patrones y estructura de tests unitarios y headless
- **`build.md`**: Comandos y opciones de build con CMake
- **`log.md`**: Sistema de logs y archivos de registro para builds largos
- **`memory.md`**: Memoria de trabajo y contexto entre sesiones del agente

## Cómo Utilizar Múltiples Skills en Conjunto

Cuando se trabaja en una tarea, se suele seguir este procedimiento:

1. **Leer `agents.md`** (en .local) para entender la arquitectura
2. **Consultar `code.md`** para estándares de implementación
3. **Revisar `feat.md` o `fix.md`** dependiendo de si es nueva funcionalidad o corrección
4. **Verificar `git.md`** para el flujo de commits y ramas
5. **Ejecutar tests** según `test.md`
6. **Generar logs** según `log.md` para builds largos
7. **Actualizar documentación** siguiendo `doc.md`
8. **Registrar contexto** en `memory.md` para sesiones futuras

## Referencia Cruzada Rápida

| Habilidad | Para Qué Sirve | Cuándo Usar |
|-----------|----------------|-------------|
| `agents.md` (.local) | Estructura general del proyecto | Antes de empezar cualquier tarea |
| `code.md` | Estándar de código y estilo | Al escribir o revisar código |
| `feat.md` | Implementar nuevas features | Cuando se añade funcionalidad |
| `fix.md` | Corregir bugs | Cuando hay un problema reportado |
| `arq.md` | Restricciones arquitectónicas | Al tocar módulos sensibles |
| `test.md` | Estructura de tests | Al escribir validación |
| `build.md` | Comandos de build | Configurar y compilar |
| `log.md` | Sistema de logs | Builds largos o exportaciones |
| `git.md` | Flujo de Git | Commits y ramas |
| `doc.md` | Documentación de usuario | Manuales y guides |
| `readme.md` | README del proyecto | Presentación del proyecto |

### Integración en el Flujo de Trabajo

Al iniciar una nueva tarea:

1. **Revisar `agents.md`** primero para entender restricciones
2. **Consultar `code.md`** para convenciones de estilo aplicables
3. **Si es feature**: Revisar `feat.md` para estructura propuesta
4. **Si es bug**: Revisar `fix.md` para procedimiento de depuración
5. **Ejecutar build**: Usar comandos de `build.md`
6. **Generar log** si la tarea es larga: Seguir `log.md`
7. **Ejecutar tests**: Según patrones en `test.md`
8. **Actualizar docs**: Si es necesario, consultar `doc.md`
9. **Registrar en `memory.md`** para la próxima sesión
10. **Hacer commit** siguiendo `git.md`

Este sistema asegura que ninguna tarea se inicie sin el contexto necesario y que todas las decisiones estén documentadas siguiendo estándares consistentes en todo el proyecto.
### Ejemplo de Comentario Malo (a evitar)
```cpp
// esto es un comentario
