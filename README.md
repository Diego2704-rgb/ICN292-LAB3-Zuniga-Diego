# ICN292 - Laboratorio 3: Triage de devoluciones AndesHogar SpA (n8n)

- **Autor:** Diego Alonso Zuñiga Cortez
- **RUT (sin DV):** 21.824.858 → semilla S = 858, U = $38.000, D = 21 días
- **Fecha:** 21 de septiembre de 2026
- **Curso:** ICN-292 Sistemas de información para la gestión, USM
- **Repositorio:** https://github.com/Diego2704-rgb/ICN292-LAB3-Zuniga-Diego

## Archivos

| Archivo | Contenido |
|---|---|
| `ICN292-Lab3-Zuniga-Diego.pdf` | Informe (resumen ejecutivo, partes A, B y C, capturas) |
| `ICN292-Lab3-Zuniga-Diego.docx` | Mismo informe en Word |
| `ICN292-Lab3-Zuniga-Diego-triage.json` | Workflow de triage (Webhook → Switch Rules → Edit Fields → UF → registro → Gmail → respuesta) |
| `ICN292-Lab3-Zuniga-Diego-emisor.json` | Workflow que envía las 15 solicitudes por POST al webhook |
| `ICN292-Lab3-Zuniga-Diego-resumen.json` | Workflow programado (08:00 diario) que consolida el día con Summarize y envía un correo |
| `capturas/` | Capturas de las ejecuciones citadas en el informe |

## Cómo reproducir

1. En n8n, menú **Workflows → Import from File**, e importar los tres `.json`.
2. Crear una **Data Table** llamada `registro_devoluciones` con las columnas:
   `fecha, fecha_hora, id_solicitud, sku, estado_producto, email_cliente, ruta, motivo` (texto) y
   `unidades, monto, valor_uf, monto_uf, dias_desde_compra, U, D` (número).
   Luego seleccionarla en los nodos **Registrar en tabla** (triage) y **Leer registro del dia** (resumen), ya que el `.json` guarda el ID de la tabla de la instancia original.
3. Conectar una credencial de **Gmail OAuth2** en los nodos **Notificar cliente** y **Enviar resumen** (y cambiar el destinatario si corresponde).
4. **Publicar** el workflow de triage y reemplazar en el nodo **POST al webhook de triage** del emisor la URL de producción por la de la nueva instancia.
5. Ejecutar el emisor con **Execute workflow**. Para probar el resumen sin esperar al día siguiente, usar el trigger **Prueba manual (hoy)**.

Los `.json` no contienen `pinData` ni credenciales (solo el nombre e ID de la credencial de Gmail).
