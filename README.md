# Informe de Auditoría de Red Wi-Fi Insegura

## 1. Introducción

El objetivo de esta práctica es analizar los riesgos de seguridad que pueden existir al navegar por una red Wi-Fi pública utilizando una conexión HTTP.

Para realizar el análisis, se inspeccionó una solicitud web mediante las herramientas de desarrollador de Mozilla Firefox. Se observaron los datos de la solicitud, el protocolo utilizado y los encabezados enviados por el navegador.

Esta actividad permite comprender qué información puede quedar expuesta cuando la comunicación no cuenta con cifrado HTTPS.

## 2. Sitio analizado

- **Sitio web:** [NeverSSL](http://neverssl.com)
- **Herramienta utilizada:** Mozilla Firefox – Herramientas de desarrollador (F12).
- **Sección:** Network (Red).
- **Solicitud analizada:** GET /online/

Se utilizó NeverSSL debido a que permite realizar conexiones HTTP sin cifrado TLS, facilitando la observación de las solicitudes web.

## 3. Evidencia observada

En la pestaña Network de Firefox se seleccionó la solicitud correspondiente a /online/. En el panel Headers se observaron los siguientes datos:

- **URL solicitada:** http://youngbrightshiningyawn.neverssl.com/online/
- **Método HTTP:** GET
- **Host:** youngbrightshiningyawn.neverssl.com
- **Protocolo:** HTTP/1.1
- **Scheme:** http
- **Headers enviados**:
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:153.0) Gecko/20100101 Firefox/153.0 |
Referer: http://neverssl.com/
Connection: keep-alive
Accept-Language: en-US, en;q=0.9

### Análisis de la evidencia

Método GET: permite al navegador solicitar un recurso al servidor web.

Host: identifica el servidor al que se dirige la solicitud, mientras que User-Agent proporciona información sobre el navegador y el sistema operativo utilizado.

User-Agent: Expone información sobre que navegador utilizamos, sistema operativo, versión, etc.

Accept-Language: Permite saber nuestras preferencias de idioma para que la pagina nos muestre directamente el que preferimos.

Referer: indica la página desde la cual se originó la solicitud. En este caso, http://neverssl.com/.

La captura también muestra que el esquema utilizado es HTTP. Por lo tanto, la comunicación no está protegida mediante cifrado TLS.

### Captura de pantalla

La siguiente evidencia corresponde a la solicitud HTTP mediante las herramientas de desarrollador de Mozilla Firefox.

<img width="1919" height="883" alt="image" src="https://github.com/user-attachments/assets/d4661f68-379f-4ef0-97f9-5641ba96526b" />

## 4. Riesgos encontrados

Si la comunicación utiliza HTTP, una persona en la misma red podría capturar:

**Headers:** información del navegador, sistema operativo, host y referer, entre otros tipos de información.
**Paginas visitadas:** Direcciones URL y sitios que estamos utilizando.
**Datos personales:** Información escrita en formularios.
**Credenciales y contenido de las páginas:** En otros entregables observamos que podrían obtener nuestras credenciales y el contenido de páginas si navegamos a través de HTTP.

**Tres escenarios de ataque:**
**Sniffing:** Un atacante conectado a la misma red que nosotros podría utilizar herramientas como Wireshark para intentar observar las comunicaciones sin cifrado, es decir HTTP.
**Evil Twin:** Consiste en una red Wi-Fi falsa que imita el nombre de una red legitima, por ejemplo Starbucks_libre imitaría una red de un local de Starbucks. En este caso se podría capturar información personal, redirigir al usuario a páginas falsas o robar credenciales.
**Man in the Middle:** Es un escenario en el cual una atacante logra ubicarse entre el usuario y el servidor, obteniendo la posibilidad de interceptar la comunicación y cuando no exista cifrado, observar o modificar los datos transmitidos. Podría leer información privada, modificar páginas web, obtener credenciales y datos personales.

## 5. Como nos ayuda una VPN.

Una VPN (Red privada virtual) ayuda a proteger nuestra conexión cuando utilizamos una red Wi-Fi pública, cifra el tráfico y crea un túnel seguro entre nuestro dispositivo y el servidor VPN. En cambio HTTPS protege la comunicación entre el navegador y el sitio web, es decir que se complementan.

**Cifrado:** La VPN convierte todos los datos en información ilegible para alguien que intente interceptarlos.

**Túnel seguro:** Crea un túnel cifrado entre nuestro dispositivo y el servidor VPN, esto nos protege ya que la información viaja protegida incluso en una red Wi-Fi pública.

**Protección del tráfico:** Si alguien intenta capturar nuestra conexión mediante herramientas como Wireshark, podrá ver los paquetes de datos pero el contenido debería ser ilegible dentro del túnel seguro de la VPN.

**Privacidad:** Los sitios web que visitamos obtienen la dirección IP del servidor VPN en lugar de nuestra IP pública.

## 6. Mis tres reglas de Oro

**Verificar siempre que la conexión sea HTTPS y modo incógnito**: Antes de ingresar credenciales, observar que el certificado sea de un emisor confiable y que también corresponda al sitio web que estamos visitando. Por otro lado utilizar modo incognito para evitar que queden rastros de nuestra navegación.

**Utilizar una VPN confiable**: Cifrar el trafico utilizando una VPN para dificultar que terceros puedan interceptar y leer nuestra información, activar la opción KILL SWTICH en la VPN para evitar que en caso de caída de la VPN nos redirija sin utilizarla.

**Comportamiento** Evitar operaciones sensibles, ingresar datos personales y/o confidenciales.
