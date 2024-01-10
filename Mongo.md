

| **Consulta** | **Resultado** | **Descripción** |
|--------------|---------------|-----------------|
| **Create (InsertOne):**<br>`db.empleados.insertOne({Nombre: "Juan", Apellido: "García", "Categoría": "Analista", "Salario anual": 55000, Oficina: 3})` | Acknowledged: true, InsertedId: ObjectId(...) | Crea un nuevo documento en la colección `empleados` con la información proporcionada. El ID del documento recién creado es mostrado en "InsertedId". |
| **Read (Find):**<br>`db.empleados.find({"Categoría": "Analista"}).limit(1).pretty()` | ```json { "_id": ObjectId(...), "Nombre": "Juan", "Apellido": "García", "Categoría": "Analista", "Salario anual": 55000, "Oficina": 3 }``` | Encuentra y muestra el primer documento en la colección `empleados` donde la categoría es "Analista". |
| **Update (UpdateOne):**<br>`db.empleados.updateOne({Nombre: "Juan"}, {$set: {Salario: 60000}})` | MatchedCount: 1, ModifiedCount: 1 | Actualiza el salario del empleado con nombre "Juan" a 60000. "MatchedCount" indica cuántos documentos coincidieron con la consulta, y "ModifiedCount" muestra cuántos fueron modificados. |
| **Delete (DeleteOne):**<br>`db.empleados.deleteOne({Nombre: "Juan"})` | DeletedCount: 1 | Elimina el documento del empleado con nombre "Juan" de la colección `empleados`. "DeletedCount" indica cuántos documentos fueron eliminados. |

<br>
<br>
<br>

| Operación | Consulta | Resultado | Descripción |
|-----------|----------|-----------|-------------|
| `$eq` | `db.empleados.find({"Salario anual": 48500}).pretty().limit(1)` | ```json _id: ObjectId('659c26440337f567515c25d1'), EmpID: 41, Apellido: 'Costa', Nombre: 'Maria', 'Categoría': 'Almacenista', 'Fecha contrato': '16/1/07', Oficina: 4, Extension: '400', 'Informes a': 21, 'Salario anual': 48500 ``` | Compara valores iguales al especificado. |
| `$gt` | `db.empleados.find({"Salario anual": {"$gt": 160000}}).pretty().limit(1)` | ```json _id: ObjectId('659c26440337f567515c25b7'), EmpID: 2, Apellido: 'Palacios', Nombre: 'Antonio', 'Categoría': 'Presidente', 'Fecha contrato': '26/9/03', Oficina: 1, Extension: '101', 'Informes a': null, 'Salario anual': 160000 ``` | Compara valores mayores que el especificado. |
| `$gte` | `db.empleados.find({"Salario anual": {"$gte": 48500}}).pretty().limit(1)` | ```json _id: ObjectId('659c26440337f567515c25d1'), EmpID: 41, Apellido: 'Costa', Nombre: 'Maria', 'Categoría': 'Almacenista', 'Fecha contrato': '16/1/07', Oficina: 4, Extension: '400', 'Informes a': 21, 'Salario anual': 48500 ``` | Compara valores mayores o iguales al especificado. |
| `$in` | `db.empleados.find({"Salario anual": {"$in": [48500, 160000]}}).pretty().limit(1)` | ```json _id: ObjectId('659c26440337f567515c25d1'), EmpID: 41, Apellido: 'Costa', Nombre: 'Maria', 'Categoría': 'Almacenista', 'Fecha contrato': '16/1/07', Oficina: 4, Extension: '400', 'Informes a': 21, 'Salario anual': 48500 ``` | Compara con cualquiera de los valores especificados en un array. |
| `$lt` | `db.empleados.find({"Salario anual": {"$lt": 48000}}).pretty().limit(1)` | ```json _id: ObjectId('659c26440337f567515c25b7'), EmpID: 2, Apellido: 'Palacios', Nombre: 'Antonio', 'Categoría': 'Presidente', 'Fecha contrato': '26/9/03', Oficina: 1, Extension: '101', 'Informes a': null, 'Salario anual': 160000 ``` | Compara valores menores que el especificado. |
| `$lte` | `db.empleados.find({"Salario anual": {"$lte": 48000}}).pretty().limit(1)` | ```json _id: ObjectId('659c26440337f567515c25b7'), EmpID: 2, Apellido: 'Palacios', Nombre: 'Antonio', 'Categoría': 'Presidente', 'Fecha contrato': '26/9/03', Oficina: 1, Extension: '101', 'Informes a': null, 'Salario anual': 160000 ``` | Compara valores menores o iguales al especificado. |
| `$ne` | `db.empleados.find({"Salario anual": {"$ne": 160000}}).pretty().limit(1)` | ```json _id: ObjectId('659c26440337f567515c25b7'), EmpID: 2, Apellido: 'Palacios', Nombre: 'Antonio', 'Categoría': 'Presidente', 'Fecha contrato': '26/9/03', Oficina: 1, Extension: '101', 'Informes a': null, 'Salario anual': 160000 ``` | Compara con todos los valores que no son iguales al especificado. |
| `$nin` | `db.empleados.find({"Salario anual": {"$nin": [48500, 160000]}}).pretty().limit(1)` | ```json _id: ObjectId('659c26440337f567515c25d1'), EmpID: 41, Apellido: 'Costa', Nombre: 'Maria', 'Categoría': 'Almacenista', 'Fecha contrato': '16/1/07', Oficina: 4, Extension: '400', 'Informes a': 21, 'Salario anual': 48500 ``` | Compara con ninguno de los valores especificados en un array. |

