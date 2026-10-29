# Test: Estructura y Ejecución de Tests

## Propósito
Plantilla genérica para la estructura y ejecución de tests en proyectos C++. Sirve como referencia para definir, organizar y correr la suite de tests de cualquier repositorio.

## Organización de Tests

### Directorio de Tests
- Los targets de test se registran en `CMakeLists.txt`
- Los tests headless validan lógica sin dependencias de GPU
- Separar tests por módulo o funcionalidad
- Usar nombres descriptivos: `<modulo>-tests` o `<funcion>-tests`

### Tipos de Tests Recomendados

#### Tests Unitarios
- Validar funciones y clases individuales
- Ejecutar rápido (miliseconds)
- No depender de estado global
- Ejemplo: `./renderer-tests`, `./math-tests`

#### Tests de Integración
- Validar interacción entre módulos
- Pueden requerir setup previo
- Ejecutar después de cambios mayores

#### Tests Headless
- Validar sin dependencias de renderizado/GUI
- Ejecutar en targets sin display
- Ideales para CI/CD pipelines
- Ejemplo: `./build/<ejecutable>-tests`

## Ejecutar Suite de Tests

### Ejecutar Todas las Pruebas
```bash
cd build && ctest --output-on-failure
```

### Ejecutar Suite Concreta
```bash
# Ejemplo de nombres de targets registrados en CMakeLists:
./<nombre-suite>-tests
# Ejemplos:
./rendering-tests
./particulas-tests
./scripts-tests
./fisica-tests

# Con output detallado de fallos
cd build && ctest --output-on-failure -V
```

### Ejecutar Test Específico por Nombre
```bash
# Si el target se llama rendering-tests
./rendering-tests

# O mediante ctest con filter
cd build && ctest -R "rendering*" --output-on-failure
```

## Definir Tests en CMakeLists.txt

```cmake
# Registrar target de test headless
add_test(
  NAME rendering_test
  COMMAND ./rendering-tests
  WORKING_DIRECTORY build
)

# Registrar target de test particulas
add_test(
  NAME particulas_test  
  COMMAND ./particulas-tests
  WORKING_DIRECTORY build
)

# Habilitar testing a nivel de proyecto
enable_testing()
```

## Convenios de Nomenclatura

### Nombres de Targets
- Usar guiones bajos para separar palabras: `rendering_tests`
- Prefijo opcional por módulo: `rendering-`, `particulas-`, `scripts-`
- Evitar espacios y caracteres especiales

### Contenido de Tests
- Tests deben ser autónomos y no depender del orden
- Cada test debe tener un caso de uso claro
- Usar framework Catch2, Google Test, o similar
- Evitar dependencias globales entre tests

## Integración con Otras Skills

### Con `repo.md`
- Ver comandos esenciales: `cd build && ctest --output-on-failure`
- Configuración CMake para habilitar testing
- Flags de build importantes (Debug vs Release)

### Con `ci.md`
- Agregar targets de test a suite de CI/CD
- Badges de cobertura y status
- Trigger de tests en push y pull request

### Con `fix.md`
- Verificar que tests pasen después de aplicar fix
- `ctest --output-on-failure` debe quedar en verde
- Documentar en `fix.md` sección Bugs Resueltos si aplica

### Con `code.md`
- Revisar convenciones antes de escribir tests
- Definiciones rigurosas para términos de test
- Menciona esta skill en convenciones de código