# Lagerhaus API


## Pagination
Paginated requests always accept these query parameters:

||||
|-|-|-|
| `limit` | int | The maximum amount of batches to be returned |
| `page` | int | The page to return (_entry offset = (page - 1) * limit_) |

## Patching
When updating via the `PATCH` method properties can be ommitted
in order to be left unchanged.

## Deletion
When deleting there is usually no response, unless otherwise specified.

When deleting a resource that other resources depend on, the deletion
will fail unless the query parameter `force` is set to true, in which
case all dependent resources will be deleted as well. (__Note:__ This
does not apply to resources where the reference can be set to `null`.
These references will be nullified unless different behaviour is
specified.)


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


### `POST` `/regions`
Creates a new region

#### Body:
```json
{
	"name": "Eferding",
	"area": "Upper Austria",
	"level": 500
}
```

| Property | Optional |
|-|-|
| `name` | __NO__ |
| `area` | YES |
| `level` | YES |


### `PATCH` `/regions/:region_name`

#### Body:
```json
{
	"area": "Upper Austria",
	"level": 500
}
```

`area` is nullable.


### `DELETE` `/regions/:region_name`
Deletes a region


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


### `POST` `/fruit`
Creates a new fruit type, optionally with ripeness grades

#### Body:
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

| Property | Optional |
|-|-|
| `name` | __NO__ |
| `ripeness_grades` | YES |

For the properties of each of the ripeness grades, please see
`POST` `/fruit/:fruit_name/ripeness_grades` below.


### `PATCH` `/fruit/:fruit_name`
Updates a fruit type

#### Body:
```json
{
	"name": "Apples"
}
```


### `DELETE` `/fruit/:fruit_name`
Deletes a fruit type

If the fruit type has batches this operation will fail


### `POST` `/fruit/:fruit_name/ripeness_grades`
Creates a new ripeness grade for a fruit type

#### Body:
```json
{
	"name": "Grade A",
	"minimum_storage_span": 50
}
```

| Property | Optional |
|-|-|
| `name` | __NO__ |
| `minimum_storage_span` | YES |


### `PATCH` `/fruit/:fruit_name/ripeness_grades/:ripeness_grade_name`
Updates a ripeness grade for a fruit type

#### Response:
```json
{
	"name": "Grade A",
	"minimum_storage_span": 50
}
```

### `DELETE` `/fruit/:fruit_name/ripeness_grades/:ripeness_grade_name`
Deletes a ripeness grade for a fruit type



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


### `POST` `/weather`
Posts a new weather report

#### Body:
```json
{
	"year": 2019,
	"month": 6,
	"region": "Eferding",
	"rainy_days": 5,
	"sunny_days": 25
}
```

| Property | Optional |
|-|-|
| `rainy_days` | YES |
| `sunny_days` | YES |


### `PATCH` `/weather/:year/:month/:region_name`
Updates a weather report

#### Body:
```json
{
	"rainy_days": 5,
	"sunny_days": 25
}
```


### `DELETE` `/weather/:year/:month/:region_name`
Deletes a weather report
