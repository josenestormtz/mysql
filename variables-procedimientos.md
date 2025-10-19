# Variables en Procedimientos

En MySQL, las **variables locales** se usan dentro de procedimientos, funciones, triggers o eventos.  
Se declaran con `DECLARE` y existen solo dentro del bloque `BEGIN ... END`.

---

## 1. Sintaxis básica

```sql
DECLARE nombre_variable TIPO [DEFAULT valor_inicial];
```

## 2. Tipos de variables más comunes
Tipo	Ejemplo de declaración	Descripción
INT	DECLARE contador INT DEFAULT 0;	Enteros.
VARCHAR(n)	DECLARE nombre VARCHAR(100);	Texto de hasta n caracteres.
DECIMAL(m,n)	DECLARE precio DECIMAL(10,2) DEFAULT 0.00;	Números con decimales.
DATETIME	DECLARE fecha DATETIME;	Fecha y hora.
BOOLEAN	DECLARE activo BOOLEAN DEFAULT TRUE;	Valor lógico (0 = FALSE, 1 = TRUE).

## 3. Asignar valores a variables
Con SET

```sql
SET contador = 1;
SET nombre = 'Producto A';
```

Con SELECT ... INTO
```sql
SELECT COUNT(*) INTO contador FROM tblProspectos;
```

## 4. Ejemplo completo de procedimiento
```sql
DELIMITER $$

CREATE PROCEDURE EjemploVariables()
BEGIN
    DECLARE contador INT DEFAULT 0;
    DECLARE mensaje VARCHAR(100);
    DECLARE precio DECIMAL(10,2) DEFAULT 0.00;
    DECLARE fecha_creacion DATETIME;
    DECLARE activo BOOLEAN DEFAULT TRUE;

    SET mensaje = 'Hola, esta es una variable dentro del procedimiento';
    SET contador = contador + 1;
    SET fecha_creacion = NOW();
    SET precio = 99.99;

    SELECT mensaje AS Mensaje, contador AS Contador, precio AS Precio, fecha_creacion AS Fecha, activo AS Activo;
END $$

DELIMITER ;
```

## 5. Buenas prácticas

Declarar todas las variables al inicio del bloque BEGIN ... END.

Usar nombres claros y consistentes.

Inicializar variables siempre que sea posible.

Para resultados de consultas, usar SELECT ... INTO en lugar de asignaciones manuales.
