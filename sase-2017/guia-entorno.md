
# Entorno de desarrollo

Guía de instalación y configuración del entorno de desarrollo basado en [Eclipse](http://wwww.eclipse.org).

---

## GNU ARM Eclipse
Como primer paso, se instalará Eclipse CDT, el GNU ARM Embedded Toolchain, Windows Build Tools (si se utiliza Windows), Java (en caso de no estar ya instalado), y la serie de extensiones [GNU ARM Eclipse](http://gnuarmeclipse.github.io/).

Para esto, seguir la guía de instalación paso a paso de [GNU ARM Eclipse](http://gnuarmeclipse.github.io/install/).
* No es necesario realizar los pasos para instalar SEGGER J-Link o QEMU.

Estas son las guías a seguir en el enlace anterior (en orden):
* [GNU ARM Embedded Toolchain](http://gnuarmeclipse.github.io/toolchain/install)
* [Windows Build Tools](http://gnuarmeclipse.github.io/windows-build-tools/install/)
* [OpenOCD](http://gnuarmeclipse.github.io/openocd/install)
* [Eclipse CDT](http://gnuarmeclipse.github.io/plugins/install/)
* [GNU ARM Eclipse Plug-ins](http://gnuarmeclipse.github.io/plugins/install/)
* [Configuración adicional del workspace](http://gnuarmeclipse.github.io/eclipse/workspace/preferences) (no es obligatorio, aunque es recomendado)

---

## Plug-ins adicionales
Adicionalmente, instalar los siguientes plugins:
* [FreeRTOS Task Aware Debugger (TAD)](https://mcuoneclipse.com/2016/07/06/freertos-kernel-awareness-for-eclipse-from-nxp/) de NXP.
* [Percepio FreeRTOS Tracealyzer Plugin](https://percepio.com/docs/FreeRTOS/manual/Recorder.html#eclipse). Consultar esta [guía](https://mcuoneclipse.com/2017/03/08/percepio-freertos-tracealyzer-plugin-for-eclipse/) para información adicional.

---

## Percepio Tracealyzer para FreeRTOS
Instalar la aplicación [Percepio Tracealyzer para FreeRTOS](https://percepio.com/tz/freertostrace/):
* Para Windows ofrece un instalador.
* Para Linux / MacOS, un paquete `tar.gz`.

---

## pyOCD

PyOCD requiere Python 2.7, y no soporta Python 3. Si no esta ya instalado, descargar la última versión de Python 2.7 desde [www.python.org](http://www.python.org). Durante la instalación, seleccionar la opción **[Add to path]**, o agregar posteriormente el directorio de instalación al *path* del sistema.

Para verificar que Python haya sido instalado correctamente, ejecutar lo siguiente desde una linea de comandos, para obtener la versión instalada:
```
$ python --version
Python 2.7.10
$
```
Luego, para instalar pyOCD ejecutar desde una linea de comandos:
```
$ pip install pyocd
```
Para verificar que se haya instalado correctamente el `pyocd-gdbserver`, ejecutar lo siguiente desde una linea de comandos, para obtener la versión instalada:
```
$ pyocd-gdbserver --version
0.8.1a1
$
```

---

## Git
Descargar Git desde [https://git-scm.com]() e instalarlo.

Se puede utilizar la interfaza gráfica `git-gui` ya incluida con Git, o seleccionar algún [cliente de terceros](https://git-scm.com/downloads/guis).

En esta guía solo se utilizarán comandos básicos de Git. Se pueden consultar estos tutoriales para conocer con más detalle su operación:
* Git in 15 minutes: [https://try.github.io/]()
* Colección de tutoriales: [https://www.atlassian.com/git/tutorials]()
* Git Tutorial: [https://git-scm.com/docs/gittutorial]()
* Pro Git book: [https://book.git-scm.com/book/en/v2]()

---

## Proyecto de prueba
A continuación se descargará mediante Git un proyecto de prueba para la placa [mbed LPC1768](https://developer.mbed.org/platforms/mbed-LPC1768/).

### Clonar el proyecto de prueba
En primer lugar, clonar el proyecto de prueba usando Git: [https://github.com/unpsjb-rtsg/mbed-blinky-makefile]()
* Desde un cliente, usar la opción **[Clone]**.
* Desde la linea de comandos utilizar el comando `git clone`.

*Tip*: si tienen cuenta en GitHub, pueden probar con realizar un *fork* del proyecto.

### Importar el proyecto en Eclipse
Una vez clonado localmente, agregar el proyecto en Eclipse:
* Seleccionar **[File > Makefile project with existing code]**. 
* En la nueva ventana:
    * En **[Existing Code Location]** indicar el *path* al proyecto (usar el botón **[Browse...]**).
    * En **[Toolchain for Indexer]** seleccionar la opción *Cross ARM GCC* (¡importante!).

El proyecto debe aparecer ahora en la vista *Project Explorer*: 
* Hacer clic derecho sobre el mismo, y seleccionar **[Properties]** en el menú contextual.
* En la nueva ventana, seleccionar **[C/C++ Build > Settings]**. Si todo esta bien configurado, en la pestaña **[Toolchains]**, el campo *Name* debe indicar *GNU Tools for ARM Embedded Processors*.
* Hacer clic en **[Ok]**.

Verificar que dentro del proyecto exista el directorio `build`. En caso que no exista, crearlo haciendo clic derecho sobre el proyecto en la vista *Project Explorer*, y seleccionando **[New > Folder]** en el menú contextual.

### Compilar
Finalmente, para compilar el proyecto se puede:
* Hacer clic derecho sobre el proyecto en la vista *Project Explorer* y seleccionar **[Build]** en el menú contextual.
* Seleccionar en la barra de menúes de Eclipse **[Project > Build Project]**.
* Hacer clic en el ícono *Build* (un martillo).

Si el proyecto compilo correctamente, en la vista **[Console]** debe indicarse que se generó correctamente el archivo `build/blink.elf`.

### Ejecutar
Primero, verificar que el `pyocd-gdbserver` este correctamente configurado en Eclipse:
* Seleccionar **[Windows > Preferences]** en el menú de Eclipse.
* En la nueva ventana, seleccionar **[Run / Debug > PyOCD]** en la lista izquierda.
* En el campo *Executable* debe indicar `pyocd-gdbserver.exe` (sin la extensión en Linux o MacOS), y el campo *Folder* debe contener el *path* al ejecutable (en Windows `C:\Python27\Scripts`).
* Hacer clic en **[Ok]**.

A continuación se creará y ejecutará una configuración de *debug*:
* Seleccionar **[Run > Debug Configurations...]** en el menú de Eclipse.
* En la nueva ventana, hacer doble clic sobre **[GDB PyOCD debugging]** en el menú izquierdo. Esto crea una nueva configuración basada en este perfil.
* En el panel derecho:
    * En la pestaña **[Main]**, el campo *Project* debe indicar el nombre del proyecto de prueba. El campo *C/C++ Application* debe indicar el nombre del archivo ELF, en este caso `build/blink.elf`. Si no estuviera presente escribir el nombre del mismo, o bien hacer clic en el botón **[Search project]** o **[Explore]** para buscarlo.
    * En la pestaña **[Debugger]**, el campo *Executable* debe contener el valor `${pyocd_path}\${pyocd_executable}`. Estas dos variables son reemplazadas por los valores especificados el menú **[Run / Debug > PyOCD]**.
    * En la pestaña **[Common]**, seleccionar la opción **[Shared file:]**, indicando en el campo el nombre del proyecto. De esta manera el archivo `*.launch` con la configuración es guardado dentro del proyecto.
    * Hacer clic en el botón **[Apply]**.
* Con la placa mbed LPC1768 conectada a la PC, hacer clic en el botón **[Debug]**. Es posible que Eclipse pregunte si se desea cambiar a la perspectiva *Debug*, responder que sí.

---

Eso sería todo :)

