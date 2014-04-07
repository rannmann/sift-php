# Sift Science PHP Bindings

## Installation
### With Composer
1. Add siftscience/sift-php as a dependency in composer.json.

    ```
    "require": {
        ...
        "siftscience/sift-php" : "1.*"
        ...
    }
    ```

2. Run `composer update`.
3. Now `SiftClient` will be autoloaded into your project.


    ```
    require 'vendor/autoload.php';

    $sift = new SiftClient('my_api_key');
    ```

### Manually
1. Download the latest release.
2. Extract into a folder in your project root named "sift-php".
2. Include `SiftClient` in your project like this:

    ```
    require 'sift-php/lib/Services_JSON-1.0.3/JSON.php';
    require 'sift-php/lib/SiftRequest.php';
    require 'sift-php/lib/SiftResponse.php';
    require 'sift-php/lib/SiftClient.php';

    $sift = new SiftClient('my_api_key');
    ```

## Usage
### Track an event
Here's an example that sends a `$transaction` event to sift.

```
$sift = new SiftClient('my_api_key');
$response = $sift->track('$transaction', array(
    '$user_id' => '23056',
    '$user_email' => 'buyer@gmail.com',
    '$seller_user_id' => '2371',
    '$seller_user_email' => 'seller@gmail.com',
    '$transaction_id' => '573050',
    '$currency_code' => 'USD',
    '$amount' => 15230000,
    '$time' => 1327604222,
    'trip_time' => 930,
    'distance_traveled' => 5.26,
));
```
### Label a user as good/bad

```
$sift = new SiftClient('my_api_key');
$response = $sift->label('23056', array(
    '$is_bad' => true,
    '$reasons' => array('$chargeback')
));
```
### Get a user's score

```
$sift = new SiftClient('my_api_key');
$response = $sift->score('23056');
$response->body['score']; // => 0.030301357270181357
```


## Contributing
Run the tests from the project root with [PHPUnit](http://phpunit.de) like this:

```
phpunit --bootstrap vendor/autoload.php test/SiftClientTest
```


## License
MIT
