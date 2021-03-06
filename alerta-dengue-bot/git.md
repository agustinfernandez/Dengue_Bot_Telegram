Bienvenidos al repositorio Alerta Dengue Bot!!!

Manual de uso https://git-scm.com/book/en/v2

-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --

Índice 

0. Instalar git
1. Crear ssh key
2. Configuracion
3. Uso básico de Bash
4. Bajar proyecto por primra vez
5. Introducción conceptual
6. Flujo conceptual de trabajo local
7. Status de los archivos
8. Crear nueva versión
9. Historia y diferencias
10. Bajar y Compartir los cambios con el resto. 
11. Conflictos
12. Buenas prácticas. 
13. Archivos ignorados
0. Biblio



Antes de empezara a hacer algo, leerlo completo una vez. 

0. INSTALAR GIT

  - WINDOWS
   
   a - Ir a http://git-scm.com/download/win , descargar. 

   b - Instalar los parametros por defecto.

   c - Abrir "Git Bash". (Si no sabés donde quedó, poné "bash" en el buscador de windows). 

  - Ubuntu

   a - Abrir una terminal

   b - ``sudo apt-get install git``   
   
1. Crear SSH KEY (TODOS)

   Para usar git tenes que darle una clave propia de tu computadora a gitlab. Esto hay que hacerlo en cada computadora que quieras usar git.  

   a - Tenemos abierto bash

   b - Verificamos si tenemos una clave escribiendo: ``cat ~/.ssh/id_rsa.pub`` y presionar ENTER. 

   c - Si en b no sale nada, creamos la clave escribiendo: ``ssh-keygen`` y presionar enter todas las veces hasta que termine

   d - Realizar el paso b y copiar el contenido completo. 

   e - Pegar el contenido en la página de gitlab. Una vez logeado en profile/key o https://gitlab.com/profile/key

2. CONFIGURACION 

  2.1 QUIEN SOS
    
```
    git config --global user.name "Tu Nombre y Apellido"
    git config --global user.email tucorreo@gamil.com
```

  2.2 Ver la configuración

```
    git config --list
```

3. BASH

Comandos básicos: 

**ls** 
 Lista los archivos y carpetas en la posición donde estás parado
(**ls -a** te muestra los archivos ocultos)

**cd nombreCarpeta**
  Entra a la carpeta nombreCarpeta. Para ir a la carpeta padre escribimos cd .. porque ".." es como se llama toda carpeta padre. cd ../.. sube dos carpetas. cd sin nada más te lleva al HOME de tu pc, donde están las carpetas Documentos Descargas y etc. Usa ls para mirar que hay cada vez que te vas moviendo
  
**mkdir nombreCareta**
  Crea una carpeta en el lugar donde estás parado con el nombre nombreCarpeta
  Te recomiendo crearte una carpeta con el nombre git donde vas a poner todos tus proyectos.  
   
**pwd**
  Te dice como se llama la dirección de tu computadora en la que estás parado

**mv nombreArchivoOriginal NuevoNombre**
  Este comando sirve para renombrar y para mover un archivo de carpeta. Usalo en la posición del archivo original. Para moverlo, se pone la direccion/nombreNombre. Ejemplo mv logo.jpg ../logo.jpg . Ahí estamos mandando el archivo a la carpeta de arriba y lo dejamos con el mismo nombre.

**rm nombreArchivo**
  Borra el archivo. CUIDADO que no pasa a la papelera con eso. 

**rm -r nombreCarpeta**
  Borra toda la carpeta. CUIDADO que no pasa por papelera. 

4. BAJAR EL PROYECTO por primera vez

  Primero, en bash, parate en la carpeta donde querés tener el proyecto. Una vez ahí, escribir lo siguiente: 

```
    git clone https://gitlab.com/argonautasdelcaos/argonautasdelcaos.git
```

   (Si no añadiste en gitlab en tu profile/key una ssh key para la computadora que estás usando, entonces no vas a poder bajarlo)

