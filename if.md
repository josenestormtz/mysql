# 🧩 Mini Tutorial: Uso de estructuras `IF` en procedimientos MySQL

En MySQL, las estructuras condicionales (`IF`, `ELSEIF`, `ELSE`) se utilizan **dentro de bloques** como procedimientos almacenados, funciones o triggers.

> ⚠️ Importante: No confundir con la función `IF(expr, true_val, false_val)` usada en consultas.  
> Este tutorial explica el **bloque de control de flujo** usado en código procedural.

---

## 🧱 Sintaxis básica

```sql
IF condición THEN
    -- acciones si la condición es verdadera
END IF;
```

## 💡 Ejemplo 1: Validar un valor y mostrar un mensaje

```sql
BEGIN
    DECLARE mensaje VARCHAR(50);

    IF 10 > 5 THEN
        SET mensaje = 'Verdadero';
    END IF;

    SELECT mensaje AS resultado;
END;
```

📘 Resultado:
Verdadero

## 🧩 Estructura completa con ELSEIF y ELSE
```sql
IF condición1 THEN
    -- acciones si condición1 es verdadera
ELSEIF condición2 THEN
    -- acciones si condición2 es verdadera
ELSE
    -- acciones si ninguna se cumple
END IF;
```

## 💡 Ejemplo 2: Evaluar un número
```sql
BEGIN
    DECLARE numero INT DEFAULT 5;
    DECLARE mensaje VARCHAR(50);

    IF numero > 10 THEN
        SET mensaje = 'Mayor que 10';
    ELSEIF numero = 10 THEN
        SET mensaje = 'Igual a 10';
    ELSE
        SET mensaje = 'Menor que 10';
    END IF;

    SELECT mensaje AS resultado;
END;
```

📘 Resultado:
```sql
Menor que 10
```

## 💡 Ejemplo 3: Validar antes de insertar (caso práctico)
```sql
DELIMITER $$

CREATE PROCEDURE spInsertarUsuario(
    IN p_nombre VARCHAR(100),
    IN p_correo VARCHAR(100)
)
BEGIN
    DECLARE mensaje VARCHAR(100);

    IF EXISTS (SELECT 1 FROM tblUsuarios WHERE correo = p_correo) THEN
        SET mensaje = 'El correo ya existe';
    ELSE
        INSERT INTO tblUsuarios (nombre, correo, fechaRegistro)
        VALUES (p_nombre, p_correo, NOW());
        SET mensaje = 'Usuario insertado correctamente';
    END IF;

    SELECT mensaje AS mensaje;
END $$

DELIMITER ;
```

📘 Este procedimiento:
- Revisa si el correo ya existe.
- Si existe → muestra el mensaje correspondiente.
- Si no existe → inserta el usuario y muestra confirmación.

## 💡 Ejemplo 4: Anidar condiciones

Puedes colocar IF dentro de otro IF:
```sql
IF a > 0 THEN
    IF b > 0 THEN
        SET mensaje = 'Ambos son positivos';
    ELSE
        SET mensaje = 'Solo A es positivo';
    END IF;
ELSE
    SET mensaje = 'A no es positivo';
END IF;
```

📘 Notas importantes
- Cada IF se cierra con END IF;
- Cada sentencia dentro del bloque debe terminar con ;
- Si estás creando un procedimiento, usa DELIMITER para evitar errores.
- Puedes usar variables, parámetros o subconsultas en las condiciones.
- Si solo necesitas comparar valores en un SELECT, puedes usar la función:
```sql
SELECT IF(edad >= 18, 'Adulto', 'Menor') AS resultado;
```

## ✅ Buenas prácticas
- Usa prefijos (p_, v_) para distinguir parámetros y variables locales.
- Siempre incluye END IF; aunque la acción sea simple.
- Combina IF con EXISTS, IS NULL, = o LIKE para validaciones lógicas.
- Incluye siempre un ELSE cuando esperes múltiples caminos.
