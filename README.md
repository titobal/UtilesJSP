UtilesJSP
=========

Clases utiles para usar con JSP, sin ningún framework

La clase conexón tiene principalmente dos metodos, el metodo s(String query), que ejecuta un String(query) sin retornar valores, ideada para insert, update, delete se puede utilizar getFilasAfectadas() para objener la cantidad de filas afectadas.

El otro metodo que posee es q(String query), que ejecuta un String(query) y retorna un valor de tipo List<Map<String,String>> idealmente para convertir a JSON con la librería GSON (code.google.com/p/google-gson/).

Se está planeando implementar un metodo similar al LastInsertedId de PHP para obtener el último id, en el caso de un insert con un auto_increment. Utiliza base de datos MySql, se deben cambiar el nombre de la base de datos, el usuario y el password.

Ejemplo de uso q(String query, String[] columnas)

dada la tabla Prueba

mysql> desc Prueba;

| Field  | Type         | Null | Key | Default | Extra          |

| Id     | int(11)      |      | PRI | NULL    | auto_increment |

| Nombre | varchar(200) |

con los datos

select * from Prueba;
mysql> Select * From Prueba;

| Id | Nombre   |

|  1 | asdadasd |

|  2 | asdadasd |

|  3 | asdadasd |

El método q(String query) retornará un Map por cada fila, que contendrá la siguiente estructura:

q("SELECT * FROM Prueba", new String[]{"Id", "Nombre"}) //en el array de String se especifican los alias de las columnas

"0"=>"1"

"Id"=>"1"

"1"=>"asdadasd"

"Nombre","asdadasd"

El List<> contendrá todas las filas de los Map, convertido con GSON, el objeto JSON queda de la siguiente forma:

[{"1":"asdadasd","0":"1","Id":"1","Nombre":"asdadasd"},{"1":"asdadasd","0":"2","Id":"2","Nombre":"asdadasd"},{"1":"asdadasd","0":"3","Id":"3","Nombre":"asdadasd"}]

