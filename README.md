# Laravel Api Resource filterable

Provides the filtering trait for Laravel 5 Api Resources.

## Install

Via composer:

`$ composer require vskut/laravel-api-resource-filterable`

## Usage
### Resource
```php
namespace App\Http\Resources;

use vskut\laravel-api-resource-filterable\Filterable;
use Illuminate\Http\Resources\Json\JsonResource;

class UserResource extends JsonResource
{
    use Filtratable;

    public function toArray($request)
    {
        return $this->filtrateFields([
            'id' => $this->id,
            'name' => $this->name,
            'email' => $this->email,
        ]);
    }
}
```

### Collection
```php
namespace App\Http\Resources;

use vskut\laravel-api-resource-filterable\Filterable;
use Illuminate\Http\Resources\Json\ResourceCollection;

class UserResourceCollection extends ResourceCollection
{
    use Filtratable;

    public function toArray($request)
    {
        return [
            'data' => $this->processCollection($request),
        ];
    }
}
```

### Controller
```php
namespace App\Http\Controllers;

use App\Http\Controllers\Controller;
use App\Http\Resources\UserResource;
use App\User;

class UserController extends Controller
{

    public function index()
    {
        $users = User::all();
    
        return UserCollection::make($users)->only(['id', 'name', 'email']);
        return UserCollection::make($users)->except(['email']);
    }

    public function show(User $user)
    {
        return UserResource::make($user)->only(['id', 'name', 'email']);
        // return UserResource::make($user)->except(['email']);
    }
}
```


## Credits

* [Markus Lind](https://github.com/vskut)
* [All Contributors](https://github.com/vskut/laravel-api-resource-filterable/contributors)

## License

The MIT License (MIT).