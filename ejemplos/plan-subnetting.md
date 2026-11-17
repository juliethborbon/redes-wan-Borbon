# Subnetting / IP planning — resultados de ejemplo

Generado con `herramienta-wan.html` (pestaña **1 · Subnetting**). Solo datos de ejemplo.

## 1. Cálculo de una dirección

| Entrada | Red | Broadcast | Máscara | Rango utilizable | Hosts |
|---|---|---|---|---|---|
| 192.168.10.70/27 | 192.168.10.64 | 192.168.10.95 | 255.255.255.224 | 192.168.10.65 – 192.168.10.94 | 30 |
| 192.168.1.10/24 | 192.168.1.0 | 192.168.1.255 | 255.255.255.0 | 192.168.1.1 – 192.168.1.254 | 254 |

Validación: `999.1.1.1/24` se rechaza (cada octeto va de 0 a 255).

**Cómo se calcula 192.168.10.70/27:** /27 = 27 bits de red y 5 de host → máscara 255.255.255.224 → bloques de 32 → 70 cae en el bloque 64–95 → red .64, broadcast .95, hosts = 2^5 − 2 = 30.

## 2. División de 192.168.1.0/24 en /26

| # | Red | Rango | Broadcast | Hosts |
|---|---|---|---|---|
| 1 | 192.168.1.0/26 | 192.168.1.1 – 192.168.1.62 | 192.168.1.63 | 62 |
| 2 | 192.168.1.64/26 | 192.168.1.65 – 192.168.1.126 | 192.168.1.127 | 62 |
| 3 | 192.168.1.128/26 | 192.168.1.129 – 192.168.1.190 | 192.168.1.191 | 62 |
| 4 | 192.168.1.192/26 | 192.168.1.193 – 192.168.1.254 | 192.168.1.255 | 62 |

## 3. Plan por piso (VLSM) sobre 192.168.0.0/22

| VLAN | Área | Hosts pedidos | Red | Máscara | Gateway | Broadcast |
|---|---|---|---|---|---|---|
| 10 | Piso 1 Ventas | 100 | 192.168.0.0/25 | 255.255.255.128 | 192.168.0.1 | 192.168.0.127 |
| 20 | Piso 2 Soporte | 50 | 192.168.0.128/26 | 255.255.255.192 | 192.168.0.129 | 192.168.0.191 |
| 30 | Piso 3 Gerencia | 20 | 192.168.0.192/27 | 255.255.255.224 | 192.168.0.193 | 192.168.0.223 |
| 40 | Sala de servidores | 10 | 192.168.0.224/28 | 255.255.255.240 | 192.168.0.225 | 192.168.0.239 |

Regla VLSM: se asignan primero las áreas más grandes para no desperdiciar direcciones.
