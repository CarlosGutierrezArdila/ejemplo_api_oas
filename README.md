# ejemplo_api_oas
### Requerimientos
postgres 9.5 go&beego pgmodeler
### Creacion del repo
Se debe establecer inicialmente el nombre del negocio separado por un guión bajo ( _ ) seguido del nombre del contexto.
El contexto está dado por este el siguiente dominio:
Todo el nombre debe estar en minúscula
- mid (logica de negocio ej go)
- crud (crud de la bd, api beego)
-cliente (angular)
#### branches
- dev (desarrollo)
- test (produccion pruebas)
- master (produccion definitiva)
crear rama local
```git
  git branch <feature_branch>
```
cambiarse a la rama
```git
  git checkout <feature_branch>
```
subir los cambios a la rama
```git
    git add .
    git commit -m "adding a change from the feature branch"
    git push origin <feature>
```
#### Readme
- debe decir que hace el repo
- debe decir como implementar paso a paso
- definir la licencia
#### Git ignore
para el [api beego](https://github.com/udistrital/introduccion_oas/blob/master/repositorios_institucionales/gitignore.md) 
### Modelo de datos
a desarrolar en pgmodeler para exportar
- las bases de datos tienen esquemas que se nombran por **funcionalidad** y **NO por aplicacion**
- **tablas:** siempre nombre en singular _ como separador
- **columnas:** siempre en singular, la claver se llama **id** serial o int con secuencia y su constraint **pk_tabla**
- **fk:** la columna que referencia se llama **"tablareferenciada"_id** el constraint se llama **fk_tablaquereferencia_tablareferenciada**
- **campos:** moneda numeric(20,7)  porcentajenumeric(5,4)
- Indicar la longitud del campo si el tipo de dato es character varying:
character varying(15)
- Especificar longitud y precisión del campo si el tipo de dato es Numeric:
numeric(5,2).
- **unique:** uq_<nombre_columna>_<nombre_tabla>
- **checks:** ck_<nombre_columna>_<nombre_tabla>
- **index:** <idx>_<tabla>_<campo>_<aux> aux es para diferenciarlo de otros indices.
  
  ### Uso de beego para generar api
  
  - se crea en postgres la base de datos a la que se le va a apuntar
  - si se genera sql por consola se puede exportar:
  ```sql
  psql -U postgres -d <db objetivo> -a -f <archivo>.sql
  ``` 
  - se cambia a la ruta en la que va a quedar el api, debe estar en el $GOPATH 
  - se ejecuta el comando:
  ```shell
  bee api testApi -driver=postgres -conn=postgres://MyUsuarioBD:MyPassDB@127.0.0.1/bd_oas?sslmode=disable&search_path=public
  ``` 
  - ajustar el serial en los modelos, en la carpeta generada en cada clase de models:
  ```go
   Id       int    `orm:"column(id);pk;auto"` //se añande el ;auto
  ``` 
  - [agregar el cors para consumir con el cliente, generar documentacion con swagger ](https://github.com/udistrital/introduccion_oas/blob/master/generacion_de_apis/generar_api.md)
  - para incluir los [logs](https://github.com/udistrital/introduccion_oas/blob/master/generacion_de_apis/logs_api.md) en la api de beego
  - las [respuestas de error json](https://github.com/udistrital/introduccion_oas/blob/master/generacion_de_apis/json_api.md) se deben configurar usando un script de python para refactor para que el ai responda con el error y no genere problemas con wso2 
  - si se necesita migrar la bd a otra, la estructura se puede migrar directamnete desde el api siguiendo los pasos descritos en este [repositorio](https://github.com/udistrital/introduccion_oas/blob/master/generacion_de_apis/migrar.md)
  
  
  
  
  
