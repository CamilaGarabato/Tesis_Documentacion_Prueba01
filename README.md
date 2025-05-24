# Tesis_Documentacion_Prueba01
En este repositorio voy a poner el código útil para el análisis de datos de mi proyecto de investigacion 

# ─── CARGA DE PAQUETES ─────────────────────────────────────────────
library(googlesheets4)  # Para leer Google Sheets
library(dplyr)          # Manipulación de datos
library(tidyr)          # Transformaciones si son necesarias
library(lubridate)      # Manejo de fechas
library(readr)          # Para funciones más rápidas de lectura/escritura

# ─── AUTENTICACIÓN GOOGLE (solo si es necesario) ───────────────────
gs4_auth()  # Te abre el navegador si no estás autenticada

# ─── CARGA DEL SHEET ───────────────────────────────────────────────
url_sheet <- "https://docs.google.com/spreadsheets/d/1yn91IP-jtoK2_SHl4mz-b5ykh6__8alEZoTQy9IDyrg/edit?gid=542417067#gid=542417067"
datos <- read_sheet(url_sheet)

# ──────────────────────────────────────
# 3. LIMPIEZA BÁSICA DE DATOS
# ──────────────────────────────────────

#### CAMBIAMOS EL FOMRATO DE FECHAMEDICION A DATE
datos$fecha_medicion <- as.Date(datos$fecha_medicion)
class(datos$fecha_medicion)
# En el caso de fecha_aparicion_complicaicon exiten filas con la palabra "Ninguna" los vamos a convertir a NA
datos$fecha_aparicion_complicacion <- unlist(datos$fecha_aparicion_complicacion) ### desempacamos la lista
datos$fecha_aparicion_complicacion <- ifelse (tolower(datos$fecha_aparicion_complicacion) == "ninguna",NA, datos$fecha_aparicion_complicacion)
datos$fecha_aparicion_complicacion <- as.Date(datos$fecha_aparicion_complicacion, format = "%Y-%m-%d")
class(datos$fecha_aparicion_complicacion)                                              

### conversion de datos a factor
datos$sexo <- as.factor(datos$sexo)
class(datos$sexo)
datos$hta <- as.factor(datos$hta)
datos$dislipemia <- as.factor(datos$dislipemia)
datos$presente = as.factor(datos$presente)
datos$tratamiento_farmacologico_diabetes = as.factor(datos$tratamiento_farmacologico_diabetes)
datos$numero_farmacos = as.factor(datos$numero_farmacos)
datos$otras_terapias_farmacologicas = as.factor(datos$otras_terapias_farmacologicas)


# ─── CHEQUEO FINAL ─────────────────────────────────────────────────
str(datos)              # Ver estructura y tipos finales
summary(datos)          # Resumen rápido
head(datos, 10)         # Ver los primeros registros

