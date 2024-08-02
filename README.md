# STUDENT DATABASE

## Learn SQL by Building a Student Database: Part 2

En este tutorial, se practicó la administración y el análisis de bases de datos de estudiantes usando SQL y PostgreSQL. 
Se aprendió a realizar consultas avanzadas mediante **_`JOIN`_** para combinar datos de múltiples tablas y a utilizar funciones de agrupamiento (**_`GROUP BY`_** ) y ordenamiento (**_`ORDER BY`_**). 
Se utilizó las funciones agregadas para sumarizar datos y la modificación de estructuras de tablas existentes con **_`ALTER TABLE`_**. Esta parte incluye la creación de copias de seguridad y restauración de bases de datos, y el uso de scripts Bash para una gestión más eficiente y segura de tu entorno.

## Comandos Ejecutados

### Paso 1: Iniciar la terminal
En el terminal bash se ejecuta el siguiente comando:
```bash
echo hello SQL
```
La terminal muestra el siguiente mensaje: ` hello SQL `

### Paso 2: Iniciar sesión en terminal de SQL
En el terminal bash se ejecuta el siguiente comando:
```bash 
psql --username=freecodecamp --dbname=postgres
```
Se visualiza esto en la terminal:
``` bash
Border style is 2.
Title is " ".
Pager usage is off.
psql (12.17 (Ubuntu 12.17-1.pgdg22.04+1))
SSL connection (protocol: TLSv1.3, cipher: TLS_AES_256_GCM_SHA384, bits: 256, compression: off)
Type "help" for help.
```

### Paso 3: Reconstruir la base de datos
Se usa el archivo .sql que se creó al final de la Parte 1 para reconstruirlo. Para ello se ejecuta el siguiente comando:
 ```bash
camper: /proyecto$ psql -U postgres < estudiantes.sql
```
### Paso 4: Verificar que la base de datos se reconstruyó correctamente

1. Se utiliza el comando abreviado **_`\l`_** para ver si la base de datos se reconstruyó.
2. Se verifica que la base de datos **_`students`_** se reconstruyó de forma correcta y nos conectamos a ella.
 ```bash
postgres=> \c students
```
3. Se visualiza las tablas y relaciones en la base de datos **_`students`_** para ver si todo está correcto.
 ```bash
students=> \d
```
4. Se requiere observar los detalles de la **_`tabla students`_** para asegurarse de que la estructura sea la correcta.
 ```bash
students=> \d students
```
5. Por último se comprueba que los datos de la tabla **_`tabla students`_**.
 ```bash
students=> SELECT * FROM students;
```

### Paso 5: Crear el script **_`student_info.sh`_**
1. Se usa **_`el comando touch`_** en la terminal bash para crear el archivo **_`student_info.sh`_**, con ello se crea un script para imprimir información sobre los alumnos.
 ```bash
camper: /project$ touch student_info.sh
```
2. Se utiliza el **_`comando chmod +x`_** para darle nuevos permisos ejecutables de script.
 ```bash
camper: /project$ chmod +x student_info.sh
```
3. En el archivo **_`student_info.sh`_** inserta un **_`shebang`_** en la primera línea:  **_`#!/bin/bash`_**
4. Debajo del **_`shebang`_**, se agrega el siguiente comentario **_`Info about my computer science students from students database`_**.
5. Se agrega un título al script **_`student_info.sh`_** con la siguiente línea de código dentro del archivo-
 ```bash
echo -e "\n~~ My Computer Science Students ~~\n"
```
6. Se ejecuta el script para ver si se imprime el título archivo.
 ```bash
camper: /project$ ./student_info.sh
```

### Paso 6: Agregar la variable PSQL
Se agrega la variable **_`PSQL`_** que usa en su script **_`insert_data.sh`_** de la parte 1, para poder realizar consultas a la base de datos **_`students`_** 
 ```bash
PSQL="psql -X --username=freecodecamp --dbname=students --no-align --tuples-only -c"
```

