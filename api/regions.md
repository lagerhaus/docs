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