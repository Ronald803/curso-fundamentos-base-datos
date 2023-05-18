# *Apuntes: Curso de Fundamentos de Base de datos*
_Docente: Israel Vazquez Morales_

*¿Qué ventajas nos trae la nube?*
- La nuve es accesible desde cualquier parte del mundo
- Puede ser utilizada por varias personas al mismo tiempo

*Tipos de bases de datos*
- Bases de datos Relacionales
    - Ejemplos de Bases de datos Relacionales
        - SQL Server
        - PostSQL
        - MySQL
        - MariaDB
        - Oracle
- Bases de datos No Relacionales
    - Ejempolos de datos no relacionales
        - Cassandra
        - neo4j
        - MongoDB

*Clasificacion de bases de datos por servicios*
- Auto administrados
    Es la que se instala en una PC, uno mismo se encarga de su instalacion, mantenimiento, etc.
- Administrados 
    Son servicios que ofrecen las nubes modernas por ejemplo: Google, Amazon, Assure. Sólo se usan, no se necesitan instalarse ni ocuparse del mantenimiento.


*Clase 2, Playground*
        SELECT (2+2);
        -- Escribe aquí las demás sentencias SQL 👇
        SELECT (18/3);
        SELECT ("Esto es una sentencia SELECT");
eso imprime en consola lo siguiente: 4      6       Esto es una sentencia SELECT

Se debe tener en cuenta utilizar SELECT con mayusculas, un espacio despues del SELECT, y despues del parentesis ";"

*Clase 4, ¿Qué son entidades y atributos?*
Entidad:
    - Parecido a un objeto
    - Representa algo en la vida real
    - Las entidades tienen atributos
    - Por convención las entenidades se escriben en plural
Atributos:
    - Son las cosas que la hacen ser una entidad

ejemplo 1:
    Autos (Entidad)
        * Motor (Atributo)
        * Volante (Atributo)
        * Parabrisas (Atributo)
        * Modelo (Atributo)
ejemplo 2:
    Laptops (Entidad)
        * Pantalla (Atributo)
        * Color (Atributo)
        * Año (Atributo)
        * Modelo (Atributo)
        * No de serie (Atributo) (en este ejemplo este atributo sirve como llave ya que es único, sirve como ID, y para graficarlo se le debe subrayar)
        * Disco duro (Atributo) (en el gráfico podría tener más de una línea debido a que una laptop puede tener más de un disco duro)
        * Método de entrada (Atributo)
        * Antiguedad (Atributo) (en el gráfico está con línea punteada debido a que este atributo se puede inferir a partir del año)

Existen dos tipos de atributos llave
    1. Los atributos naturales, es inherente al objeto, como un número de serie, isbn(caso libros)
    2. Los atributos artificiales, es un atributo que se le puede asignar, no viene inherente al objeto 

Existen dos tipos de entidades
    1. Entidades fuertes, no necesitan de ninguna entidad extra para sobrevivir
    2. Entidades débiles, no pueden existir sin una entidad fuerte  
            Pueden ser débiles por dos motivos
                * Por identidad, no se diferencian entre si, más que por la clave de su identidad fuerte (Ejemplo: libros, ejemplares)
                * Por existencia, pueden tener un id artificial, sin embargo no pueden existir sin su identidad fuerte

*Entidades de Platzi Blog*
- 1er Paso. Identificar las identidades 
    * posts
    * usuarios
    * comentarios
    * categorias
- 2do Paso. Entidades
    * Posts: (titulo, fecha_publicacion, contenido, status, etiquetas, id)
    * Usuarios: (login, password, apodo, email, id)

*Relaciones*
- Se definen por convención con verbos
- Graficamente las relaciones son rombos
- Propiedad Cardinalidad de las relaciones, 
    * (ejemplo 1:1, 1 persona tiene 1 dato de contacto) 
    * (ejemplo cardinalidad 0:1, es opcional)
    * (ejemplo cardinalidad 1 a N, uno a muchos)
    * (ejemplo cardinalidad 0 a N, es opcional)
    * (ejemplo cardinalidad N a N, muchos a muchos, como alumno a clase)

*Diagrama*
- usuarios escribe(relacion) posts [cardinalidad 1:N]
- usuarios escribe(relacion) comentarios [cardinalidad 1:N]
- posts tiene(relacion) comentarios [cardinalidad 1:N]
- posts tiene(relacion) etiquetas [cardinalidad N:N]
- categorias tiene(relacion) posts [cardinalidad 1:N]

*Diagrama Físico*
    -   Tipos de dato
        * Texto [CHAR(n), VARCHAR(n), TEXT]
        * Números [INTEGER, BIGINT, SMALLINT, DECIMAL(n,s), NUMERIC(n,s)]
        * Fecha/hora [DATE, TIME, DATETIME, TIMESTAMP]
        * Lógicos [BOOLEAN ]
    -   Constraints (Restricciones)
        * NOT NULL, se asegura que la columna no tenga valores nulos
        * UNIQUE, se asegura que cada valor en la columna no se repita
        * PRIMARY KEY, es una combinacion de NOT NULL y UNIQUE
        * FOREIGN KEY, identifica de manera única una tupla en otra tabla
        * CHECK, se asegura que el valor en la columna cumpla una condición dad
        * INDEX, se crea por columna para permitir búsquedas más rápidas