### Paso 7: Imprimir estudiantes con un GPA de 4.0
Se usa **_`echo`_** para imprimir el nombre, apellido y GPA de los estudiantes con un GPA de 4.0:. Utilice la bandera **_`-e`_** para poner una nueva línea al principio de la oración.
 ```bash
echo -e "\nFirst name, last name, and GPA of students with a 4.0 GPA:"
```
### Paso 8: Consultar las columnas de la tabla **_`students`_**
SQL significa _"lenguaje de consulta estructurado"_. Es el lenguaje que ha estado utilizando para administrar sus bases de datos relacionales. Se ve los datos en la tabla de **_`students`_** realizando las siguientes consultas:
1. Consultar todos los datos de la tabla de **_`students`_**.
 ```bash
students=> SELECT * FROM students;
```
2. Se puede devolver columnas específicas poniendo el nombre de la columna en la consulta en lugar de *. Consultar la columna **_`first_name`_** de la tabla de **_`students`_**.
 ```bash
students=> SELECT first_name FROM students;
```
3. Se puede especificar tantas columnas como desee separándolas con comas. Se consulta  las columnas **_`first_name, last_name y gpa`_** de la tabla de **_`students`_**.
 ```bash
students=> SELECT first_name, last_name, gpa FROM students;
```
4. Se puede devolver solo las filas que desee agregando **_`WHERE <condición>`_** a su consulta. Una condición puede constar de una columna, un operador y un valor. Se utiliza uno de estos para ver las mismas columnas que antes, pero solo filas **_`WHERE gpa < 2,5`_**.
 ```bash
students=> SELECT first_name, last_name, gpa FROM students WHERE gpa < 2.5;
```

