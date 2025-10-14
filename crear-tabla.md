# Ejemplo de tabla en MySQL

Este ejemplo muestra cómo crear una tabla que incluye los tipos de datos:
`VARCHAR`, `INTEGER`, `DATETIME`, `DECIMAL` y `BOOLEAN`.

```sql
CREATE TABLE productos (
    id INT NOT NULL AUTO_INCREMENT,
    nombre VARCHAR(100) NOT NULL,
    cantidad INT DEFAULT 0,
    precio DECIMAL(10,2) NOT NULL,
    fecha_creacion DATETIME DEFAULT CURRENT_TIMESTAMP,
    activo BOOLEAN DEFAULT TRUE,
    PRIMARY KEY (id)
);
```

Explicación de los campos
id	INT AUTO_INCREMENT	Identificador único del producto. Se incrementa automáticamente.

nombre	VARCHAR(100)	Nombre del producto (hasta 100 caracteres).

cantidad	INT	Cantidad disponible en inventario.

precio	DECIMAL(10,2)	Precio del producto, con 2 decimales.

fecha_creacion	DATETIME	Fecha y hora de creación del registro. Se llena automáticamente.

activo	BOOLEAN	Indica si el producto está activo (TRUE) o inactivo (FALSE).

Notas adicionales

AUTO_INCREMENT en MySQL equivale a IDENTITY en SQL Server.

BOOLEAN es un alias de TINYINT(1), donde 0 = FALSE y 1 = TRUE.

Puedes iniciar el contador de AUTO_INCREMENT desde un número diferente con:
```sql
ALTER TABLE productos AUTO_INCREMENT = 1000;
```
