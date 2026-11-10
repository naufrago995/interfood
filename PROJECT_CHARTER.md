# Acta de consolidación de proyecto

## 1. Información general del proyecto

- **Nombre del proyecto:** Interfood
- **Fecha de formulación:** 13 de octubre de 2025
- **Estado del documento:** Consolidado
- **Autor:** Analista de sistemas de información
- **País de operación:** Colombia

---

## 2. Justificación y contexto

El restaurante Interfood gestiona sus pedidos y cuentas en papel, lo que retrasa la atención y dificulta llevar un seguimiento real del negocio. Al depender de anotaciones manuales, el servicio pierde agilidad al personalizar platos o dividir cuentas por comensal. Además, la ausencia de restricciones por roles expone los cierres de caja a inconsistencias. Como consecuencia, la administración se queda sin registros confiables para analizar la operación y las ventas.

---

## 3. Objetivos del proyecto

### 3.1 Objetivo general

Crear una aplicación web para gestionar los pedidos, el cierre de cuentas y los indicadores de rendimiento del restaurante.

### 3.2 Objetivos específicos

- Digitalizar la toma de pedidos **por comensal**, permitiendo personalizar platos por ingredientes con cobro dinámico de cada componente.
- Automatizar el **cálculo de la cuenta** (IVA del 19 % y propina opcional del 2 % sobre el valor neto).
- Garantizar la **separación de roles** para que únicamente el administrador cobre y libere las mesas.
- Generar los **indicadores de cierre de día**: Top 3 de platos, Top 3 de clientes frecuentes, bebida más asociada al plato #1 y zona más visitada.

---

## 4. Alcance del proyecto

### 4.1 Componentes incluidos (lo que SÍ hará el sistema)

- **Controlar el salón por zonas:** visualizar la distribución del salón mediante tarjetas que agrupan las 14 mesas fijas en 3 zonas (Pasillo: 5 mesas de 4 puestos; Balcón: 3 mesas de 6 puestos; Central: 6 mesas de 4 puestos), indicando dinámicamente su estado y capacidad.
- **Personalizar platos y bebidas:** gestionar bebidas (tipo, marca, precio) y modificar platos por ingredientes individuales, cobrando dinámicamente el valor de cada componente seleccionado.
- **Separar cuentas por persona:** registrar y organizar los pedidos dividiendo el consumo de forma individual por cada comensal dentro de una misma mesa.
- **Calcular la cuenta:** procesar de forma automática el total a pagar sumando el IVA (19%) y agregando un 2% de propina opcional calculada sobre el valor neto.
- **Mostrar tarjetas informativas de rendimiento:** visualizar el Top 3 de platos, el Top 3 de clientes, la bebida más asociada al plato #1 y la **zona más visitada**.

### 4.2 Componentes excluidos (lo que NO hará el sistema)

- **No maneja inventario:** no controlará existencias de materia prima, insumos ni compras a proveedores.
- **No procesa pagos electrónicos:** no tendrá integraciones con datáfonos ni pasarelas de pago; solo registrará el cierre administrativo de la cuenta.
- **No emite factura electrónica ante la DIAN:** el sistema calcula y desglosa el IVA, pero no realiza la emisión ni el envío de facturas electrónicas a la DIAN.
- **No gestiona domicilios:** no incluirá despachos ni integraciones con apps como Rappi o Uber Eats.
- **No maneja reservas:** no se implementará un módulo de reservas anticipadas.

---

## 5. Reglas de negocio y operativas

| Módulo | Regla de negocio |
| :--- | :--- |
| **Autenticación y control de acceso** | Registro e inicio de sesión mediante credenciales de acceso. El sistema valida el rol del usuario (Administrador o Mesero) para regular el acceso a las funciones de cobro, cierre de caja, liberación de mesas y visualización de indicadores de rendimiento." |
| **Gestión de mesas y distribución del salón** | 14 mesas fijas en 3 zonas: Pasillo (5 × 4 puestos), Balcón (3 × 6 puestos) y Central (6 × 4 puestos). Cada mesa registra cuatro estados en tiempo real: *Libre, Ocupada, Esperando pedido y Cuenta solicitada*. |
| **Catálogo** | Gestión de bebidas (tipo, marca, precio) y platos compuestos por ingredientes. Si se retira o modifica un componente, el sistema cobra o descuenta dinámicamente su valor. |
| **Toma de pedidos** | Los pedidos se registran de forma individual por comensal, pero suma todo en una sola cuenta general para la mesa. |
| **Facturación y cierre de cuenta** | Al solicitar la pre-cuenta, la mesa pasa a *Cuenta solicitada* y se bloquean nuevos pedidos. Se suma el IVA del 19% sobre el total consumido y se calcula el 2% de propina opcional. Los meseros solo piden la pre-cuenta; cobrar y liberar la mesa es tarea exclusiva del administrador. |
| **Reportes e indicadores** | Visualización de tarjetas informativas con el top 3 de platos, el top 3 de clientes frecuentes, la bebida más asociada al plato principal y la zona más visitada del restaurante. |

---

## 6. Stack tecnológico (propuesta)

| Capa | Tecnología | Justificación |
| :--- | :--- | :--- |
| **Frontend** | Vue 3 + Vite + Tailwind CSS | Interfaz reactiva y ligera. Permite actualizar el estado de las mesas en tiempo real y maquetar rápido. |
| **Backend (API REST)** | Node.js + Express (JavaScript) | Servidor web con arquitectura cliente-servidor. Gestiona las rutas de la API, controladores y reglas de negocio. |
| **Base de datos** | SQLite (`better-sqlite3`) | Base de datos relacional incrustada en un archivo local. Cero configuración externa y rendimiento óptimo para la escala del restaurante. |
| **Pruebas (Testing)** | Vitest + Supertest + Playwright + k6 | **Vitest** para pruebas unitarias de cálculo (IVA/propina). **Supertest** para automatizar pruebas de rutas en Express. **Playwright** para el flujo E2E en interfaz. **k6** para simular concurrencia de peticiones en la API. |
| **Despliegue (Local)** | Red Local (LAN) / Servidor local | La aplicación corre en un equipo local del restaurante que actúa como servidor, sirviendo la API al resto de dispositivos de la red. |

---

## 7. Restricciones técnicas y de calidad (Requisitos No Funcionales)

* **Usabilidad (RNF-01):** Interfaz con enfoque Mobile-First mediante Flexbox y Grid, priorizando agilidad y facilidad de uso en pantalla táctil (Tablets y celulares).
* **Seguridad por roles (RNF-02):** Control de acceso donde los meseros tienen restringida la acción de cobro y cierre definitivo de caja.
* **Rendimiento local (RNF-03):** Operación sobre red local (LAN) con Node.js y SQLite, ofreciendo tiempos de respuesta que no dependen de conexión a internet.
* **Mantenibilidad (RNF-04):** Arquitectura desacoplada en capas (Frontend, API REST y Base de Datos) para facilitar la lectura y evolución del código.

---

## 8. Matriz de roles y responsabilidades

| Rol | Responsabilidad operativa en el sistema |
| :--- | :--- |
| **Administrador** | Gestión del menú y la distribución del salón, consulta del tablero de indicadores, registro definitivo de cierres de cuenta y liberación de mesas. |
| **Mesero** | Visualización del estado del salón por zonas, apertura de mesas, registro de comandas individuales por comensal y solicitud de pre-cuentas. |
| **Sistema** | Procesamiento dinámico de costos por ingredientes, cálculo automático de impuestos y propinas, validación de permisos por rol y persistencia transaccional de los datos. |

---
