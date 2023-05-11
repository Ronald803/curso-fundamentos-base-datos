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
    -   usuarios escribe(relacion) posts [cardinalidad 1:N]
    -   usuarios escribe(relacion) comentarios [cardinalidad 1:N]
    -   posts tiene(relacion) comentarios [cardinalidad 1:N]
    -   posts tiene(relacion) etiquetas [cardinalidad N:N]
    -   categorias tiene(relacion) posts [cardinalidad 1:N]

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
|                    alumnos                      |
| ----------------------------------------------- |
| alumno_id | alumno | nivel_curso | nombre_curso |
| --------- | ------ | ----------- | ------------ |
|     1     | Juan   |  Maestría   | Data Engenee |
|     2     | Pepe   | Licenciatur | Programacion |

|              materias            |
| -------------------------------- |
| materia_id | alumno_id | materia |
|     1      |     1     | MySQL   |
|     2      |     1     | Python  |
|     3      |     2     | MySQL   |
|     4      |     2     | Python  |

    * Tercera forma normal (3FN), cumple 1FN y 2FN y los campos que NO son clave NO deben tener dependencias

|             alumnos           |
| ----------------------------- |
| alumno_id | alumno | curso_id |
| --------- | ------ | -------- |
|     1     | Juan   |     1    |
|     2     | Pepe   |     2    |

|               cursos                  |
| ------------------------------------- |
| curso_id | nivel_curso | nombre_curso |
| -------- | ----------- | ------------ |
|     1    |  Maestría   | Data Engenee |
|     2    | Licenciatur | Programacion |

|              materias            |
| -------------------------------- |
| materia_id | alumno_id | materia |
|     1      |     1     | MySQL   |
|     2      |     1     | Python  |
|     3      |     2     | MySQL   |
|     4      |     2     | Python  |

* Cuarta forma normal (4FN), cumple 1FN, 2FN y 3FN los campos multivaluados se identifican por una clave única, Algunos autores precisan una 5FN que hace referencia a que después de realizar esta normalizaciòn a través de uniones (JOIN) permita regresar a la data original de la cual partió
|             alumnos           |
| ----------------------------- |
| alumno_id | alumno | curso_id |
| --------- | ------ | -------- |
|     1     | Juan   |     1    |
|     2     | Pepe   |     2    |

|               cursos                  |
| ------------------------------------- |
| curso_id | nivel_curso | nombre_curso |
| -------- | ----------- | ------------ |
|     1    |  Maestría   | Data Engenee |
|     2    | Licenciatur | Programacion |

|        materias      |
| -------------------- |
| materia_id | materia |
|     1      | MySQL   |
|     2      | Python  |

|       materia_por_alumno        |
| ------------------------------- |
| mpa_id | materia_id | alumno_id |
|   1    |     1      |     1     |
|   2    |     2      |     1     |
|   3    |     1      |     2     |
|   4    |     2      |     2     |

*Diagrama Físico*
| ------------------------ |
|        usuarios          |
| ------------------------ |
| id: INTEGER (PK)         |
| ------------------------ |
| login: VARCHAR(30) NN    |
| password: VARCHAR(32) NN |
| nickname: VARCHAR(40) NN |
| email: VARCHAR(40)UNIQUE |
| ------------------------ |

| --------------------------------------------- |
|                    posts                      |
| --------------------------------------------- |
| id: INTEGER (PK)                              |
| --------------------------------------------- |
| titulo: VARCHAR(30) NN                        |
| fecha_publicacion: TIMESTAP                   |
| contenido: TEXT                               |
| status: CHAR(8)CHECK(IN)("activo","inactivo") |
| --------------------------------------------- |

| ------------------------ |
|       comentarios        |
| ------------------------ |
| id: INTEGER (PK)         |
| ------------------------ |
| comentario: TEXT         |
| ------------------------ |

| ------------------------ |
|         categorias       |
| ------------------------ |
| id: INTEGER (PK)         |
| ------------------------ |
| categoria: VARCHAR(30)   |
| ------------------------ |

| ---------------------------- |
|           etiquetas          |
| ---------------------------- |
| id: INTEGER (PK)             |
| ---------------------------- |
| nombre_etiqueta: VARCHAR(30) |
| ---------------------------- |

Una relación especial que se tiene en este ejemplo es la que existe entre "posts" y "etiquetas" es de N a N (muchos a muchos), ya que un post puede tener varias etiquetas, y una etiqueta puede estar en muchos diferentes posts.
La forma de relacionar en una tabla es en "post_etiquetas" en donde el id de cada elemento será la combinación de ambos ids 
| ---------------------------- |
|       post_etiquetas         |
| ---------------------------- |
| post_id: INTEGER (PK,FK)     |
| etiqueta_id: INTEGER (PK,FK) |
| ---------------------------- |

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
CREATE TABLE `platzi_blog_dos`.`people` (
  `person_id` INT NOT NULL AUTO_INCREMENT,
  `last_name` VARCHAR(255) NULL,
  `first_name` VARCHAR(255) NULL,
  `address` VARCHAR(255) NULL,
  `city` VARCHAR(255) NULL,
  PRIMARY KEY (`person_id`));

*PLAYGROUND*
Debes crear una tabla de datos que permita almacenar información sobre personas, llamada people. La tabla tendrá cinco campos: person_id, last_name, first_name, address, y city.

