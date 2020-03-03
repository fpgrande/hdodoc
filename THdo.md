
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

##### **Argumentos:**

- *<_DB>* 

  Base datos en el que tratará de hacer la conexión.

- *<_CONN>* 

  Cadena de conexión que lleva los siguientes datos: 
  
  - Dirección IP del servidor
  - Usuario que hace la conexión
  - Contraseña del usuario que hace la conexión
  - Puerto usado para la conexión
  - Socket
  - Bandera 

##### Devuelve:

Valor lógico con el resultado de la conexión.

##### Descripción:

Hace la conexión con la base de datos, hay bases de datos que no necesitan todos los parámetros por los que no habrá que pasarle ese parámetro o sencillamente el gestor de la base de datos los ignorará.

Por ejemplo SQLite solo necesita el nombre de la base de datos.

##### Ejemplo:

```Xbase
oDb:connect( _DB, _CONN )
```



#### disconnect()

##### Sintaxis:

oDb:disconnect()

##### Argumentos:

Sin parámetros.

##### Devuelve:

Un valor lógico con el resultado de la desconexión.

##### Descripción:

Desconecta y libera la memoria. Es una especie de destructor.

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

oCon:free()

##### Argumentos:

Sin parámetros.

##### Devuelve:

Un valor lógico con el resultado de la desconexión.

##### Descripción:

Desconecta y libera la memoria. Es igual que el método **disconnect()**

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

oDb:exec( cCreaTabla )

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



#### execDirect()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```Xbase
#define _CREA_TB_IMG "CREATE TABLE IF NOT EXISTS test_img ( uid INTEGER, foto LONGBLOB );"
#define _INS_IMG "INSERT INTO test_img( uid, foto ) VALUES( ?, ? );"
local oDb, oStmt
oDb := THDO():new( _DBMS )
if oDb:connect( _DB, _CONN )
   oDb:execDirect( _CREA_TB_IMG )
   oStmt := oDb:prepare( _INS_IMG )
   oStmt:bindValue( 1, 1 )
   oStmt:bindValue( 2, oDb:loadFromFile( "Img_00.png" ) )
   oStmt:execute()
   
   oStmt:bindValue( 1, 2 )
   oStmt:bindValue( 2, oDb:loadFromFile( "img_01.bmp" ) )
   oStmt:execute()
	
   oStmt:free()
endif
oDb:free()
```



#### execScalar()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase
local oDb
oDb := THDO():new( _DBMS )
if oDb:connect( _DB, _CONN )       //count(*)
   msg( oDb:execScalar( "SELECT *  FROM test", 12 ), "Num. Reg. en Test" )
endif
oDb:disconnect()

```



#### prepare()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase
local oDb, oStmt, e
local cTabla := "test"
local first, last, street, city, state, zip, hiredate, married, age, salary, notes
local cSql := "INSERT INTO " + cTabla + ;
      " ( first, last, street, city, state, zip, hiredate, married, age, salary, notes ) "  + ;
      "VALUES ( ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ? );"
oDb := THDO():new( _DBMS )
if oDb:connect( _DB, _CONN )
   TRY
     oDb:beginTransaction()
////////////////////////////////////////////////////////////////////////////////
// Sepuede usar eto:			
//            oStmt := oDb:prepare( cSql ) // Prepara la sentencia
// o esto:
			oStmt := TStmt():new( oDb )
			oStmt:prepare( cSql )
////////////////////////////////////////////////////////////////////////////////
           // ----------------------------------------------------------------
            // Enlaza los valores con los parametros de sustitucion
            oStmt:bindValue( 1, 'Maria' )
            oStmt:bindValue( 2, 'Gimenez' )
            oStmt:bindValue( 3, 'Pintor Velazquez, 89' )
            oStmt:bindValue( 4, 'Dos Hermanas' )
            oStmt:bindValue( 5, 'ES' )
            oStmt:bindValue( 6, '41700' )
            oStmt:bindValue( 7, myDate() )
            oStmt:bindValue( 8, .t. )
            oStmt:bindValue( 9,  33 )
            oStmt:bindValue( 10, 5670.50 )
            oStmt:bindValue( 11, 'Esta es la nota de Maria...' )

            oStmt:execute()
            oStmt:free()

			oStmt := TStmt():new( oDb )
			oStmt:prepare( cSql )
	CATCH e
            eval( errorblock(), e )
			oDb:rollBack()
    FINALLY
            oStmt:free()
    end
