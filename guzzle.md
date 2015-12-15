# Guzzle

[Guzzle official doc](http://docs.guzzlephp.org/en/latest/)

Send POST request with JSON content

```php
$client = new Client(array('base_uri' => 'http://127.0.0.1/'));
$response = client->post('new', array('json' => array()));
```
