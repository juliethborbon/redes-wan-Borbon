# Configuraciones generadas — las 4 marcas

Generadas con la pestaña **3 · Configuraciones** de `herramienta-wan.html` a partir de `ejemplos/topologia-ejemplo.json`.

| Archivo | Equipo | Marca | Corte |
|---|---|---|---|
| R1-cisco.txt | R1 (Bogotá) | Cisco IOS | 2 |
| R2-huawei.txt | R2 (Medellín) | Huawei VRP | 2 |
| R1-huawei.txt | R1 visto en Huawei | Huawei VRP | 2 |
| FW1-fortinet.txt | FW1 (Cali) | Fortinet FortiOS | 3 |
| R1-fortinet.txt | R1 visto en Fortinet | Fortinet FortiOS | 3 |
| MK1-mikrotik.txt | MK1 (Barranquilla) | MikroTik RouterOS | 3 |
| R1-mikrotik.txt | R1 visto en MikroTik | MikroTik RouterOS | 3 |

Todas usan `<CAMBIAR_CLAVE>` en lugar de contraseñas, solo SSH y administración limitada a la LAN.
Revisar antes de aplicar y solo en el laboratorio autorizado.

## Equivalencias entre las 4 marcas

| Qué hace | Cisco IOS | Huawei VRP | Fortinet FortiOS | MikroTik RouterOS |
|---|---|---|---|---|
| Nombre del equipo | `hostname R1` | `sysname R2` | `set hostname "FW1"` | `/system identity set name=MK1` |
| VLAN | `encapsulation dot1Q 10` | `dot1q termination vid 30` | `set vlanid 40` | `/interface vlan add vlan-id=50` |
| Dirección IP | `ip address IP MÁSCARA` | `ip address IP MÁSCARA` | `set ip IP MÁSCARA` | `/ip address add address=IP/PREFIJO` |
| Ruta por defecto | `ip route 0.0.0.0 0.0.0.0 GW` | `ip route-static 0.0.0.0 0.0.0.0 GW` | `config router static` | `/ip route add dst-address=0.0.0.0/0` |
| Salida a Internet (NAT) | `ip nat … overload` | `nat outbound 2000` | `set nat enable` (en la política) | `action=masquerade` |
| Filtrar tráfico | ACL | ACL | `config firewall policy` | `/ip firewall filter` |
| Solo SSH | `transport input ssh` | `protocol inbound ssh` | `set allowaccess ping ssh https` | `/ip service disable telnet…` |
| Guardar | `write memory` | `save` | (automático) | (automático) |
