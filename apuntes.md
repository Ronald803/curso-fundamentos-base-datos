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
