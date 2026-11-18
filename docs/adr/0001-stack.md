# ADR 0001 — Stack tecnológico de CaféDMC

**Estado:** Aceptado
**Fecha:** 2026-11-16

## Contexto
El equipo sabe Python. Cada alumno ejecuta el proyecto en su propia laptop, sin
Docker, con la menor fricción de instalación posible. Además, los agentes de IA
deben poder leer, probar y modificar el sistema con facilidad, por lo que se
valora un stack pequeño, explícito y fácil de razonar.

## Decisión
Adoptar: **Python 3.11+**, **Poetry** (gestión de dependencias y entorno),
**FastAPI + Pydantic** (API y validación), **SQLite** (persistencia en archivo),
**Streamlit** (pantalla), **pytest** (pruebas) y **ruff** (estilo/lint).

## Consecuencias
**(+)**
- Un solo lenguaje (Python) de extremo a extremo; curva de entrada mínima.
- SQLite no requiere servidor: funciona en cualquier laptop sin Docker.
- Stack ligero y explícito, fácil de leer, probar y modificar por humanos e IA.
- FastAPI + Pydantic dan tipos y validación claros; pytest y ruff cuidan calidad.

**(−)**
- SQLite escala mal en concurrencia/escritura; no apto para producción grande.
- Streamlit es cómodo pero limita el control fino de la interfaz.
- Dos procesos separados (API y pantalla) que hay que arrancar y coordinar.

## Alternativas consideradas
- **Django** (en vez de FastAPI): framework completo con ORM y admin, pero más
  pesado y con más convenciones que aprender. Para una API pequeña añade
  complejidad innecesaria; FastAPI es más ligero y directo para este alcance.
- **PostgreSQL** (en vez de SQLite): más robusto y concurrente, pero exige un
  servidor (o Docker) por laptop, lo que rompe el requisito de instalación
  simple. SQLite basta para el tamaño y el uso didáctico del proyecto.
