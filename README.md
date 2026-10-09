# Kit de demos · Sesión 03 · Ingeniería de prompts y de contexto

Diplomado en Ingeniería de Software con IA y Sistemas Agénticos · FET

## Preparación (una vez)

```bash
ollama pull qwen3.5:4b
ollama pull phi4-mini
ollama pull qwen3.5:0.8b
pip install -U ollama pydantic
```

Ejecute los scripts desde la carpeta `scripts/`. Todos usan `qwen3.5:4b` con el razonamiento apagado,
temperatura 0 y semilla 42, salvo que se indique otra cosa.

## Orden de uso en clase

| Diapositiva | Demo | Archivo |
|---|---|---|
| Un modelo, dos prompts | Pegar A y luego B en `ollama run qwen3.5:4b --think=false` | `prompts/01_gancho_A.txt`, `01_gancho_B.txt` |
| Primer uso | Terminal y luego Python | `scripts/01_primer_uso.py` |
| Parámetros de inferencia | Misma pregunta con temperatura alta y con 0 | `scripts/demo_temperatura.py` |
| System prompt · práctica 1 | `/set system` + función con error | `revisor-fet/system_revisor_fet_una_linea.txt` |
| System prompt · práctica 2 | `ollama create revisor-fet -f Modelfile` (desde la carpeta `revisor-fet`) | `revisor-fet/Modelfile` |
| Puente a agentes | Mostrar el archivo | `revisor-fet/AGENTS.md` |
| La fórmula aplicada | Antes y después | `prompts/02_formula_antes.txt`, `02_formula_despues.txt` |
| Zero-shot | Cambiar el reporte por los otros tres de la diapositiva | `prompts/03_zero_shot.txt` |
| Few-shot | | `prompts/04_few_shot.txt` |
| Delimitadores | | `prompts/05_delimitadores.txt` |
| Cadena de pensamiento | `ollama run phi4-mini`: primero sin, luego con | `prompts/06_cot_sin.txt`, `06_cot_con.txt` |
| Modelo razonador | `ollama run qwen3.5:4b` **sin** `--think=false` (tarda minutos en CPU) | `prompts/06_cot_razonador.txt` |
| Encadenamiento | A mano (paso 1 a 4) o automático | `prompts/07_cadena_*.txt`, `scripts/cadena.py` |
| Rol | Tres roles, misma pregunta | `prompts/08_rol_*.txt` |
| Formato: tabla | | `prompts/09_formato_tabla.txt` |
| Formato: JSON Schema | | `scripts/reporte_json.py` |
| Más no es mejor | `--num_ctx 2048` y luego `--num_ctx 8192` | `scripts/demo_contexto.py` |
| Prompt injection | System ingenuo en `qwen3.5:0.8b` vs. `revisor-fet` | `prompts/10_*.txt` |
| Optimizar con IA | Pegar en un modelo grande | `prompts/11_meta_prompt.txt` |
| Evaluar prompts | v1 contra v2 | `scripts/evalua.py` |

## Notas

- **Razonamiento:** si su versión de Ollama no reconoce `--think=false`, dentro del chat use `/set nothink`.
  En Python se controla con `think=False` (ya incluido en `scripts/comun.py`).
- **Resultados variables:** con modelos de 1–4 B la salida cambia entre versiones. Ensaye cada demo antes de clase.
- **demo_contexto.py:** el corte exacto depende del modelo y de la versión de Ollama. El script muestra cuántos
  tokens leyó el modelo; si con 2048 todavía responde bien, suba `--articulos`.
- **Respuestas esperadas del zero-shot:** «avisara por correo» → MEJORA; «¿cuántos libros…?» → DUDA;
  «renovar es lentísimo» → BUG (decisión del equipo; es el caso ambiguo).
