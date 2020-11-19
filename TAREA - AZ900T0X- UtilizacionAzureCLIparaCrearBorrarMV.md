

JOSE VICENTE TEJERO CALDERERA - 19/11/2020

## Creacion de la maquina virtual en Azure Cli

### Conectarse desde Azure Cli A Azure

```
az login
```

![image-20201119091750242](image-20201119091750242.png)



![image-20201119092332350](image-20201119092332350.png)





### Creando un grupo de recursos

```
az group create -l EastUS -n myRGCLI 
```

![image-20201119091915133](image-20201119091915133.png)



### Creando una máquina virtual Linux

```
az vm create ^
 --name myVMCLI ^
 --resource-group myRGCLI ^
 --image UbuntuLTS ^
 --location EastUS ^
 --admin-username azureuser ^
 --admin-password Pa$$w0rd1234 ^
 --no-wait
```

![image-20201119092359234](image-20201119092359234.png)

![](image-20201119092448789.png)



Conectarse a la máquina Virtual de Linux

```
ssh azureuser@104.211.52.252
Nota: Dar que si en la creación del certificado SSH
```

ssh manager@52.146.38.240

Password12345678

![image-20201119120717481](image-20201119120717481.png)

1 - Actualizar en Linux

```
sudo apt-get update
```

![image-20201119120929244](image-20201119120929244.png)



2 - Hacer el upgrade

```
sudo apt upgrade
```

![image-20201119121357620](image-20201119121357620.png)

3 - Instalar un servidor web

```
sudo apt install -y apache2 apache2-utils
```

![image-20201119121740629](image-20201119121740629.png)



4 - Vemos el estatus de Apache

```
systemctl status apache2
```



![](image-20201119121618928.png)

5 - Ponemos un mensaje en nuestra página de Apache

```
cd /var/www/html
```

6 - Poner una nota en la página index.html

```
sudo vi index.html <ENTER>
<ESC> : 198 <ENTER> // irme a la linea 198 que es donde esta el mensaje de index.html
<i> PONER EL MENSAJE <ESC>
: x <ENTER>

```

![image-20201119122032048](image-20201119122032048.png)

![image-20201119131440547](image-20201119131440547.png)

![image-20201119125844610](image-20201119125844610.png)



7 - Salir del SSH

```
exit <ENTER>
```

![image-20201119122151017](image-20201119122151017.png)

**Nota:**

El puerto 80 deberá ser abierto desde NSG.

Destination PortRanges: 80

Name: Port_80

![image-20201119123143038](image-20201119123143038.png)

Probariamos que llegamos a la maquina virtual: con la IP desde cualquier navegador.

![image-20201119144954963](image-20201119144954963.png)

## Parar y "deallocate" la máquina virtual

```
az vm stop --resource-group myRGCLI --name myVMCLI --no-wait
```

```
az vm deallocate -g myRGCLI -n myVMCLI --no-wait
```

## Iniciar la máquina virtual

```
az vm start -g myRGCLI -n myVMCLI --no-wait
```

## Borrar la máquina virtual

```
az vm delete -g myRGCLI -n myVMCLI --yes --no-wait
```

### Mostrar informacion de la máquina virtual

```
az vm show -g myRGCLI -n myVMCLI -d
```

Borrar el grupo de recursos

```
az group delete -n myRGCLI  --yes --no-wait
```

## Desconectamos de Azure

```
az logout
```

Mas información:

[Manage Linux or Windows virtual machines.](https://docs.microsoft.com/en-us/cli/azure/vm?view=azure-cli-latest)

