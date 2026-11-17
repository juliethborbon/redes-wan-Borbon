# Configuraciones generadas (Corte 2)

Generadas con la pestaña **3 · Configuraciones** a partir de `ejemplos/topologia-ejemplo.json`.

| Archivo | Equipo | Marca |
|---|---|---|
| R1-cisco.txt | R1 (Bogotá) | Cisco IOS |
| R2-huawei.txt | R2 (Medellín) | Huawei VRP |
| R1-huawei.txt | R1 visto en Huawei, para comparar con Cisco | Huawei VRP |

Todas usan `<CAMBIAR_CLAVE>` en lugar de contraseñas, solo SSH y administración limitada a la LAN.
Revisar antes de aplicar y solo en el laboratorio autorizado.

## Equivalencias Cisco ↔ Huawei

| Qué hace | Cisco IOS | Huawei VRP |
|---|---|---|
| Entrar a configurar | `configure terminal` | `system-view` |
| Nombre del equipo | `hostname R1` | `sysname R2` |
| Subinterfaz por VLAN | `encapsulation dot1Q 10` | `dot1q termination vid 30` |
| Ruta estática | `ip route RED MÁSCARA SIGUIENTE` | `ip route-static RED MÁSCARA SIGUIENTE` |
| Solo SSH | `transport input ssh` | `protocol inbound ssh` |
| Apagar Telnet | (no se habilita en vty) | `undo telnet server enable` |
| Guardar | `write memory` | `save` |