endif
oDb:disconnect()
```



#### query()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase
local oDb, oStmt, e
local cSql := "SELECT * FROM test"
	
oDb := THDO():new( _DBMS )

if oDb:connect( _DB, _CONN )

   TRY		
		oStmt := oDb:query( cSql )
   CATCH e
        msg( "Se ha producido un error" )
        eval( errorblock(), e )
   FINALLY
        // Cierra el objeto sentencia para liberar memoria
        oStmt:free()
   end
endif
oDb:disconnect()
```



#### rowset()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase
#define STMT_SEL "SELECT * FROM test;"
local oDb, oRS
oDb := THDO():new( _DBMS )
if oDb:connect( _DB, _CONN )
        oRS := oDb:rowSet( STMT_SEL )
        oRS:load()
        oRS:GoTop()
		miBrwCursor( oRS, 0, 0, maxrow(), maxcol() )
        oRS:free()
endif
oDb:disconnect()
```



#### lastInsertID()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase
local oDb, i, e
oDb := THDO():new( _DBMS )
TRY
   oDb:connect( _DB, _CONN )		
        msg( _DB + " abierta;;" + if( oDb:inTransaction(), "Esta ", "No esta " ) + "en una trasaccion" )			
        oDb:beginTransaction()
        msg( "Ahora " + if( oDb:inTransaction(), "esta ", "no esta " ) + "en una trasaccion" )			
        i := oDb:exec( cIns )
        msg( hb_ntos( i ) + " - " + hb_ntos( oDb:lastInsertId() ), "Columnas afectadas y lastInsertId" )			
        oDb:commit()
CATCH e
        muestra( e:SubSystem + ";" + padl( e:SubCode, 4 ) + ";" + ;
           e:Operation + ";" + e:Description, "Error desde Harbour" )
        oDb:rollBack()
finally
        oDb:disconnect()
        msg( _DB + " cerrada" )
end
```



#### beginTransaction()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase
local oDb, i, e
oDb := THDO():new( _DBMS )
TRY
   oDb:connect( _DB, _CONN )		
        msg( _DB + " abierta;;" + if( oDb:inTransaction(), "Esta ", "No esta " ) + "en una trasaccion" )			
        oDb:beginTransaction()
        msg( "Ahora " + if( oDb:inTransaction(), "esta ", "no esta " ) + "en una trasaccion" )			
        i := oDb:exec( cIns )
        msg( hb_ntos( i ) + " - " + hb_ntos( oDb:lastInsertId() ), "Columnas afectadas y lastInsertId" )			
        oDb:commit()
CATCH e
        muestra( e:SubSystem + ";" + padl( e:SubCode, 4 ) + ";" + ;
           e:Operation + ";" + e:Description, "Error desde Harbour" )
        oDb:rollBack()
finally
        oDb:disconnect()
        msg( _DB + " cerrada" )
end
```



#### commit()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase
local oDb, i, e
oDb := THDO():new( _DBMS )
TRY
   oDb:connect( _DB, _CONN )		
        msg( _DB + " abierta;;" + if( oDb:inTransaction(), "Esta ", "No esta " ) + "en una trasaccion" )			
        oDb:beginTransaction()
        msg( "Ahora " + if( oDb:inTransaction(), "esta ", "no esta " ) + "en una trasaccion" )			
        i := oDb:exec( cIns )
        msg( hb_ntos( i ) + " - " + hb_ntos( oDb:lastInsertId() ), "Columnas afectadas y lastInsertId" )			
        oDb:commit()
CATCH e
        muestra( e:SubSystem + ";" + padl( e:SubCode, 4 ) + ";" + ;
           e:Operation + ";" + e:Description, "Error desde Harbour" )
        oDb:rollBack()
finally
        oDb:disconnect()
        msg( _DB + " cerrada" )
end
```



