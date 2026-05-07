![Consolidación de correos institucionales](https://github.com/user-attachments/assets/e518c1f4-66ae-48b2-a10b-8052411057e1)
<hr>

<p align="center">
  <img src="https://img.shields.io/badge/Estado-Finalizado-blue">
  <img src="https://img.shields.io/badge/Pandas-Data_Cleaning-orange">
</p>

### Índice
- [Descripción del proyecto](#computer-descripción-del-proyecto)
- [Arquitectura de Consolidación](#gear-arquitectura-de-consolidación)
- [Desafíos Técnicos Resueltos](#shield-desafíos-técnicos-resueltos)
- [Acceso al proyecto](#unlock-acceso-al-proyecto)
- [Tecnologías usadas](#briefcase-tecnologías-usadas)
- [Desarrollador](#bowtie-desarrollador)

## :computer: Descripción del proyecto
<p align="justify">
Este proyecto consiste en la creación de un sistema de consolidación y limpieza de datos para la gestión de correos institucionales de una organización con más de 1,050 colaboradores. El objetivo principal fue unificar información dispersa en tres fuentes de datos distintas (Base de Personal, Google Workspace y Directorio Activo) para asignar correctamente el correo electrónico institucional a cada trabajador.

Debido a la inconsistencia en los registros (nombres mal escritos, DNIs con formatos variables y cuentas funcionales), se implementó una estrategia de cruce multinivel que combina búsquedas exactas, mapeo por identidad (DNI) y algoritmos de lógica difusa (Fuzzy Matching) para garantizar la integridad de la información y reducir al mínimo la intervención manual.

Como oportunidad mejora, se puede implementar una `Selección Inteligente por Relevancia` en casos de múltiples cuentas asociadas a un mismo DNI. Al respecto, se recomienda realizar un análisis de similitud basado en apellidos e iniciales de los nombres para seleccionar el correo con mayor confianza.
</p>

## :gear: Arquitectura de Consolidación
El proceso se divide en etapas incrementales para asegurar la precisión:

:heavy_check_mark: `Normalización de Identidades:` Limpieza de DNIs (formato de 8 dígitos con ceros a la izquierda) y estandarización de nombres (eliminación de tildes, espacios extra y conversión a mayúsculas).

:heavy_check_mark: `Cruce por Identidad (DNI):` Primer nivel de vinculación utilizando el DNI como llave primaria entre la base de personal y el Directorio Activo, logrando la mayor tasa de acierto inicial.

:heavy_check_mark: `Búsqueda Difusa (Fuzzy Matching):` Para registros sin DNI, se utilizó la biblioteca **RapidFuzz** para comparar nombres con errores ortográficos, estableciendo un umbral de similitud del 90% para evitar falsos positivos.

:heavy_check_mark: `Consolidación Final:` Unificación de todos los niveles de cruce en un DataFrame maestro, eliminando redundancias y garantizando que cada uno de los 1,050 registros mantenga su integridad.

## :shield: Desafíos Técnicos Resueltos
- **El "Caso de las Celdas Invisibles":** Identificación y conversión de cadenas de espacios en blanco (`" "`) a valores nulos reales (`NaN`) para evitar errores en las métricas de cobertura.
- **Ambigüedad de Homónimos:** Resolución de conflictos donde un apellido común generaba múltiples coincidencias, identificando los índices de los cruces de información incorrectos tras una validación visual de la cuenta de correo correcta.
- **Optimización de Memoria:** Uso de técnicas de mapeo (`.map()`) en DataFrames de gran escala.

## :unlock: Acceso al proyecto
Puedes acceder al desarrollo completo en el cuaderno de Jupyter haciendo [click aquí](https://github.com/JLuceroVasquez/cruce_de_correos/blob/main/notebooks/cruce_correos_github.ipynb).

En el repositorio, se puede abrir el cuaderno de Jupyter en Google Colab haciendo click en el badge de color azul que está al principio.

*Nota: Para fines de demostración en este repositorio, se incluye un script generador de datos dummies que replica los errores de la base real de forma anonimizada.*

## :briefcase: Tecnologías usadas
- **Python**: Lenguaje principal.
- **Pandas**: Procesamiento y transformación de estructuras de datos.
- **Numpy**: Manejo de valores nulos y operaciones vectorizadas.
- **RapidFuzz**: Motor de búsqueda difusa de alta velocidad.
- **Faker**: Generación de datos sintéticos para pruebas y anonimización.
- **Regular Expressions (Re)**: Limpieza avanzada de patrones de texto.

## :bowtie: Desarrollador
|[<img src="https://avatars.githubusercontent.com/u/176303607?v=4" width=115> <br> <sub>Jimmy Octavio Lucero Vasquez</sub>](https://github.com/JLuceroVasquez)|
|:---:|
