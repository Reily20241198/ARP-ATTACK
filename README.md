
📌 ARP-MITM-ATTACK

ENLACE DEL VIDEO DEMOSTRATIVO: https://www.youtube.com/watch?v=g4BYVeUXJQ4&t=5s

 ARP Spoofing MitM Attack Tool
 Descripción General

Herramienta de auditoría de seguridad desarrollada en Python utilizando Scapy que demuestra vulnerabilidades en el protocolo ARP (Address Resolution Protocol) mediante la técnica de ARP Spoofing.

El script realiza un ataque Man-in-the-Middle (MitM) interceptando la comunicación entre una víctima y el gateway, posicionando al atacante como intermediario invisible.

 ADVERTENCIA:
Esta herramienta es únicamente para fines educativos y pruebas de seguridad autorizadas en entornos controlados. El uso no autorizado en redes de producción es ilegal.

 Objetivo del Script

El script mitm_arp.py realiza un ataque ARP Spoofing con los siguientes objetivos:

Envenenar la tabla ARP de la víctima y del gateway

Redirigir el tráfico de red a través del atacante

Interceptar paquetes transmitidos

Demostrar vulnerabilidades del protocolo ARP

Concienciar sobre la importancia de implementar controles de seguridad en capa 2

 Comportamiento del Ataque

Envía respuestas ARP falsificadas continuamente

Asocia la IP del router con la MAC del atacante

Asocia la IP de la víctima con la MAC del atacante

Mantiene el envenenamiento activo mediante reenvíos periódicos

Permite captura de tráfico en tiempo real

 Capturas de Pantalla
Topología de Red
![Imagen1](https://github.com/user-attachments/assets/463f4dad-a50c-4876-a54b-f2856d75f69b)

Cript completo 
<img width="819" height="429" alt="Screenshot_6" src="https://github.com/user-attachments/assets/4573bac5-90b6-447d-bfed-a15dc20cb936" />
<img width="867" height="434" alt="Screenshot_7" src="https://github.com/user-attachments/assets/6dec3a69-fd40-4dd9-95b6-f809b2cea226" />
<img width="876" height="430" alt="Screenshot_8" src="https://github.com/user-attachments/assets/f9a50e61-80aa-4b86-b687-05cc9a85938e" />
<img width="773" height="424" alt="Screenshot_9" src="https://github.com/user-attachments/assets/cd5fce09-0681-4b0e-8eca-661012d1b9bf" />
<img width="669" height="413" alt="Screenshot_10" src="https://github.com/user-attachments/assets/2219320e-7e26-491a-a403-b3dcefef7544" />

 Ejecución del Script
<img width="553" height="132" alt="Screenshot_4" src="https://github.com/user-attachments/assets/535d5966-6498-4003-bd0c-0590d0feb08d" />

 Tráfico Interceptado
<img width="742" height="212" alt="Screenshot_5" src="https://github.com/user-attachments/assets/df200bab-1220-49ba-999c-0084a30e6559" />

 Detalles de Conectividad
Dispositivo	Interfaz	IP	Máscara	VLAN	Conectado a
Atacante (Kali)	eth0	11.98.1.3	/24	1	SW-1
Switch	e0/0	-	-	1	Atacante
Switch	e0/1	-	-	1	Router
Switch	e0/2	-	-	1	Víctima
Router	e0/0	11.98.1.1	/24	1	Switch
Víctima	eth0	11.98.1.2	/24	1	Switch
 Configuración de VLANs

VLAN 1 (Default)
Segmento de red: 11.98.1.0/24
Gateway: 11.98.1.1

 Parámetros y Configuración
Parámetros principales del script:
target_ip = "11.98.1.2"
gateway_ip = "11.98.1.1"
interface = "eth0"
interval = 2

Función de spoofing:

Envío de paquetes ARP reply falsificados

Asociación IP ↔ MAC falsa

Loop continuo para mantener ataque activo

 Requisitos del Sistema
Sistema Operativo

Linux (Kali Linux recomendado)

Python

Python 3.7 o superior

Librerías

scapy >= 2.4.5

 Instalación de dependencias
sudo apt update
sudo apt install python3 python3-pip -y
sudo pip3 install scapy

 Habilitar forward de paquetes
echo 1 | sudo tee /proc/sys/net/ipv4/ip_forward

 Uso de la Herramienta
cd /home/reily
sudo python3 mitm_arp.py

Salida esperada:
[+] Enviando paquetes ARP falsificados...
[+] Ataque MitM activo
[Ctrl + C para detener]

 Verificación del Ataque

En el router o switch:

show arp


Indicadores:

 Dirección MAC del atacante asociada a IP víctima/gateway
 Tráfico redirigido
 Comunicación interceptada

 Medidas de Mitigación
1. Dynamic ARP Inspection (DAI)
ip arp inspection vlan 1

2. Deshabilitar ARP innecesario

Usar seguridad por VLANs y puertos.

3. Port Security
interface ethernet 0/0
switchport port-security
switchport port-security maximum 2
switchport port-security violation restrict

4. Monitoreo ARP

IDS/IPS

Herramientas como arpwatch

5. Uso de cifrado

HTTPS

VPN

 Análisis Técnico

El ataque manipula el funcionamiento básico de ARP:

ARP Request → ¿Quién tiene X IP?
ARP Reply falso → Yo tengo esa IP

El atacante suplanta:

Gateway

Víctima

Logrando interceptar todo el tráfico.

 Resultados Observados
Antes del Ataque:

Tabla ARP normal con direcciones legítimas.

Durante el Ataque:

Entradas ARP alteradas

MAC del atacante presente en múltiples IPs

 Impacto y Riesgos

Intercepción de credenciales

Manipulación de tráfico

Posible DoS

Base para ataques avanzados

 Contramedidas Recomendadas

✔ DAI
✔ Segmentación por VLANs
✔ Seguridad en switches
✔ IDS
✔ Buenas prácticas de red

 Consideraciones Legales

 Permitido en laboratorios propios
 Permitido con autorización
 Prohibido en redes reales sin permiso

El autor no se responsabiliza por uso indebido.

👤 Autor

Reily
Laboratorio de Seguridad en Redes
Práctica de ARP Spoofing MitM

 Licencia

Proyecto educativo para investigación en seguridad informática.

 Changelog

v1.0 (Febrero 2026)

Implementación inicial del ARP Spoofing

Envenenamiento continuo

Intercepción de tráfico

 Entorno de Pruebas

Kali Linux

Cisco Router + Switch (Packet Tracer / GNS3)

Red aislada 11.98.1.0/24

 Referencias

Scapy Documentation

Cisco ARP Security

MITRE ATT&CK – ARP Poisoning


