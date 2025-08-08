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



