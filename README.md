# pdf2image

This package provides an easy to work with class to convert PDF's to images.

## Requirements

You should have [Imagick](http://php.net/manual/en/imagick.setresolution.php)

## Installation

The package can be installed via composer:
``` bash
composer require tal7aouy/pdf2image
```

## Usage

Converting a pdf to an image is easy.

```php
$pdf = new Tal7aouy\PdfToImage\Pdf($pathToPdf);
$pdf->saveImage($pathToWhereImageShouldBeStored);
```

If the path you pass to `saveImage` has the extensions `jpg`, `jpeg`, or `png` the image will be saved in that format.
Otherwise the output will be a jpg.

## Other methods

You can get the total number of pages in the pdf:
```php
$pdf->getNumberOfPages(); //returns an int
```

By default the first page of the pdf will be rendered. If you want to render another page you can do so:
```php
$pdf->setPage(2)
    ->saveImage($pathToStoreImage); //saves the second page
```

You can override the output format:
```php
$pdf->setOutputFormat('png')
    ->saveImage($pathToStoreImage); //the output wil be a png, no matter what
```

You can set the quality of compression from 0 to 100:
```php
$pdf->setCompressionQuality(100); // sets the compression quality to maximum
```

You can specify the width of the resulting image:
```php
$pdf
   ->width(400)
   ->saveImage($pathToWhereImageShouldBeStored);
```

## Issues regarding Ghostscript

This package uses Ghostscript through Imagick. For this to work Ghostscripts `gs` command should be accessible from the PHP process. For the PHP CLI process (e.g. Laravel's asynchronous jobs, commands, etc...) this is usually already the case. 

However for PHP on FPM (e.g. when running this package "in the browser") you might run into the following problem:

```
Uncaught ImagickException: FailedToExecuteCommand 'gs'
```

This can be fixed by adding the following line at the end of your `php-fpm.conf` file and restarting PHP FPM. If you're unsure where the `php-fpm.conf` file is located you can check `phpinfo()`. If you are using Laravel Valet the `php-fpm.conf` file will be located in the `/usr/local/etc/php/YOUR-PHP-VERSION` directory.

```
env[PATH] = /usr/local/bin:/usr/bin:/bin
```

This will instruct PHP FPM to look for the `gs` binary in the right places.

## Testing

``` bash
composer test
```

## Changelog

Please see [CHANGELOG](CHANGELOG.md) for more information what has changed recently.

## Security

If you've found a bug regarding security please mail [tal7aouy@gmail.com](tal7aouy@gmail.com) instead of using the issue tracker.

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.