#### inTrasaction()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase
local oDb, i, e
oDb := THDO():new( _DBMS )
TRY
   oDb:connect( _DB, _CONN )		
        msg( _DB + " abierta;;" + if( oDb:inTransaction(), "Esta ", "No esta " ) + "en una trasaccion" )			
        oDb:beginTransaction()
        msg( "Ahora " + if( oDb:inTransaction(), "esta ", "no esta " ) + "en una trasaccion" )			
        i := oDb:exec( cIns )
        msg( hb_ntos( i ) + " - " + hb_ntos( oDb:lastInsertId() ), "Columnas afectadas y lastInsertId" )			
        oDb:commit()
CATCH e
        muestra( e:SubSystem + ";" + padl( e:SubCode, 4 ) + ";" + ;
           e:Operation + ";" + e:Description, "Error desde Harbour" )
        oDb:rollBack()
finally
        oDb:disconnect()
        msg( _DB + " cerrada" )
end
```



#### rollback()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase
local oDb, i, e
oDb := THDO():new( _DBMS )
TRY
   oDb:connect( _DB, _CONN )		
        msg( _DB + " abierta;;" + if( oDb:inTransaction(), "Esta ", "No esta " ) + "en una trasaccion" )			
        oDb:beginTransaction()
        msg( "Ahora " + if( oDb:inTransaction(), "esta ", "no esta " ) + "en una trasaccion" )			
        i := oDb:exec( cIns )
        msg( hb_ntos( i ) + " - " + hb_ntos( oDb:lastInsertId() ), "Columnas afectadas y lastInsertId" )			
        oDb:commit()
CATCH e
        muestra( e:SubSystem + ";" + padl( e:SubCode, 4 ) + ";" + ;
           e:Operation + ";" + e:Description, "Error desde Harbour" )
        oDb:rollBack()
finally
        oDb:disconnect()
        msg( _DB + " cerrada" )
end
```



#### setAttribute()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase
#define HDO_ATTR_DEF_STR_PAD 		    100003	/* IO PAD por defecto */
#define HDO_ATTR_DEF_TINY_AS_BOOL 	    100004	/* IO Tiny as bool por defecto */ 
   
local lRet

oDb := THDO():new( _DBMS )
	
lRet := oDb:connect( _DB, _CONN )
	
if lRet
   oDb:setAttribute( HDO_ATTR_DEF_STR_PAD, .t. )
   oDb:setAttribute( HDO_ATTR_DEF_TINY_AS_BOOL,.t. )
   preparaStmt()
endif
```



#### getAttribute()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase
local oDb
oDb := THDO():new( _DBMS )
if oDb:connect( _DB, _CONN )
        msg( "Base de datos " + _DB + " abierta" )
endif
muestra( oDb:rdlInfo() )
cls
? "Estado actual de los atributos de HDO:"
? "-------------------------------------------------------------------------"
? "HDO_ATTR_RDL_NAME ------------->", oDb:getAttribute( HDO_ATTR_RDL_NAME )
? "HDO_ATTR_CASE ----------------->", oDb:getAttribute( HDO_ATTR_CASE )
? "HDO_ATTR_AUTOCOMMIT ----------->", oDb:getAttribute( HDO_ATTR_AUTOCOMMIT )
? "HDO_ATTR_TIMEOUT -------------->", oDb:getAttribute( HDO_ATTR_TIMEOUT )
? "HDO_ATTR_CONNECTION_STATUS ---->", oDb:getAttribute( HDO_ATTR_CONNECTION_STATUS )
? "HDO_ATTR_ERRMODE -------------->", oDb:getAttribute( HDO_ATTR_ERRMODE )
? "HDO_ATTR_DEF_STR_PAD ---------->", oDb:getAttribute( HDO_ATTR_DEF_STR_PAD )
? "HDO_ATTR_DEF_TINY_AS_BOOL------>", oDb:getAttribute( HDO_ATTR_DEF_TINY_AS_BOOL )
? "HDO_ATTR_SERVER_VERSION ------->", oDb:getAttribute( HDO_ATTR_SERVER_VERSION )
? "HDO_ATTR_CLIENT_VERSION ------->", oDb:getAttribute( HDO_ATTR_CLIENT_VERSION )
? "HDO_ATTR_SERVER_INFO ---------->", oDb:getAttribute( HDO_ATTR_SERVER_INFO )
? "HDO_ATTR_CLIENT_INFO ---------->", oDb:getAttribute( HDO_ATTR_CLIENT_INFO )
? "-------------------------------------------------------------------------"
espera()
oDb:free()
msg( _DB + " cerrada" )    
```



