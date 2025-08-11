# Tarea 1:
## Enunciado:
La tarea consiste en crear un usuario llamado rose con una non-interactive Shell.

1.	Añadir un usuario con la opción non-interactive shell
```
sudo useradd -s rose /sbin/nologin
```
# Tarea 2:
## Enunciado:
Crear una cuenta de usuario llamada javed que este configurada para expirar el 2024-15-04.

1.	Acceder al servidor mediante ssh.

2.	Añadir un usuario llamado javed y configurar la fecha de expiración para la cuenta.
```
sudo useradd -e 2024-15 -04 javed
```

3.	Verificar la fecha de expiración con:
```
sudo chage -l javed
```

# Tarea 3:
## Enunciado:
Hay que deshabilitar el inicio de sesión SSH directo como root en todos los servidores de aplicaciones dentro del Centro de Datos Stratos. Para los tres servidores APP.

1.	Accedemos a cada servidor y dentro modificamos el archivo sshd_config.
```
sudo vi /etc/ssh/sshd_config
```

2.	cambiamos el valor de PermitRootLogin que aparece como “yes”.

NOTA: No vale simplemente con comentarlo para que no lo aplique, debemos modificar el valor “yes” por “no”.

3.	Reiniciamos el servidor.
```
sudo systemctl restart sshd
```

# Tarea 4:
## Enunciado:
Tu tarea es otorgar permisos de ejecución al script /tmp/xfusioncorp.sh en el Servidor de Aplicaciones 3. Además, asegúrate de que todos los usuarios tengan la capacidad de ejecutarlo.

1.	Acceder al servidor stapp03 mediante ssh.
```
ssh banner@stapp03
```
2.	Otorgar permisos al script de lectura y ejecución.
```
sudo chmod a+rx /tmp/xfusioncorp.sh
```
3. Acceder al servidor stapp03 mediante ssh.
```
ssh banner@stapp03
```
4.  Otorgar permisos al script de lectura y ejecución.
```
sudo chmod a+rx /tmp/xfusioncorp.sh
```

# Tarea 5:
## Enunciado:
Después de una auditoría de seguridad, el equipo de seguridad de xFusionCorp Industries ha decidido mejorar la seguridad de las aplicaciones y servidores utilizando SELinux. Para iniciar las pruebas, se han establecido los siguientes requisitos para el Servidor de Aplicaciones 3 en el Centro de Datos Stratos:

1.  Instalar los paquetes necesarios de SELinux.
```
sudo yum install -y selinux-policy selinux-policy-targeted
```

2.  Deshabilitar SELinux de forma permanente por el momento; será reactivado después de realizar los cambios de configuración necesarios.
```
sudo vi /etc/selinux/config
```

Dentro del archivo cambiar la linea "SELINUX=enforcing" por:
```
SELINUX=disabled
```
Para comprobar:
```
grep SELINUX= /etc/selinux/config
```
Debería mostrar:
```
SELINUX=disabled
```
3.  No es necesario reiniciar el servidor ahora, ya que hay un reinicio programado para esta noche.

4.  Ignorar el estado actual de SELinux desde la línea de comandos; el estado final después del reinicio debe ser "deshabilitado".

# Tarea 6:
## Enunciado:
El equipo de administradores del sistema de Nautilus ha preparado scripts para automatizar varias tareas diarias. Quieren que estos scripts se desplieguen en todos los servidores de aplicaciones del centro de datos Stratos en un horario programado.
Antes de eso, necesitan probar una funcionalidad similar con un trabajo de cron de prueba.

1.  Instalar el paquete cronie y arrancar el servicio crond en todos los servidores de aplicaciones de Nautilus:
```
sudo yum install -y cronie          # En sistemas RHEL/CentOS
sudo systemctl enable crond
sudo systemctl start crond
```
2.  Agregar un cron para el usuario root que se ejecute cada 5 minutos y escriba "hello" usando crontab:
```
sudo crontab -e
```
Agregar esta línea al final del archivo:
```
*/5 * * * * echo hello > /tmp/cron_text
```
Guardar y salir.

NOTA: Tienes que hacer estos pasos en todos los servidores donde quieres el crond. Para verificar:
```
sudo crontab -l
```
y para confirmar que el servicio está activo:
```
systemctl status crond
```
# Tarea 7:
## Enunciado:
El equipo de administradores del sistema de xFusionCorp Industries ha configurado algunos scripts en el jump host que se ejecutan a intervalos regulares y realizan operaciones en todos los servidores de aplicaciones del Datacenter Stratos.
Para que estos scripts funcionen correctamente, debemos asegurarnos de que el usuario thor en el jump host tenga acceso SSH sin contraseña a todos los servidores de aplicaciones a través de sus respectivos usuarios con privilegios sudo (es decir, tony para el servidor de aplicaciones 1, etc.).

1.  Desde el jump host, como el usuario thor, generar la clave SSH (si no existe)
```
sudo su - thor
ssh-keygen -t rsa -b 2048
```
Presiona Enter en todas las preguntas (no pongas passphrase). Esto creará los archivos ~/.ssh/id_rsa y ~/.ssh/id_rsa.pub.
2.  Copiar la clave pública a cada servidor y usuario sudo correspondiente
```
ssh-copy-id tony@stapp01
ssh-copy-id steve@stapp02
ssh-copy-id banner@stapp03
```
Cada vez que lo hagas, acepta el fingerprint y escribe la contraseña del usuario (una sola vez). Esto instala la clave pública en ~/.ssh/authorized_keys del usuario remoto.

3.  Probar que funciona sin contraseña, si entras directamente sin que te pida contraseña, está todo correcto.


