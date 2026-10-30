# Corpus documental – ACA 1 (Pilar Ventas)

Corpus **mixto**: tres documentos académicos simulados en español y un manual de usuario real del fabricante.

## 1. Inventario

| ID | Archivo | Tipo (`doc_type`) | Naturaleza | Idioma | Fuente |
|---|---|---|---|---|---|
| D1 | `01_politica_devoluciones_reembolsos.md` | `politica_devoluciones` | Simulado (tienda ficticia NovaLectura) | es | Elaboración propia para el ACA |
| D2 | `02_politica_garantia.md` | `politica_garantia` | Simulado | es | Elaboración propia para el ACA |
| D3 | `03_terminos_servicio_sla.md` | `terminos_servicio_sla` | Simulado | es | Elaboración propia para el ACA |
| D4 | `04_manual_<producto>.pdf` | `manual_usuario` | **Real** | en | Fabricante – **URL pendiente de verificar** |
| DS | Reseñas (muestra del dataset) | `review` | Real | en | Datafiniti (2019), Kaggle |

**Reglas:**
- Los documentos D1–D3 son ficticios. Se declaran como *material académico simulado* en el notebook, el póster y el video.
- El manual D4 **no se sube al repositorio público**. El notebook lo descarga desde `MANUAL_URL`, o se carga manualmente en Colab.
- El producto del manual D4 se elige **después de explorar el dataset**: será uno de los productos más reseñados, para enlazar ambas fuentes con el metadato `product`.

## 2. Metadatos por fragmento (payload en Qdrant)

`chunk_id`, `doc_id`, `source_file`, `doc_type`, `simulated` (bool), `language`, `page` (solo PDF), `chunk_index`, `product` (manual y reseñas), `rating` (reseñas), `text`.

## 3. Referencias normativas citadas en D1–D3 (verificar texto oficial vigente)

- Ley 1480 de 2011, Estatuto del Consumidor: art. 47 (retracto), art. 51 (reversión del pago) y garantía legal.
- Ley 2439 de 2024: modifica el art. 47 de la Ley 1480.
- Decreto 587 de 2016: reglamenta el art. 51 de la Ley 1480. Disponible en https://sedeelectronica.sic.gov.co/sites/default/files/normatividad/Decreto_587_2016.pdf
- Ley 1581 de 2012: protección de datos personales.

## 4. Conjunto de preguntas de prueba (referencia esperada)

Este conjunto alimenta la Sección 10 del notebook. Las preguntas sobre D4 se ajustarán al manual que se descargue.

| ID | Pregunta | Tipo | Documento esperado | Sección esperada |
|---|---|---|---|---|
| Q01 | ¿Cuántos días tengo para retractarme de una compra? | Respondible | D1 | 2. Derecho de retracto |
| Q02 | ¿En cuánto tiempo me devuelven el dinero si ejerzo el retracto? | Respondible | D1 | 2. Derecho de retracto |
| Q03 | ¿Qué pasos debo seguir para solicitar un reembolso? | Respondible | D1 | 5. Procedimiento |
| Q04 | Me llegó el producto roto, ¿qué hago? | Respondible | D1 | 4. Producto dañado |
| Q05 | ¿Cuánto dura la garantía de un lector electrónico? | Respondible | D2 | 2. Términos por categoría |
| Q06 | ¿La garantía cubre si se me cae el dispositivo al agua? | Respondible | D2 | 4. Exclusiones |
| Q07 | ¿Qué pasa si la misma falla se repite después de la reparación? | Respondible | D2 | 6. Repetición de la falla |
| Q08 | ¿Cuánto tarda un envío a Bogotá? | Respondible | D3 | A.5 Envíos |
| Q09 | ¿Puedo cancelar un pedido que ya fue despachado? | Respondible | D3 | A.4 Cancelación |
| Q10 | ¿En cuánto tiempo responden una queja o reclamo? | Respondible | D3 | B.2 Tiempos de respuesta |
| Q11 | ¿Cómo cargo la batería del dispositivo? | Respondible | D4 | Pendiente (según el manual) |
| Q12 | ¿Qué opinan los clientes sobre la duración de la batería? | Respondible | DS | Reseñas |
| Q13 | Tengo un problema con mi pedido | Ambigua | D1 / D3 | Varias |
| Q14 | ¿Cuánto tiempo tengo? | Ambigua | D1 / D2 | Varias |
| Q15 | ¿Venden teléfonos celulares? | Sin respaldo | Ninguno | — |
| Q16 | ¿Ofrecen financiación a cuotas sin intereses? | Sin respaldo | Ninguno | — |
| Q17 | ¿Cuál es la dirección de la tienda física? | Sin respaldo | Ninguno (D3 indica que no hay tienda física) | B.1 |

Q17 es una prueba de borde: el corpus responde indirectamente que **no existe** tienda física.
