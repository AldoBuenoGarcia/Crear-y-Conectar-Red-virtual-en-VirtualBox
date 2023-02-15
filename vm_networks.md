## Crear una red virtual en Virtual Box

En este ejercicio uniremos tres máquinas virtuales con distinto Sistema Operativo.

Un Windows 10 pro, Windows Server y CentOS 7.

## Esquema

![](Media\00.png)



### 1. Crear red NAT en Virtual Box



Seleccionamos el **desplegable** de **herramientas** y le damos a **Red**.

![](.\Media\01.png)

Seleccionaremos la pestaña **NAT Networks** seleccionamos **Crear** para crear nuestra red.

![](.\Media\02.png)



Normalmente se crea con una ip válida que puedes modificar a tu gusto, la dejaremos por defecto y dejaremos **Enable DHCP** activado.



### Conectar Red a una Virtual Machine

Ahora seleccionamos una de nuestras máquinas y selecionamos **Configuración**, despues vamos a **Red**, en **conectado a** selecionamos **Red NAT** y finalmente seleccionamos la **red creada anteriormente**.

![](.\Media\03.png)





### Comprobar las conexiones de cada máquina



Activaremos la capacidad de hacer y recibir ping en caso de ser necesario como explicaremos a continuación y en caso de CentOS algo más.



Tanto en Windows 10 pro como en Windows Server 2019 activaremos lo mismo y se accede de la misma forma.



1. Averiguamos nuestra **ip privada** en la consola **cmd** de Windows y ejecutamos el programa **ipconfig**.

   **Windows 10**

![](.\Media\04.png)

 **Windows server2019**

![](.\Media\05.png)



3. Para que el ping fuese efectivo hay que activar el servicio de recibir ping en **ambos** **windows**.

   Iremos a **System and Security** > **Windows Defender Firewall** > **Advanced Seetings**

![](.\Media\06.png)

Activaremos en **Inbound Rules** y en **Outbound Rules** la regla de **File and Printer Sharing (Echo Request icmpv4)**

![](.\Media\07.png)



4. Ahora configuraremos **CentOS 7**

En caso de que al usar el comando

```
hostname -I
```

Puede que no obtengamos una IP, tendremos que conectar la red manualmente



![](.\Media\10.png)



Empezamos usando el comando **nmcli device status**.

![](.\Media\11.png)



Este nos indicara todas las redes, y veremos que la red **ethernet** que hemos activado desde VirtualBox anteriormente esta **desconectada**.

Para **conectar** a dicha red usaremos el comando **nmcli device connect enp0s3**

![](.\Media\12.png)



ahora volvemos a comprobar si nos devuelve la ip el comando **hostname -I**



![](.\Media\13.png)



Finalmente ya están todas las máquinas listas para comunicarse entre ellas.



## Comprobar conexiones entra las máquinas.

Hacemos ping entre las máquinas con el comando **ping** y la **direccion ip privada** de la otra máquina para comprobar si tienen conexión.

**Windows10 a WindowsSever2019**

![](.\Media\08.png)



**Windows10 a CentOS**

![](.\Media\14.png)



**WindowsSever2019 a Windows 10**

![](.\Media\09.png)



**WindowsSever2019 a CentOs**

![](.\Media\15.png)



**CentOS a Windows server**

![](.\Media\16.png)



**CentOS a Windows 10**

![](.\Media\17.png)