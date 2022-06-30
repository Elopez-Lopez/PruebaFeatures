# Target Cloud
# Instalar Docker
Ejecutar Windows PowerShell ISE ( Como administrador) y ejecutar siguientes instrucciones

Opcionalmente se puede sustituir ```BCTC``` por cualquier otro nombre
```
$artifactUrl = Get-BcArtifactUrl -type onprem -country es -select Latest 

$credential = get-credential -UserName "admin" -Message "Introduzca sus credenciales:"

New-BCContainer -accept_eula `
                 -containerName "BCTC" `
                 -auth NavUserPassword `
                 -artifactUrl $artifactUrl `
                 -useGenericImage "$(Get-BestGenericImageName)-dev" `
                 -Credential $credential `
                 -includeTestLibrariesOnly `
                 -includeTestToolkit `
                 -isolation hyperv                  
```
En la ventana emergente con usuario **admin** introducir contraseña **admin**

Después de instalar contender se pueden consultar datos de BC en pestaña Logs

![pasted image 0.png](/.attachments/pasted%20image%200-f3913d68-8182-4e0a-988f-cd895af8eb83.png)

**Nota!**
Si da error ```DockerDo : a Windows version 10.0.20348-based image is incompatible with a 10.0.19044 host``` ejecutar siguientes comandos:

```
Remove-Module BcContainerHelper 
Uninstall-module bccontainerHelper -allversions 
Install-module bccontainerhelper
```

# Instalar .app
Localizar carpeta compartida con el contender

![pasted image 0 (1).png](/.attachments/pasted%20image%200%20(1)-4e765738-8001-417b-bb34-7308de3c8dd3.png)

Dejar en dicha carpeta la .app, descargada previamente del último PR en GitHub https://github.com/liderit-bc-tc/tc/actions

![pasted image 0 (2).png](/.attachments/pasted%20image%200%20(2)-c64116e5-ecd7-475e-b6c2-d71a7fcb829a.png)
Ejecutar Power Shell (con permisos de administrador) y acceder al contendedor con siguiente comando
```
Enter-BcContainer -containerName [Nombre del contender]
```
![pasted image 0 (3).png](/.attachments/pasted%20image%200%20(3)-49b36d28-ef82-42c3-a865-deb5a432b3a7.png)

![pasted image 0 (4).png](/.attachments/pasted%20image%200%20(4)-f6c25eb6-376a-4629-ba83-84abb2de3b8e.png)

Publicar .app mediante siguiente comando
```
Publish-NAVApp -ServerInstance [Instancia del contender] -Path ".\[Nombre de la APP].app" -SkipVerification
```
![pasted image 0 (7).png](/.attachments/pasted%20image%200%20(7)-d5b35d90-1eab-452e-acf5-84f789a4635a.png)

Por último, desde Business Central, instalar la extensión TC

![pasted image 0 (5).png](/.attachments/pasted%20image%200%20(5)-a5de8a51-4b78-45a9-afa4-c5305d77a656.png)

Habilitar desarrollo TC desde siguiente pantalla

![pasted image 0 (6).png](/.attachments/pasted%20image%200%20(6)-1338987d-5be7-4a25-a602-5209958b0560.png)

# Servicios API

Listar empresas

http://test:7048/BC/api/v2.0/companies

Listar metada

http://test:7048/BC/ODataV4/$metadata
