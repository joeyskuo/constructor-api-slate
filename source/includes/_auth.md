# Authentication

> Example request with key query parameter:

```javascript

const url = `https://service.cnstrc.com/browse/style_group/Bohemian?key=api-public-key`;

fetch(url).then((response) => {
  // …
});

```

CIO expects the API key to be included as a query parameter in all requests

`GET https://service.cnstrc.com/browse?`**`key=publicKeyHere`**

<aside class="notice">
You must include the <code>key</code> query parameter
</aside>