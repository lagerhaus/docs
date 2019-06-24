## Batches

### `GET` `/batches`
List all batches

__Paginated:__ YES

#### Query Parameters:
||||
|-|-|-|
| `fruit` | string | The name of the fruit to filter the batches for |
| `month` | integer | The month to filter the batches for |
| `year` | integer | The year to filter the batches for |
| `order` | string | Can be one of: `month`, `amount`, `fruit`, `region`, `ripeness` |
| `order_desc` | boolean | If true, order descending |
| `search` | string | A string to search for |

#### Response:
```json
[
	{
		// ...batch (see batch response below)
	},
	{
		// ...batch
	},
	{
		// ...batch
	},
	// ...
]
```


### `GET` `/batches/:fruit_name/:year/:month`
Gets a single batch

#### Response:
```json
{
	"fruit_name": "Apple",
	"year": 2019,
	"month": 6,
	"amount": 300,
	"storage_date": "2019/06/12",
	"region": "Eferding",
	"ripeness": "Grade A"
}
```


### `POST` `/batches`
Creates a new batch

#### Body:
```json
{
	"fruit_name": "Apple",
	"year": 2019,
	"month": 6,
	"amount": 300,
	"storage_date": "2019/06/12",
	"region": "Eferding",
	"ripeness": "Grade A"
}
```

| Property | Optional |
|-|-|
| `fruit_name` | __NO__ |
| `year` | __NO__ |
| `month` | __NO__ |
| `amount` | YES |
| `storage_date` | YES |
| `region` | YES |
| `ripeness` | YES |


### `PATCH` `/batches/:fruit_name/:year/:month`
Updates a batch

#### Body:
```json
{
	"amount": 300,
	"storage_date": "2019/06/12",
	"region": "Eferding",
	"ripeness": "Grade A"
}
```

No properties are nullable.

#### Response:
The updated batch


### `DELETE` `/batches/:fruit_name/:year/:month`
Deletes a batch
