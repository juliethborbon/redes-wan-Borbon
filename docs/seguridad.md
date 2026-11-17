# docs/seguridad.md — Medidas de seguridad aplicadas

Herramienta WAN v1.1. Resumen de las medidas de seguridad que aplica la herramienta y el repositorio.

## 1. Contraseñas y secretos
- La herramienta **no tiene ningún campo de contraseña** y no guarda claves.
- Las configuraciones generadas usan el marcador `<CAMBIAR_CLAVE>`: la clave real se escribe directamente en el equipo, nunca en el repositorio.
- Si un archivo de topología importado trae campos como `clave`, `password`, `token` o `secret`, la herramienta **los elimina y avisa**.
- El repositorio tiene `.gitignore` con `.env`. Solo se sube `.env.example`, sin datos reales.

## 2. Accesos a los equipos (lo que generan las configuraciones)
| Medida | Cisco | Huawei | Fortinet | MikroTik |
|---|---|---|---|---|
| Solo SSH (sin Telnet) | `transport input ssh` | `undo telnet server enable` | sin telnet en `allowaccess` | `/ip service disable telnet` |
| Sin administración web insegura | `no ip http server` | `undo http server enable` | solo HTTPS en la LAN | `www` desactivado |
| Administración solo desde la LAN | ACL `GESTION` en vty | ACL 2001 en vty | WAN solo responde ping | `set ssh address=` redes LAN |
| Usuario propio (no "admin") | `adminlab` | `adminlab` | `adminlab` | `adminlab` + `disable admin` |
| Cierre de sesión por inactividad | 10 min | 10 min | 10 min | — |
| Firewall con lo mínimo | — | — | servicios HTTP, HTTPS, DNS, PING | reglas input/forward con bloqueo final |

## 3. Validación de entradas
- IPs, prefijos, VLAN (2–4094), hostnames y redes se validan antes de usarse.
- Lo que parece código (`<script>`, `javascript:`, `onerror=`) se **rechaza** y queda en el **registro de entradas rechazadas**.
- Todo texto se muestra en pantalla como texto plano (no se interpreta como HTML).
- Los archivos importados se limitan a 200 KB y se cargan "todo o nada": si un equipo tiene errores, no se carga ninguno.

## 4. Advertencias de configuraciones inseguras
La pestaña **4 · Ciberdefensa** advierte (riesgo alto o medio): Telnet activo, credenciales por defecto, administración desde la WAN, reglas "permitir todo" (any-any), HTTP sin cifrar, redes solapadas, enlaces mal declarados y salida al ISP sin ruta por defecto.

## 5. La página misma
- Política de seguridad de contenido (CSP): la página **no puede conectarse a otros sitios** ni cargar código externo.
- Funciona sin servidor; la topología se guarda solo en el navegador de quien la usa.

## 6. Uso de IA y laboratorio
- Con IA pública solo se usaron datos de ejemplo (redes privadas y rangos de documentación).
- Las configuraciones se aplican solo en el laboratorio autorizado, después de revisarlas.
- Detalle de las reglas: [politicas-ia.md](politicas-ia.md). Comprobación: [pruebas.md](pruebas.md).
