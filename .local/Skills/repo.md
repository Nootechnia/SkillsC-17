# Repo: Guía de Corrección de Problemas

## Propósito
Esta plantilla sirve como referencia para establecer informacion relacionada al repositorio en cuestion, la idea es que se modifique segun las necesidades del repositorio.

## Comandos Esenciales (Plataforma Independiente)

### Configuración y Compilación (CMake es el único build soportado)

```bash
# Configurar y compilar
cmake -S <directorio_proyecto> -B <directorio_build>
cmake --build <directorio_build> -j$(nproc)
```

- **CMake sin `-DCMAKE_BUILD_TYPE` fuerza Debug** (`CMakeLists.txt`), y en Debug se activan ASan+UBSan para compiladores GNU/Clang
- **Para build de trabajo normal y igualar la CI**:

```bash
cmake -S <directorio_proyecto> -B <directorio_build>     -DCMAKE_BUILD_TYPE=Release -DENABLE_ASAN=OFF
```
- **Con generador de Visual Studio**: el sanitizer no se activa ( `CMAKE_CXX_COMPILER_ID` no es GNU/Clang), así que el flag es inofensivo

### Flags de Build Importantes

```bash
# Build Release sin ASAN (común para trabajo diario)
cmake -S . -B build -DCMAKE_BUILD_TYPE=Release -DENABLE_ASAN=OFF

# Build con sanitizers (solo GNU/Clang, MSYS2 GCC no los linkea)
cmake -S . -B build -DCMAKE_BUILD_TYPE=Release -DENABLE_ASAN=ON -fsanitize=address
```

### Ejecutar la Suite de Tests

```bash
# Ejecutar todos los targets headless registrados
cd <directorio_build> && ctest --output-on-failure

# Nota: los targets de test se registran en CMakeLists.txt
# Agregar cualquier target de test nuevo en .github/workflows/ci.yml
```

### Ejecutar el Editor para Prueba Manual

```bash
# Linux
cd <directorio_proyecto> && ./build/<Ejecutable>

# Windows
cd <directorio_proyecto> && ./build/<Ejecutable>.exe
```

- **Lanzarlo desde el directorio del proyecto**: los assets y rutas relativas se resuelven contra el cwd
- **Salida (stdout y stderr)**: Se redirige a un archivo por arranque en `logs/`, junto al ejecutable —`<Proyecto>_<AAAAMMDD_HHMMSS>.log`, con timestamp **UTC**—, así que el editor no abre consola
- **Lo primero que hay que mirar** cuando algo falla es el archivo de log
```

## Flujo de Trabajo Básico

```bash
# 1. Configurar y compilar
cmake -S . -B build -DCMAKE_BUILD_TYPE=Release -DENABLE_ASAN=OFF
cmake --build build -j$(nproc)

# 2. Ejecutar
cd build && ./<Ejecutable>

# 3. Ejecutar tests
cd build && ctest --output-on-failure

# 4. Revisar logs si hubo problemas
ls -la logs/
```

## Convenios de Build

- **`cmake` sin `-DCMAKE_BUILD_TYPE` fuerza Debug**: los compiladores GNU/Clang activan ASan+UBSan en Debug
- **Build de trabajo normal**: Usar `-DCMAKE_BUILD_TYPE=Release -DENABLE_ASAN=OFF`
- **MSVC/Visual Studio**: El generador por defecto crea la solución dentro del directorio de build, no se versiona
- **Tests como parte del cambio**: Al tocar código fuente (o `CMakeLists.txt` y tests), revisar SIEMPRE si hay que actualizar el build y la suite
- **Build con cambios ajenos**: Si el build falla y hay archivos modificados por otros colaboradores (no tocados por el agente), reportar el fallo e indicar que hay cambios ajenos pendientes; NO modificar archivos ajenos para "arreglar" el build
