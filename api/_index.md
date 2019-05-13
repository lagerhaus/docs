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


## Overview
The API is split into four parts:
  + [__Fruit API:__](fruit.md) Information about fruit types (mostly static)
  + [__Regions API:__](regions.md) Information about regions (mostly static)
  + [__Batches API:__](batches.md) Information about sesional fruit batches
  + [__Weather API:__](weather.md) Weather reports (for each month and region)