#### errorCode()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase
local oDb
oDb := TMyHDO():new( _DBMS )
if oDb:connect( _DB, _CONN )
...
...
else
        Msg( oDb:errorCode(), "Codigo del Error" )
        Msg( Str( oDb:errorNo() ),"Numero del Error")
        Msg( oDb:errorStr(),"Cadena de error")
        msg( "No se ha establecido la conexion" )
endif
oDb:disconnect()
```



#### errorNo()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase
local oDb
oDb := TMyHDO():new( _DBMS )
if oDb:connect( _DB, _CONN )
...
...
else
        Msg( oDb:errorCode(), "Codigo del Error" )
        Msg( Str( oDb:errorNo() ),"Numero del Error")
        Msg( oDb:errorStr(),"Cadena de error")
        msg( "No se ha establecido la conexion" )
endif
oDb:disconnect()
```



#### errorStr()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase
local oDb
oDb := TMyHDO():new( _DBMS )
if oDb:connect( _DB, _CONN )
...
...
else
        Msg( oDb:errorCode(), "Codigo del Error" )
        Msg( Str( oDb:errorNo() ),"Numero del Error")
        Msg( oDb:errorStr(),"Cadena de error")
        msg( "No se ha establecido la conexion" )
endif
oDb:disconnect()
```



#### escapeStr()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase
msg( oDb:escapeStr( [Manuel's kely \todo mi\o /\/\ y mira las comillas dobles "j2j2"] ), "Ejemplo de escapeStr" )
msg( oDb:escapeStr( "" ), "Ejemplo de escapeStr" )
msg( oDb:escapeStr( 1 ), "Ejemplo de escapeStr" )
msg( oDb:escapeStr(), "Ejemplo de escapeStr" )
```



#### ping()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase
???
```



#### parse()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase
???
```



#### throwException()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase
???
```



#### throw()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase
???
```



#### rdlInfo()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase
local oDb
oDb := THDO():new( _DBMS )
if oDb:connect( _DB, _CONN )
   msg( "Base de datos " + _DB + " abierta" )
endif
muestra( oDb:rdlInfo() )
...
...
oDb:free()
msg( _DB + " cerrada" )
```



#### getHandle()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase
// Procesa los datos:
HDO_rowProcess( oCon:getHandle(), hBackFile, cTbName )
```



#### getRdlName()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase
CLASS TMyHDO INHERIT THDO

    METHOD info()

END CLASS

PROCEDURE info() CLASS TMyHDO

    local a := ::rdlInfo()

    aadd( a, ;
        "Host: "        + ::getHost()        + ";" + ;
        "DbName: "      + ::getDbName()      + ";" + ;
        "User: "        + ::getUser()        + ";" + ;
        "Password: "    + ::getPassword()    + ";" + ;
        "Port: "    	+ AllTrim( Str( ::getPort() ) ) + ";" + ;
        "UnixSocket: "  + ::getUnixSocket()  + ";" + ;
        "ClientFlag: "  + AllTrim( Str( ::getClientFlag() ) ) + ";" + ;
        "RdlName: "     + ::getRdlName() )
		
    muestra( a, "Clase " + ::className() )

