###############################################################################
#
# IG - Informática Gráfica
# Grado en Ingeniería Informática
#
# 2014 - Ernesto Serrano <erseco@correo.ugr.es>
# ---------------------------------------------
#
# Fichero Makefile para generacion de ejecutables, paquetes y documentacion
# Compila tanto en linux como en mac
#
###############################################################################

# VARIABLES
BIN 	= bin
SRC 	= src
OBJ 	= obj
LIB 	= lib
INCLUDE = include

# Definición de compiladores
CXX = g++ -Ofast -Wno-write-strings
CC = gcc -Ofast

# banderas para el compilador (C y C++). Se indican los directorios donde se puenden
# encontrar ficheros para incluir mediante la opcion -I
# la opcion -g sirve para permitir la depuración
CFLAGS=    -DXWINDOWS -DSHM -I/usr/include -I$(INCLUDE) -Wno-deprecated
CXXFLAGS=  -DXWINDOWS -DSHM -I/usr/include -I$(INCLUDE) -Wno-deprecated

# banderas para el enlazador
# Se indica directorios donde encontrar las funciontecas con -L. Usando -l seguido del
# nombre se indica la funcionteca que se desea enlazar.
OS := $(shell uname)
ifeq ($(OS),Darwin) #flags para MAC OS X
LDFLAGS=  -framework OpenGL -framework GLUT
else  #flags para linux
LDFLAGS=  -lGLU -lGL -lglut
endif

# Nombre del fichero ejecutable
TARGETS = practica1


# TODO (sin empaquetado)
all: clean $(TARGETS)

# COMPILACION

$(TARGETS):
	$(CXX) -o $(BIN)/$@ $(CXXFLAGS) $(SRC)/file_ply_stl.cc $(SRC)/model.cpp $(SRC)/model_ply.cpp $(SRC)/model_cube.cpp $(SRC)/model_pyramid.cpp $(SRC)/practica1.cc $(LDFLAGS)



# DOCUMENTACION
# Genera la documentacion mediante doxygen en la carpeta doc
.PHONY: doc
doc:
	doxygen doc/doxys/Doxyfile

# EMPAQUETADO
# Genera el archivo .zip de la práctica mediante la linea de comandos
# Omite los archivos propios de MacOSX y coge el nombre del directorio como nombre
.PHONY: package
package: clean
	@echo "Empaquetando..."
	zip $(shell basename "$(CURDIR)")_Ernesto_Serrano.zip -9 -r ./* -x "*.DS_Store" -x "__MACOSX"


tgz: clean #REVISAR
	@echo "Empaquetando .tgz..."
	tar -zcvf $(TARGETS).tgz * -x "*.DS_Store" -x "__MACOSX"

# LIMPEZA
# Limpia los archivos compilados, así como los archivos objeto y los paquetes zip
.PHONY: clean
clean:
	@echo "Limpiando..."
	@rm -f $(OBJ)/*\
        $(BIN)/*\
        ./*.zip
