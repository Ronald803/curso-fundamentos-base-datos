##### ¿Qué es Postgresql?
Postgres es un motor de base de datos permite estructurar toda la información dentro de un servidor.
* Lenguaje: lo que permite agregar información o realizar querys en una base de datos. Ejemplo: SQL (Structured Query Language)
* Motor: permite estructurar la información dentro d eun servidor. Ejemplo: PostgreSQL, MySQL
* Servidor: un equipo el cual tiene una memoria y una ram para que funcione el motor de la base de datos 
Estandar ACID: 
- Atomicity(atomicidad), separar las funciones desarrolladas en la BD como pequeñas tareas y ejecutarlas como un todo. Si alguna tarea falla se hace un rollback(se deshacen los cambios)
- Consistency(consistencia), todo lo que se desarrolló en base al objeto relacional. Los datos tienen congruencia. 
- Isolation(Aislamiento), varias tareas ejecutandose al mismo tiempo dentro de la BD
- Durability(durabilidad), puedes tener seguridad que la información no se perderá por un fallo catastrófico. PostgreSQL guarda la información en una Bitácora.

¿Porqué PostgreSQL?
* Tipos de datos
* Integridad de datos
* Concurrencia. Rendimiento
* Fiabilidad, recuperación ante desastres
* Seguridad
* Extensibilidad
* Internacionalización, busqueda de texto.

#### Interacción con Postgres desde la consola
- Consola, útil porque la interfaz gráfica muchas veces presenta problemas o tiene algunos bugs.
- Comandos útiles de consola:
    * "\" : con ese comando podemos ver todos los comandos que existen
    * "\l" : es para listar todas las bases de datos que tienes (por defecto aunque no tengamos ninguna base de datos, mostrará 3 bases de datos)
    * "\dt" muestra las tablas que contiene la base de datos de postgres
    * "\c nombre_DB" cambiar a base de datos nombre_DB
    * "\d nombre_tabla" describe la tabla nombre_tabla, muestra las columnas y el tipo de información que tiene
    * "\h" con este comando podemos ver todas las funciones sql que podemos ejecutar
    * "\h nombre_funcion" útil para ver como se ejecura el comando nombre_funcion sql
    * control+c : para cancelar lo que se este viendo en ese momento
    * "SELECT version();" con este comando podemos ver que versión de postgres está instalada
    * "\g" permite volver a ejecutar el último comando que se ejecutó en la consola
    * "\timing" inicializa el contador de tiempo para verificar cuánto se tarda en ejecutar una función
No olvidar que la base de datos de postgresSQL funciona con SQL estandar por lo que es importante que al terminar una instrucción se utilice ";" ya que la consola esperará el punto y coma para dar por finalizada una instrucción  
__________________________________
##### Archivos Configuración
- postgresql.conf
- pg_hba.conf
- pg_ident.conf
A través de la sentencia "SHOW config_file"  se nos muestra donde están los archivos de configuarción.
* Postgresql.conf: configuración general de postgres, múltiples opciones referentes a direcciones de conexión de entrada, memoria, cantidad de hilos de procesamiento, réplica, etc.
* pg_hba.conf: muestra los roles así como los tipos de acceso a la base de datos.
* pg_ident.conf: permite realizar el mapeo de usuarios. Permite definir roles a usuarios del sistema operativo donde se ejecuta postgres.
_________________________________
La consola en PostgreSQL es una herramienta muy potente par crear, administrar y depurar neustra base de datos. Podemos acceder a ella después de instalar PostgreSQL y haber seleccionado la opción de instalar la consola junto a la base de datos.

PostgreSQL está más estrechamente acoplado al entorno UNIX que algunos otros sistemas de bases de datos, utiliza las cuentas de usuario nativas para determinar quién se conecta a ella (de forma predeterminada). El programa que se ejecuta en la consola y que permite ejecutar consultas y comandos se llama psql, psql es la terminal interactiva para trabajar con PostgreSQL, es la interfaz de línea de comando o consola principal, así como PgAdmin es la interfaz gráfica de usuario principal de PostgreSQL.

