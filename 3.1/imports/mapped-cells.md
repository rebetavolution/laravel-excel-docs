---
pageClass: no-toc
---

# Mapped Cells

In case you have a more custom spreadsheet and only want to access specific **cells**, you can implement the `WithMappedCells` concern.

You might have a speadsheet looking like this:
-|A    |B    |
-|---- |----|
-|name | Patrick Brouwers|
-|---- |----|
1| email | patrick@maatwebsite.nl |

We can now map `name` to `A1` and `email` to `B1`. The value of those coordinates will then be available under the given array key.

```php
namespace App\Imports;

use App\User;
use Maatwebsite\Excel\Concerns\ToModel;
use Maatwebsite\Excel\Concerns\WithMappedCells;

class UsersImport implements WithMappedCells, ToModel 
{
    public function mapping(): array
    {
        return [
            'name'  => 'A1',
            'email' => 'B1',
        ];
    }
    
    public function model(array $row)
    {
        return new User([
            'name' => $row['name'],
            'email' => $row['email'],
        ]);
    }
}
```

::: warning
This concern is not meant to map **columns**, only specific **cell** reference are allowed.
:::
