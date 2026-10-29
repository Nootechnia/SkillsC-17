# License

## Propósito
Guía para crear y mantener archivos de licencia en el proyecto.

## Estructura de Licencias en el Repositorio

Según ARQUITECTURA.md, la licencia principal y las de terceros deben organizarse en tres áreas:

### 1. Licencias raíz
- `LICENSE` - Licencia principal del proyecto (Apache 2.0, MIT, GPL, etc.)
- `NOTICE` - Avisos legales breves

### 2. Licencias en `.local/`
- `.local/LICENSE` - Copia o referencia a la licencia principal
- `.local/NOTICE` - Avisos adicionales

### 3. Documentación en `Skills/license.md`
- Guía sobre cómo crear y mantener las licencias



## Terceros (THIRD_PARTY_NOTICES.md)

Estructura de tabla para documentar bibliotecas externas:

| Componente | Ubicación | Licencia | Titular |
|---|---|---|---|
| <nombre> | <ruta> | <tipo> | <copyright> |

## Tipos Comunes

- **Apache 2.0**: Permisiva, requiere mantener copyright y license notice
- **MIT**: Extremadamente permisiva, solo copyright + permission notice
- **GPL v3**: Copyleft fuerte, obras derivadas bajo misma licencia
- **BSD 3-Clause**: Similar a MIT con cláusula de no-endorsement

## Buenas Prácticas

1. Mantener THIRD_PARTY_NOTICES.md actualizada al cambiar dependencias
2. Usar formato consistente en todos los archivos de licencia
3. Hacer los archivos de licencia fácilmente encontrables
4. Incluir sección de licencia en README.md

## Ejemplo de Estructura de Archivos

/project-root/
├── LICENSE
├── NOTICE
├── THIRD_PARTY_NOTICES.md
├── .local/LICENSE
├── .local/NOTICE
└── Skills/license.md

## Cómo Aplicar la Licencia

```
Copyright [year] [nombre del autor]

Licensed under the <License Name>, Version <X.X> (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-<version>

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
