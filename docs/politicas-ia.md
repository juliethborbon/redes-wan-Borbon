# docs/politicas-ia.md — Ciberdefensa y uso de IA en la herramienta

1. La herramienta nunca guarda contraseñas ni tokens en el código; van en .env (protegido por .gitignore).
2. Con IA pública solo se usan datos de ejemplo, nunca IPs reales, credenciales ni topologías sensibles.
3. Todo lo que ingresa el usuario se valida y sanea antes de usarse.
4. La herramienta advierte cuando una configuración es insegura (puertos abiertos, credenciales por defecto) y aplica el mínimo privilegio.
5. No se ejecuta ningún comando o configuración que no se entienda; lo generado por IA se revisa y se prueba primero.
6. Toda automatización/acceso a equipos se hace solo en el laboratorio autorizado.
7. La calidad se mide con pruebas y se reporta el % de confianza (docs/pruebas.md).

## Cómo las aplica la herramienta
- No existe ningún campo para escribir contraseñas: las configuraciones usan el marcador <CAMBIAR_CLAVE>.
- Si un archivo importado trae campos como "clave", "password" o "token", se eliminan y se avisa.
- Hostnames, VLAN, IPs y archivos se validan; lo que parece código (<script>, javascript:) se rechaza y queda en el registro.
- El análisis de seguridad advierte Telnet, HTTP, credenciales por defecto, administración desde la WAN y reglas any-any.
- Por defecto: solo SSH, administración limitada a la LAN, firewall con lo mínimo necesario.
- La pestaña Pruebas ejecuta las pruebas automáticas y calcula el % de confianza.