<br>
<br>
<br>


| Operación | Consulta | Resultado | Descripción |
|-----------|----------|-----------|-------------|
| `$and` | `db.empleados.find({$and: [{"Salario anual":48500},{"Oficina":4}]}).pretty().limit(1)` | ```json _id: ObjectId('659c26440337f567515c25d1'), EmpID: 41, Apellido: 'Costa', Nombre: 'Maria', 'Categoría': 'Almacenista', 'Fecha contrato': '16/1/07', Oficina: 4, Extension: '400', 'Informes a': 21, 'Salario anual': 48500 ``` | Combina cláusulas de consulta con un AND lógico, devuelve documentos que cumplen ambas condiciones. |
| `$not` | `db.empleados.find({"Salario anual": {"$not": {"$eq": 48500}}}).pretty().limit(1)` | ```json _id: ObjectId('659c26440337f567515c25b7'), EmpID: 2, Apellido: 'Palacios', Nombre: 'Antonio', 'Categoría': 'Presidente', 'Fecha contrato': '26/9/03', Oficina: 1, Extension: '101', 'Informes a': null, 'Salario anual': 160000 ``` | Invierte el efecto de una expresión de consulta, devuelve documentos que no coinciden. |
| `$nor` | `db.empleados.find({$nor: [{"Salario anual": 48500}, {"Oficina": 4}]}).pretty().limit(1)` | ```json _id: ObjectId('659c26440337f567515c25d1'), EmpID: 41, Apellido: 'Costa', Nombre: 'Maria', 'Categoría': 'Almacenista', 'Fecha contrato': '16/1/07', Oficina: 4, Extension: '400', 'Informes a': 21, 'Salario anual': 48500 ``` | Combina cláusulas de consulta con un NOR lógico, devuelve documentos que no cumplen ambas condiciones. |


<br>
<br>
<br>


