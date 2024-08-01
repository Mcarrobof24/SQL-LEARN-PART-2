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

### Paso 14:


