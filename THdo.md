
 # HDO Documentación


 ## Clase THdo

Encapsula la complejidad de la conexión al servidor y a la base de datos.

# Métodos

#### new()

##### **Sintaxis:**

THDO():new( _DBMS )

##### **Argumentos:**

- *<_DBMS>* 

  Objeto que representa la conexión con la base de datos.


##### **Devuelve:**

Una referencia al objeto THdo recién creado.

##### **Descripción:**

Es el método constructor de la clase.

##### **Ejemplo:**

```xbase
oDb := THDO():new( _DBMS )
```



#### connect()

##### Sintaxis:

oDb:connect( _DB, _CONN )

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```Xbase
oDb:connect( _DB, _CONN )
```



#### disconnect()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```Xbase
local oDb
local cTabla := "test"
local cCreaTabla := "CREATE TABLE IF NOT EXISTS test ( "  + ;
                                "id INTEGER PRIMARY KEY " + cAutoInc + ","  + ;
                                "first    VARCHAR( 20 ),"     + ;
                                "last     VARCHAR( 20 ),"     + ;
                                "street   VARCHAR( 30 ),"     + ;
                                "city     VARCHAR( 30 ),"     + ;
                                "state    VARCHAR( 2 ),"      + ;
                                "zip      VARCHAR( 10 ),"     + ;
                                "hiredate DATE,"              + ;
                                "married  BOOL,"              + ;
                                "age      INTEGER,"           + ;
                                "salary   DECIMAL( 9, 2 ),"   + ;
                                "notes    VARCHAR( 70 ) );"
oDb := THDO():new( _DBMS,  )
if oDb:connect( _DB, _CONN )
        msg( _DB + " abierta" )
	try
        oDb:exec( cCreaTabla )
        msg( "La tabla " + cTabla + " se ha creado correctamente" )
	catch
        msg( "Codigo del error: " + oDb:errorCode() + ;
             ";Numero de error: " + hb_ntos( oDb:errorCode() ) + ;
             ";Descripcion del error: " + oDb:errorStr(), ;
             "Error al crear la tabla " + cTabla )
    end
endif
oDb:disconnect()
msg( _DB + " cerrada" )
```



#### free()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```Xbase
oCon := THDO():new( _DBMS )
if oCon:connect( _DB, _CONN )
...
endif
oCon:free()
```



#### exec()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```Xbase

```



#### execDirect()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```Xbase

```



#### execScalar()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase

```



#### prepare()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase

```



#### query()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase

```



#### rowset()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase

```



#### lastInsertID()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase

```



#### beginTransaction()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase

```



#### commit()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase

```



#### inTrasaction()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase

```



#### rollback()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase

```



#### setAttribute()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase

```



#### getAttribute()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase

```



#### errorCode()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase

```



#### errorNo()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase

```



#### errorStr()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase

```



#### escapeStr()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase

```



#### ping()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase

```



#### parse()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase

```



#### throwException()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase

```



#### throw()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```
xbase
```



#### rdlInfo()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase

```



#### getHandle()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase

```



#### getRdlName()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase

```



#### getDbName()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase

```



#### getHost()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase

```



#### getUser()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase

```



#### getPassword()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase

```



#### getPort()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase

```



#### getUnixSocket()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase

```



#### getClientFlag()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase

```



#### loadFromFile()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase

```



#### listTables()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase

```



#### xCreateTable()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xb

```





