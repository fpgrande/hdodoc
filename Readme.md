
# HDO Documentación 


## ¿Qué es HDO?

El nombre HDO, es el acrónimo formado por las iniciales de las palabras: Harbour Data Objects ( Objetos de datos de Harbour ).

HDO está formado por un conjunto de bibliotecas para Harbour que podemos enlazar con nuestros programas para conseguir acceder a los datos guardados en una base de datos. Además de gestionar completamente el acceso y el mantenimiento de la misma.

En la actualidad hay varias librerías que hacen eso en el universo Harbour. Entoces, qué hace que un programador se pueda decidir a usar **HDO** y no otras como **Eagle1**? 

Pues bien, hay varios motivos:

* **HDO** es muy ligera. El código está hecho 100% en **Lenguaje C**.

* Super rápida. Accede directamente al *API* de cada gestor de Bases de datos, sin ninguna capa más, incluida la *Máquina Virtual de Harbour*.

* Se puede utilizar como núcleo para crear clases más complejas, ya que a pesar de estar hecha en *C* permite la herencia como cualquier otra clase hecha en *PRG*.

* Es la única clase que soporta 100% sentencias preparadas en el lado del servidor, que hacen que vayan más rápidas, evitan código inyectado y facilitan en el cliente su manejo.

* Para el acceso a cada bases de datos hay que tener disponible su correspondiente *driver*. En **HDO** se llaman **RDL** *(Replaceable Data Link)* enlace de datos reemplazables. En la actualidad están terminados el **RDL** para **MySQL** y el **RDL** para **SQLite**.

  Si se utilizan sentencias compatibles, se podrían crear programas sin cambiar nada de código, salvo el que indica a **HDO** con qué **RDL** tiene que trabaja de las que se tengan enlazadas.

  oDb := THDO():new( DBMS ) // Donde DBMS puede ser "MySQL" o "SQLite" de momento

  Lo demás puede ser compatible. 

* Las clases que componen **HDO** se abstraen completamente del gestor de bases datos que se esté usando. Para poder acceder a una determinada bases de datos sólo tenemos que enlazar los **RDL** necesarios.

* Clases que componen HDO


  **HDO** está compuesto por muy pocas clases por lo que hace más fácil su uso:

  * ***THDO***: Representa la conexión con el servidor. Encapsula todo lo necesario para conectarse con un servidor, crear y mantener una base de datos, gestionar las transacciones y enviar sentencias directas al servidor.
    Tiene métodos que generan objetos de las clases que se explican más abajo.
  * ***TStmt***: Gestiona las sentencias preparadas en el lado del servidor, esta pueden ser de dos tipos básicamente, las que sólo son comandos que se envían al servidor como insert, update o delete y las que devuelven un conjunto de resultados. Para estas últimas TStmt tiene métodos para recorrer el conjunto de resultados muy rápido pero sólo hacia adelante, se suelen usar para listados. Además cuenta con métodos que devuelven dicha información en un array de memoria, en un hashtable o en JSon, registro a registro o todo el conjunto.
  * ***TRowSet***: Se parece al TStmt en el sentido de que envía sentencias al servidor, pero sólo las que devuelven un conjunto de datos. Este tipo de objetos son especiales porque crean un array en **Lenguaje C** completamente navegable en cualquier modo, hacia adelante y hacia detrás. Tiene la posibilidad de usar metodos de mantenimiento de las tablas *(:insert(), :update() y :delete())*. Estos métodos tan sólo se limitan a enviar a la sentencia un array con los valores. Esto es muy importante ya que si se hace un *JOIN* entre más de una tabla el mantenimiento sería imposible ya que el sistema no sabrá que hacer cuando el conjunto de resultados está formado por más de una tabla, ahí está la mágia de esta clase.
  * ***TRDL***: Esta clase solo gestiona las **RDL** disponibles. HDO se apoya en ella para la gestión de registro de las **RDL** por lo que su uso a ni vel de programación es escaso o nulo. 

  Junto a **HDO** se proporcionan dos clases auxiliares que, aunque independientes, van muy bien con **HDO**:

  * ***TMemList***: Gestiona un array de memoria del tipo:

    {
    	{ item01, item02, item03, ...}
    	{ item11, item12, item13, ...}
    	...
    }

  * ***THashList***: Gestiona un array de hashtables:

    {
    	{key1=> item01, key2=> item02, key3=> item03, ...}
    	{ key1=> item11, key2=> item12, key3=> item13, ...}
    	...
    }

    Son compatibles entre ellas por lo que se puede usar una u otra según la preferencia o necesidad del programador.

    Son ideales para recibir el array o el hash con los métodos *:fetchAllArray()* y *:fetchAllHash()* de la clase **TStmt** para hacerla navegable con array y hashtables compatibles con **harbour**.