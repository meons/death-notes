# PHP Exceptions

http://www.w3schools.com/php/php_exception.asp

Example with re-throw

```php
try {
    try {
        $ki = 4000;
        $strength = 5500;
        $power = $ki + $strength;

        if ($power > 9000) {
            throw new Exception("Over 9000!");
        }

        echo '(1st block) power: ' . $power;
    } catch (Exception $e) {
        echo '(1st block) broken: ' . $e->getMessage();
        throw $e;
    }

    echo '(2nd block) power: ' . $power;
} catch (Exception $e) {
    echo '(2nd block) broken: ' . $e->getMessage();
}
```
