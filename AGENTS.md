# AGENTS.md — CaféDMC

## 1. Qué es el sistema
CaféDMC es un sistema de pedidos para una cafetería: API en FastAPI, pantalla en
Streamlit y persistencia en SQLite. Gestionado con Poetry (`package-mode = false`).

## 2. Comandos (Poetry)
> Solo se listan comandos que ya existen en el proyecto.
- Instalar dependencias:  `poetry install`
- Pruebas:                `poetry run pytest -q`
- Estilo / lint:          `poetry run ruff check .`

Aún no hay dependencias de ejecución (FastAPI/Streamlit) instaladas, por lo que
todavía no existen comandos de arranque. Se añadirán aquí cuando se instalen.

## 3. Arquitectura
- `app/`       — código de la API FastAPI y la lógica de la aplicación.
- `tests/`     — pruebas con pytest.
- `scripts/`   — utilidades y tareas de apoyo.
- `db/`        — base de datos SQLite y esquema.
- `docs/adr/`  — Architecture Decision Records (pendiente de crear).

## 4. Reglas
- Dependencias **solo** con `poetry add` (nunca editar `pyproject.toml` a mano).
- SQL siempre **parametrizado**; prohibido concatenar valores en consultas.
- Cada endpoint debe llevar su prueba en `tests/`.
- No leer `.env` ni `data/`.
