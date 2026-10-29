# Memory: Memoria de Trabajo y Estructura del Agente

## Propósito
Sistema completo para que los agentes organicen su memoria de trabajo usando la carpeta `.local/.agentes/`. Esta skill define cómo crear, estructurar y mantener la memoria durante el trabajo en proyectos C++, con sintaxis específica para tareas y ramas.

## Estructura de Memoria del Agente

### Ubicación Base
Todos los agentes deben usar la carpeta `.local/.agentes/` en la raíz del proyecto para almacenar su memoria temporal. Esta carpeta no se versiona (debe estar en `.gitignore`), es persistente entre corridas del agente y almacena planes, estados, dudas pendientes y logs rápidos.

.agentes/(
(Informacion para trabajar)

PLAN-FIX/<TIPO_DE_PLAN>.md
PLAN-FEAT/<TIPO_DE_PLAN>.md
PLAN-REFACTOR/<TIPO_DE_PLAN>.md
PLAN-DOC/<TIPO_DE_PLAN>.md

MEMORY-FIX/<TIPO_DE_PLAN>.md
MEMORY-FEAT/<TIPO_DE_PLAN>.md
MEMORY-REFACTOR/<TIPO_DE_PLAN>.md
MEMORY-DOC/<TIPO_DE_PLAN>.md
)

## Comandos Rápidos para Gestionar Memoria

```bash
# Iniciar nueva tarea
mkdir -p .local/agentes/PLAN-nueva-tarea
# Copiar esta skill a la memoria del agente
cp /home/ggmaster/Desktop/Agentes/Trabajo/Skills/memory.md .local/agentes/PLAN-nueva-tarea/memoria.md
# Iniciar el progreso con timestamp UTC
echo "### $(date -u '+%Y-%m-%d %H:%M')" > .local/agentes/PLAN-nueva-tarea/progress.md

# Cambiar de branch
# Copiar estado del branch actual al nuevo
cp .local/agentes/BRANCH-antiguo/estado-branch.md .local/agentes/BRANCH-nuevo/estado-branch.md
# Actualizar según sea necesario

# Append progress (siempre append, nunca edit)
echo "### $(date -u '+%Y-%m-%d %H:%M')" >> .local/agentes/PLAN-*/progress.md

# Revisar dudas pendientes
ls .local/agentes/*/pendiente-revision/
```

## Referencias Cruzadas

### Sistema Integrado Complete
- **`code.md`**: Convenciones, sanitizador, definiciones rigurosas
- **`arq.md`**: Restricciones arquitectónicas a considerar
- **`feat.md`**: Estructura para nuevas funcionalidades
- **`fix.md`**: Procedimiento formal de corrección
- **`repo.md`**: Comandos Git y build esenciales
- **`test.md`**: Estructura y ejecución de tests
- **`ci.md`**: Integración Continua considerations
- **`log.md`**: Sistema obligatorio de logs .txt
- **`issues.md`**: Vincular issues a tasks y objectives

### Flujo de Trabajo Recomendado
1. **Iniciar**: Copiar `memory.md` a `.local/agentes/PLAN-*/`
2. **Ejecutar**: Follow `plan.md` estructura, append al `progress.md`
3. **Detectar duda**: Generar en `pendiente-revision/`, parar trabajo afectado
4. **Build/test**: `cmake --build build -j$(nproc)` y `ctest --output-on-failure`
5. **Documentar**: Si build largo, generar log en `logs/` siguiendo `log.md`
6. **Cambiar tarea**: `append progress.md`, guardar estado en `estado-branch.md`
7. **Terminar**: `commit: descripción`, limpiar o archive `.agentes/`
