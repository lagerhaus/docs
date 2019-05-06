# Lagerhaus API


## Pagination
Paginated requests always accept these query parameters:
||||
|-|-|-|
| `limit` | int | The maximum amount of batches to be returned |
| `page` | int | The page to return (_entry offset = (page - 1) * limit_) |


## Batches

### `GET` `/batches`
List all batches

__Paginated:__ YES

#### Query Parameters:
||||
|-|-|-|
| `fruit` | string | The name of the fruit to filter the batches for |
| `month` | string | The month to filter the batches for |
| `order` | string | Can be one of: `month`, `amount`, `fruit`, `region`, `ripeness` |
| `order_desc` | boolean | If true, order descending |
| `search` | string | A string to search for |

`month` is in the form of `2019/06`. It can also just be a year
(without a slash), in which case all batches for that year will be
returned.

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


## Regions

### `GET` `/regions`
Lists all regions

__Paginated:__ NO


### `GET` `/regions/:region_name`

#### Response:
```json
{
	"name": "Eferding",
	"area": "Upper Austria",
	"level": 500
}
```



## Fruit

### `GET` `/fruit`
Lists all fruit types

__Paginated:__ NO


### `GET` `/fruit/:fruit_name`
Gets information about a specific fruit type

#### Response:
```json
{
	"name": "foo",  // The name of the fruit
	"ripeness_grades": [
		{
			"name": "Grade A",  // The name of the ripeness grade
			"minimum_storage_span": 50
		}
	]
}
```

`minimum_storage_span` is the minimum amount of days each fruit needs
to spend in storage to reach the specific ripeness grade.



## Weather

### `GET` `/weather/:year/:month`
Lists the weather reports for a specific time

__Paginated:__ YES

__This URL can be shortened to apply a different filter:__
|||
|-|-|
| `/weather` | Lists all weather reports, ever |
| `/weather/:year` | Lists all weather reports in a specific year |
| `/weather/:year/:month` | Lists all weather reports in a specific year and month |

#### Response:
```json
[
	{
		// ...weather report (see below)
	},
	// ...
]
```


### `GET` `/weather/:year/:month/:region_name`
Gets the single weather report for the specified year, month and region

#### Response:
```json
{
	"year": 2019,
	"month": 6,
	"region": "Eferding",
	"rainy_days": 5,
	"sunny_days": 25
}
```
