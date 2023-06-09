# SimulacroBD2
## ENUNCIADOS
1. Muestra todas las piezAs que sean de color rojo.
2. Muestra todos los proveedores que estén ubicados en la ciudad de 'Madrid'.
3. Muestra el nombre de la pIeza más pesada.
4. Muestra el nombre del proveedor que suministra la mayor cantidad de piezas diferentes.
5. Saca todos los proveedores que suministren al menos una pieza de color azul.
6. Visualiza el nombre de la pieza más ligera que es suministrada por el proveedor 'Proveedor A'.
7. Saca el nombre del proveedor que suministra la pieza más pesada.
8. Muestra todas las piezas que sean suministradas por proveedores de la ciudad de 'Barcelona'.
9. Muestra el nombre del proveedor que suministra la mayor canitdad de piezas de color verde.
10. Muestra el nombre de la pieza más pesada que es suministrada por un proveedor de la ciudad de Valencia.

## RESPUESTAS
1. SELECT nombre_pieza FROM piezas WHERE color='Rojo'

2. SELECT nombre_proveedor FROM proveedores WHERE ciudad_proveedor = 'Madrid'

3. SELECT nombre_pieza 
FROM piezas 
ORDER BY peso DESC
LIMIT 1

4. SELECT proveedores.nombre_proveedor
FROM proveedores
INNER JOIN piezas ON proveedores.id_proveedor = piezas.id_proveedor
HAVING COUNT(piezas.id_proveedor) AS contador
GROUP BY piezas.id_pieza
ORDER BY  contador DESC
LIMIT 1

5. SELECT proveedores.nombre_proveedor
FROM proveedores
INNER JOIN piezas ON proveedores.id_proveedor = piezas.id_proveedor
WHERE piezas.id_pieza EXISTS (SELECT * 
                              FROM piezas 
                              WHERE color = 'Azul')

6. SELECT piezas.nombre_pieza
FROM piezas
INNER JOIN proveedores ON piezas.id_proveedor = proveedores.id_proveedor
WHERE proveedores.id_proveedor EXISTS (SELECT * 
                                       FROM proveedores
                                       WHERE nombre_proveedor = 'Proveedor A')

7. SELECT proveedores.nombre_proveedor
FROM proveedores
INNER JOIN piezas ON proveedores.id_proveedor = piezas.id_proveedor
WHERE piezas.id_pieza EXISTS (SELECT * 
                              FROM piezas 
                              ORDER BY peso DESC 
                              LIMIT 1)

8. SELECT DISTINCT piezas.nombre_pieza
FROM piezas
INNER JOIN proveedores ON piezas.id_proveedor = proveedores.id_proveedor
WHERE piezas.id_proveedor EXISTS (SELECT * 
                                  FROM piezas 
                                  WHERE ciudad_proveedor = 'Barcelona')

9.SELECT proveedores.nombre_proveedor
FROM proveedores
INNER JOIN piezas ON proveedores.id_proveedor = piezas.id_proveedor
WHERE piezas.color = 'verde'
HAVING COUNT(piezas.id_pieza)
GROUP BY piezas.id_proveedor
LIMIT 1

10.SELECT piezas.nombre_pieza
FROM piezas
INNER JOIN proveedores ON piezas.id_proveedor = proveedores.id_proveedor
WHERE piezas.id_pieza = (SELECT MAX(peso), id_pieza
                         FROM piezas) AND proveedores.ciudad_proveedor = 'Valencia'

## CORRECCIONES
- Tras haber comprovado las Quearys en la base de datos, observamos que del ejercicio 5 al 8 hay errores en el WHERE debido a un fallo de sintaxis.
- En el ejercicio 9 también hay un error de sintaxis.
- En el ejercicio 10 habria tambien un error de sintaxis.
