# CI: Integración Continua y Entrega

## Propósito
Plantilla genérica para configuración e información sobre integración continua y entrega continua en proyectos C++. Sirve como referencia para cualquier sistema de CI (GitHub Actions, GitLab CI, Jenkins, etc.).

## Configuración de CI/CD

### GitHub Actions (Ejemplo Básico)
```yaml
name: CI

on:
  push:
    branches: [main, dev]
  pull_request:
    branches: [main, dev]

jobs:
  build:
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v3
    
    - name: Configurar CMake
      run: cmake -S . -B build -DCMAKE_BUILD_TYPE=Release -DENABLE_ASAN=OFF
    
    - name: Compilar
      run: cmake --build build -j$(nproc)
    
    - name: Ejecutar Tests
      run: ctest --output-on-failure
```

### GitLab CI (Ejemplo Básico)
```yaml
stages:
  - build
  - test

build:
  stage: build
  script:
    - cmake -S . -B build -DCMAKE_BUILD_TYPE=Release -DENABLE_ASAN=OFF
    - cmake --build build -j$(nproc)

test:
  stage: test
  script:
    - ctest --output-on-failure
```

### Configuración Cruzada (Linux/Windows)
- **Linux**: Usar `ubuntu-latest` o `windows-latest` para GitHub Actions
- **Windows**: El generador por defecto crea solución MSVC dentro del directorio de build
- **Sanitizers**: Solo activan en GNU/Clang, no en MSVC cl.exe
- **Build types**: Debug activa ASan+UBSan en compiladores GNU/Clang

## Comandos de Prueba Recomendados

```bash
# Verificar que el build de CI funcione localmente
cmake -S . -B build -DCMAKE_BUILD_TYPE=Release -DENABLE_ASAN=OFF
cmake --build build -j$(nproc)
ctest --output-on-failure

# Con AddressSanitizer
cmake -S . -B build -DCMAKE_BUILD_TYPE=Release -DENABLE_ASAN=ON
cmake --build build -j$(nproc)
ctest --output-on-failure
```

## Cobertura de Tests

### Targets Headless
- Los tests headless validan lógica sin dependencias de GPU
- Ejecutar en cada push para detectar regresions
- Utilizar para validar cambios en módulos de bajo nivel

### Tipos de Tests
- **Unitarios**: Validar funciones y clases individuales
- **Integración**: Validar interacción entre módulos
- **Headless**: Validar sin renderizado (requiere build con ASAN opcional)

## Badges Recomendados

```markdown
[![CI Build](https://github.com/usuario/repo/actions/workflows/ci.yml/badge.svg)](https://github.com/usuario/repo/actions/workflows/ci.yml)
[![Test Coverage](https://codecov.com/usuario/repo/badge.svg)](https://codecov.com/usuario/repo)
[![Build Status](https://ci.example.com/build/status/repo)](https://ci.example.com/build/status/repo)
```

## Integración con Otras Skills

### Con `repo.md`
- Verificar que los comandos de build y test coincidan con los documentados
- Revisar flags de CMake antes de agregar a CI

### Con `test.md`
- Documentar qué targets de test ejecutar en la CI
- Agregar nuevos targets de test en la suite de CI

### Con `log.md`
- Generar logs de build largos en `logs/` directory
- Redirigir output de ctest a archivos por corrida

### Con `code.md`
- Revisar convenciones de código antes de fusionar
- Verificar que los commits sigan formato convencional