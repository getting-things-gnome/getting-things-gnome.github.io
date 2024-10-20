# python-geoclue

python-geoclue is a Geoclue python module. This module does not
implement python bindings in Geoclue. Maybe it will sometime in the
future.  
This module uses the Geoclue D-Bus API to implement a nice API for
python developers and facilitate their life.  

## Where to get it

- **Code** - You can get the code by cloning the Git repository with
  the command below. Alternatively, you can [browse the
  code](http://cgit.freedesktop.org/python-geoclue/)
  - `git clone git://anongit.freedesktop.org/git/python-geoclue`   
    mirror: `git@github.com:pcabido/python-geoclue.git`
- **Source releases** - You can get the latest tarball here:
  - [python-geoclue-0.1.0.tar.gz](http://www.paulocabido.com/soc/python-geoclue/python-geoclue-0.1.0.tar.gz)

## How to install it

Python-geoclue is available in all major distributions. Use the
application installer software for your distro to install the
python-geoclue package.

From the source it can be installed by running (this example is valid in
Ubuntu, in other distros the root access method might be different):

- `sudo ./setup.py install` (you have to install it as root)

## How to use it

There is a test file (test.py) in a folder named tests/ that is
available with the source. This file provides examples of how you can
use all or almost all the methods available.

The **API** for the existing methods is available
[here](http://www.paulocabido.com/soc/python-geoclue/docs/Geoclue.Base.DiscoverLocation-class.html).

### Example

```python
import Geoclue

# Note: this program will work in Ubuntu without
# the need to install any additional packages, but for 
# other distributions you'll need to install a suitable
# position provider. In Debian and Ubuntu you can
# add additional providers by installing the geoip-*
# packages
POS_PROVIDER = 'Ubuntu GeoIP'

location = Geoclue.DiscoverLocation()
location.init()
location.set_position_provider(POS_PROVIDER)
position = location.get_location_info()

print position['latitude']
print position['longitude']
```