| Operación | Consulta | Resultado | Descripción |
|-----------|----------|-----------|-------------|
| `$exists` | `db.empleados.find({"Extension": {"$exists": true}}).pretty().limit(1)` | ```json _id: ObjectId('659c26440337f567515c25b7'), EmpID: 2, Apellido: 'Palacios', Nombre: 'Antonio', 'Categoría': 'Presidente', 'Fecha contrato': '26/9/03', Oficina: 1, Extension: '101', 'Informes a': null, 'Salario anual': 160000 ``` | Selecciona documentos que tienen el campo especificado. |
| `$type` | `db.empleados.find({"Extension": {"$type": "string"}}).pretty().limit(1)` | ```json _id: ObjectId('659c26440337f567515c25b7'), EmpID: 2, Apellido: 'Palacios', Nombre: 'Antonio', 'Categoría': 'Presidente', 'Fecha contrato': '26/9/03', Oficina: 1, Extension: '101', 'Informes a': null, 'Salario anual': 160000 ``` | Selecciona documentos si un campo es del tipo especificado. |
| `$expr` | `db.empleados.find({"$expr": {"$gt": ["$Salario anual", "$Extension"]}}).pretty().limit(1)` | ```json _id: ObjectId('659c26440337f567515c25b7'), EmpID: 2, Apellido: 'Palacios', Nombre: 'Antonio', 'Categoría': 'Presidente', 'Fecha contrato': '26/9/03', Oficina: 1, Extension: '101', 'Informes a': null, 'Salario anual': 160000 ``` | Permite el uso de expresiones de agregación dentro del lenguaje de consulta. |
| `$jsonSchema` | `db.empleados.find({"$jsonSchema": {"properties": {"Salario anual": {"type": "number"}}}}).pretty().limit(1)` | ```json _id: ObjectId('659c26440337f567515c25b7'), EmpID: 2, Apellido: 'Palacios', Nombre: 'Antonio', 'Categoría': 'Presidente', 'Fecha contrato': '26/9/03', Oficina: 1, Extension: '101', 'Informes a': null, 'Salario anual': 160000 ``` | Valida documentos contra el JSON Schema dado. |
| `$mod` | `db.empleados.find({"EmpID": {"$mod": [2, 0]}}).pretty().limit(1)` | ```json _id: ObjectId('659c26440337f567515c25b8'), EmpID: 3, Apellido: 'Canton', Nombre: 'Raul', 'Categoría': 'Comercial', 'Fecha contrato': '20/10/04', Oficina: 5, Extension: '102', 'Informes a': 4, 'Salario anual': 61500 ``` | Realiza una operación de módulo en el valor de un campo y selecciona documentos con un resultado específico. |
| `$regex` | `db.empleados.find({"Apellido": {"$regex": /^C/i}}).pretty().limit(1)` | ```json _id: ObjectId('659c26440337f567515c25b8'), EmpID: 3, Apellido: 'Canton', Nombre: 'Raul', 'Categoría': 'Comercial', 'Fecha contrato': '20/10/04', Oficina: 5, Extension: '102', 'Informes a': 4, 'Salario anual': 61500 ``` | Selecciona documentos donde los valores coinciden con una expresión regular especificada. |
| `$text` | `db.empleados.find({$text: {$search: "Raul"}}).pretty().limit(1)` | ```json _id: ObjectId('659c26440337f567515c25b8'), EmpID: 3, Apellido: 'Canton', Nombre: 'Raul', 'Categoría': 'Comercial', 'Fecha contrato': '20/10/04', Oficina: 5, Extension: '102', 'Informes a': 4, 'Salario anual': 61500 ``` | Realiza una búsqueda de texto. |
| `$where` | `db.empleados.find({$where: "this.Extension === '101'"}).pretty().limit(1)` | ```json _id: ObjectId('659c26440337f567515c25b7'), EmpID: 2, Apellido: 'Palacios', Nombre: 'Antonio', 'Categoría': 'Presidente', 'Fecha contrato': '26/9/03', Oficina: 1, Extension: '101', 'Informes a': null, 'Salario anual': 160000 ``` | Coincide con documentos que satisfacen una expresión JavaScript específica. |