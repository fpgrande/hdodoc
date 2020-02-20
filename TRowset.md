

# HDO Documentación 


## Clase TRowSet

Esta clase se utiliza para enviar sentencias al servidor que devuelvan un conjuto de resultados.

Una vez obtenida la información se guardará en un array local navegable.

Incorpora métodos para poder realizar altas, bajas y modificaciones.

En cualquier momento se podrá refrescar el resultado obteniendo la información actual desde el servidor.

La velocidad está optimizada ya que incorpora un sistema de reciclaje de datos.

Hay dos maneras de obtener objetos de esta clase:

Al estilo xBase:

```xbase
oRS := TRowSet():new( <oHDO>, <cStatement> )
```

y al estilo java:
```xbase
oRS := <oHDO>:rowSet( <cStatement> )
```
Una vez creado el objeto lo siguiente sería establecer los atributos si son necesarios y enlazar las variables harbour con los parámetros de la sentencia por su posición.

Cuando el sistema esté configurado a nuestras necesidades se envía el metodo :load() que carga la información en el cliente desde el servidor.

Un ejemplo básico:
```xbase
...
local cName , aRec
local oRS

oRS := oDb:rowSet( "SELECT * FROM test WHERE first = ?;" ) // Crea el objeto RowSet
oRS:setAttribute( ATTR_STR_PAD, .t. ) // Hace que se rellene de espacios los campos string
oRS:bindParam(  1, @cName ) // Vincula la variable cName con el primer y único parámetro, el 1

cName := "Lailton"

oRS:load() // Carga el resultado desde el serbidor al cliente. Es como si se ejecutara:
// SELECT * FROM test WHERE first = 'Lailton';

...

oRS:goTo( 10 ) // Va al registro
? oRS:fieldGet( 1 ), oRS:fieldGet( "first" ) // Muestra un campo por posición o por nombre
aRec := oRS:getValues() // Carga el contenido del registro en una array

cName := "Jose" // Cambia el valor de la variable vinculada
oRS:reLoad() // Recarga el cliente desde el servidor con el nuevo valor. Se ejecuta:
// SELECT * FROM test WHERE first = 'Jose';

...
```
### Métodos

#### new()

##### **Sintaxis:**

TRowSet():new( <oHDO>, <cStatement> )

##### **Argumentos:**

- *<oHDO>* 

  Objeto que representa la conexión con la base de datos.

- *<cStatement>* 

  Sentencia SQL para obtener los campos seleccionados, de una o mas tablas.

##### **Devuelve:**

Una referencia al objeto TRowSet recien creado.

##### **Descripción:**

Es el método constructor de la clase.

##### **Ejemplo:**

```xbase
oRowset := TRowSet():new( oDataBase, "SELECT * FROM test WHERE last like 'R%'" )
```
### bindParam()

**Sintaxis:**

bindParam( <xParameter>, <variable> )

**Argumentos:**

- *<xParameter>* 

  Identificador del parámetro, posicion del parametro de sustición en el comando SQL.

  En algunos gestores como SQLite se puede usar el nombre precedido de "":"", por ejemplo:

  :bindParam( ":code",  @cCode )

  En próximas versiones de HDO se implementará esta sintaxis para todos las bases de datos.

- *<cSentence>* 

  Nombre de la variable de Harbour a vincular al parámetro de la sentencia SQL.

  Importante, se debe pasar por referencia o sea precedida por @.

**Devuelve:**

Vedadero, en caso de éxito, falso en caso de error.

**Descripción:**

Vincula una variable de harbour a un parámetro de sustitución con el signo de interrogación o con el :nombre (si el gestor lo admite) correspondiente de la sentencia SQL.

**Ejemplo:**

```xbase
	....
	local cLast
	
	oRowset := TRowSet():new( oDataBase, "SELECT * FROM test WHERE last like ?" )
	oRowset:bindParam( 1, @cLast )
	
	cLast := "Pepito"
	
	oRowSet:load()
```

Tambié se puede usar así, si el gestor lo permite, como en SQLite:


```xbase
	...
	local cLast
	
	oRowset := TRowSet():new( oDataBase, "SELECT * FROM test WHERE last like :lastname" )
	oRowset:bindParam( ":lastaname", @cLast )
	
	cLast := "pepito"
	
	oRowSet:load()
```

### bindValue()

**Sintaxis:**

bindValue( <nParameter>, <cValue> )

**Argumentos:**

- *<nParameter>* 

  Identificador del parámetro, posicion del parametro de sustición en el comando SQL.

- *<cValue>* 

  Valor a vincular al parámetro de la sentencia SQL.

**Devuelve:**

Vedadero, en caso de éxito, falso en caso de error.

**Descripción:**

Vincula un valor a un parámetro de sustitución con el signo de interrogación correspondiente de la sentencia SQL.

**Ejemplo:**

```xbase
	oRowset := TRowSet():new( oDataBase, "SELECT * FROM test WHERE last like ?" )
	oRowset:bindParam( 1, "R%" )
	oRowSet:load()
```

### getQueryStr()

**Sintaxis:**

getQueryStr()

**Devuelve:**

La sentencia SQL con la que se invoco el la creación del RowSet.

**Descripción:**

Muestra la sentecia completa con la que se creo el objeto RowSet.

**Ejemplo:**

```xbase
	oRowset := TRowSet():new( oDataBase, "SELECT * FROM test WHERE last like R%" )
	oRowset:getQueryStr() // --> "SELECT * FROM test WHERE last like R%"
```

### bindParamCount()

**Sintaxis:**

bindParamCount()

**Devuelve:**

El número de parametros de sustitución de la sentecncia SQL del RowSet.

**Descripción:**

Muestra el número de parametros de la sentecia completa con la que se creo el objeto RowSet.

**Ejemplo:**

```xbase
	oRowset := TRowSet():new( oDataBase, "SELECT * FROM test WHERE last like ?" )
	oRowset:bindParam( 1, "R%" )
	oRowSet:bindParamCount() // --> 1
```

### errorCode()

**Sintaxis:**

errorCode()

**Devuelve:**

El último código de error, en la ejecución de RowSet.

**Descripción:**

Muestra el código de error en la última ejecución de RowSet, o ceros, si no hubo errores.

**Ejemplo:**

```xbase
	oRowset := TRowSet():new( oDataBase, "SELECT * FROM test WHERE last like ?" )
	oRowset:errorCode() // --> 00000
```

### errorNo()

**Sintaxis:**

errorNo()

**Devuelve:**

El último número de error, en la ejecución de RowSet.

**Descripción:**

Muestra el número de error en la última ejecución de RowSet, o cero, si no hubo errores.

**Ejemplo:**

```xbase
	oRowset := TRowSet():new( oDataBase, "SELECT * FROM test WHERE last like ?" )
	oRowset:errorNo() // --> 0
```

### errorStr()

**Sintaxis:**

errorStr()

**Devuelve:**

El último texto de error, en la ejecución de RowSet.

**Descripción:**

Muestra el texto de error en la última ejecución de RowSet, o cero, si no hubo errores.

**Ejemplo:**

```xbase
	oRowset := TRowSet():new( oDataBase, "SELECT * FROM test WHERE last like ?" )
	oRowset:errorStr() // --> ""
```

