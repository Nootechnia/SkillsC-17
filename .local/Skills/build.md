# Build: Comandos de Build y Flujo de Trabajo

## Propósito
Plantilla genérica para comandos de build, configuración CMake y flujo de trabajo de compilación en proyectos C++. Sirve como referencia rápida para compilar, configurar y gestionar builds de cualquier repositorio.

## Configuración CMake

### Comando Base
```bash
# Desde la raíz del proyecto
cmake -S <directorio_proyecto> -B <directorio_build> [flags]
```

### Flags de Build Importantes

#### Tipo de Build
```bash
# Debug (activa ASan+UBSan en GNU/Clang)
cmake -S . -B build -DCMAKE_BUILD_TYPE=Debug

# Release (predeterminado, optimizado)
cmake -S . -B build -DCMAKE_BUILD_TYPE=Release

# Release con AddressSanitizer (GNU/Clang solo)
cmake -S . -B build -DCMAKE_BUILD_TYPE=Release -DENABLE_ASAN=ON

# Release con flags múltiples
cmake -S . -B build -DCMAKE_BUILD_TYPE=Release -DENABLE_ASAN=OFF -DFUNSHI_JAVA=ON -DFUNSHI_WEBUI=OFF
```

#### Generadores
```bash
# Generador por defecto (Linux)
cmake -S . -B build

# Generador Ninja (rápido)
cmake -S . -B build -G Ninja

# Generador Visual Studio (Windows)
cmake -S . -B build -G "Visual Studio 17 2022"

# Para igualar CI: construir Release sin ASAN por defecto
cmake -S . -B build -DCMAKE_BUILD_TYPE=Release -DENABLE_ASAN=OFF
```

## Build (Compilación)

### Comando Base
```bash
cmake --build build -j$(nproc)
```

### Build en Modos Específicos
```bash
# Release
cmake --build build -j$(nproc)

# Debug
cmake -S . -B build -DCMAKE_BUILD_TYPE=Debug
cmake --build build -j$(nproc)

# Con AddressSanitizer
cmake -S . -B build -DCMAKE_BUILD_TYPE=Release -DENABLE_ASAN=ON
cmake --build build -j$(nproc)
```

### Limpiar y Reiniciar
```bash
# Borrar build completo
rm -rf build/

# Reiniciar configuración desde cero
cmake -S . -B build -G Ninja -DCMAKE_BUILD_TYPE=Release -DENABLE_ASAN=OFF
cmake --build build -j$(nproc)
```

## Flujo de Trabajo Completo

### 1. Configurar Build
```bash
cmake -S . -B build -DCMAKE_BUILD_TYPE=Release -DENABLE_ASAN=OFF
```

### 2. Compilar
```bash
cmake --build build -j$(nproc)
```

### 3. Ejecutar
```bash
# Linux
cd build && ./<Ejecutable>

# Windows
cd build && ./<Ejecutable>.exe
```

### 4. Ejecutar Tests
```bash
cd build && ctest --output-on-failure
```

### 5. Verificar Build Limpio
```bash
# Build desde cero (limpio)
rm -rf build/
cmake -S . -B build -DCMAKE_BUILD_TYPE=Release -DENABLE_ASAN=OFF
cmake --build build -j$(nproc)
ctest --output-on-failure  # todos deberían pasar
```

## Flags de Build por Plataforma

### Linux (GNU/Clang)
- ASan por defecto en Debug: sí activar
- Release sin ASAN: trabajo diario
- Flags extra: `-fsanitize=address` si no usa CMake presets

### Windows (MSVC)
- El generador crea solución dentro de build dir
- No versionar archivos de solución .sln
- Sanitizers no activan ( incompatibles con MSVC cl.exe)
- Build Release es el estándar

### Cross-compilation
- Para Windows desde Linux: considerar MinGW
- CMakePresets.json para perfiles guardados
- Probar build en plataforma objetivo cuando sea posible

## Convenios de Build

### Debug vs Release
- **Debug**: `CMAKE_BUILD_TYPE=Debug` - activar ASan+UBSan en GNU/Clang
- **Release**: `CMAKE_BUILD_TYPE=Release` - trabajo diario, sin sanitizers
- **Híbrido**: `cmake -DCMAKE_BUILD_TYPE=Release -DENABLE_ASAN=ON` - debugging con sanitizers

### Build diarios vs CI
- **Daily work**: `cmake -S . -B build -DCMAKE_BUILD_TYPE=Release -DENABLE_ASAN=OFF`
- **CI/CD**: Igualar al trabajo diario para consistencia
- **Debugging**: Usar `cmake -DCMAKE_BUILD_TYPE=Debug` o `-DENABLE_ASAN=ON`

### Cuando Fallar el Build
1. Verificar cambios ajenos no modificados intencionalmente
2. Reportar fallo e indicar hay cambios pendientes
3. NO modificar archivos ajenos para "arreglar" build ajeno
4. Esperar a que cambios ajenos sean aplicados oficialmente

## Integración con Otras Skills

### Con `repo.md`
- Ver referencia rápida de comandos
- Casos de uso comunes documentados
- Estructura del repositorio

### Con `ci.md`
- Configuración de workflows de CI/CD
- Agregar nuevos targets de build a la suite

### Con `test.md`
- Ejecutar `ctest --output-on-failure` después de build
- Definir targets de test en CMakeLists.txt
- Convenios de nombres de targets

### Con `fix.md`
- Compilar con `cmake --build build -j$(nproc)` debe pasar después de fix
- Probar builds con `ENABLE_ASAN=ON` para verificar memory leaks
- Documentar en `fix.md` si el cambio afecta build

### Con `log.md`
- Generar log en `logs/` directory para builds largos
- Formato obligatorio: timestamps UTC, configuración CMake, progreso, duración
- No editar logs posteriores, generar nuevos entries