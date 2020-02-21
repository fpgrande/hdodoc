
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



#### free()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:



#### exec()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:



#### execDirect()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:



#### execScalar()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:



#### prepare()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:



#### query()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:



#### rowset()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:



#### lastInsertID()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:



#### beginTransaction()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:



#### commit()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:



#### inTrasaction()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:



#### rollback()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:



#### setAttribute()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:



#### getAttribute()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:



#### errorCode()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:



#### errorNo()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:



#### errorStr()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:



#### escapeStr()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:



#### ping()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:



#### parse()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:



#### throwException()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:



#### throw()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:



#### rdlInfo()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:



#### getHandle()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:



#### getRdlName()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:



#### getDbName()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:



#### getHost()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:



#### getUser()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:



#### getPassword()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:



#### getPort()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:



#### getUnixSocket()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:



#### getClientFlag()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:



#### loadFromFile()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:



#### listTables()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:



#### xCreateTable()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo: