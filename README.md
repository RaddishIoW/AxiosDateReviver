# AxiosDateReviver

A simple [AxiosTransformer](https://axios-http.com/docs/req_config) utility to revive dates from JSON data.

Any JSON returned that has a key containing "date" or "time" will be tested against a regex for conversion to a date object.

## Usage

```js
import axios from 'axios'
import dateTransformer from 'axios-date-reviver'

axios.defaults.transformResponse = [dateTransformer]
```

then use axios:

```js
const res = await axios.get('https://someserver.net/api/endpoint/dates/')
```

## Example

For the data:

```json
{
  "items": [
    {
      "name": "Item 1",
      "id": "1",
      "dateAdded": "2012-04-23T18:25:43.511Z"
    },
    {
      "name": "Item 2",
      "id": "2",
      "dateAdded": "2012-04-23T18:25:43.511Z",
      "dateModified": "2012-04-30T13:20:21.323Z",
      "timeRequested": "2019-07-06T14:28:42.398Z"
    }
  ]
}
```

the `dateAdded`, `dateModified` and `timeRequested` fields would be converted to `Date` instances.

## Format

Dates are tested against the following Regex, which detects dates in the **ISO 8601** format.

`/[+-]?\d{4}(-[01]\d(-[0-3]\d(T[0-2]\d:[0-5]\d:?([0-5]\d(\.\d+)?)?[+-][0-2]\d:[0-5]\dZ?)?)?)?/`

For more info on JSON date formats, see [this Stackoverflow question](https://stackoverflow.com/questions/10286204/what-is-the-right-json-date-format).
