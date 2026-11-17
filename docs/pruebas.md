# docs/pruebas.md — Reporte de pruebas

Herramienta: Herramienta WAN v1.0 (pestaña Pruebas → botón "Ejecutar pruebas")
Fecha de ejecución: 15/11/2026, 4:35:24 p. m.

## Qué probé
- [P1] 192.168.10.70/27 → red 192.168.10.64  -> OK
- [P2] 192.168.10.70/27 → broadcast 192.168.10.95  -> OK
- [P3] 192.168.10.70/27 → 30 hosts utilizables  -> OK
- [P4] 192.168.1.10/24 → red 192.168.1.0 y máscara 255.255.255.0  -> OK
- [P5] /31 da 2 hosts y /32 da 1 host  -> OK
- [P6] Rechaza la IP inválida 999.1.1.1/24  -> OK
- [P7] Rechaza texto sin formato ("hola")  -> OK
- [P8] Público / privado: 10.x y 172.20.x privadas; 8.8.8.8 y 172.32.x públicas  -> OK
- [P9] IPv6 2001:db8:abcd:12::1/64 → red 2001:db8:abcd:12::  -> OK
- [P10] IPv6 /64 tiene 2^64 direcciones y fd00::/8 es privada (ULA)  -> OK
- [P11] Rechaza la IPv6 inválida 2001:::1  -> OK
- [P12] Dividir 192.168.1.0/24 en /26 → 4 subredes; la 3.ª es 192.168.1.128  -> OK
- [P13] Plan por piso (VLSM) 100, 50 y 20 hosts en 192.168.0.0/24 → /25, /26 y /27  -> OK
- [P14] Plan por piso: avisa cuando las áreas no caben  -> OK
- [P15] Carga la topología de ejemplo (4 equipos, sin errores)  -> OK
- [P16] Rechaza un hostname con código (<script>)  -> OK
- [P17] Elimina una contraseña real del archivo y avisa  -> OK
- [P18] Rechaza un JSON mal formado  -> OK
- [P19] Rechaza la VLAN 5000 y una red que no es dirección de red  -> OK
- [P20] Cisco (R1): hostname, VLAN 10 e IP con máscara  -> OK
- [P21] Cisco (R1): ruta estática hacia la LAN de R2 y ruta por defecto  -> OK
- [P22] Huawei (R2): sysname, dot1q VLAN 30 y ruta por defecto  -> OK
- [P23] Fortinet (FW1): hostname, VLAN 40 y política de firewall  -> OK
- [P24] MikroTik (MK1): identidad, VLAN 50 y ruta por defecto  -> OK
- [P25] Las 4 marcas generan configuración para el mismo equipo  -> OK
- [P26] Ninguna configuración contiene una clave real (usa <CAMBIAR_CLAVE>)  -> OK
- [P27] Por defecto: solo SSH (Cisco sin Telnet, Huawei y MikroTik lo desactivan)  -> OK
- [P28] Advierte si se activa Telnet  -> OK
- [P29] Advierte credenciales por defecto y política any-any  -> OK
- [P30] Detecta redes solapadas entre equipos  -> OK
- [P31] Neutraliza código al mostrar texto (escape de HTML)  -> OK
- [P32] La topología de ejemplo no tiene advertencias de seguridad  -> OK

## Resultado
Pruebas superadas: 32 de 32  =  100% de confianza

## Qué falta / errores encontrados
- Ninguno: todas las pruebas pasaron.
