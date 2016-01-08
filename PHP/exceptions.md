# PHP Exceptions

http://www.w3schools.com/php/php_exception.asp

[Good explanation](http://stackoverflow.com/questions/5551668/what-are-the-best-practices-for-catching-and-re-throwing-exceptions)

[Symfony LDAP example](https://github.com/symfony/symfony/blob/582f4753a343f230fbe18b4e9a0747d48351ddfb/src/Symfony/Component/Security/Core/User/LdapUserProvider.php#L64)

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
