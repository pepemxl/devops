# devops
Tutorials and Ideas for DevOps

## Pasos para generar un empaquetado en Linux( probado en Ubuntu 16.04 )
* Descargar la aplicación linuxdeployqt del repositorio de GitHub
	https://github.com/probonopd/linuxdeployqt
* Instalar dependencias de del software, revisar con ldd. La aplicación linuxdeployqt utiliza el comando ldd para revisar las dependencias del programa y poder empaquetarlos. Si el comando ldd no encuentra dichas dependencias faltantes, provocará un error. 
* Antes de empaquetar el software es necesario eliminar archivos innecesarios(en este caso archivos de Qt) con el siguiente comando:
* ELIMINAR ARCHIVOS INNECESARIOS DE LA CARPETA DEL EJECUTABLE
```bash
find build_release \( -name "moc_*" -or -name "*.o" -or -name "qrc_*" -or -name "Makefile*" -or -name "*.a" \) -exec rm {} \;
```
* Crear una estructura estilo AppDir.
```bash
./linuxdeployqt-continuous-x86_64.AppImage usr/share/applications/Test_R.desktop
```
```bash
./linuxdeployqt-continuous-x86_64.AppImage usr/bin/Test_R -qmake=/home/tracker/Qt_B/5.7/gcc_64/bin/qmake -appimage
```
El primer comando toma la imagen que se encuentra en share/applications/ y el segundo realiza el empaquetado.
* Si todo concluye sin errores solamente se debe permitir ejecución del archivo como programa ejecutable y listo. 

## Como agregar imagenes al proyecto de Qt.
http://korbinin.blogspot.com/2012/03/adding-icons-to-application-with-qt.html

## Estructura del árbol de directorios

Es necesario proveer la estructura básica `AppDir` (como el del ejemplo de la carpeta directory_tree_structure/) y debería verse como lo siguiente:
```
└── usr
    ├── bin
    │   └── your_app
    ├── lib
    └── share
        ├── applications
        │   └── your_app.desktop
        └── icons
            └── <theme>
                └── <resolution>
                    └── apps
                        └── your_app.png
```
Remplaza `<theme>` y `<resolution>` con (por ejemplo) `hicolor` y `256x256` respectivamente.

El archivo desktop debería verse como lo siguiente:
```
[Desktop Entry]
Type=Application
Name=Amazing Qt App
Comment=The best Qt Application Ever
Exec=your_app
Icon=your_app
Categories=Office;
```

Corre el siguiente comando: `linuxdeployqt-continuous-x86_64.AppImage path/to/AppDir/usr/share/applications/your_app.desktop`

## Para más información refiérase al repositorio:
```bash
https://github.com/probonopd/linuxdeployqt
```
