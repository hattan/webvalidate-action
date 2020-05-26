# Web Validate Action- A GitHub Action for Invoking [Web Validate](https://github.com/retaildevcrews/webvalidate)

![License](https://img.shields.io/badge/license-MIT-green.svg)


## WebV Action Quick Start

Run a sample validation test against `microsoft.com`

```yaml
  - name: Web Validate
    uses: hattan/webvalidate@v1.0.0
    with:
        server: 'https://www.microsoft.com'
        filename: 'msft.json'
```


## Inputs

* server
  - base Url (i.e. `https://www.microsoft.com`)
  - required

* filename
  - a json test file
  - default baseline.json
  - default location ./TestFiles/

## Sample `microsoft.com` validation tests

The [msft.json](TestFiles/msft.json) file contains sample validation tests that will will successfully run against the `microsoft.com` endpoint (assuming content hasn't changed)

- note that http status codes are not specified when 200 is expected
- note that ContentType is not specified when the default of application/json is expected

### Redirect from home page

- Note that redirects are not followed

```json

{
  "Url":"/",
  "Validation":
  {
    "Code":302
  }
}

```

### home page (en-us)

```json

{
  "Url":"/en-us",
  "Validation":
  {"
    ContentType":"text/html",
    "Contains":
    [
      { "Value":"<title>Microsoft - Official Home Page</title>" },
      { "Value":"<head data-info=\"{" }
    ]
  }
}

```

### favicon

```json
{
  "Url": "/favicon.ico",
  "Validation":
  {
    "ContentType":"image/x-icon"
  }
}
```

### robots.txt

```json
{
  "Url": "/robots.txt",
  "Validation":
  {
    "ContentType": "text/plain",
    "MinLength": 200,
    "Contains":
    [
      { "Value": "User-agent: *" },
      { "Value": "Disallow: /en-us/windows/si/matrix.html"}
    ]
  }
}
```

## Contributing

This project welcomes contributions and suggestions. 