En consola los dos principales comandos conlos que podemos revisar todos los comandos y consultas son:
- "\?" Con el cual podemos ver la lista de todos los comandos disponibles en consola, comandos que empiezan con backslash ( \ )
- "\h" con este comando veremos la informacion de todas las consultas SQL disponibles en consola. Sirve también para buscar ayuda sobre una consulta específica, para buscar información sobre una consulta específica basta con escribir \h seguido del inicio de la consulta de la que se requiera ayuda, así: \h ALTER
###### Comandos de navegación y consulta de información
- "\c" saltar entre bases de datos
- "\l" listar base de datos disponibles
- "\dt" listar las tablas de la base de datos
- "\d <nombre_tabla>" Describir una tabla
- "\dn" listar los esquemas de la base de datos actual
- "\df" listar las funciones disponibles de la base de datos actual
- "\dv" listar las vistas de la base de datos actual
- "\du" listar los usuarios y sus roles de la base de datos actual 
###### Comandos de inspección y ejecución
- "\g" volver a ejecutar el comando ejecutando justo antes
- "\s" ver el historial de comandos ejecutados
- "\s <nombre_archivo>" si se quiere guardar la lista de comandos ejecutados en un archivo de texto plano
- "\i <nombre_archivo>" ejecutar los comandos desde un arvhico
- "\e" permite abrir un editor de texto plano, escribir comandos y ejecutar en lote. "\e" abre el editor de texto, escribir allí todos los comandos, luego guardar los cambios y cerrar , al cerrar se ejecutarán todos los comandos guardados.
- "\ef" equivalente al comando anterior pero permite editar también funciones en PostgreSQL
###### Comandos para debug y optimizacion
- "\timing" activar / desactivar el contador de tiempo por consulta
###### Comandos para cerrar la consola
- "\q" cerrar la consola
__________________________________________
###### Tipos de datos
- Numéricos(Numeros enteros, Numeros Decimales, Seriales)
- Monetarios(cantidad de moneda)
- Texto(almacenar cadenas y texto, existen tres VARCHAR, CHAR, TEXT)
- Binario(1 Y 0)
- Fecha/Hora(Para almacenar Fechas y/o Horas, DATE TYPE, TIME TYPE, TIMESTAMP, INTERVAL)
- Boolean(Verdadero o Falso)
- Especiales propios de postgres
- Geométricos: Permiten calcular distancias y áreas usando dos valores X y Y.
- Direcciones de Red: Cálculos de máscara de red
- Texto tipo bit: Cálculos en otros sistemas, ejm(hexadecimal, binario)
- XML, JSON: Postgres no permite guardar en estos formatos
- Arreglos: Vectores y Matrices.

###### Jerarquía de Bases de Datos
* Servidor de base de datos: Computador que tiene un motor de base de datos instalado y en ejecución.
* Motor de base de datos: Software que provee un conjunto de servicios encargados de administrar una base de datos
* Base de datos: grupo de datos que pertenecen a un mismo contexto.
* Esquema de base de datos en PostgreSQL: grupo de objetos de base de datos que guarda relación entre si (tablas, funciones, relaciones, secuencias)
* Tablas de base de datos: estructura que organiza los datos en filas y columnas formando una matriz.

*PostgreSQL es un motor de base de datos*

