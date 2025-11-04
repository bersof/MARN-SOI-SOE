# Insumos Técnicos Necesarios

## A. Insumos para configuración de entorno de desarrollo

1. **Versión de ArcGIS Server objetivo** (por ejemplo: `10.8.1` o `11.x`).  
   - Proporcionar el SDK correcto (.NET).
2. **Versión de ArcGIS Enterprise SDK** (debe coincidir con la versión del servidor).
3. **Versión de C# .NET:**  
   - Indicar la versión a utilizar.
4. **Instancia de ArcGIS Server** de desarrollo o sandbox.
5. **Certificados o credenciales** necesarios para utilizar ArcGIS Enterprise.
6. **Metadatos y catálogo de publicación:**  
   - Proporcionar datos de los catálogos y el formato en que serán publicados (CSV, JSON, JSON a través de APIs).  
   - Describir las capas, atributos y relaciones necesarias para la integración.

---

## B. Insumos de Datos Geoespaciales

Proporcionar datos de ejemplo o réplicas de las capas reales con su estructura.

**Ejemplos de datos requeridos:**

- Capas vectoriales y ráster en formato *feature class* o *shapefile*:
  - Cobertura de ecosistemas
  - Zonas protegidas
  - Pendientes o curvas de nivel
  - Parcelas o polígonos de prueba
- Metadatos de cada capa (unidad, sistema de referencia, fuente).
- Tabla con ponderaciones, parámetros y umbrales (para los cálculos de sensibilidad y biodiversidad).
- Polígonos de prueba (AOI o zonas de interés).

---

## C. Insumos Funcionales

Proporcionar diagramas de flujo que muestren cómo se desea procesar o automatizar las tareas, indicando los actores involucrados (usuario, sistema, administradores, etc.). Incluir:

1. **Descripción funcional clara de los análisis geoespaciales:**
   - Qué variables se combinan.
   - Qué tipo de operación espacial se realiza (intersect, union, buffer, etc.).
   - Cómo se calcula el resultado final (por ejemplo, promedio ponderado, índice normalizado).
2. **Esquemas o fórmulas de cálculo** (aunque sean aproximadas).
3. **Ejemplo de salida esperada** (formato JSON o tabla resumen).

---

## D. Insumos de Interfaz (para el SOI)

Como el SOI intercepta peticiones del cliente (por ejemplo desde un visor o aplicación web), se necesita:

1. Ejemplo de petición del cliente (URL, parámetros, headers, etc.).
2. Formato de respuesta esperado (por ejemplo, JSON con indicadores por zona).
3. Especificación de cómo el usuario define su zona de interés (indicar componente que ya lo realiza y accesos a ellos):
   - Polígono dibujado en el mapa.
   - Selección de una parcela existente.
   - Envío de coordenadas.

---

## E. Artefactos o Diagramas Necesarios

Para documentar y asegurar la correcta integración de los módulos, se requiere al menos:

- **Diagrama de flujo de procesos (SOE):** indicar paso a paso y qué rol ejecuta cada paso.  
- **Diagrama de flujo (SOI):** indicar paso a paso y qué rol ejecuta cada paso.

> *(Opcional, pero recomendado: diagrama de arquitectura general, diagrama de secuencia y modelo de datos simplificado.)*

---

## F. Casos de uso

Describir los procesos requeridos paso a paso utilizando casos de uso. Esto permite una mejor comprensión de lo que se debe desarrollar.

> **Nota:** Asignar identificadores incrementales (por ejemplo: `CU-001`, `CU-002`, ...).

Describir los procesos de la forma más natural posible: cómo se realizan actualmente (manual) o cómo se desea que se realicen.

---

### Ejemplo de Caso de Uso

**Caso de uso:** Consultar información geoespacial de una zona de interés  
**Identificador:** `CU-001`  
**Actor principal:** Usuario analista técnico

**Descripción:**  
El usuario dibuja un polígono en el mapa para definir una zona de interés. El sistema (a través del API SOI) intercepta la petición, identifica el polígono y devuelve información dinámica (por ejemplo: uso del suelo, parcelas, cobertura forestal) correspondiente a esa zona.

**Flujo principal:**

1. El usuario inicia sesión en la plataforma web.  
2. El usuario selecciona la herramienta “Definir zona de interés”.  
3. El usuario dibuja un polígono sobre el mapa.  
4. La plataforma envía la solicitud al **API SOI**.  
5. El **SOI** intercepta la petición, valida la zona y llama al **SOE** para realizar el análisis geoespacial.  
6. El **SOE** ejecuta el análisis sobre las capas configuradas (por ejemplo, calcula el área de cobertura boscosa o el número de parcelas dentro del polígono).  
7. El resultado se devuelve al usuario en formato JSON o se visualiza sobre el mapa.

**Flujo alterno:**

- Si el usuario no dibuja correctamente el polígono, el sistema muestra un mensaje indicando que la zona no es válida.  
- Si el servidor no encuentra capas disponibles, devuelve un error de servicio.