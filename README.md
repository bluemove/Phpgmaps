## Phpgmaps
A none CI implementation of BIOINSTALL's [CodeIgniter library](http://github.com/BIOSTALL/CodeIgniter-Google-Maps-V3-API-Library).

---

I found this library to be incredibly useful when I was working in CodeIgniter. However a little bit of work needed to be done to use it in a Laravel project. I can't take any of the credit for the actual "heavy lifting" going on in the class.

---

[![Latest Stable Version](https://poser.pugx.org/appitventures/phpgmaps/v/stable.svg)](https://packagist.org/packages/bluemove/phpgmaps)
[![Total Downloads](https://poser.pugx.org/appitventures/phpgmaps/downloads.svg)](https://packagist.org/packages/bluemove/phpgmaps)
[![Monthly Downloads](https://poser.pugx.org/appitventures/phpgmaps/d/monthly.png)](https://packagist.org/packages/bluemove/phpgmaps)
[![License](https://poser.pugx.org/appitventures/phpgmaps/license.svg)](https://packagist.org/packages/bluemove/phpgmaps)

#Installation

Add this package in your `composer.json` and update composer.

For Laravel 4.\* use the below line. Please be aware that I only have the time to support the latest stable release of Laravel. So any future updates (features, security, or otherwise) will not be applied to the branch for laravel4 compatibility

```php
"bluemove/phpgmaps": "dev-master"
```


After updating composer, add the ServiceProvider to the providers array in `app/config/app.php`

```php
'bluemove\Phpgmaps\PhpgmapsServiceProvider',
```

And the Facade

```php
'Gmaps' => 'bluemove\Phpgmaps\Facades\Phpgmaps',
```

### Example 
The following code will prompt the user for access to their geolocation and then creates a map centered on their lat/lng

    Route::get('/', function(){
        $config = array();
        $config['center'] = 'auto';
        $config['onboundschanged'] = 'if (!centreGot) {
                var mapCentre = map.getCenter();
                marker_0.setOptions({
                    position: new google.maps.LatLng(mapCentre.lat(), mapCentre.lng())
                });
            }
            centreGot = true;';
            
        Gmaps::initialize($config);

        // set up the marker ready for positioning
        // once we know the users location
        $marker = array();
        Gmaps::add_marker($marker);

        $map = Gmaps::create_map();
        echo "<html><head><script type="text/javascript">var centreGot = false;</script>".$map['js']."</head><body>".$map['html']."</body></html>";
    });