```sql
CREATE TABLE pasajero(
	id serial,
	nombre character varying(100),
	direccion_residencia character varying,
	fecha_nacimiento date,
	CONSTRAINT pasajero_pkey PRIMARY KEY (id)
)
CREATE TABLE tren(
	id serial,
	modelo character varying(30),
	capacidad integer,
	CONSTRAINT tren_pkey PRIMARY KEY (id)
)
CREATE TABLE estacion(
	id serial,
	nombre character varying(30),
	direccion character varying(100),
	CONSTRAINT estacion_pkey PRIMARY KEY (id)
)
CREATE TABLE trayecto(
	id serial,
	id_tren integer,
	id_estacion integer,
	CONSTRAINT trayecto_pkey PRIMARY KEY (id),
	FOREIGN KEY (id_tren) REFERENCES estacion(id),
	FOREIGN KEY (id_estacion) REFERENCES tren(id)
)
CREATE TABLE viaje(
	id serial,
	id_pasajero integer,
	id_trayecto integer,
	inicio date,
	fin date,
	CONSTRAINT viaje_pkey PRIMARY KEY (id),
	FOREIGN KEY (id_pasajero) REFERENCES pasajero (id),
	FOREIGN KEY (id_trayecto) REFERENCES trayecto (id)
)
```
__________________________________
Particiones
- Separación física de datos: se guardan varias partes de una tabla en distintos lugares, incluso en otros discos
- Estructura lógica, el mismo SELECT es útil 
__________________________________
```sql
\h CREATE ROLE; -- Ver las funciones del comando CREATE ROLE (help)

CREATE ROLE usuario_consulta; -- crear un rol llamado usuario_consulta

\dg -- mostrar todos los usuarios junto a sus atributos

-- cambiar el atributo a LOGIN del rol de usuario_consulta
ALTER ROLE usuario_consulta WTIH LOGIN;

-- cambiar el atributo a SUPER USER del rol de usuario_consulta
ALTER ROLE usuario_consulta WITH SUPERUSER;

-- configuración del password '1234' del rol usuario_consulta
ALTER ROLE usuario_consulta WITH PASSWORD '1234';

-- eliminar el usuario o role
DROP ROLE usuario_consulta;

-- La mejor forma de crear un usuario o rol por pgadmin
CREATE ROLE usuario_consulta WITH
	LOGIN
	NOSUPERUSER
	NOCREATEDB
	NOCREATEROLE
	INHERIT
	NOREPLICATION
	CONNECTION LIMIT -1
	PASSWORD '1234';

-- Para otorgar privilegios a nuestro usuario_consulta
GRANT INSERT, SELECT, UPDATE ON TABLE public.estacion TO usuario_consulta;
GRANT INSERT, SELECT, UPDATE ON TABLE public.pasajero TO usuario_consulta;
GRANT INSERT, SELECT, UPDATE ON TABLE public.trayecto TO usuario_consulta;
GRANT INSERT, SELECT, UPDATE ON TABLE public.viaje TO usuario_consulta;
```
_________________________
###### Llaves foráneas 
```sql
ALTER TABLE IF EXISTS public.trayecto
    ADD CONSTRAINT trayecto_estacion_fkey FOREIGN KEY (id_estacion)
    REFERENCES public.estacion (id) MATCH SIMPLE
    ON UPDATE CASCADE
    ON DELETE CASCADE
    NOT VALID;
```
En la pestaña ACTION tenemos las siguientes opciones:
- NO ACTION, no hacer nada
- RESTRICT, postgres no permitirá que la tabla cambie
- CASCADE, si la tabla de origen cambia, la tabla destino cambia tambien
- SET NULL, ante un cambio de la tabla de origen la información de la tabla de destino cambiará a NULL
- SET DEFAULT, ante un cambio en la tabla origen la tabla destino pondrá un valor predeterminado.
_______________________
```sql
-- Union de la tabla pasajero con la tabla viaje, los parametros por los cuales se relacionan (son los mismos) son: viaje.id_pasajero y pasajero.id
SELECT * FROM pasajero
JOIN viaje ON (viaje.id_pasajero = pasajero.id);

-- tabla pasajero diferencia simetrica viaje, solo se desplegaran los datos de la tabla pasajero que no se intersecten con la tabla viaje, los parametros por los cuales se relacionan son los mismos que el anterior ejemplo
SELECT * FROM pasajero
LEFT JOIN viaje ON (viaje.id_pasajero = pasajero.id)
WHERE viaje.id IS NULL;
```
____________________________________________
Funciones especiales:
* ON CONFLICT DO: es una especie de sobre escritura sobre algo que ya esta creado, es como un UPDATE
* RETURNING, muestra en pantalla el último cambio hecho
```sql
INSERT INTO public.estacion(
	 nombre, direccion)
	VALUES ('Pamela Zambrana', 'Said')
	RETURNING *;
```
* LIKE / ILIKE: busqueda por similitudes la diferencia entre ambas es que like busca en minúsculas y ilike busca en mayúsculas/minúsculas, se utiliza los simbolos "%" y "_" 
* IS / IS NOT: comparación para atributos especiales como el NULL
Funciones Especiales Avanzadas
* COALESCE: compara dos valores y retorna el primer elemento que no es nulo
* NULLIF: retorna null si son iguales
* GREATEST: compara un arreglo y retorna el mayor
* LEAST: compara un arreglo de valores y retorna el menor
* BLOQUES ANONIMOS: ingresa condicionales dentro de una consulta de BD
```sql
-- Aumenta una columna llamada case que indica si es niño o mayor
SELECT id, nombre, direccion_residencia, fecha_nacimiento,
CASE
WHEN fecha_nacimiento > '2015-01-01' THEN
'niño'
ELSE
'mayor'
END
FROM public.pasajero;
```
Para no realizar las mismas consultas varias veces, se utilizan las vistas, existen dos tipos:
- Vista Volátil, siempre que se haga la consulta en la vista, la BD hace la ejecución de la consulta en la BD, por lo que siempre se va a tener información reciente
- Vista Materializada Persistente, hace la consulta una sola vez, y la información queda almaenada en memoria, la siguiente vez que se consulte, trae el dato almacenado, eso es bueno y malo a la vez, bueno porque la velocidad con la que se entrega la información es rápida, malo porque la información no es actualizada.
```sql
-- Creamos la vista
CREATE OR REPLACE VIEW public.rango_view
AS
    SELECT *,
        CASE
        WHEN fecha_nacimiento > '2015-01-01' THEN
            'Mayor'
        ELSE
            'Menor'
        END AS tipo
    FROM pasajero ORDER BY tipo;
ALTER TABLE public.rango_view OWNER TO postgres;

-- mostramos la vista
SELECT * FROM public.rango_view;

-- Vistas Materializada, no se cambia a menos que queramos que se cambie
SELECT * FROM viaje WHERE inicio > '22:00:00';

CREATE MATERIALIZED VIEW public.despues_noche_mview
AS
    SELECT * FROM viaje WHERE inicio > '22:00:00';
WITH NO DATA;
ALTER TABLE public.despues_noche_mview OWNER TO postgres;

-- observamos la vista
SELECT * FROM despues_noche_mview;

-- Damos refresh
REFRESH MATERIALIZED VIEW despues_noche_mview;

-- Borramos una tupla de viaje cuando el id = 2, para observar que no se borro
DELETE FROM viaje WHERE id = 2;
```
![]
(https://static.platzi.com/media/user_upload/Captura4-96ab9d65-0f83-48c7-b035-b515011ac551.jpg)

______________________________________
Transacciones 
Las transacciones, tienen la capacidad para empaquetar varios pasos en una sola operación "todo o nada", y si ocurre alguna falla que impida que se complete la transacción, entonces ninguno de los pasos se ejecuta y no se afecta la base de datos en absoluto.
Las transacciones tienen la siguiente estructura postgres:
BEGIN;
<Instrucciones>
COMMIT|ROLLBACK
______________________________________
Formatos del backup
- Custom, un formato propio de Postgres
- Tar, un archivo comprimido que contiene la estructura de la BD
- Plain, SQL plano
- Directory, estructura sin comprimir 