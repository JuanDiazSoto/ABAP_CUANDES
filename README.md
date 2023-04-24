# Buenas Practicas ABAP.

la idea de estas, es poder tener un codigo elegible y optimo.

## SQL

- no utilizar la sentencia **SELECT * FROM**.
- no utilizar la sentencia **FOR ALL ENTRIES**.
- no utilizar la sentencia **INTO CORRESPONDING FIELDS**, ni tampoco utilizar **INTO CORRESPONDING FIELDS TABLE**.

## VALIDACIÓN DE DATOS

- al utilizar la sentencia **READ TABLE** debe asegurarse de ordenar segun parametros de lectura antes de ser
  utilizada dicha sentencia, ademas debera incluir la sentencia **BINARY SEARCH**.
  
  Ejemplo:
  
  **SORT** itab **BY** key1.
  
  **READ TABLE** itab **WITH KEY** key1 = value1 **BINARY SEARCH**.
  
  
  
- no validar retornos de sentencias SQL  
  
  Ejemplo:
  
  **SELECT** zcampo1, zcampo2 **INTO TABLE** lt_interna  
  **FROM** zejemplo  
  **WHERE** zcampo1 **EQ** lv_valor.  
  
  
  
  **IF** SY-SUBRC **EQ** 0. "esta sentenia deberia siempre deberia ir despues de una consulta SQL  
  **ENDIF**.
  
    
 - siempre validar rangos antes de ser utilizados en una sentencia SQL.
    
    Ejemplo:
    
    **IF** rg_campo1 **IS NOT INITIAL**.
    
    **SELECT** campo1, campo2 **INTO TABLE** lt_interna   \
    **FROM** zejemplo  \
    **WHERE** zcampo **IN** RG_CAMPO1.
     
    **ENDIF**.
    
 ## DECLARACIÓN DE DATOS
 
- No ocupar datos en duro, se recomienda declarar constantes en el TOP o al inicio del PERFORMS donde vaya ser instanciado,  \
  otra manera seria dejar constantes en la tvarvc o crear un set de datos.
- No utilizar tablas con cabecera.
- Declarar datos y no utilizarlos.

## ERRORES A NIVEL DE PROGRAMA.

- es necesario que a las tablas estandar se accedan con sus respectivas llaves o indices.
- no utilizar sentencia select dentro de un loop ni en capas inferiores.
- si es necesario Modularizar sentencias que se utilizan repetitivamente, ejemplo formatos de fecha y hora.
- siempre diseñar el programa a nivel de performs y no todo en uno mismo, con la idea principal que el codigo sea siempre  \
  entendible.
- A todos los programas y tablas debera solicitar objeto de autorización.
  
## NOMENCLATURAS.

- siempre ocupar las nomenclaturas ya establecidas por la empresa, tanto a nivel de codigo como creacion de objetos.

### NOMENCLATURAS OBJETOS
  
  en sap hay distintos tipos de objetos, cualquiera que sea este si es creado por un ABAP, para disponibilizarlo como solución  \
  este debe empezar con una **Z**.
  Ademas debe considerar el modulo al que pertenece dicho objeto:
  
  Tabla de modulos SAP. (tabla 1)
  
| Paquete |  Descripción |
|---------| -------------|
|BC| Uso genérico |
|BW| Business Warehouse|
|CO| Controlling|
|CS| Servicio al Cliente|
|FI| Finanzas|
|HR| Recursos Humanos|
|MM| Materiales|
|PM| Mantenimiento|
|PP| Producción|
|PS| Gestión de Proyectos|
|QM| Calidad|
|SD| Ventas y Distribución|
|WM| Gestión de Almacenes|
  
Los nombres de estos objetos tendrán la siguiente forma Z[MS][T][NNNN] donde:

Z : Por definición SAP  \
MS : Módulo SAP (ver tabla 1) \
T : Tipo de programa (ver tabla 2)  \
NNNN : nombre o correlativo según empresa.
  
Ejemplo (tabla 2)
  
| TIPO DE OBJETO | NOMENCLATURA | EJEMPLO |
| ---------------| -------------|---------|
| TABLA          | T  | ZMS_T_NNNN|
| ESTRUCTURA     | S  | ZMS_S_NNNN|
| TIPO TABLA      | TT | ZMS_TT_NNNN|
| ELEMENTO DE DATOS | E | ZE_NNNN|
| DOMINIO DE DATOS | D | ZD_NNNN|
| AYUDA DE BUSQUEDA | H | ZH_NNNN|
| ESTILO (SAPSCRIPT) | ST | ZST_NNNN|
| SMARTFORMS | SF | ZMS_SF_NNNN|
| MODULO DE TEXTO | MT | ZMT_NNNN|
| GRUPO DE FUNCIONES | GF | ZMS_GF_NNNN|
| MODULO DE FUNCIONES | F | ZMS_F_NNNN|
| PROGRAMA | RP | ZMS_RP_NNNN |

