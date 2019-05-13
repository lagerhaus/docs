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