*Normalización*
* Primera forma normal (1FN), atributos atómicos sin campos repetidos 
- Todos los atributos son atómicos. Un atributo es atómico si los elementos del dominio son simples e indivisibles
- No debe existir variación en el número de columnas
- Los campos no clave deben identificarse por la clave(dependencia funcional)
- Debe existir una independencia del orden tanto de las filas como de las columnas; es decir, si los datos cambian de orden no deben cambiar sus significados
    Sin normalizar:

| alumno | nivel_curso | nombre_curso | materia_1 | materia 2 |
| ------ | ----------- | ------------ | --------- | --------- |
| Juan   |  Maestría   | Data Engenee | My SQL    |  Python   |
| Pepe   | Licenciatur | Programacion | My SWL    |  Python   |

    Aplicando la primera forma normal

| alumno_id | alumno | nivel_curso | nombre_curso | materia |
| --------- | ------ | ----------- | ------------ | ------- |
|     1     | Juan   |  Maestría   | Data Engenee | My SQL  |
|     1     | Juan   |  Maestría   | Data Engenee | Python  |
|     2     | Pepe   | Licenciatur | Programacion | My SWL  |
|     2     | Pepe   | Licenciatur | Programacion | Python  |

* Segunda forma normal (2FN), cumple 1FN y cada campo de la table debe depender de una clave única.
- Está en 1FN
- Si los atributos que no forman parte de ninguna clave dependen de forma completa de la clave principal. Es decir, que no existen dependencias parciales.
- Todos los atributos que no son clave principal deben depender únicamente de la clave principal.
                    alumnos                      

| alumno_id | alumno | nivel_curso | nombre_curso |
| --------- | ------ | ----------- | ------------ |
|     1     | Juan   |  Maestría   | Data Engenee |
|     2     | Pepe   | Licenciatur | Programacion |

              materias            

| materia_id | alumno_id | materia |
| ---------- | --------- | ------- |
|     1      |     1     | MySQL   |
|     2      |     1     | Python  |
|     3      |     2     | MySQL   |
|     4      |     2     | Python  |

    * Tercera forma normal (3FN), cumple 1FN y 2FN y los campos que NO son clave NO deben tener dependencias

             alumnos           
| alumno_id | alumno | curso_id |
| --------- | ------ | -------- |
|     1     | Juan   |     1    |
|     2     | Pepe   |     2    |

               cursos                  
| curso_id | nivel_curso | nombre_curso |
| -------- | ----------- | ------------ |
|     1    |  Maestría   | Data Engenee |
|     2    | Licenciatur | Programacion |

              materias            

| materia_id | alumno_id | materia |
| ---------- | --------- | ------- |
|     1      |     1     | MySQL   |
|     2      |     1     | Python  |
|     3      |     2     | MySQL   |
|     4      |     2     | Python  |

* Cuarta forma normal (4FN), cumple 1FN, 2FN y 3FN los campos multivaluados se identifican por una clave única, Algunos autores precisan una 5FN que hace referencia a que después de realizar esta normalizaciòn a través de uniones (JOIN) permita regresar a la data original de la cual partió

                alumnos           

| alumno_id | alumno | curso_id |
| --------- | ------ | -------- |
|     1     | Juan   |     1    |
|     2     | Pepe   |     2    |

               cursos                  

| curso_id | nivel_curso | nombre_curso |
| -------- | ----------- | ------------ |
|     1    |  Maestría   | Data Engenee |
|     2    | Licenciatur | Programacion |

|        materias      |
| -------------------- |
| materia_id | materia |
|     1      | MySQL   |
|     2      | Python  |

       materia_por_alumno        

| mpa_id | materia_id | alumno_id |
| ------ | ---------- | --------- |
|   1    |     1      |     1     |
|   2    |     2      |     1     |
|   3    |     1      |     2     |
|   4    |     2      |     2     |

*Diagrama Físico*
|        usuarios          |
| ------------------------ |
| id: INTEGER (PK)         |
| login: VARCHAR(30) NN    |
| password: VARCHAR(32) NN |
| nickname: VARCHAR(40) NN |
| email: VARCHAR(40)UNIQUE |

|                    posts                      |
| --------------------------------------------- |
| id: INTEGER (PK)                              |
| titulo: VARCHAR(30) NN                        |
| fecha_publicacion: TIMESTAP                   |
| contenido: TEXT                               |
| status: CHAR(8)CHECK(IN)("activo","inactivo") |

|       comentarios        |
| ------------------------ |
| id: INTEGER (PK)         |
| comentario: TEXT         |

