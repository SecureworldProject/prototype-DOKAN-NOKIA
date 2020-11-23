# prototype-DOKAN-NOKIA
This is the code for the mirror application running on dokan

To download dokan: https://github.com/dokan-dev/dokany

Replace the file samples/dokan_mirror/mirror.c with this file

Para hacer pruebas con el prototipo de dokan:

1. Descargar el proyecto de VisualStudio de git
2. Instalar las dependencias indicadas en el paso anterior (WDK, y WSDK)
3. Para usar drivers modificados por ti sin firmar, hay que escribir esto en una consola de comandos y reiniciar:
    > bcdedit -set loadoptions DDISABLE_INTEGRITY_CHECKS
    
    > bcdedit -set TESTSIGNING ON
4. En el menú, elegimos build=>batch build y marcamos las opciones de win32/x64 release de todos los proyectos (se puede obviar memfs, ya que usaremos el ejemplo mirror)
5. Una vez compilado hay que llevar los ficheros de las dll y el driver .sys desde la carpeta del proyecto a sus ubicaciones finales.
    > x64\Release\Driver\dokan1.sys ===> %WINDIR%\system32\drivers
    
    > x64\Release\dokan1.dll ==========> %WINDIR%\system32
    
    > x64\Release\dokannp.dll =========> %WINDIR%\system32
    
6. Instala el driver desde/x64/Release con la instrucción 
    > dokanctl.exe /i d
7. Ya puedes montar el filesystem desde la misma ruta en la que se encuentra mirror.exe con la instrucción:
    > mirror.exe /r C:\Users /l m

Con esto ya tienes compilado, instalado y montado el VFS en tu ordenador en la ruta M:\
Si haces cambios, solo cambias el mirror, no hace falta desinstalar ni cambiar ficheros.
