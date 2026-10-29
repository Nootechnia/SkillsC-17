# Refactor: Guía de Refactorización de Código

## Propósito
Esta plantilla sirve como referencia para refactorizar código existente en proyectos C++ que sigan la arquitectura definida. El objetivo es mejorar la estructura, legibilidad y mantenibilidad sin cambiar el comportamiento externo.

## Estructura Obligatoria para un Refactor

Todo proceso de refactorización debe seguir estas fases:

### 1. Análisis Previo
- **Codigo a refactorizar**: Identificar funciones, clases o módulos específicos
- **Riesgos potenciales**: Qué podría romper el cambio
- **Tests existentes**: Qué tests validan el comportamiento actual
- **Dependencias**: Qué otras partes del código tocan los cambios

### 2. Checklist de Refactorización
- [ ] El build sigue compilando (`cmake --build build -j$(nproc)`)
- [ ] Las tests pasan (`ctest --output-on-failure`)
- [ ] El comportamiento es idéntico (misma salida esperada)
- [ ] No hay nuevos warnings del compilador
- [ ] Documentación actualizada si firma de API cambió
- [ ] Código revisado por pares (obligatorio para cambios significativos)

## 3. Proceso de trabajo
- **Documentecion**: Antes de proceder se debe analizar la arquitectura asociada al problema.
- **Analisis**: Se debe plantear un analisis de la arquitectura relacionada al problema.
- **Verificacion**: Aprovechando la lectura se debe revisar la consistencia de la arquitectura revisada.
- **Sanitizacion**: En caso de encontrar problemas de arquitectura, bugs o inconsistencias. Se debe realizar una refactorizacion del codigo para resolver la problematica y segun el caso leer las  Skills necesarias.
- **Planificacion**: Una vez todo este preparado, realizamos el plan de refactor asociado al problema.

.agentes/(
(Informacion para trabajar)
PLAN-FIX/<TIPO_DE_PLAN>.md
PLAN-FEAT/<TIPO_DE_PLAN>.md
PLAN-REFACTOR/<TIPO_DE_PLAN>.md
PLAN-DOC/<TIPO_DE_PLAN>.md
)

- **Tests**: Una vez terminada la implementacion se deben realizar test que permitan validar la correctitud del codigo generado y de la funcionalidad.
- **Documentación**: Si se logra verificar la consistencia del codigo producido, se debe proceder con la documentacion del nuevo codigo y de los cambios realizados (en caso de ser necesario).

### 4. Validación Post-Refactor
```
# Build limpio
cmake -B build -S . -G Ninja -DCMAKE_BUILD_TYPE=Release
cmake --build build -j$(nproc)

# Todas las tests
cd build && ctest --output-on-failure -j$(nproc)

# Comparar comportamiento (si aplica)
./build/<ejecutable> # Ver misma salida esperada
```

## Riesgos Comunes y Cómo Evitarlos

| Riesgo | Consecuencia | Prevención |
|--------|-------------|------------|
| Romper API_scripting | Scripts dejen de funcionar | Probar con scripts existentes después |
| Cambiar firma de función | Quebrar compatibilidad C11 | Documentar cambios en `doc/MANUAL_DE_USO.md` |
| Introducir memory leak | Sanitizer detecta problema | Compilar con `ENABLE_ASAN=ON` y verificar |
| Romper compatibilidad Windows/MSVC | No compila en Visual Studio | Probar build en ambas plataformas |
