# Manual de usuario — Herramienta WAN v1.1

Herramienta para diseñar y gestionar una red WAN: calcula subredes, carga la topología, genera configuraciones para **Cisco, Huawei, Fortinet y MikroTik** y revisa la seguridad.

> Todo se hace con **datos de ejemplo**. Las configuraciones se aplican solo en el laboratorio autorizado, después de revisarlas.

---

## 1. Instalación y ejecución

No hay que instalar nada. La herramienta es **un solo archivo**: `herramienta-wan.html`.

1. En GitHub, abre `herramienta-wan.html` y pulsa **Download raw file** (ícono de descarga).
2. Busca el archivo descargado y dale **doble clic**. Se abre en el navegador.
3. Navegadores probados: **Google Chrome** y **Microsoft Edge** (computador o celular).
4. No necesita internet ni servidor. Solo la tipografía se descarga si hay conexión; sin ella se usa la letra del sistema.

La herramienta recuerda la topología en el navegador. Para llevarla a otro computador usa **Topología → Exportar JSON** e **Importar JSON**.

## 2. Pantalla de Inicio

- Muestra cuántos **dispositivos, enlaces WAN, VLAN** y **advertencias** hay.
- El botón **Cargar topología de ejemplo** carga 4 sedes ficticias (Bogotá, Medellín, Cali y Barranquilla), una por marca.
- La tabla **Qué capturar para la entrega** indica qué pantalla corresponde a cada captura.
- El botón **Cambiar tema** alterna modo claro y oscuro.

## 3. Pestaña 1 · Subnetting

### Calcular una dirección
1. Escribe la IP con su prefijo, por ejemplo `192.168.10.70/27` (también acepta IPv6, como `2001:db8::1/64`).
2. Pulsa **Calcular** o la tecla Enter.
3. Verás: dirección de red, broadcast, máscara, wildcard, primer y último host, hosts utilizables, clase y tipo (privada o pública). También la IP en binario y los pasos del cálculo.
4. Si la IP no es válida (por ejemplo `999.1.1.1/24`), aparece un mensaje en rojo y no se calcula nada.

### Dividir una red
1. Escribe la red base (por ejemplo `192.168.1.0/24`) y elige el nuevo prefijo (por ejemplo `/26`).
2. Pulsa **Dividir**: aparece la tabla de subredes con su rango y broadcast.

### Plan por piso o sede (VLSM)
1. Escribe la red base, por ejemplo `192.168.0.0/22`.
2. En **Áreas** escribe una por línea: `NOMBRE, HOSTS` (ejemplo: `Piso 1 Ventas, 100`).
3. Pulsa **Calcular plan**: cada área recibe su red, su VLAN (10, 20, 30…) y su gateway. Las áreas grandes se asignan primero.
4. Opcional: en **Usar este plan como VLAN de**, elige un equipo y pulsa **Aplicar al dispositivo**.

## 4. Pestaña 2 · Topología

### Cargar
- **Cargar ejemplo:** las 4 sedes de prueba.
- **Importar JSON:** elige un archivo como `ejemplos/topologia-ejemplo.json`. Si tiene errores, no se carga nada y se explica qué falló.
- **Exportar JSON:** descarga la topología actual.
- **Vaciar:** borra todo (con botón **Deshacer**).

### Agregar o editar un equipo
1. Llena **Hostname** (letras, números y guion; empieza con letra), **Rol**, **Marca** y **Sede**.
2. **Interfaz LAN** y **gateway** son opcionales.
3. **VLAN**, una por línea: `ID, NOMBRE, RED/PREFIJO` → `10, VENTAS, 192.168.10.0/26`.
4. **Enlaces WAN**, uno por línea: `INTERFAZ, IP/PREFIJO, HACIA` → `GigabitEthernet0/1, 10.0.0.1/30, R2`. Para Internet escribe `ISP` en "HACIA".
5. Pulsa **Agregar dispositivo** (o **Guardar cambios** si estás editando).
6. Las casillas rojas de **Opciones inseguras** solo sirven para demostrar las advertencias de seguridad.

Cada tarjeta de equipo tiene los botones **Editar**, **Ver configuración** y **Eliminar**. El dibujo de arriba se actualiza solo.

## 5. Pestaña 3 · Configuraciones

1. En **Equipo**, elige el router o firewall.
2. En **Marca**, deja "La marca del equipo" o elige otra para comparar (Cisco, Huawei, Fortinet o MikroTik).
3. Lee las advertencias, si las hay (recuadro amarillo).
4. Pulsa **Copiar** o **Descargar .txt**.
5. Antes de aplicar en el equipo del laboratorio, reemplaza `<CAMBIAR_CLAVE>` por la clave real **directamente en el equipo**.

Qué incluye cada configuración: nombre del equipo, VLAN, direcciones IP, rutas hacia las otras sedes, ruta por defecto, NAT hacia Internet (también para las sedes vecinas que salen por ese equipo) y acceso solo por SSH desde la LAN.

## 6. Pestaña 4 · Ciberdefensa

- **Análisis de seguridad:** lista los riesgos (alto o medio) de toda la topología y cómo corregirlos.
- **Probar la validación:** escribe un hostname para ver si se acepta o se rechaza.
- **Políticas:** las 7 reglas de uso seguro de la IA. Botón **Descargar politicas-ia.md**.
- **Registro de entradas rechazadas:** hora, lugar y motivo de cada dato rechazado.

## 7. Pestaña Pruebas

1. Pulsa **Ejecutar pruebas**.
2. Verás el porcentaje de confianza, el resumen por función y la tabla de las 37 pruebas (OK o FALLA).
3. Pulsa **Descargar docs/pruebas.md** para guardar el reporte.

## 8. Problemas frecuentes

| Problema | Solución |
|---|---|
| "IPv4 inválida" | Cada número va de 0 a 255 y debe llevar prefijo: `192.168.1.10/24`. |
| "no es dirección de red" | Usa la red que indica el mensaje (ej. `192.168.10.0/26` en vez de `.5/26`). |
| El archivo JSON no carga | Revisa comas y llaves; el mensaje dice qué equipo y qué campo fallan. |
| No aparece la configuración | Primero carga el ejemplo o agrega equipos en Topología. |
| Desapareció la topología | Se borró el historial del navegador: vuelve a importar tu JSON. |
