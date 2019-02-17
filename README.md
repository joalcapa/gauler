# Gauler
Api standar Rest --

### Creando proyecto Gauler

```
composer create-project joalcapa/gauler
```

# Rutas del modelo 
Gauler establece un criterio para habilitar o no el acceso a un determinado modelo, en el 
caso de que desees que el modelo heroes sea alcanzable por el endpoint heroes/ para ejecutar cualquier
operacion CRUD, solo basta con agregarlo al metodo Rest de la siguiente manera:

`` php

// routes/rest.php

<?php

Rest::Model('heroes');

```

De esta manera, al recibir Gauler una solicitud cuya uri este compuesta por el prefijo 
heroes/, se iniciara una busqueda del modelo por medio del metodo Rest, y ejecutara la logica correspondiente,
en caso de no estar declarado el modelo en el metodo Rest, Gauler arrojara el codigo http 404 de recurso no encontrado.

# Gaulerium CLI
Gaulerium es una interfaz de linea de comandos capaz de crear modelos, controladores,
migraciones, entre otras cosas.

## crear modelo
Siendo Gauler una api REST, el modelo debe tener concordancia con el endpoint objetivo, ejemplo: para el 
uri: /heroes/{id} el modelo asociado es: HeroesModel, 
para crear un modelo, gaulerium necesita el nombre del modelo, de manera opcional
puedes especificar los atributos del modelo.
```
php gaulerium createModel heroe [attr:TypeAttrQ::TYPE,....,attr:TypeAttrQ::TYPE]
```

El resultado es la creacion de una nueva clase en el directorio api/models del proyecto.

``` php
// api/models/HeroesModel.php
<?php

namespace Gauler\Api\Models;

use Joalcapa\Fundamentary\App\Models\BaseModel as Model;

class HeroesModel extends Model {

	public static $model = 'Heroes';

	protected $tuples = [
		'name',
		'powerType',
	];

	protected $hidden_tuples = [
	];
}
```

El comando createModel recibe el nombre del modelo en singular, estableciendo la creacion del modelo
en plural como (nombre en singular)sModel, el nombre de la tabla asociada al modelo tambien debe estar en plural,
si deseas eliminar esta convencion, puedes especificar directamente en el modelo, el nombre de la tabla a la 
cual el modelo apunta.

#### TypeAttrQ
Gauler establece diferentes tipos de datos para los atributos de un modelo mediante la clase [TypeAttrQ](https://github.com/joalcapa/Elementary/blob/master/src/Generics/TypeAttrQ.php), entre los mas
utilizados tenemos:

``` php
TypeAttrQ::STRING;
TypeAttrQ::INTEGER;
TypeAttrQ::DOUBLE;
TypeAttrQ::BOOLEAN;
TypeAttrQ::FLOAT;
```

#### creacion del modelo con su migracion
Si el modelo se crea con sus atributos, Gauler creara el correspondiente archivo de migracion asociado al modelo. 
       
## crear controlador
Por defecto Gauler ejecuta un proceso CRUD automatico cuando no existe un controlador asociado al modelo, 
en caso de que desees añadir logica en algun proceso de operacion CRUD, puedes optar por la creacion de un 
controlador, podras sobreescribir el metodo Rest que desees,
para crear un controlador, gaulerium necesita el nombre del controlador asociado al modelo.
```
php gaulerium createController heroe
```

El resultado es la creacion de una nueva clase en el directorio api/controllers del proyecto.

``` php
// api/controllers/HeroesController.php
<?php

namespace Gauler\Api\Controllers;

class HeroesController extends Controller {

	/**
	* @param  \Fundamentary\Http\Interactions\Request\Request  $request
	* @return  array
	*/
	public function index($request) {
	}


	/**
	* @param  $id
	* @return  array
	*/
	public function show($id) {		
	}


	/**
	* @param  \Fundamentary\Http\Interactions\Request\Request  $request
	* @return  array
	*/
	public function store($request) {		
	}


	/**
	* @param  $id
	* @param  \Fundamentary\Http\Interactions\Request\Request  $request
	* @return  array
	*/
	public function update($id, $request) {		
	}


	/**
	* @param  $id
	* @return  array
	*/
	public function destroy($id) {		
	}
}
```

Para que la busqueda del controlador asociado al modelo sea exitosa, el controlador debe tener concordancia con el nombre del modelo,
ejemplo: para el modelo: HeroesModel, el controlador asociado es: HeroesController

## crear migracion
Para crear un archivo de migracion asociado a un modelo, gaulerium necesita el nombre del modelo, de manera opcional
puedes especificar los atributos del modelo.
```
php gaulerium createMigration heroe [attr:TypeAttrQ::TYPE,....,attr:TypeAttrQ::TYPE]
```

El resultado es la creacion de una nueva clase en el directorio database/migrations del proyecto, notaras
que en el nombre del archivo se antepone la fecha en la cual fue creada la migracion en el formato TimesTamp, esto es necesarios para que
Gauler tenga un control de las migraciones realizadas.

```
1550349238HeroesMigration.php
```

``` php
// database/migrations/HeroesMigration.php
<?php

namespace Gauler\Database\Migrations;

use Joalcapa\Elementary\Generics\TypeAttrQ as TypeAttrQ;
use Joalcapa\Elementary\Migrations\BaseMigration as Migration;

class HeroesMigration extends Migration {

	public $attributes = [
		'name' => TypeAttrQ::STRING,
		'power' => TypeAttrQ::STRING,
	];
}
```

## migrar a la base de datos
Si deseas migrar a la base de datos bastara con ejecutar el siguiente comando,
de esta forma Gauler ejecutara las migraciones almacenadas, de manera opcional puedes realizar la
migracion de un solo modelo en la base de datos.

```
php gaulerium migrate [nameModel]
```