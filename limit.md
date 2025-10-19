# Uso de `LIMIT` (equivalente a `TOP` en MySQL)

En MySQL, el comando `TOP n` (usado en SQL Server) **no existe**.  
En su lugar, se utiliza la cláusula **`LIMIT`** para restringir el número de filas devueltas por una consulta.

---

## 🧩 Sintaxis básica

```sql
SELECT columnas
FROM nombre_tabla
WHERE condiciones
LIMIT n;
```
- n: número máximo de filas que quieres obtener.

## 💡 Ejemplo 1: Obtener los primeros 5 registros

```sql
SELECT *
FROM tblProspectos
LIMIT 5;
```

🔹 Devuelve las primeras 5 filas de la tabla tblProspectos.

## 💡 Ejemplo 2: Obtener los primeros 10 registros ordenados
```sql
SELECT nombre, apellidos
FROM tblProspectos
ORDER BY fechaCreacion DESC
LIMIT 10;
```
🔹 Devuelve los 10 prospectos más recientes.

## 🚀 Conclusión
- Usa LIMIT para limitar resultados.
- Siempre combina con ORDER BY para obtener resultados consistentes.
- No existe TOP en MySQL, pero LIMIT cumple el mismo propósito.
