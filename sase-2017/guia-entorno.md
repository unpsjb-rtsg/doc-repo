
# Entorno de desarrollo

Guía de instalación y configuración del entorno de desarrollo basado en [Eclipse](http://www.eclipse.org).

Tabla de Contenidos:
- [GNU ARM Eclipse](#gnu-arm-eclipse)
- [Plug-ins adicionales](#plug-ins-adicionales)
- [Percepio Tracealyzer para FreeRTOS](#percepio-tracealyzer-para-freertos)
- [pyOCD](#pyocd)
- [Git](#git)
- [A continuación](#a-continuaci-n)

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
Descargar Git desde https://git-scm.com e instalarlo.

Se puede utilizar la interfaza gráfica `git-gui` ya incluida con Git, o seleccionar algún [cliente de terceros](https://git-scm.com/downloads/guis).

En esta guía solo se utilizarán comandos básicos de Git. Se pueden consultar estos tutoriales para conocer con más detalle su operación:
* Git in 15 minutes: https://try.github.io/
* Colección de tutoriales: https://www.atlassian.com/git/tutorials
* Git Tutorial: https://git-scm.com/docs/gittutorial
* Pro Git book: https://book.git-scm.com/book/en/v2

---

## A continuación
* Importar y compilar el [proyecto de prueba para la placa LPC1768](proyecto-prueba-lpc1768.md).

---

Eso sería todo :)