5. Conceptual de GIT. Las 3 AREAS.  

  **.git directory**
	Es nuestro repositorio local, donde están toda las versiones hitoricas que alguna vez se generaron (Mediante un "commit" que después veremos) y toda la información de nuestro proyecto. Si en la carpeta antropocaos corren el comando ls -a van a ver que hay una carpeta oculta que se llama .git . En los hechos ese el .git directory , donde está depositada toda la información del proyecto en nuestra computadora. Esa carpeta nosotros no la tocamos.  

  **Working directory**
  	Un de todas las versiones que están guardadas en el .git directory está disponble para que trabajemos con ella. Son todos los archivos y las carpetas que tenemos visible. A eso le llamamos Working directory. En general vamos a tener visible la última versión. El resto está comprimido en el directorio .git . Si quisiéramos trabajar con otra versión, una anterior, la podemos hacer que sea la versión visible (mediante un "checkout" que vamos a ver después)
  
  **Staging Area**
  	Es un archivo que contiene la información que preparamos (mediante un "add" que después veremos) pensando en enviar cuando generemos la próxima versión. Puede ser las modificaciones sobre archivos que ya estaban en el repositorio o la incorporación de archivos nuevos para el repositorio.    

6. FLUJO 

  6.1 Modificamos archivos en nuestro working directory
  6.2 Preparamos los archivos antes de enviarlos al .git driectory, añadiendo snapshot a la Staging Area
  6.3 Consignamos el conjunto cambios ("commit") de nuestra Staging Area a nuestro .git directory de forma definitiva generando una nueva versión. 

7. STATUS

  Los archivos que tenemos en la carpeta de nuestro repositorio "antropocaos" pueden tener 4 estados diferentes. Para saber en que estado están, parados dentro de antropocaos, 

  ESCRIBIR: 

```
    git status
```

  Los estados pueden ser: 

    **Untracked**
    Son archivos que están dentro de la carpeta del proyecto antropocaos pero que no forman parte de la versión con la cual estamos trabajando, de nuestro working directory. Git no los incluye hasta que nosotros se lo digamos explicitamente. 

    **Unmodified**
    Son archivos que están en el mismo estado al de la versión del repositorio con la cual estamos trabajando. No fueron modificados por nosotros con respecto a esa versión.

    **Modified**
    Archivos que abrimos y modificamos en algo, sea una coma o un espacio y coincide con la imagen de la versión que tenemos en el repositorio.

    **Staged** 
    Archivos que dejamos preparados con la idea de generar la próxima versión. Son las modificamos que queremos ennviar o los archivos que nunca fueron añadidos que ahora queremos enviar. 

8 CREAR NUEVA VERSION  

  8.1 Untracked/Modified -> Staged 

  Elegir una opción de las tres

```
    git add nombreArchivo
    git add nombreCarpeta (Agrega todos los archivos de la carpeta)
    git add -A .
```
    El primero agrega el archivo.
    El segundo agrega lo que haya en esa carpeta.
    El tercero agrega todo lo que haya de la carpeta actual para abajo.

  8.2 Staged -> Unmodified 

```
    git commit -m "Un comentario que aclare lo que estamos agragando en esta nueva versión que estamos creando. Si no ponen el -m los lleva a un editor de texto algo molesto para el que no lo sabe usar"
```

  8.3 Modified -> Staged -> Unmodified 

```
    git commit -a -m "el mensaje"
```

ME ARRPEINTO EN EL CAMINO. 

  8.4 Staged -> Untracked/Modified

```
    git reset HEAD nombreArchivo 
```

  8.5 Modified -> Unmodified 

```
    git checkout -- nombreArchivo
```

  8.6 Tracked -> Untracked

    Elegir una de las dos opciones
 
```
git rm --cached nombreArchivo 
git rm --cached -r nombreCarpeta
```

Sin ``--cached`` lo BORRA! de la pc. El ``-r`` es por recursivo, todos sus archivos

