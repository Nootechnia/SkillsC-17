# Fix: Guía de Corrección de Problemas

## Propósito
Esta plantilla sirve como referencia para solucionar problemas y bugs comunes en proyectos C++ que sigan la arquitectura definida. Proporciona un procedimiento estandarizado para identificar, analizar y corregir problemas sin copiar contenido de proyectos específicos.

## Estructura para la Corrección de Problemas

Todo proceso de corrección debe seguir estas fases:

### 1. Identificación del Problema
- **Síntoma**: Describir el comportamiento inesperado observado
- **Ubicación**: Identificar el archivo, línea y función afectada
- **Contexto**: Version del build, plataforma, circunstancias al observarse

### 2. Análisis de Causa
- **Investigación**: Revisar código, logs y historial de commits
- **Hipótesis**: Proponer causas posibles basadas en el análisis
- **Validación**: Verificar hipótesis cambiando una variable a la vez

### 3. Desarrollo del Fix
- **Solución**: Implementar la corrección mínima necesaria
- **Pruebas**: Compilar y ejecutar tests relevantes
- **Sanitizer**: Corregir build con `ENABLE_ASAN=ON` y verificar no haya memory leaks
- **Compatibilidad**: Verificar en ambas plataformas (Linux y Windows)

### 4. Validación Final
- **Build completo**: `cmake --build build -j$(nproc)` exitoso
- **Tests**: `ctest --output-on-failure` en verde
- **Usuario**: Probar el fix en la aplicación real (criterio de aceptación)
- **Documentación**: Actualizar docs si la API cambió

## Procedimiento Formal ante Ambigüedades

Cuando un bug no se resuelve leyendo el código, seguir la cadena: `síntoma → evidencia → causa → fix → test`, usando instrumentación y reproducirlo de forma determinista, aislando una sola variable por corrida.

## Patrones y Buenas Prácticas

- Usar tipo ej: `Expected<T>`, propio para errores
- Seguir cadena `síntoma → evidencia → causa → fix → test`
- Reducir fallos a tests headless antes que corridas manuales
- Usar sondas y laboratorios en directorios locales ignorados por git (en .local/.agentes)
- Experimentos deterministas: fijar todo lo que no es la variable bajo prueba
- Comparar hechos, no apariencias: bytes, mtimes y tamaños con herramientas del toolchain
- Sanitizadores en C++ con `ENABLE_ASAN` (por defecto ON, OFF en MSYS2 GCC)
- Varias circunstancias, un solo fix: reproducir en variantes distintas

## Errores Comunes a Evitar

| Error | Consecuencia |Prevención|
|-------|-------------|----------|
| Romper API de scripts | Scripts dejan de funcionar | Probar con scripts existentes después |
| Introducir memory leak | Sanitizer detecta problema | Compilar con `ENABLE_ASAN=ON` y verificar |
| Cambiar firma de función | Quebrar compatibilidad C11 | Documentar cambios en `doc/MANUAL_DE_USO.md` |
| Romper compatibilidad Windows | No compila en Visual Studio | Probar build en ambas plataformas |