|         categorias       |
| ------------------------ |
| id: INTEGER (PK)         |
| categoria: VARCHAR(30)   |

|           etiquetas          |
| ---------------------------- |
| id: INTEGER (PK)             |
| nombre_etiqueta: VARCHAR(30) |

Una relación especial que se tiene en este ejemplo es la que existe entre "posts" y "etiquetas" es de N a N (muchos a muchos), ya que un post puede tener varias etiquetas, y una etiqueta puede estar en muchos diferentes posts.
La forma de relacionar en una tabla es en "post_etiquetas" en donde el id de cada elemento será la combinación de ambos ids 
|       post_etiquetas         |
| ---------------------------- |
| post_id: INTEGER (PK,FK)     |
| etiqueta_id: INTEGER (PK,FK) |

*Instalación local de un RDBMS (Windows)*
Hay dos maneras de acceder a manejadores de bases de datos:
- Instalar en máquina local un administrador de bases relacional
- Tener ambientes de desarrollo especiales o servidores cloud

*RDBMS*
Relational Database Management System

*Clientes gráficos*
MySQL Workbench, es una forma muy gráfica de ver como es nuestra base de datos internamente, como tablas

Hoy en día muchas empresas ya no tienen instalados en sus servidores los RDBMS sino que los contratan a otras personas. Estos servicios administrados cloud te permiten concentrarte en la base de datos y no en su administración y actualización.

*SQL* significa Structured Query Language y tiene una estructura clara y fija. Su objetivo es hacer un solo lenguaje para consultar cualquier manejador de bases de datos volviéndose un gran estándar.
Ahora existe el NOSWL o Not Only Structured Query Language que significa que no sólo se utiliza SWL en las bases de datos no relacionales. (ejemplo cassandra, big query)

*DDL* Data Definition Language
Comandos:
- Create (crear)
- Alter (alterar o modificar: una tabla, agregar fila o columna, cambiar tipo de dato)
- Drop (borrar: una columna, fila, tabla, base de datos)
Objetos que se van a manipular:
* Database o bases de datos
* Table o tablas, son la traduccion a SQL de las entidades
* View o vistas, se ofrece la proyección de los datos de la base de datos de forma entendible

Ejemplo sentencias:
CREATE DATABASE test_db;     donde "test_db" es el nombre que le ponemos a la base de datos
USE DATABASE test_db;   este comando se utiliza para apuntar, con este comando la consola o el programa sabrá a que base datos(que en este caso es "test_db") deberá realizar las consultas.
CREATE TABLE people (
    person_id int,
    last_name varchar (255),
    first_name varchar (255),
    address varchar (255),
    city varchar (255)
);
Traducido a código: 
```sql
CREATE TABLE `platzi_blog_dos`.`people` (
  `person_id` INT NOT NULL AUTO_INCREMENT,
  `last_name` VARCHAR(255) NULL,
  `first_name` VARCHAR(255) NULL,
  `address` VARCHAR(255) NULL,
  `city` VARCHAR(255) NULL,
  PRIMARY KEY (`person_id`));
```
*PLAYGROUND*
Debes crear una tabla de datos que permita almacenar información sobre personas, llamada people. La tabla tendrá cinco campos: person_id, last_name, first_name, address, y city.

- La columna person_id debe ser de tipo entero y debe la llave primaria de la tabla y debe ser autoincremental y recuerda no permitir valores NULOS.
- La columna last_name debe ser de tipo texto y debe tener un tamaño máximo de 255 caracteres y permita valores NULOS.
- La columna first_name debe ser de tipo texto y debe tener un tamaño máximo de 255 caracteres y permita valores NULOS.
- La columna address debe ser de tipo texto y debe tener un tamaño máximo de 255 caracteres y permita valores NULOS.
- La columna city debe ser de tipo texto y debe tener un tamaño máximo de 255 caracteres y permita valores NULOS.
Cualquier tabla puedes crearla de la siguiente manera:
```sql
CREATE TABLE COMPANY(
   ID INT PRIMARY KEY AUTOINCREMENT NOT NULL,
   NAME           TEXT    NOT NULL,
   AGE            INT     NOT NULL,
   ADDRESS        CHAR(50),
   SALARY         REAL
);
```
RESOLUCIÓN:
```sql
CREATE TABLE people (
  person_id INTEGER PRIMARY KEY AUTOINCREMENT NOT NULL,
  last_name VARCHAR(255),
  first_name VARCHAR(255),
  address VARCHAR(255),
  city VARCHAR(255)
)
```
Para agregar la vista de clientes, puedes usar el siguiente código desde la pestaña query 1:
```sql
INSERT INTO `platziblog`.`people` (`person_id`, `last_name`, `first_name`, `address`, `city`) 
VALUES ('1', 'Vásquez', 'Israel', 'Calle Famosa Num 1', 'México'),
	       ('2', 'Hernández', 'Mónica', 'Reforma 222', 'México'),
	       ('3', 'Alanis', 'Edgar', 'Central 1', 'Monterrey');
```
*CREATE VIEW*
Lo que hacen es tomar datos de la base de datos ponerlas en una forma presentable y convertirlas en algo que podamos consultar de manera recurrente.
El comando "view" tiene dos partes principales 
```sql
CREATE VIEW v_brasil_customers AS
    SELECT customer_name, contact_name
    FROM customers
    WHERE country = "Brasil";
```
*ALTER TABLE*
```sql
ALTER TABLE people
ADD date_of_birth date;     // añade una columna llamada date_of_birth de tipo date a la tabla people

ALTER TABLE people
ALTER COLUMN date_of_birth year;    // cambia el tipo de dato de la columna date_of_birth de la tabla people, al tipo de dato year

ALTER TABLE people
DROP COLUMN date_of_birth;    // elimina la columna date_of_birth de la tabla people
```
*DDL DROP*
DROP TABLE people       // comando para eliminar la tabla "people"
DROP DATABASE test_db   // comando para eliminar la base de datos "test_db"

                        SQL Commands                          