return
```



#### getDbName()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase
CLASS TMyHDO INHERIT THDO

    METHOD info()

END CLASS

PROCEDURE info() CLASS TMyHDO

    local a := ::rdlInfo()

    aadd( a, ;
        "Host: "        + ::getHost()        + ";" + ;
        "DbName: "      + ::getDbName()      + ";" + ;
        "User: "        + ::getUser()        + ";" + ;
        "Password: "    + ::getPassword()    + ";" + ;
        "Port: "    	+ AllTrim( Str( ::getPort() ) ) + ";" + ;
        "UnixSocket: "  + ::getUnixSocket()  + ";" + ;
        "ClientFlag: "  + AllTrim( Str( ::getClientFlag() ) ) + ";" + ;
        "RdlName: "     + ::getRdlName() )
		
    muestra( a, "Clase " + ::className() )

return
```



#### getHost()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase
CLASS TMyHDO INHERIT THDO

    METHOD info()

END CLASS

PROCEDURE info() CLASS TMyHDO

    local a := ::rdlInfo()

    aadd( a, ;
        "Host: "        + ::getHost()        + ";" + ;
        "DbName: "      + ::getDbName()      + ";" + ;
        "User: "        + ::getUser()        + ";" + ;
        "Password: "    + ::getPassword()    + ";" + ;
        "Port: "    	+ AllTrim( Str( ::getPort() ) ) + ";" + ;
        "UnixSocket: "  + ::getUnixSocket()  + ";" + ;
        "ClientFlag: "  + AllTrim( Str( ::getClientFlag() ) ) + ";" + ;
        "RdlName: "     + ::getRdlName() )
		
    muestra( a, "Clase " + ::className() )

return
```



#### getUser()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase
CLASS TMyHDO INHERIT THDO

    METHOD info()

END CLASS

PROCEDURE info() CLASS TMyHDO

    local a := ::rdlInfo()

    aadd( a, ;
        "Host: "        + ::getHost()        + ";" + ;
        "DbName: "      + ::getDbName()      + ";" + ;
        "User: "        + ::getUser()        + ";" + ;
        "Password: "    + ::getPassword()    + ";" + ;
        "Port: "    	+ AllTrim( Str( ::getPort() ) ) + ";" + ;
        "UnixSocket: "  + ::getUnixSocket()  + ";" + ;
        "ClientFlag: "  + AllTrim( Str( ::getClientFlag() ) ) + ";" + ;
        "RdlName: "     + ::getRdlName() )
		
    muestra( a, "Clase " + ::className() )

return
```



#### getPassword()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase
CLASS TMyHDO INHERIT THDO

    METHOD info()

END CLASS

PROCEDURE info() CLASS TMyHDO

    local a := ::rdlInfo()

    aadd( a, ;
        "Host: "        + ::getHost()        + ";" + ;
        "DbName: "      + ::getDbName()      + ";" + ;
        "User: "        + ::getUser()        + ";" + ;
        "Password: "    + ::getPassword()    + ";" + ;
        "Port: "    	+ AllTrim( Str( ::getPort() ) ) + ";" + ;
        "UnixSocket: "  + ::getUnixSocket()  + ";" + ;
        "ClientFlag: "  + AllTrim( Str( ::getClientFlag() ) ) + ";" + ;
        "RdlName: "     + ::getRdlName() )
		
    muestra( a, "Clase " + ::className() )

return
```



#### getPort()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase
CLASS TMyHDO INHERIT THDO

    METHOD info()

END CLASS

PROCEDURE info() CLASS TMyHDO

    local a := ::rdlInfo()

    aadd( a, ;
        "Host: "        + ::getHost()        + ";" + ;
        "DbName: "      + ::getDbName()      + ";" + ;
        "User: "        + ::getUser()        + ";" + ;
        "Password: "    + ::getPassword()    + ";" + ;
        "Port: "    	+ AllTrim( Str( ::getPort() ) ) + ";" + ;
        "UnixSocket: "  + ::getUnixSocket()  + ";" + ;
        "ClientFlag: "  + AllTrim( Str( ::getClientFlag() ) ) + ";" + ;
        "RdlName: "     + ::getRdlName() )
		
    muestra( a, "Clase " + ::className() )

return
```