### Paso 9: Realizar consultas desde el script **_`student_info.sh`_**
En el archivo **_`student_info.sh`_** se agrega el comando **_`echo "$($PSQL "<query_here>")"`_** que realice la siguiente consulta: Imprimir el nombre, apellidos y gpa de los estudiantes que tengan un gpa=4.0.
 ```bash
echo "$($PSQL "SELECT first_name, last_name, gpa FROM students WHERE gpa = 4.0")"
```
En el terminal de bash se ejecuta el script **_`student_info.sh`_**  para ver los resultados de la consulta.
 ```bash
camper: /project$ ./student_info.sh
```
![Imagen12](https://github.com/user-attachments/assets/3b0170d6-5774-4b63-bd3b-6562bd9dfd57)

### Paso 10: Agregar **_`echo`_** al script **_`student_info.sh`_**
Se realiza una declaración que imprima todos los nombres de los cursos cuya primera letra esté antes de la 'D' en el alfabeto:
 ```bash
echo -e "\nAll course names whose first letter is before 'D' in the alphabet:"
```

### Paso 11:  Consultar las columnas de la tabla **_`majors`_**

1. Consultar todos los datos de la tabla **_`majors`_**.
 ```bash
students=> SELECT * FROM majors;
```
2. Se utiliza `el operador =` para ver todas las majors (especialidades) denomindas **_`Game Design`_** de la tabla **_`majors`_**.
 ```bash
students=> SELECT * FROM majors WHERE major ='Game Design';
```
3. Se utiliza `el operador mayor que >` para ver las majors que le siguen en orden alfabético.
 ```bash
students=> SELECT * FROM majors WHERE major > 'Game Design';
```

### Paso 12:  Realizar consultas desde el script **_`student_info.sh`_**
En el archivo **_`student_info.sh`_** se agrega el comando **_`echo "$($PSQL "<query_here>")"`_** que realice la siguiente consulta: Imprimir los cursos que su nombre comience antes de la letra D.
 ```bash
echo "$($PSQL "SELECT course FROM courses WHERE course < 'D'")"
```
En el terminal de bash se ejecuta el script **_`student_info.sh`_**  para ver los resultados de la consulta.
 ```bash
camper: /project$ ./student_info.sh
```
![Imagen13](https://github.com/user-attachments/assets/0f7b2310-20bd-405f-a897-585fd03d25e4)

### Paso 13: Agregar otra declaración y consulta desde el script **_`student_info.sh`_**
En el archivo **_`student_info.sh`_** se agrega la siguiente declaración:
 ```bash
echo -e "\nFirst name, last name, and GPA of students whose last name begins with an 'R' or after and have a GPA greater than 3.8 or less than 2.0:"
```
Debajo de esta declaración se agrega el comando **_`echo "$($PSQL "<query_here>")"`_** que realice la siguiente consulta: Imprimir nombre, apellido y gpa de los estudiantes cuyo apellido comienza con R o después y tienen un gpa mayor a 3.8 o menor a 2.0.
 ```bash
echo "$($PSQL "SELECT first_name, last_name, gpa FROM students WHERE last_name >= 'R' AND (gpa > 3.8 OR gpa < 2.0)")"
```
En el terminal de bash se ejecuta el script **_`student_info.sh`_**  para ver los resultados de la consulta.
 ```bash
camper: /project$ ./student_info.sh
```
![Imagen14](https://github.com/user-attachments/assets/ee9c44dc-198c-44be-960e-ed0c61b34ec8)

### Paso 14: Consultar las columnas de la tabla **_`courses`_**
1. Consultar todos los datos de la tabla **_`courses`_**.
 ```bash
students=> SELECT * FROM courses;
```
2. Se utilizar **_`LIKE`_** para buscar patrones en texto como este: **_`WHERE <column> LIKE '<pattern>'`_**. Un guión bajo (_) en un patrón devolverá filas que tengan algún carácter en ese lugar. Se consulta las filas de esta tabla con un nombre de curso que coincida con el patrón **_`'_lgorithms'`_** .
 ```bash
students=> SELECT * FROM courses WHERE courses LIKE ='_lgorithms';
```
3. Hay otro carácter de patrón es **_`%`'_**. Significa que cualquier cosa puede estar ahí. Para buscar nombres que comiencen con W, puedes usar **_`W%`'_**. Se consulta los cursos que terminan en **_`'lgorithms'`_**.
 ```bash
students=> SELECT * FROM courses WHERE courses LIKE '%lgorithms';
```
4. Consulte los cursos que comiencen con Web.
 ```bash
students=> SELECT * FROM courses WHERE courses LIKE 'Web%';
```
5. Combine los dos caracteres de coincidencia de patrones para consultar cursos que tienen una segunda letra **_`e`_**.
 ```bash
students=> SELECT * FROM courses WHERE courses LIKE '_e%';
```
6. Consultar los cursos que tenga un espacios en sus nombres.
 ```bash
students=> SELECT * FROM courses WHERE courses LIKE '% %';
```
7. Se utiliza **_`NOT LIKE`_** para encontrar cosas que no coincidan con un patrón. Consultar los cursos que no contienen un espacio.
 ```bash
students=> SELECT * FROM courses WHERE courses NOT LIKE '% %';
```
8. Con **_`ILIKE`_** ignorará el caso de las letras al hacer coincidir. Úselo para ver los cursos con una A o una.
 ```bash
students=> SELECT * FROM courses WHERE courses ILIKE '%A%';
```
9. Se puede poner **_`NOT`_** delante de **_`ILIKE`_**. Úselo para ver los cursos que no contienen una A o una.
 ```bash
students=> SELECT * FROM courses WHERE courses NOT ILIKE '%A%';
```

### Paso 15: Agregar otra declaración y consulta desde el script **_`student_info.sh`_**

Se agrega otro **_`comando de eco`_**, un comentario que diga: **_`Last name of students whose last name contains a case insensitive 'sa' or have an 'r' as the second to last letter:`_**

 ```bash
echo -e "\nLast name of students whose last name contains a case insensitive 'sa' or have an 'r' as the second to last letter:"
```
En el script de **_`student_info.sh`_**, se agrega una declaración de **_`eco`_** para imprimir los resultados de la consulta de el apellido de los estudiantes cuyo apellido contiene una 'sa' que no distingue entre mayúsculas y minúsculas o tiene una 'r' como penúltima letra.
 ```bash
echo "$($PSQL "SELECT last_name FROM students WHERE last_name ILIKE '%sa%' OR last_name ILIKE '%r_'")"
```
En el terminal de bash se ejecuta el script **_`student_info.sh`_**  para ver los resultados de la consulta.
 ```bash
camper: /project$ ./student_info.sh
```
![Imagen2](https://github.com/user-attachments/assets/d9ea1247-c925-4777-8d87-e0080e912152)
![Imagen1](https://github.com/user-attachments/assets/09062595-03e8-40ef-95c3-4b0464a5098b)

### Paso 16: Consultar las columnas de la tabla **_`students`_**
1. Se puede acceder a los campos vacíos usando **_`IS NULL`_** como condición como esta: **_`WHERE <column> IS NULL`_**. Consultar los estudiantes que no tienen un GPA.
 ```bash
students=> SELECT * FROM students WHERE gpa IS NULL;
```
2. Se utiliza **_`NOT NULL`_** para ver filas que no son nulas. Consultar la información sobre los estudiantes que sí tienen un GPA.
 ```bash
students=> SELECT * FROM students WHERE gpa IS NOT NULL;
````
3. Consultar los estudiantes que no tienen major ni gpa
 ```bash
students=> SELECT * FROM students WHERE major_id IS NULL AND gpa IS NULL;
```

### Paso 17: Agregar otra declaración y consulta desde el script **_`student_info.sh`_**
Se agrega otro **_`comando de eco`_**.  Que diga: **_`First name, last name, and GPA of students who have not selected a major and either their first name begins with 'D' or they have a GPA greater than 3.0:`_**
 ```bash
echo -e "\nFirst name, last name, and GPA of students who have not selected a major and either their first name begins with 'D' or they have a GPA greater than 3.0:"
```
Se agrega un **_`comando de eco`_** para imprimir los resultados de el nombre, apellido y GPA de los estudiantes que no han seleccionado una especialización y su nombre comienza con 'D' o tienen un GPA superior a 3.0:

 ```bash
echo "$($PSQL "SELECT first_name, last_name, gpa FROM students WHERE major_id IS NULL AND (first_name LIKE 'D%' OR gpa > 3.0)")"
```
En el terminal de bash se ejecuta el script **_`student_info.sh`_**  para ver los resultados de la consulta.
 ```bash
camper: /project$ ./student_info.sh
```
![Imagen2](https://github.com/user-attachments/assets/5b8fe822-0d10-4367-927a-752137feee82)
![Imagen1](https://github.com/user-attachments/assets/81d2adb5-af45-4094-bc75-793b3b473faf)

### Paso 18:  Consultar las columnas de la tabla **_`students`_**
1. Se puede especificar el orden en el que desea que estén sus resultados agregando **_`ORDER BY <column_name>`_** al final de una consulta. En el indicador de psql, se consulta toda la información en la tabla de estudiantes en orden según el GPA.
 ```bash
students=> SELECT * FROM students ORDER BY gpa;
```
2. Se puede agregar más columnas al orden separándolas con una coma como esta: **_`ORDER BY <columna_1>, <columna_2>`_**. Cualquier valor coincidente en la primera columna ordenada se ordenará en la siguiente. Se consulta toda la información de los estudiantes con el GPA más alto en la parte superior y en orden alfabético por nombre si el GPA coincide.
 ```bash
students=> SELECT * FROM students ORDER BY gpa DESC, first_name;
````
3. Se puede agregar **_`LIMIT <número>`_** al final de la consulta para obtener solo la cantidad que desea. Se consulta a los estudiantes en el mismo orden que el último comando, pero solo devuelva las primeras 10 filas.
 ```bash
students=> SELECT * FROM students ORDER BY gpa DESC, first_name LIMIT 10;
```
4. El orden de las palabras clave en su consulta es importante. No se puede poner LIMIT antes de ORDER BY, ni ninguno de ellos antes de WHERE. Se consulta la misma cantidad de estudiantes, en el mismo orden, pero no obtenga los que no tienen un GPA.
 ```bash
students=> SELECT * FROM students WHERE gpa IS NOT NULL ORDER BY gpa DESC, first_name LIMIT 10;
```

### Paso 19: Agregar otra declaración y consulta desde el script **_`student_info.sh`_**
Se agrega otro **_`comando de eco`_**.  Que diga: **_`Course name of the first five courses, in reverse alphabetical order, that have an 'e' as the second letter or end with an 's':`_**
 ```bash
echo -e "\nCourse name of the first five courses, in reverse alphabetical order, that have an 'e' as the second letter or end with an 's':"
```
Se agrega un **_`comando de eco`_** para imprimir los resultados de: Nombre del curso de los primeros cinco cursos, en orden alfabético inverso, que tienen una 'e' como segunda letra o terminan con una 's'
 ```bash
cho "$($PSQL "SELECT course FROM courses WHERE course LIKE '_e%' OR course LIKE '%s' ORDER BY course DESC LIMIT 5")"
```
En el terminal de bash se ejecuta el script **_`student_info.sh`_**  para ver los resultados de la consulta.
 ```bash
camper: /project$ ./student_info.sh
```
![Imagen2](https://github.com/user-attachments/assets/af852cc4-41ca-42d8-9419-38872dcd5439)
![Imagen5](https://github.com/user-attachments/assets/325270f4-e67b-44b4-b7d1-edda7de88a94)

### Paso 20:  Consultar las columnas de la tabla **_`students`_**
1. Hay varias funciones matemáticas que se pueden usar con columnas numéricas. Uno de ellos es **_`MIN`_**, se usa al seleccionar una columna de esta manera: **_`SELECT MIN(<column>) FROM <table>`_**. Con esto se encuentra el valor más bajo en la columna. En el indicador de psql, se consulta el valor más bajo en la columna gpa de la tabla de estudiantes.
 ```bash
students=> SELECT MIN(gpa) FROM students;
```
2. Se utiliza **_`MAX`_** para ver el gpa más grande de la tabla
 ```bash
students=> SELECT MAX(gpa) FROM students;
````
3. Se usa la **_`función SUM`_** para descubrir cuánto suman todos los valores de la columna **_`major_id`_** en la tabla de estudiantes.
 ```bash
students=> SELECT SUM(major_id) FROM students;
```
4. La **_`función AVG`_** le dará el promedio de todos los valores de una columna. Se usa para ver el promedio de la misma columna.
 ```bash
students=> SELECT AVG(major_id) FROM students;
```
5. Se puede redondear decimales hacia arriba o hacia abajo al número entero más cercano con **_`CEIL y FLOOR`_**, respectivamente. Se utiliza **_`CEIL`_** para redondear el **_`major_id`_** promedio al número entero más cercano. Aquí hay un ejemplo: **_`CEIL(<número_a_redondear>)`_**.
 ```bash
students=> SELECT CEIL(AVG(major_id)) FROM students;
```
6. Se puede redondear un número al número entero más cercano con **_`ROUND(<number_to_round>, <decimals_places>)`_**. Se utiliza para redondear el promedio de la columna major_id a cinco decimales.
 ```bash
students=> SELECT ROUND(AVG(major_id), 5) FROM students;
```

### Paso 21: Agregar otra declaración y consulta desde el script **_`student_info.sh`_**
Se agrega otro **_`comando de eco`_**.  Que diga: **_`Average GPA of all students rounded to two decimal places:`_**
 ```bash
echo -e "\nAverage GPA of all students rounded to two decimal places:"
```
Se agrega un **_`comando de eco`_** para imprimir los resultados de: GPA promedio de todos los estudiantes redondeado a dos decimales.
 ```bash
echo "$($PSQL "SELECT ROUND(AVG(gpa), 2) FROM students")"
```
En el terminal de bash se ejecuta el script **_`student_info.sh`_**  para ver los resultados de la consulta.
 ```bash
camper: /project$ ./student_info.sh
```
![Imagen7](https://github.com/user-attachments/assets/a839c616-7307-4402-aafe-5c5a081b5f09)
![Imagen8](https://github.com/user-attachments/assets/4c89955a-3ae6-4282-bbe0-2cb036fbc6b6)

### Paso 22:  Consultar las columnas de las tablas **_`students`_** y **_`majors`_**

1. Se puede utilizar las **_`función COUNT`_** así: **_`COUNT(<columna>)`_**. Le dirá cuántas entradas hay en una tabla para la columna. Se usa **_`COUNT(*)`_** para ver cuántas especialidades hay.
 ```bash
students=> SELECT COUNT(*) FROM majors;
```
2. Se utiliza **_`función COUNT`_** para ver cuantos estudiantes hay.
 ```bash
students=> SELECT COUNT(*) FROM students;
````
3. Se utiliza **_`GROUP BY`_** para consultar los valores únicos de major_id en la tabla de estudiantes.
 ```bash
students=> SELECT major_id FROM students GROUP BY major_id;
```
4. Otra opción con GROUP BY es **_`HAVING`_**. Puede agregarlo al final de esta manera: **_`SELECT <column> FROM <table> GROUP BY <column> HAVING <condition>`_**. Utilice **_`HAVING`_** para mostrar solo filas que tengan un GPA máximo de 4,0.
 ```bash
students=> SELECT major_id, MIN(gpa), MAX(gpa) FROM students GROUP BY major_id HAVING MAX(gpa)=4.0;
```

### Paso 23: Agregar otra declaración y consulta desde el script **_`student_info.sh`_**
Se agrega otro **_`comando de eco`_**.  Que diga: **_`Major ID, total number of students in a column named 'number_of_students', and average GPA rounded to two decimal places in a column name 'average_gpa', for each major ID in the students table having a student count greater than 1:`_**
 ```bash
echo -e "\nMajor ID, total number of students in a column named 'number_of_students', and average GPA rounded to two decimal places in a column name 'average_gpa', for each major ID in the students table having a student count greater than 1:"
```
Se agrega un **_`comando de eco`_** para imprimir los resultados de: ID de especialidad, número total de estudiantes en una columna llamada 'number_of_students' y GPA promedio redondeado a dos decimales en una columna llamada 'average_gpa', para cada ID de especialidad en la tabla de estudiantes que tenga un recuento de estudiantes mayor que 1:
 ```bash
echo "$($PSQL "SELECT major_id, COUNT(*) AS number_of_students, ROUND(AVG(gpa), 2) AS average_gpa FROM students GROUP BY major_id HAVING COUNT(*) > 1")"
```
En el terminal de bash se ejecuta el script **_`student_info.sh`_**  para ver los resultados de la consulta.
 ```bash
camper: /project$ ./student_info.sh
```
![Imagen9](https://github.com/user-attachments/assets/ed10d748-9d61-479e-930a-35ddf98ec4f4)
![Imagen10](https://github.com/user-attachments/assets/241b31a9-420b-41ac-aef6-5db062379da3)

### Paso 24:  Consultar las columnas de las tablas **_`students`_** y **_`majors`_**
Las tablas de **_`majors`_** y **_`students`_** están vinculadas con la clave externa **_`major_id`_**. Si desea ver el nombre de una especialización que está cursando un estudiante, debe  hacer **_`JOIN`_** las dos tablas. Se muestra un ejemplo de cómo hacerlo:
```bash
SELECT * FROM <table_1> FULL JOIN <table_2> ON <table_1>.<foreign_key_column> = <table_2>.<foreign_key_column>;
```
1. Unir las dos tablas de **_`students`_** y **_`majors`_**
```bash
SELECT * FROM students FULL JOIN majors ON students.major_id = majors.major_id;
```
2. Las dos **_`columnas major_id`_** son las mismas en cada fila para las que lo tienen. Puede ver que hay algunos estudiantes sin especialización y algunas especialidades sin estudiantes. El **_`FULL JOIN`_** que se utiliza incluye todas las filas de ambas tablas. Se utiliza **_`LEFT JOIN`_** para unir las mismas dos tablas de la misma manera.
```bash
SELECT * FROM students LEFT JOIN majors ON students.major_id = majors.major_id;
```
3. Hay algunas filas menos que la última consulta. En **_`LEFT JOIN`_** que utilizó, la tabla de estudiantes era la tabla izquierda ya que estaba en el lado izquierdo de JOIN. majors era la tabla correcta. En un **_`LEFT JOIN`_** obtiene todas las filas de la tabla de la izquierda, pero solo las filas de la tabla de la derecha que están vinculadas desde la de la izquierda. Al observar los datos, se puede ver que todos los estudiantes regresaron, pero las carreras sin estudiantes no. Únase a las mismas dos tablas con una **_`RIGHT JOIN`_** esta vez.
```bash
SELECT * FROM students RIGHT JOIN majors ON students.major_id = majors.major_id;
```
4. **_`RIGHT JOIN`_**  mostró todas las filas de la tabla derecha (majors), pero solo las filas de la tabla izquierda (students) si tienen una majors. Hay un tipo más que debes conocer. Une las dos tablas con una **_`INNER JOIN`_**.
```bash
SELECT * FROM students INNER JOIN majors ON students.major_id = majors.major_id;
```

### Paso 25: Agregar otra declaración y consulta desde el script **_`student_info.sh`_**
Se agrega otro **_`comando de eco`_**.  Que diga: **_`List of majors, in alphabetical order, that either no student is taking or has a student whose first name contains a case insensitive 'ma':`_**
 ```bash
echo -e "\nList of majors, in alphabetical order, that either no student is taking or has a student whose first name contains a case insensitive 'ma':"
```
Se agrega un **_`comando de eco`_** para imprimir los resultados de: Lista de especialidades, en orden alfabético, que ningún estudiante está cursando o que tiene un estudiante cuyo nombre contiene 'ma' que no distingue entre mayúsculas y minúsculas:"
 ```bash
echo "$($PSQL "SELECT major FROM students FULL JOIN majors ON students.major_id = majors.major_id WHERE major IS NOT NULL AND (student_id IS NULL OR first_name ILIKE '%ma%') ORDER BY major")"
```
En el terminal de bash se ejecuta el script **_`student_info.sh`_**  para ver los resultados de la consulta.
 ```bash
camper: /project$ ./student_info.sh
```
![Imagen9](https://github.com/user-attachments/assets/8c0e9c28-83b0-4b81-829c-3a1105be94e7)
![Imagen11](https://github.com/user-attachments/assets/ab6a1746-e145-435a-be53-6dbe884d8d8d)









