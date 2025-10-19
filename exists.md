# Uso de `EXISTS` en consultas SQL (MySQL)

El operador **`EXISTS`** se utiliza en MySQL para comprobar si **una subconsulta devuelve al menos una fila**.  
Devuelve `TRUE` (1) si la subconsulta tiene resultados, y `FALSE` (0) si no tiene ninguno.

---

## 🧩 Sintaxis básica

```sql
SELECT EXISTS (
    SELECT 1
    FROM nombre_tabla
    WHERE condiciones
) AS existe;
```

- SELECT 1 → No importa el valor, solo verifica si hay filas.
- WHERE condiciones → Especifica qué estás buscando.
- AS existe → Alias opcional para el resultado (1 o 0).

## 💡 Ejemplo 1: Verificar si existe un registro
```sql
SELECT EXISTS(
    SELECT 1
    FROM tblProspectos
    WHERE correo = 'juan@example.com'
) AS existe;
```

Resultado:
```sql
existe
1
```

🔹 Devuelve 1 si el correo existe en la tabla tblProspectos.
🔹 Devuelve 0 si no existe.

## 💡 Ejemplo 2: Usar EXISTS dentro de una condición

Puedes usar EXISTS en una cláusula WHERE para filtrar resultados según otra tabla.

```sql
SELECT nombre, apellidos
FROM tblProspectos p
WHERE EXISTS (
    SELECT 1
    FROM tblEstados e
    WHERE e.id = p.estadoId
);
```

🔹 Esto devuelve solo los prospectos cuyo estadoId exista en la tabla tblEstados.

## 💡 Ejemplo 3: Uso con NOT EXISTS

Para comprobar que no existe un registro relacionado:
```sql
SELECT nombre, apellidos
FROM tblProspectos p
WHERE NOT EXISTS (
    SELECT 1
    FROM tblCorreosBloqueados b
    WHERE b.correo = p.correo
);
```

🔹 Esto devuelve todos los prospectos que no estén bloqueados.

## 📘 Comparación rápida: EXISTS vs IN
- Caso	Recomendado
- Subconsulta con muchas filas	✅ EXISTS (más eficiente)
- Lista corta de valores	✅ IN
- Validar existencia (sí/no)	✅ EXISTS

## 🚀 Conclusión

- EXISTS devuelve TRUE si hay al menos una coincidencia.
- NOT EXISTS devuelve TRUE si no hay coincidencias.
- Ideal para validaciones rápidas, subconsultas correlacionadas, y control de duplicados.
