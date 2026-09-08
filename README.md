<div align="center">

### 🇪🇸 Español · [🇬🇧 English](https://github.com/ervingpinell/ervingpinell/blob/main/README.en.md)

</div>

# Hola, soy Erving

Recepcionista por obligación, desarrollador por profesión, gamer por decisión.

Trabajo desde Costa Rica, sobre todo con **Laravel, JavaScript, PHP y PostgreSQL**.

Antes de programar fui recepcionista en turismo, atendiendo huéspedes en español
e inglés todos los días.

Mis proyectos:

## PURAPP

**[purappcr.com](https://purappcr.com)**

En producción: **[greenvacationscr.com](https://greenvacationscr.com)** ·
**[lutantravelcr.com](https://lutantravelcr.com)**

ERP y motor de reservas para operadores turísticos en Costa Rica. No es un sitio
de reservas con un panel detrás: cubre la operación completa de una empresa de
tours, desde que el cliente entra a la web hasta que Hacienda acepta la factura,
en una plataforma multiempresa donde cada cliente corre con su propio despliegue
y su propia base de datos.

Cada empresa sale con su sitio público en **cinco idiomas** (español, inglés,
francés, alemán y portugués) con `hreflang`, y su panel administrativo detrás.

**Estado:** más de un año de trabajo y sigue en desarrollo activo. Hay empresas
operando sobre la plataforma todos los días mientras se le agregan módulos. Las
conexiones con **Viator y GetYourGuide ya funcionan**: las agencias consultan
disponibilidad y crean reservas contra nuestra API, y esas reservas caen en el
mismo panel que las de la web.

<details>
<summary><b>Módulos</b></summary>

<br>

| Módulo | Qué resuelve |
|---|---|
| **Reservas** | Carrito y pago en línea, enlaces de cobro, cobros sin reserva, códigos promocionales, precio acordado a mano, edición de reserva con cobro del saldo. |
| **Canales de venta** | Viator y GetYourGuide conectadas como proveedor: disponibilidad, reserva, modificación y cancelación, con avisos salientes hacia la agencia. |
| **Precios** | Tarifas por temporada y por cantidad de personas, precio de venta contra precio neto, comisiones por socio con cambios de porcentaje según la fecha, e impuestos incluidos o sumados según el acuerdo. |
| **Facturación electrónica** | Emisión a Hacienda de Costa Rica (v4.4): factura, tiquete, nota de crédito, factura de compra y mensaje receptor. Firma XAdES-EPES con el certificado del cliente, validación contra los esquemas oficiales y control de clave y consecutivo. |
| **Operaciones** | Lista diaria de salidas, asignación de guía, chofer y vehículo, registro de entrada en el campo, citas, incidencias y bitácoras. |
| **Seguimiento** | GPS en vivo sobre Traccar, con hora estimada de llegada y emparejamiento del punto de recogida cuando la agencia lo manda como texto libre. |
| **Traslados** | Buscador punto a punto: ubica el origen en el mapa, lo resuelve contra zonas y áreas, y arma el precio por tramo con los recargos que correspondan. |
| **Punto de venta** | Mesas, comandas, modificadores, cocina, apertura y cierre de caja. Régimen simplificado o tradicional, con su propia configuración de impuestos. |
| **Contabilidad** | Una sola fuente de verdad para ingresos y gastos. Importación de facturas de proveedor desde el XML, cuentas por cobrar y por pagar, y archivo de pagos para el banco. |
| **Inventario y compras** | Catálogo, recetas e ingredientes, movimientos de existencias, órdenes de compra y desperdicio. |
| **Recursos humanos** | Planilla con cargas sociales de Costa Rica, vacantes, candidatos, entrevistas, ausencias y liquidaciones. Próximamente, integración con ZETKO. |
| **Mensajería** | Chat por reserva con el correo entrante y saliente hilado, plantillas en los cinco idiomas y traducción automática al crear. |
| **Reseñas** | Sincronización con Google y Viator, moderación y solicitudes de reseña. |
| **Sitio público** | Página de inicio por empresa, catálogo, posicionamiento en buscadores, mapa del sitio y la marca (nombre, logo, colores, redes) resuelta desde la base de datos y no escrita a mano en el código. |

</details>

<details>
<summary><b>Detalles técnicos</b></summary>

<br>

- **Multiempresa sin base compartida.** Cada cliente tiene su propia base de
  datos. Se puede compartir el servidor, pero nunca la base de datos.
- **La firma electrónica, escrita a mano.** XAdES-EPES en PHP, sin librería de
  por medio: si el XML sale mal firmado, Hacienda lo rechaza y no hay factura.
  Se valida contra los esquemas oficiales antes de enviarlo, con un detalle que
  costó encontrar: un XML sin firmar reporta un falso «falta el nodo», así que
  la validación inserta una firma de prueba para no engañarse a sí misma.
- **Una sola verdad contable.** El ingreso puede entrar por una reserva, por un
  cobro suelto o por el punto de venta, y los tres pueden referirse al mismo
  dinero. Todo pasa por un único servicio que descuenta lo ya contado en otro
  lado; si no, el mismo monto aparece tres veces en el reporte del mes.
- **Correo por la API de Microsoft Graph**, en cola con Horizon, y las
  respuestas del cliente vuelven al hilo de chat de su reserva.
- **Cerca de 2.400 pruebas automatizadas** sobre reservas, precios, impuestos,
  emisión fiscal y los contratos de las agencias.

</details>

`Laravel 12` · `PHP 8.3` · `PostgreSQL` · `Redis / Horizon` · `Vue`
· `Bootstrap` · `NativePHP` · `PayPal` · `Traccar` · `DigitalOcean` + `Forge`

---

## Passiflora Massages

**[passifloramassages.com](https://passifloramassages.com)**

Sitio para un servicio de masajes en La Fortuna. Bilingüe español/inglés y
pensado para el celular: el cliente reserva desde el teléfono mientras está de
viaje.

HTML, CSS y JavaScript planos, sin compilación, sin framework, unas 1.200 líneas
en total, servidos como archivos estáticos. El cambio de idioma es un atributo
por texto, y la reserva termina en WhatsApp con el mensaje ya redactado, que es
donde el negocio realmente contesta.

Carga rápido incluso con el wifi de un hotel, que era el punto.

`Sitio a la medida` · `Bilingüe` · `Reservas`

---

## BabyShower Play

**[babyshowerplay.com](https://babyshowerplay.com)**

Diez juegos para animar un baby shower, jugados por todos los invitados a la vez
desde su propio celular. Quien organiza abre una sala, comparte un código y el
resto entra desde el navegador: sin instalar nada y sin crear cuentas.

Salió de un problema real: mi novia se ofreció a coordinar los juegos de un baby
shower y no le dio tiempo de organizarlos.

<details>
<summary><b>Detalles técnicos</b></summary>

<br>

- **Sin dependencias en el navegador.** HTML, CSS y JavaScript servidos tal
  cual: sin compilación, sin framework, sin `node_modules`. La página abre antes
  de que un framework hubiera terminado de arrancar.
- **Estado compartido por WebSocket.** Quince teléfonos viendo el mismo marcador
  actualizarse en vivo, con el reloj sincronizado entre dispositivos: el reloj de
  cada teléfono está desfasado y eso rompía la cuenta regresiva.
- **Rompecabezas deterministas.** Cada sala tiene una semilla y de ahí salen la
  sopa de letras, el crucigrama y los cartones de bingo: todos juegan el mismo
  tablero sin que el servidor tenga que enviarlo.
- **Validación en el servidor.** El bingo se canta contra lo realmente sorteado
  y el cartón se reconstruye del lado del servidor, así que marcar de más no
  sirve.
- **Bilingüe de verdad.** Los menús siguen el idioma del teléfono y los juegos el
  de la sala; si no, media fiesta jugaría un rompecabezas distinto.
- **Nueve suites de pruebas**, incluidas de carga y de flujo completo contra un
  servidor real.

</details>

`Node.js` · `WebSocket` · `PWA` · `Capacitor`

---

## Contacto

- **GitHub**: [@ervingpinell](https://github.com/ervingpinell)
- **Correo**: erving@purappcr.com
