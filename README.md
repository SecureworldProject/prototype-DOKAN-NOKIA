# prototype-DOKAN-NOKIA
Este es el código para la aplicación mirror que corre sobre dokan

Para descargar dokan: https://github.com/dokan-dev/dokany

Reemplaza el fichero samples/dokan_mirror/mirror.c con este fichero

Para hacer pruebas con el prototipo de dokan:

1. Descargar el proyecto dokany de github (https://github.com/dokan-dev/dokany)
2. Instalar las dependencias de Visual Studio indicadas en el git de dokan (WDK, y WSDK) 
3. Abrir la solucion de dokan en Visual Studio
3. En el menú de visual studio elegimos build=>batch build y marcamos las opciones de win32/x64 release de todos los proyectos (se puede obviar memfs, ya que usaremos el ejemplo mirror). (https://github.com/dokan-dev/dokany/wiki/Build)
4. Si da algun problema añadir a visual studio las ultimas versiones de "spectre mitigated libs", desde el menu Tools ==> Get tools and features
5. Una vez compilado el proyecto, usamos los drivers
6. Para usar drivers modificados por ti sin firmar, hay que escribir esto en una consola de comandos y reiniciar:
    > bcdedit -set loadoptions DDISABLE_INTEGRITY_CHECKS
    
    > bcdedit -set TESTSIGNING ON
7. Una vez compilado hay que llevar los ficheros de las dll y el driver .sys desde la carpeta del proyecto a sus ubicaciones finales. (https://github.com/dokan-dev/dokany/wiki/Installation)
    > x64\Release\Driver\dokan1.sys ===> %WINDIR%\system32\drivers
    
    > x64\Release\dokan1.dll ==========> %WINDIR%\system32
    
    > x64\Release\dokannp.dll =========> %WINDIR%\system32
    
6. Instala el driver desde/x64/Release con la instrucción 
    > dokanctl.exe /i d
7. Ya puedes montar el filesystem desde la misma ruta en la que se encuentra mirror.exe con la instrucción:
    > mirror.exe /r C:\Users /l m

Con esto ya tienes compilado, instalado y montado el VFS en tu ordenador en la ruta M:\
Si haces cambios, solo cambias el mirror, no hace falta desinstalar ni cambiar ficheros.
