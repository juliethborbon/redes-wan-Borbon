# Topología de ejemplo

Archivo: `topologia-ejemplo.json`. Se carga en la herramienta con **2 · Topología → Importar JSON**. Datos ficticios.

| Equipo | Marca | Rol | Sede | VLAN | Enlaces WAN |
|---|---|---|---|---|---|
| R1 | Cisco (IOS) | Router | Bogota | 10 VENTAS 192.168.10.0/26<br>20 SOPORTE 192.168.10.64/27 | GigabitEthernet0/1 10.0.0.1/30 → R2<br>GigabitEthernet0/2 203.0.113.2/30 → ISP<br>GigabitEthernet0/3 10.0.0.10/30 → MK1 |
| R2 | Huawei (VRP) | Router | Medellin | 30 ADMIN 192.168.20.0/26 | GigabitEthernet0/0/1 10.0.0.2/30 → R1<br>GigabitEthernet0/0/2 10.0.0.5/30 → FW1 |
| FW1 | Fortinet (FortiOS) | Firewall | Cali | 40 CONTABILIDAD 192.168.30.0/27 | port2 10.0.0.6/30 → R2<br>port3 198.51.100.2/30 → ISP |
| MK1 | MikroTik (RouterOS) | Router | Barranquilla | 50 BODEGA 192.168.40.0/28 | ether2 10.0.0.9/30 → R1 |

Rangos usados: privados (10.x, 192.168.x) y de documentación (203.0.113.0/24, 198.51.100.0/24), que no existen en Internet.
