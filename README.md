# TPI-REPLICACION-ARTICULO
Evidencia visual y documental de la simulacion de la propuesta

# Réplica de Procesamiento Inteligente de Facturas (Coita et al., 2026)

Prototipo *low-code* y conjunto de datos sintéticos para replicar la arquitectura de automatización de cuentas por pagar (OCR + PLN + RPA) propuesta por Coita et al. (2026), adaptado al contexto de PyMes en Perú (emitidas a nombre de *Consultora Sistemas S.A.C.*).

## Arquitectura del Prototipo

* **Canal de Recepción (Trigger):** Bandeja de entrada en Gmail filtrando correos con archivos adjuntos en PDF.
* **Orquestación Low-Code:** Flujo automatizado en *Microsoft Power Automate*.
* **Almacenamiento Estructurado:** Registro automático en *Google Sheets* + validación contra `ground_truth.csv`.

## Contenido del Dataset (10 Facturas Sintéticas)

| Archivo | Formato / Diseño | Tipo Comprobante | RUC Proveedor | Total (PEN) | Caso Excepción |
|---|---|---|---|---|---|
| `100-Consultora-Sistemas-S-A-C.pdf` | Plantilla Invoice Home | Invoice (EN) | N/A | 295.00 | No |
| `2045-Consultora-Sistemas-S-A-C.pdf` | Plantilla Invoice Home | Invoice (EN) | N/A | 991.20 | No |
| `318-Consultora-Sistemas-S-A-C.pdf` | Plantilla Invoice Home | Invoice (EN) | N/A | 1,132.80 | No |
| `1290-Consultora-Sistemas-S-A-C.pdf` | Plantilla Invoice Home | Invoice (EN) | N/A | 8,602.20 | No |
| `87-Consultora-Sistemas-S-A-C.pdf` | Plantilla Invoice Home | Invoice (EN) | N/A | 3,687.50 | No |
| `F001-412-Consultora-Sistemas.pdf` | Corporativo Azul | Factura Electrónica | `20604589123` | 1,498.60 | No |
| `E001-89-Consultora-Sistemas.pdf` | Minimalista Verde | Comprobante - Factura | `20548796321` | 1,312.16 | No |
| `F002-1054-Consultora-Sistemas.pdf` | Clásico SUNAT Gris | Factura Electrónica | `20100047218` | 1,817.20 | No |
| `F004-339-Consultora-Sistemas.pdf` | Moderno Naranja | Factura de Venta | `20608877445` | 3,953.00 | No |
| `FE01-77-Consultora-Sistemas.pdf` | Ejecutivo Oscuro | Factura Electrónica | `20512398745` | 1,770.00 | **Sí** (`16-Nov-2026`) |

## Notas Metodológicas

* **Datos ficticios:** Razones sociales, números de RUC, series, correlativos y montos son sintéticos para fines académicos.
* **Consistencia tributaria:** Todos los comprobantes cumplen con $\text{Subtotal} + \text{IGV (18\%)} = \text{Total}$ en soles (`PEN`).
* **Simulación de excepción documental:** La factura `FE01-77` incorpora intencionalmente una variación textual en la fecha (`16-Nov-2026` frente al estándar `dd/mm/aaaa`) para reproducir la tasa de excepción documental (10 % en esta muestra frente al 12 % reportado en el estudio original).
* **Cómo ampliar el conjunto:** Modifica `generate_invoices.py` y ejecútalo localmente (`pip install reportlab`).
