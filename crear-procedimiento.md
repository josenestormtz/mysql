# Creación de un Procedimiento Almacenado en MySQL

Este ejemplo muestra cómo crear un **procedimiento almacenado** que inserta un registro en la tabla `productos`, utilizando parámetros de entrada (`id` y `nombre`).

---

## 📘 Código SQL

```sql
DELIMITER $$

CREATE PROCEDURE InsertarProducto (
    IN p_id INT,
    IN p_nombre VARCHAR(100)
)
BEGIN
    INSERT INTO productos (id, nombre, cantidad, precio, fecha_creacion, activo)
    VALUES (p_id, p_nombre, 0, 0.00, NOW(), TRUE);
END $$

DELIMITER ;
```

🧩 Explicación

DELIMITER $$	Cambia el delimitador para que MySQL no interprete los ; dentro del bloque como fin del comando.

CREATE PROCEDURE InsertarProducto	Define el nombre del procedimiento.

IN p_id INT	Parámetro de entrada entero (el id del producto).

IN p_nombre VARCHAR(100)	Parámetro de entrada de texto (el nombre del producto).

BEGIN ... END	Define el bloque de instrucciones del procedimiento.

INSERT INTO productos (...) VALUES (...)	Inserta un nuevo registro usando los parámetros recibidos.

DELIMITER ;	Restaura el delimitador normal.

Ejemplo de Ejecución

```sql
CALL InsertarProducto(1, 'Teclado mecánico');
```
