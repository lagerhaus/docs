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