|     DDL      |     DML       |     DCL    |       TCL        |
| ------------ | ------------- | ---------- | ---------------- |
|  CREATE      |  SELECT       |   GRANT    | COMMIT           |
|  ALTER       |  INSERT       |   REVOKE   | ROLLBACK         |
|  DROP        |  UPDATE       |  _         | SAVEPOINT        |
|  TRUNCATE    |  DELETE       |  _         | SET TRANSACTION  |
|  COMMENT     |  MERGE        |  _         |    -             |
|  RENAME      |  CALL         |  _         |    -             |
|        _     | EXPLAIN PLAN  |  _         |    -             |
|        _     | LOCK TABLE    |  -         |    -             |


1. Crear una vista en SQL basado en la tabla de people con los campos person_id, last_name, first_name:

Crea una vista llamada v_madrid_customers que muestre únicamente el person_id, last_name, y first_name de todas las personas que vivan en la ciudad de "Madrid".

CREATE VIEW v_madrid_customers AS
  SELECT person_id, last_name, first_name
  FROM people
  WHERE city = "Madrid"

2. Este comando creará una vista llamada vista_personas que selecciona solamente el person_id tabla personas.

Una vez que hayas creado la vista, puedes utilizar el siguiente comando para seleccionar los datos de la vista:
```sql
SELECT * FROM vista_personas;
```
3. El reto es agregar un nuevo campo llamado date_of_birth con el tipo de campo DATE a la tabla people.
```sql
ALTER TABLE table_name
ADD COLUMN column_definition;
```
4. El reto es eliminar el campo address de la tabla people.
```sql
ALTER TABLE table_name
DROP COLUMN ;
```
Resolucion:
```sql
CREATE VIEW v_madrid_customers AS
  SELECT person_id, last_name, first_name
  FROM people
  WHERE city = "Madrid";

SELECT * FROM v_madrid_customers;

ALTER TABLE people
ADD COLUMN date_of_birth DATE;

ALTER TABLE people
DROP COLUMN address;
```
*DML* trata del contenido de la base de datos. Son las siglas de Data Manipulation Language y sus comandos son:
* *Insert*: Inserta o agrega nuevos registrados a la tabla.
```sql
INSERT INTO people (last_name, first_name, address, city)
VALUES ('Hernandez','Laura','Calle 21','Monterrey')
```
* *Update*: Actualiza o modifica los datos que ya existen.
UPDATE platzi_blog.people   // platzi_blog es la base de datos, people es la tabla
```sql
SET last_name = 'Chavez', city = 'Merida'
WHERE person_id = 1;

UPDATE people               // el cliente gráfico frenará esto ya que es un cambio
SET first_name = 'Juan'     // masivo y peligroso, sin embargo se puede cambiar
WHERE city = 'Mérida';      // esa configuración

UPDATE people
SET first_name = 'Juan'
```
* *Delete*: Esta sentencia es riesgosa porque puede borrar el contenido de una tabla.
```sql
DELETE FROM people
WHERE person_id = 1;

DELETE FROM people
```
* *Select*: Trae información de la base de datos, con select nos permite elegir qué podemos ver, y from de donde
```sql
SELECT first_name, last_name
FROM people;
```
El CRUD (acrónimo de "Create, Read, Update, Delete) es un conjunto de operaciones básicas qeu se realizan en cualquier sistema de gestión de bases de datos
1.- Tu reto será escribir una consulta SELECT que devuelva todos los datos de la tabla students. Con esta consulta, podrás ver cómo se utiliza la sintaxis SELECT para recuperar información de una base de datos utilizando SQL.

💡 Recuerda que puedes usar el comando SELECT * para seleccionar todas las columnas de una tabla.

2.- Tu reto será escribir una consulta INSERT que inserte un nuevo registro en la tabla students, el registro a insertar debe incluir los siguientes valores.

nombre: "Alexis"
apellido: "Araujo"
edad: 33
correo_electronico: "alexis@gmail.com"
telefono: 777-1234
Con esta consulta, podrás ver cómo se utiliza la sintaxis INSERT para insertar un nuevo registro en una tabla.

💡 Recuerda que puedes usar el comando INSERT INTO para insertar un nuevo registro en una tabla. Para ejecutar una consulta INSERT lo puedes hacer de la siguiente manera: sql INSERT INTO table (column1,column2 ,..) VALUES( value1, value2 ,...);

3.- Tu reto será escribir una consulta DELETE que elimine el registro con el id "1" en la tabla students.

Con esta consulta, podrás ver cómo se utiliza la sintaxis DELETE para eliminar un registro en una tabla.

💡 Recuerda que puedes usar el comando DELETE FROM para eliminar un registro en una tabla. Para ejecutar una consulta DELETE lo puedes hacer de la siguiente manera: sql DELETE FROM table WHERE condition;

4.- Tu reto será escribir una consulta UPDATE que actualice el registro con el id "2" en la tabla students, el registro a actualizar debe incluir los siguientes valores.

edad: 55
Con esta consulta, podrás ver cómo se utiliza la sintaxis UPDATE para actualizar un registro en una tabla.

💡 Recuerda que puedes usar el comando UPDATE para actualizar un registro en una tabla. Para ejecutar una consulta UPDATE lo puedes hacer de la siguiente manera: sql UPDATE table SET column1 = value1, column2 = value2, ... WHERE condition;
```sql
CREATE TABLE people (
	person_id INT,
	last_name VARCHAR(255),
	first_name VARCHAR(255),
	address VARCHAR(255),
	city VARCHAR(255)
);

INSERT INTO people (last_name,first_name,address, city)
VALUES('Hernandez','Laura','Calle 21','Monterrey');

SELECT last_name,first_name FROM people
```
Las Foreing Key options son las siguientes:

On update: Significa qué pasará con las relaciones cuando una de estas sea modificada en sus campos relacionados, Por ejemplo, pueden utilizarse los valores:
cascade: Si el id de un usuario pasa de 11 a 12, entonces la relacion se actualizará y el post buscará el id nuevo en lugar de quedarse sin usuario.
_ restrict: _Si el id de un usuario pasa de 11 a 12, no lo permitirá hasta que no sean actualizados antes todos los post relacionados.
set null Si el id de un usuario pasa de 11 a 12, entonces los post solo no estará relacionados con nada.
no action: Si el id de un usuario pasa de 11 a 12, no se hará nada. Solo se romperá la relación.
On delete
_ cascade: Si un usuario es eliminado entonces se borrarán todos los post relacionados.
restrict: No se podrá eliminar un usuario hasta que sean eliminados todos su post relacionados.
_ set null: Si un usuario es eliminado, entonces los post solo no estará relacionados con nada.
no action: Si un usuario es eliminado, no se hará nada. Solo se romperá la relación.

Las consultas en una base de datos juegan un papel muy fundamental, puesto que facilitan de manera considerable los procesos en cualquier empresa.
*ETL* corresponde al acrónimo: Extract(extraer) Transform(transformar) Load(Cargar)

Estructura básica de un Query
```sql
SELECT city, count(*) AS total
FROM people
WHERE active = true  //filtro para que sólo muestre los que cumplen la condicion
GROUP BY city       //agrupar por ciudad
ORDER BY total DESC
HAVING total >=";
```

##### SELECT
Se encarga de proyectar o mostrar datos
* El nombre de las columnas o campos que estamos consultado puede ser cambiado utilizando AS después del nombre del campo y poniendo el nuevo que queremos tener:
```sql
SELECT titulo AS encabezado
FROM posts;
```
* Existe una función de SELECT para poder contar la cantidad de registros. Esa información (un número) será el resultado del query:
```sql
SELECT COUNT (*)
FROM posts;
```
##### FROM
Indica de dónde se deben traer los datos y puede ayudar a hacer sentencias y filtros complejos cuando se quieren unir tablas. La sentencia compañera que nos ayuda con este proceso es JOIN
Los diagramas de Venn son círculos que se tocan en algún punto para ver dónde está la intersección de conjuntos. Ayudan mucho para poder formular la sentencia JOIN de la manera adecuada dependiendo del query que se quiere hacer.

________________________________________________
Playground: FROM y LEFT JOIN en SQL
Información de las tablas:
Las y los profes se encuentran en la tabla teachers.
Los cursos se encuentran en la tabla courses.
Cada curso y profe tiene su llave primaria en la columna id.
Cada profe puede tener la llave foránea de su curso asociado en la columna course_id.
Cada curso puede tener la llave foránea de su profe asociado en la columna teacher_id.
Propiedades a imprimir en la consulta:
id (con el id del curso)
name (con el nombre del curso)
teacher_id (con el id del profe)
teacher_name (con el nombre del profe).
💡 En clases anteriores aprendiste a usar la instrucción AS para renombrar columnas en tus queries. Para renombrar columnas en consultas entre varias tablas puedes usar nombre_de_tabla.nombre_de_propidad (e.j. SELECT courses.id AS id FROM ...).
Validaciones para el query:
Selecciona únicamente los cursos que tengan profe asociado en la columna teacher_id.
No tengas en cuenta si el profesor tiene curso asociado, únicamente si el curso tiene profesor asociado.
```sql
SELECT courses.id, courses.name, courses.teacher_id, teachers.name AS teacher_name
FROM courses
LEFT JOIN teachers ON courses.id = teachers.course_id
WHERE courses.teacher_id IS NOT NULL;
```
##### WHERE
Es la sentencia que nos ayuda a filtrar tuplas o  registros dependiendo de las características que elegimos.
- La propiedad LIKE nos ayuda a traer registros de los cuales conocemos sólo una parte de la información
- La propiedad BETWEEN nos sirve para arrojar registros que estén en el medio de dos. Por ejemplo los registros con id entre 20 y 30
```sql
SELECT *        -- seleccionar todo 
FROM posts      -- de la tabla posts 
WHERE id > 50;  -- que tenga un id mayor a 50

--otro ejemplo
SELECT *                -- seleccionar todo
FROM posts              -- de la tabla posts
WHERE estatus='activo'  -- que tenga el estatus 'activo'

--otro ejemplo
SELECT *                    -- seleccionar todo
FROM posts                  -- de la tabla posts                  
WHERE estatus!='inactivo'   -- que estatus sea diferente a 'inactivo'

--ejemplo con LIKE (es útil para hallar coincidencias cuando se conoce una fracción de la información que necesitamos)
SELECT *                        -- seleccionar todo
FROM posts                      -- de la tabla posts
WHERE titulo LIKE '%escandalo%' -- que su titulo tenga la palabra "escandalo"
-- '%escandalo': útil para buscar lo que termine con la palabra escandalo
-- 'escandalo%': útil para buscar lo que inicie con la palabra escandalo

--otro ejemplo con SELECT, pero para fechas 
SELECT *                            -- seleccionar todo
FROM posts                          -- de la tabla posts
WHERE fecha_publicacion>'2025-01-01'-- que su fecha de publicacion sea despues del primero de enero de 2025

-- ejemplo con  BETWEEN
SELECT *                            
FROM posts
WHERE fecha_publicacion BETWEEN '2023-01-01' AND '2025-12-31'

-- ejemplo con BETWEEN y YEAR, seleccionar todo de la tabla de posts, que el año de la publicación esté entre 2023 y 2024
SELECT *
FROM posts
WHERE YEAR(fecha_publicacion) BETWEEN '2023' AND '2024';
```
El valor nulo en una tabal generalmente es su valor por defecto cuando nadie le asignó algo diferente. La sintaxis para hacer búsquedas de datos nulos es IS NULL. La sintaxis para buscar datos que no son nulos es IS NOT NULL
```sql
SELECT *                    --seleccionar todo
FROM posts                  -- de la tabla posts
WHERE usuario_id IS NULL;   -- que tenga usuario nulo, o que no tenga usuario

-- otro ejemplo
SELECT *                        -- seleccionar todo
FROM posts                      -- de la tabla posts
WHERE usuario_id IS NOT NULL;   -- que tenga usuario no nulo, osea que si tenga usuario

-- otro ejemplo, AND  es útil para añadir filtros
SELECT *                        -- seleccionar todo
FROM posts                      -- de la tabla posts
WHERE usuario_id IS NOT NULL    -- que tenga usuario no nulo
    AND estatus='activo'        -- y que su estatus sea 'activo'
    AND id<50                   -- y que tengan id menor a 50
```
##### GROUP BY
Indica a la base de datos qué criterios debe tener en cuenta para agrupar.
```sql
SELECT estatus, COUNT(*) post_quantity  -- esta sentencia equivale a contar
FROM posts                              -- los tipos de estatus que tienen
GROUP BY estatus                        -- los posts, en este caso sería contar
-- cuantos activos e inactivos. Devuelve una tabla la primera columna es estatus
-- la segunda columna es post_quantity.

SELECT YEAR(fecha_publicacion) AS post_year, COUNT(*) AS post_quantity
FROM posts          --esta sentencia nos permite desplegar una tabla de dos
GROUP BY post_year; --columnas, una de post_year (año de publicación) y otra de 
--post_quantity (cuantas publicaciones se hicieron)
```

##### ORDER BY y HAVING
La sentencia ORDER BY tiene que ver con el ordenamiento de los datos dependiendo de los criterios que quieras usar.
* ASC sirve para ordenar de forma ascendente.
* DESC sirve para ordenar de forma descendente.
* LIMIT se usa para limitar la cantidad de resultados que arroja el query.
HAVING tiene una similitud muy grande con WHERE, sin embargo el uso de ellos depende del orden. Cuando se quiere seleccionar tuplas agrupadas únicamente se puede hacer con HAVING
```sql
SELECT *                    -- seleccionar todo
FROM posts                  -- de la tabla posts
ORDER BY fecha_publicacion; -- ordenado ascendentemente por fecha
-- también se puede utilizar ASC o DESC para indicar si será ascendente o descendente

SELECT *                        -- seleccionar todo
FROM posts                      -- de la tabla posts
ORDER BY fecha_publicacion DESC;-- ordenar descendentemente por fecha 

SELECT *                -- seleccionar todo
FROM posts              -- de la tabla posts
ORDER BY titulo DESC;   -- ordenar descendentemente por titulo, el criterio 
-- de orden en este caso será el alfabeto

SELECT *                        -- seleccionar todo
FROM posts                      -- de la tabla posts
ORDER BY fecha_publicacion ASC  -- ordenar ascendentemente por fecha de publicaion
LIMIT 5;                        -- mostrar solamente 5

SELECT MONTHNAME(fecha_publicacion) AS post_month, status, COUNT(*) AS post_quantity               -- seleccionamos el mes de la publicaion y estatus
FROM posts                  -- los contamos como post_quantity
GROUP BY estatus, post_month-- los agrupamos por estatus y post_month
HAVING post_quantity > 1    -- solo tomamos en cuenta los que sean mayores a 1
ORDER BY post_month         -- los ordenamos por mes de manera ascendente
```
_____________________________________
Los Nested queries significan que dentro de un query podemos hacer otro query. 
Esto sirve para hacer join de tablas, estando una en memoria. También teniendo un query como condicional del otro.
Este proceso puede ser tan profundo como queramos, teniendo infinitos queries anidados.
Se le conoce como un producto cartesiano ya que se multiplican todos los registros de una tabla con todos los del nuevo query. Esto provoca que el query sea difícil de procesar por lo pesado que puede resultar
```sql
SELECT new_table_projection.date,```sql
COUNT(*) AS posts_count
FROM (
	SELECT DATE(MIN(fecha_publicacion)) AS DATE, YEAR(fecha_publicacion) AS post_year
    FROM posts
    GROUP BY post_year
) AS new_table_projection
GROUP BY new_table_projection.date
ORDER BY new_table_projection.date;
```
##### ¿Cómo convertir una pregunta en un query SQL?
* SELECT: lo que quieres mostrar
* FROM: de dónde voy a tomar los datos
* WHERE: los filtros de los datos que quieres mostrar
* GROUP BY: los rubros por los que me interesa agrupar la información
* ORDER BY: el orden en que quiero presentar mi información
* HAVING: los filtros que quiero que mis datos agrupados tengan

______________________________________________
- Reto 1: crear la tabla
Crea una tabla comentarios con las columnas id, cuerpo_comentario, usuario_id y post_id.
```sql
CREATE TABLE comentarios (
    id INT,
    cuerpo_comentario VARCHAR(255),
    usuario_id INT,
    post_id INT
);
```
- Reto 2: agrega registros
Inserta al menos 3 comentarios en la tabla. Puedes escribir tantos comentarios como quieras. Asegúrate de que solo en 2 el usuario_id sea 1.
```sql
INSERT INTO comentarios (id, cuerpo_comentario, usuario_id, post_id)
VALUES 
    (1, '¡Gran artículo!', 1, 2),
    (2, 'Excelente información', 1, 3),
    (3, 'Me gustaría saber más al respecto', 2, 4),
    (4, 'Excelente post', 3, 5),
    (5, 'Excelente trabajo', 4, 6);
```
- Reto 3: imprime registros
Imprime todas las columnas de todos los registros de la tabla comentarios.
```sql
SELECT * FROM comentarios;
```
Reto 4: imprime registros del usuario 1
Selecciona los 2 comentarios del usuario 1. Haz un JOIN para conseguir la información del post relacionado con la propiedad post_id y el usuario rerlacionado con la propiedad usuario_id. Imprime la propiedad comentarios.cuerpo_comentario como comentario, usuarios.login como usuario y posts.titulo como post.
```sql
SELECT c.cuerpo_comentario as comentario, u.login as usuario, posts.titulo as post
FROM comentarios AS c 
  LEFT JOIN usuarios as U ON c.usuario_id = u.id
  LEFT JOIN posts ON c.post_id = posts.id
  WHERE u.id = 1;
```
### Bases de datos No Relacionales
Tipos de bases de datos no relacionales:
- Clave - valor: son ideales para almacenar y extraer datos con una clave única. Manejan los diccionarios de manera excepcional. Ejemplos: DynamoDB(de aws), Cassandra (de facebook)
- Basadas en documentos: son una implementación de clave valor que varia en la forma semiestructurada en que se trata la información. Ideal para almacenar datos JSON y XML. Ejemplos: MongoDB, Firestore
- Basadas en grafos: basadas en teoria de grafos, sirven para entidades qeu se encuentran interconectadas por múltiples relaciones. Ideales para almacenar relaciones comlejas. Ejemplos: neo4j, TITAN
- En memoria: pueden ser de estructura variada, pero su ventaja radica en la velocidad, ya que al vivir en memoria la extracción de datos es casi inmediata. Ejemplos: Memcached, Redis
- Optimizadas para búsquedas: pueden ser de diversas estructuras, su ventaja radica enque se pueden hacer queries y búsquedas complejas de manera sencilla. Ejemplos: BigQuery, Elasticsearch

______________________________________________
Firebase es un servicio de Google donde puedes tercerizar muchos elementos en la nube.
Jerarquía de datos:
1. Base de datos
2. Colección
3. Documento
______________________________________________
##### Creando y borrando documentos en Firestore
Tipos de datos: string, number, boolean, map(da la opción de poner un documento dentro de otro documento, útil para anidar), array, null, timestamp, geopoint(localización geográfica), reference(nos permite referenciar a otro documento)

La particularidad de las top level collections es que existen en el primer nivel de manera intrínseca. Las subcolecciones ya no vivirán al inicio de la base de datos. Si tienes una entidad separada que vas a referenciar desde muchos lugares es recomendado usar un top level collection. Por el otro lado si se necesita hacer algo intrínseco al documento es aconsejable usar subcolecciones.

Dentro de las bases de datos relacionales tenemos diferentes niveles de datos. En primer lugar tenemos las Bases de Datos o Esquemas como repositorios donde vivirán los datos que nos interesa guardar. Dentro del esquema existen las tablas que provienen del concepto de entidades; y a su vez dentro de las tablas tenemos las tuplas o renglones.

Cuando trabajamos con bases de datos basadas en documentos como Firestore, aún existe la figura de la base de datos, sin embargo cambiaremos las tablas en favor de las colecciones y las tuplas en lugar de los documentos.

 Tabla -> Colección
 Tupla -> Documento

Dentro de las Colecciones existen 2 grandes tipos. Las Top level collection o colecciones de nivel superior y las subcollections o subcolecciones. Estas últimas viven únicamente dentro de un documento padre.

Regla 1. Piensa en la vista de tu aplicación
La primera pista que te puedo dar es que pienses en un inicio enla manera en que los datos serán extraidos. En el caso de una aplicación, la mejor forma de pensarlo es en términos de las vistas que vas a mostrar a un momento determinado enla aplicación.
Es decir, al armar la esturcutra en la base de datos que sea un espejo o que al menos contenga todos los datos necesarios para llenar las necesidades que tiene nuestra parte visual en al aplicación.

Regla 2. La colección tiene vida propia
Esta regla se refiere a que la exceptión a la regla 1 es cuando tenemos un caso en que la "entidad" que tiene necesidad de vivir y modificarse constantemente de manera independiente a las otras colecciones.

## BIG DATA
Es un concepto que nace de la necesidad de manejar grandes cantidades de datos. La tendencia comenzó con compañias como YouTube al tener la necesidad de guardar y consultar mucha información de manera rápida. Es un gran movimiento que consiste en el uso de diferentes tipos de bases de datos.

*Data warehouse* trata de guardar cantidades masivas de datos para posteridad. Allí se guarda todo lo que no está viviendo en la aplicación pero es necesario tenerlo. Debe servir para guardar datos por un largo periodo de tiempo y estos datos se deben poder usar para poder encontrar cuestiones interesantes para el negocio.

*ETL* son las siglas de Extract, Transform, Load (extraer, transformar y cargar). Se trata de tomar datos de archivos muertos y convertirlos en algo que se a de utilidad para el negocio.
También ayuda a tomar los datos vivos de la aplicación, transformarlos y guardarlos en un data warehouse periódicamente.

*Business Intelligence* es una parte muy importante de las carreras de datos ya que es el punto final del manejo de estos. Su razón de ser es tener la información lista, clara y que tenga todos los elementos para tomar decisiones en una empresa. Es necesario tener una buena sensibilidad por entender el negocio, sus necesidades y la información que puede llevar a tomar decisiones en el momento adecuado al momento de realizar business intelligence.

*Machine Learning* tiene significados que varian. Es una serie de técnicas que involucran la inteligencia artificial y la detección de patrones.
Machine Learning para datos tiene un gran campo de acción y es un paso más allá del business intelligence.
Nos ayuda a hacer modelos que encuentran patrones fortuitos encontrando correlaciones inesperadas. Tiene dos casos de uso particulares: clasificación y predicción.

*Data Science* es aplicar todas las técnicas de procesamiento de datos. En su manera más pura tiene que ver con gente con un background de estadísticas y ciencias duras.

______________________________________
Para elegir una base de datos el teorema CAP ayuda a tomar en cuenta 3 factores clave:
* Consistencia
* Disponibilidad
* Tolerancia a la partición