- La columna person_id debe ser de tipo entero y debe la llave primaria de la tabla y debe ser autoincremental y recuerda no permitir valores NULOS.
- La columna last_name debe ser de tipo texto y debe tener un tamaño máximo de 255 caracteres y permita valores NULOS.
- La columna first_name debe ser de tipo texto y debe tener un tamaño máximo de 255 caracteres y permita valores NULOS.
- La columna address debe ser de tipo texto y debe tener un tamaño máximo de 255 caracteres y permita valores NULOS.
- La columna city debe ser de tipo texto y debe tener un tamaño máximo de 255 caracteres y permita valores NULOS.
Cualquier tabla puedes crearla de la siguiente manera:
CREATE TABLE COMPANY(
   ID INT PRIMARY KEY AUTOINCREMENT NOT NULL,
   NAME           TEXT    NOT NULL,
   AGE            INT     NOT NULL,
   ADDRESS        CHAR(50),
   SALARY         REAL
);
RESOLUCIÓN:
CREATE TABLE people (
  person_id INTEGER PRIMARY KEY AUTOINCREMENT NOT NULL,
  last_name VARCHAR(255),
  first_name VARCHAR(255),
  address VARCHAR(255),
  city VARCHAR(255)
)

Para agregar la vista de clientes, puedes usar el siguiente código desde la pestaña query 1:

INSERT INTO `platziblog`.`people` (`person_id`, `last_name`, `first_name`, `address`, `city`) 
VALUES ('1', 'Vásquez', 'Israel', 'Calle Famosa Num 1', 'México'),
	       ('2', 'Hernández', 'Mónica', 'Reforma 222', 'México'),
	       ('3', 'Alanis', 'Edgar', 'Central 1', 'Monterrey');

*CREATE VIEW*
Lo que hacen es tomar datos de la base de datos ponerlas en una forma presentable y convertirlas en algo que podamos consultar de manera recurrente.
El comando "view" tiene dos partes principales 
CREATE VIEW v_brasil_customers AS
    SELECT customer_name, contact_name
    FROM customers
    WHERE country = "Brasil";

*ALTER TABLE*
ALTER TABLE people
ADD date_of_birth date;     // añade una columna llamada date_of_birth de tipo date a la tabla people

ALTER TABLE people
ALTER COLUMN date_of_birth year;    // cambia el tipo de dato de la columna date_of_birth de la tabla people, al tipo de dato year

ALTER TABLE people
DROP COLUMN date_of_birth;    // elimina la columna date_of_birth de la tabla people

*DDL DROP*
DROP TABLE people       // comando para eliminar la tabla "people"
DROP DATABASE test_db   // comando para eliminar la base de datos "test_db"

| ------------------------------------------------------------ |
|                        SQL Commands                          |
| ------------------------------------------------------------ |
|     DDL      |     DML       |     DCL    |       TCL        |
| ------------ | ------------- | ---------- | ---------------- |
|  CREATE      |  SELECT       |   GRANT    | COMMIT           |
|  ALTER       |  INSERT       |   REVOKE   | ROLLBACK         |
|  DROP        |  UPDATE       |            | SAVEPOINT        |
|  TRUNCATE    |  DELETE       |            | SET TRANSACTION  |
|  COMMENT     |  MERGE        |            |                  |
|  RENAME      |  CALL         |            |                  |
|              | EXPLAIN PLAN  |            |                  |
|              | LOCK TABLE    |            |                  |
| ------------------------------------------------------------ |

1. Crear una vista en SQL basado en la tabla de people con los campos person_id, last_name, first_name:

Crea una vista llamada v_madrid_customers que muestre únicamente el person_id, last_name, y first_name de todas las personas que vivan en la ciudad de "Madrid".

CREATE VIEW v_madrid_customers AS
  SELECT person_id, last_name, first_name
  FROM people
  WHERE city = "Madrid"

2. Este comando creará una vista llamada vista_personas que selecciona solamente el person_id tabla personas.

Una vez que hayas creado la vista, puedes utilizar el siguiente comando para seleccionar los datos de la vista:

SELECT * FROM vista_personas;

3. El reto es agregar un nuevo campo llamado date_of_birth con el tipo de campo DATE a la tabla people.

ALTER TABLE table_name
ADD COLUMN column_definition;

4. El reto es eliminar el campo address de la tabla people.

ALTER TABLE table_name
DROP COLUMN ;

Resolucion:
CREATE VIEW v_madrid_customers AS
  SELECT person_id, last_name, first_name
  FROM people
  WHERE city = "Madrid";

SELECT * FROM v_madrid_customers;

ALTER TABLE people
ADD COLUMN date_of_birth DATE;

ALTER TABLE people
DROP COLUMN address;

*DML* trata del contenido de la base de datos. Son las siglas de Data Manipulation Language y sus comandos son:
* *Insert*: Inserta o agrega nuevos registrados a la tabla.
INSERT INTO people (last_name, first_name, address, city)
VALUES ('Hernandez','Laura','Calle 21','Monterrey')
* *Update*: Actualiza o modifica los datos que ya existen.
UPDATE platzi_blog.people   // platzi_blog es la base de datos, people es la tabla
SET last_name = 'Chavez', city = 'Merida'
WHERE person_id = 1;

UPDATE people               // el cliente gráfico frenará esto ya que es un cambio
SET first_name = 'Juan'     // masivo y peligroso, sin embargo se puede cambiar
WHERE city = 'Mérida';      // esa configuración

UPDATE people
SET first_name = 'Juan'

* *Delete*: Esta sentencia es riesgosa porque puede borrar el contenido de una tabla.
DELETE FROM people
WHERE person_id = 1;

DELETE FROM people

* *Select*: Trae información de la base de datos, con select nos permite elegir qué podemos ver, y from de donde
SELECT first_name, last_name
FROM people;