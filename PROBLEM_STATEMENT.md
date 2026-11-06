# Planteamiento del problema: Interfood

## Contexto
En Interfood los pedidos se toman en papel y se pasan las cuentas a la caja para su facturación. Esto retrasa la atención, confunde los pedidos y deja el negocio sin datos claros de consumo.

---

## Descripción del problema

*   **Ineficiencia en la toma de pedidos:** El registro manual en papel, especialmente al personalizar platos por ingredientes, genera errores y retrasa la atención.
*   **Gestión fragmentada de cuentas:** Dividir el consumo por comensal en una misma mesa se vuelve complejo y dificulta el cobro final.
*   **Ausencia de inteligencia de negocio:** Al no registrar digitalmente el consumo, el restaurante desconoce qué platos se venden más, qué zonas se ocupan más o qué clientes regresan.
*   **Seguridad y control de roles:** Al no existir una diferencia de permisos entre meseros y administración, el proceso de facturación y cierre queda expuesto a errores o malos manejos.

---

### Dinámica y reglas de negocio

El funcionamiento del restaurante se rige bajo una estructura específica que define cómo se atiende, se cobra y se analiza el negocio:

* **Salón:** El salón se compone de 14 mesas fijas distribuidas en 3 zonas: Pasillo (5 mesas de 4 puestos), Balcón (3 mesas de 6 puestos) y Central (6 mesas de 4 puestos).
* **Pedidos:** Los pedidos se registran de forma individual por cada comensal y se cargan a la cuenta de la mesa. El cliente puede solicitar un plato completo o personalizarlo seleccionando ingredientes individuales, cobrando el valor específico de cada componente.
* **Menú:** Gestión de bebidas (tipo, marca, precio) y platos compuestos por ingredientes. Permite pedir el plato completo o por partes, cobrando dinámicamente el valor individual de cada componente asociado al plato.
* **Cuenta:** Cálculo de IVA y propina opcional (2% de la factura sin IVA). El mesero solo atiende y pide la cuenta; el único que puede cobrar la factura y cerrar la mesa es el Administrador.
* **Informes:** Al final del día, el administrador ve un resumen rápido con el Top 3 de platos, el Top 3 de clientes frecuentes (asociados de manera opcional por correo electrónico), la bebida más asociada al plato #1 y la zona del salón más visitada.

---

## Objetivo del Proyecto
Desarrollar una aplicación web que digitalice el ciclo de servicio en Interfood, permitiendo la gestión de mesas, el registro detallado de pedidos por comensal, el cálculo preciso de impuestos y la visualización de indicadores de rendimiento. El sistema asegurará que los meseros únicamente tomen pedidos, reservando al Administrador la facultad exclusiva de facturación y cierre de caja.