#### getUnixSocket()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase
CLASS TMyHDO INHERIT THDO

    METHOD info()

END CLASS

PROCEDURE info() CLASS TMyHDO

    local a := ::rdlInfo()

    aadd( a, ;
        "Host: "        + ::getHost()        + ";" + ;
        "DbName: "      + ::getDbName()      + ";" + ;
        "User: "        + ::getUser()        + ";" + ;
        "Password: "    + ::getPassword()    + ";" + ;
        "Port: "    	+ AllTrim( Str( ::getPort() ) ) + ";" + ;
        "UnixSocket: "  + ::getUnixSocket()  + ";" + ;
        "ClientFlag: "  + AllTrim( Str( ::getClientFlag() ) ) + ";" + ;
        "RdlName: "     + ::getRdlName() )
		
    muestra( a, "Clase " + ::className() )

return
```



#### getClientFlag()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase
CLASS TMyHDO INHERIT THDO

    METHOD info()

END CLASS

PROCEDURE info() CLASS TMyHDO

    local a := ::rdlInfo()

    aadd( a, ;
        "Host: "        + ::getHost()        + ";" + ;
        "DbName: "      + ::getDbName()      + ";" + ;
        "User: "        + ::getUser()        + ";" + ;
        "Password: "    + ::getPassword()    + ";" + ;
        "Port: "    	+ AllTrim( Str( ::getPort() ) ) + ";" + ;
        "UnixSocket: "  + ::getUnixSocket()  + ";" + ;
        "ClientFlag: "  + AllTrim( Str( ::getClientFlag() ) ) + ";" + ;
        "RdlName: "     + ::getRdlName() )
		
    muestra( a, "Clase " + ::className() )

return
```



#### loadFromFile()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase
local oDb, oStmt
local uid, foto
cls

? "Prueba con imagenes..."
? "Se crea una tabla con un campo BLOB y se inserta una imagen cargada con"
? "el metodo oDb:loadFromFile( <fic> )"

oDb := THDO():new( _DBMS )

if oDb:connect( _DB, _CONN )
   oDb:execDirect( _CREA_TB_IMG )
		
   oStmt := oDb:prepare( _INS_IMG )

   oStmt:bindParam( 1, @uid )
   oStmt:bindParam( 2, @foto ) 
		
   uid := 1
   foto := oDb:loadFromFile( "img_01.bmp" )
   oStmt:execute()
		
   uid := 2
   foto := oDb:loadFromFile( "img_00.png" )
   oStmt:execute()
	
   oStmt:free()
endif
oDb:free()
msg( "Revisa la tabla", "Fin" )	
```



#### listTables()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase
local oDb, aTables, nlen, i
oDb := THDO():new( _DBMS,  )

if oDb:connect( _DB, _CONN )
   aTables := oDb:listTables()

   // Lo podemos recorrer directamente
   cls

   ? "Tablas de la base de datos"
   ? Replicate( "_", MaxCol() )

   nlen := len( aTables )

   for i := 1 to nlen
       ? i, aTables[ i ]
   end

   muestra( aTables, "Tablas:" )
endif
```



#### xCreateTable()

##### Sintaxis:

##### Argumentos:

##### Devuelve:

##### Descripción:

##### Ejemplo:

```xbase
local oDb, aTables, nlen, i
oDb := THDO():new( _DBMS,  )

if oDb:connect( _DB, _CONN )
   aTables := oDb:listTables()

   // Lo podemos recorrer directamente
   cls

   ? "Tablas de la base de datos"
   ? Replicate( "_", MaxCol() )

   nlen := len( aTables )

   for i := 1 to nlen
       ? i, aTables[ i ]
   end

   muestra( aTables, "Tablas:" )
endif
//-------------------------------------------------
use test
aTables := DBStruct()
oDb:xCreateTable( "TbTemp", aTables )
close test
//-------------------------------------------------

oDb:disconnect()
```





