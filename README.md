# estados-municipios-localidades


Para instalar en laravel crear la migracion estados 

php artisan make:migration create_states_table

## 1. Crear la Migración

Para crear la migración de la tabla `states`:

```bash

    public function up()
    {
        Schema::create('states', function (Blueprint $table) {
            $table->id(); // ID autoincremental
            $table->string('key', 10); // Clave del estado
            $table->string('name'); // Nombre del estado
            $table->timestamps(); // Timestamps para created_at y updated_at
        });
    }




```

php artisan migrate

## 2. Crear el modelo

```bash
class State extends Model
{
    use HasFactory;

    protected $fillable = ['key', 'name'];
}

```

## 3. Crear el seeder
php artisan make:seeder StateSeeder


```bash

  public function run()
    {

        $path = File::get("database/data/states.json");
        $data = json_decode($path);
        foreach ($data as $obj) {
            State::create(array(
                'key' => $obj->key,
                'name' => $obj->name,
            ));
        }
    }

```

## 4. Ejecutar el Seeder

php artisan db:seed --class=StateSeeder