OTROS

  8.7 Mover o cambiar nombre (Tracked -> Staged)

```
    git mv nombreViejo nombreNuevo
``` 

9 Historia y Diferencias

  9.1 Ver las modificaciones con respecto versión del working area


   Las que están no están todavía en staged area:

```
    git diff
```
  9.2 La historia de versiones
  
   Opciones: 

```
    git log
    git log -p
    git log --stat
    git log --graph
```

10 Compartir los cambios con el resto. REPOSITORIO GLOBAL

  10.1 Traer los cambios que los demás compartieron

```
    git pull 
```

  10.2 Compartir cambios con los demás 

  Cuando ya commiteamos todos los cambios y estamos listos para compartilos con el resto, los enviamos al repositorio global

```
git push origin master 
```

11. CONFLICTO!


  11.1 Push

  **Si no te permite pushear, probá la siguiente**

```
    git pull --rebase
    git push origin master
```

  11.2 Pull

  Cuando dos personas modifican el mismo archivo en la misma línea, git no tiene forma de resolver el conflicto, el cual debe ser resuelto manualmente. 

  Cuando tenemos que resolver manualmente un archivo en conflicto, en ese archivo vamos a encontrar los puntos de conflicto con los siguientes marcadores

```
    <<<<<<<<<<
    UNA OPCIÓN
    ==========
    LA OTRA OPCION
    >>>>>>>>>>
```

 Lo que tenemos que hacer es dejar una de las opciones, borrar la otra y los marcadores (<<< === >>>), y cuando hagamos hecho esto para cada conflicto, hacemos ``git add ...``, ``git commit ... `` y finalemente volvemos a comprartir con el resto los cambios ``git push origine master``. 

12. BUENAS PRACTICAS. 

Verificar primero el estado de tu directorio de trabajo con ``git status``

Antes de empezar a trabajar en el proyecto, hacer un ``git pull`` del repositorio global para tener la última versión. 

**Recomendación:** Antes de hacer ``` push ``` se recomienda hacer ```git pull --rebase```, para traer eventuales modificaciones que hayan ocurrido en el ```origin``` no vistas previamente.
De esta forma, los conflictos se recuelven localmente.
Hacerlo de la siguiente forma:

```
    git add ... 
    git commit -m "..."
    git pull --rebase
    git push origin master
```

13. Todavía te pide password?

En .git/config, en la sección [remote "origin"] fijate que estés usando la conexión SSH:

```
	ssh://git@github.com/username/repo.git
```

y NO las conexiones https o git:

```
	https://github.com/username/repo.git
	git://github.com/username/repo.git
```

La URL SSH la encontrás en la página principal de tu repositorio, en Clone/Download.
Con esto la SSH key del punto 1 va a ser suficiente.

Si Git se queja que 'origin' ya había sido agregado, abrí el archivo .config y editá la url = "..." después de la sección [remote origin] comossh url = ssh://github/username/repo.git

14 ARCHIVOS IGNORADOS

**Atención**: El archivo ```.gitignore``` ignora *TODOS* los archivos *SALVO* algunas extensiones específicas a archivos fuentes. 

QUEREMOS: Solo archivo de código fuente. Si actualemnte está siendo ignorado un archivo fuente, agregarlo en el ```.gitignore```.

NO QUEREMOS: pdf, imágenes, datos, archivos "office" (.doc .docx .odt), muchos etceteras.

15 BIBLIOGRAFIA
 
  15.1 Carpeta ``biblio/``

Estructura:

- ``bayes.bib``
- ``download.sh``
- ``pdf/``

El archivo ``download.sh`` descarga toda la bibliografía guardada en ``bayes.bib`` y en el carpeta `` pdf/``

 15.1 Archivo ``.bib``

   **Reglas de estilo**: las claves de las citas del archivo ``.bib`` se espera que sigan el siguiente esquema: 

`
    apellido1999-resumenDelTitulo
`


  

 
 
