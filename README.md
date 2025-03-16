# How-to-install-BlackArch-in-USB-with-persistance

## Requisitos

Para instalar BlackArch en USB con persistencia necesitamos tener lo siguiente:

>[!Note] Requesitos 
>- Necesitamos **2 USB**, uno para instalar la ISO, y otro para instalar Blackarch dentro de el con persistencia, es decir, con el que iniciaremos Blackarch cada vez que lo enchufemos en el portail/ordenador correspondiente. 
>	 - USB mínimo 8GB para instalar la [ISO slim](https://ftp.halifax.rwth-aachen.de/blackarch/iso/blackarch-linux-slim-2023.05.01-x86_64.iso)
>     - USB **+100 GB**, **Imprescindible**, en otro caso la instalación peta. Recomendable que el USB sea 3.0 para que blackarch funcione de manera óptima
>	![[images/IMG_0441.png|286]]



## Instalación
Primero instalamos el **iso** en el siguiente enlace:

> [Install BlackArch iso](https://www.blackarch.org/downloads.html)

![[Pasted image 20250313090731-1.png|790]]

Para la instalación en el USB tenemos que instalar un software como _BalenaEtcher_ o _Rufus_, preferiblemente rufus que es el voy a estar usando durante la instalación:

> [Install Rufus](https://rufus.ie/es/)

Cuando tengamos rufus en nuestro equipo y la iso instalada, abrimos rufus, seleccionamos el USB correspondiente, seleccionamos la iso de blackarch recientemente instalada y le damos a _Start_.
> [!info] Nota 
> - Aunque en la instalación aparezca un USB de 64GB, usé uno de 128GB posteriormente al tener problemas con la instalación

![[Pasted image 20250313093740-1.png|419]]
Aquí, importante seleccionar el modo de escritura **DD Image mode** ya que sino adelante que con el modo ISO no podremos completar la instalación

![[Pasted image 20250313093814-1.png|445]]
De nuevo, asegurarse de habéis seleccionado bien el USB ya que como dice el Warning todos los ficheros del USB seleccionado serán borrados 
![[Pasted image 20250313093837-1.png|505]]
Cuando este listo, cerramos y hacemos lo siguiente
![[../ANEXOS/Pasted image 20250313094910-1.png|447]]

Con el USB aún enchufado ponemos **reiniciamos** el ordenador y cuando se este encendiendo de nuevo, dependiendo del tipo o modelo de bios del ordenador/portatil hay que pulsar  las teclas **F2** ,**F11**, **F10**, **DEL**, **ESC** que suelen ser las más comunes para entrar en la BIOS, de todas formas dejo un mini cheet sheet:
> - Acer: F2
> - ASUS: F2
> - Dell: F2
> - HP F10
> - Lenovo: F2 or Fn+F2
> - MSI: Del
> - Samsung: F2
> - Toshiba F2


Después nos tenemos que ir a **Boot Manager** y seleccionamos el USB
![[IMG_0445(1).png|577]]

![[../ANEXOS/IMG_0395.png|467]]


Una vez seleccioando, aquí seleccionamos la segunda opción y se iniciará el instalador
![[../ANEXOS/IMG_0396.png|790]]

Una vez Dentro **SIN DESENCHUFAR EL USB**, conectamos el otro USB en el donde se instalará BlackArch e iniciamos sesión.
>[!Note] Credenciales 
>Login : liveuser  
 Password : blackarch

![[../ANEXOS/IMG_0397.png|759]]

Después de logearse tenemos que tener en cueta que:
- importante **NO iniciar la instalación desde el instalador del escritorio** ya que es posible que tengamos problemas tendremos problemas.
![[Pasted image 20250316092517-1.png|705]]
- **No conectarte a una red WI-FI con Internet** ya que surgirán errores con **pacman** durante la instalación y la instalación fallará. **Los errores con pacman se solucionan más adelante**.
- **Tener enchufado el ordenador durante la instalación** ya que el proceso puedo durar **MÁS DE 2 HORAS!!!!**.

Para la instalación vamos a la terminal y ejecutamos calamares installer con `sudo`.
![[Pasted image 20250316092432-1.png|504]]

Después se abrirá el installer, Nos saltará un Warning de que no estamos conectados a Internet pero **no hay problema**, seleccionamos el idioma y continuamos.
![[Pasted image 20250316091721-1.png|730]]

Seguidamente, seleccionamos nuestra localización sea cual sea.

![[../ANEXOS/IMG_0399-1.png|626]]
Terminando, seleccionamos nuestra configuración de teclado preferida:
![[IMG_0400.png|690]]


> [!Warning] Aviso 
> No seleccionar esta opción. Esta opción hará el proceso de instalación de manera automática pero al parecer esta "deprecated" y la instalación se quedará estancada en el 4%
![[Pasted image 20250316092257-1.png|850]]

Tras completar la configuración, llega el momento de la instalación. Aquí seleccionamos el USB donde se va a instalar BlackArch, **hay que asegurarse de que el disco seleccionado es el USB** ya que el disco de nuestro portail/ordenador esta seleccionado, **se eliminaran todos sus datos**.

Después, seleccionamos "Manual partitioning".

![[Pasted image 20250316092632-1.png|782]]
Creamos una nueva partición.

![[Pasted image 20250316092655-1.png|850]]

Seleccionamos "GUID Partition Table (GPT)".
![[Pasted image 20250316092708-1.png|470]]
Después seleccionamos "Free Space" y le damos a create.

![[Pasted image 20250316092734-1.png|661]]

La primera partición es para el "boot", por lo que tiene que tener:
- Size -> 500MB 
- File System -> fat32 
- Mount Point -> /boot/efi 
- Flags -> boot
![[Pasted image 20250316092756-1.png|690]]
Después, seleccionamos el espacio restante y le damos a create.
![[Pasted image 20250316092910-1.png|645]]
En este espacio restante se instalará BlackArch por lo que debemos seleccionar: 
- Size -> The rest 
- File System -> ext4 
- Mount Point -> /
- Flags -> root

![[Pasted image 20250316092820-1.png|723]]


Cuando las particiones estén creadas, le damos a siguiente y en esta pantalla se nos mostrará el resumen de las particiones.

![[Pasted image 20250316092952-1.png|775]]

Aquí hay que asegurarse de nuevo que todo está como lo configuramos y le damos a instalar. 

Ahora simplemente debemos esperar. La instalación normalmente toma 2 horas. Hay momentos en los que se quede atascada durante un tiempo, especialmente en el 71% donde se instala el bootloader.
![[IMG_0427.png|762]]
Una vez Instalado, seleccionamos la casilla "Restart now" y le damos a Done, cuando se este reiniciando, hacemos el mismo proceso que antes y pulsamos la tecla correspondiente para entrar en la BIOS.

![[IMG_0428.png|528]]

![[IMG_0446(1).png|538]]

Cuando cargue, seleccionamos BlackArch en el GRUB e iniciamos sesión con las credenciales que configuramos anteriormente.

![[IMG_0447.png|602]]

Ahora si intentamos usar pacman para actualizar los repositorios o instalar software nos saldrá el siguiente error:
![[IMG_0431.png|691]]

Esto es por que el 1 de Marzo de 2025 hubo una migración en git de los repositorios de Arch y tenemos que cambiar lo siguiente para que funcione. Más info en ->  https://archlinux.org/news/cleaning-up-old-repositories/.

En _/etc/pacman.conf_ debemos comentar "**[community]**" y la línea posterior, es decir, "**Include = /etc/pacman.d/mirrorlist**".



![[IMG_0432.png|699]]

![[IMG_0433.png|570]]

![[IMG_0436.png|660]]


Si aún tenéis problemas, deberéis editar el _/etc/pacman.d/mirrorlist_ de la siguiente forma: 

![[IMG_0440.png|686]]


Después de comentar esas líneas, veremos que podremos actualizar los paquetes

![[IMG_0437.png|775]]

Ya tenemos instalado BlackArch en USB con persistencia. Enjoy.
![[IMG_0439.png|735]]





## ¿Por que no hacemos la instalación conectados a Internet?
Si estamos conectados a Internet, durante la instalación de hará automáticamente una actualización de paquetes usando `pacman`, el problema es que en este caso pacman esta "deprecated" debido a la migración  en git de los repositorios antiguos de Arch. Por ello, es mejor hacer la instalación sin conexión a Internet, y luego, arreglar el problema de `pacman`. 
> Ver https://archlinux.org/news/cleaning-up-old-repositories/ para más información.





## ¿Por que no hacemos la instalación con la opción "Erase disk"?
Si lo hacemos con esta opción, la instalación se quedará estancada en el 4% cuando este creando la partición para root, por ello siempre es mejor hacerlo de forma manual.
![[Pasted image 20250316092257-1.png|850]]

![[Pasted image 20250316150401-1.png]]
