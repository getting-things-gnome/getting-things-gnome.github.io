# Installing and start using Liblarch

## Downloading liblarch

### From tarballs

[0.1 release tarballs](http://gtg.fritalk.com/publique/gtg.fritalk.com/liblarch/0.1/)

### Packages

\- Ubuntu: [dev version available in GTG's daily PPA](https://launchpad.net/~gtg/+archive/gtg-daily)

### Latest dev version

    git clone https://github.com/liblarch/liblarch

## Using liblarch in your pything application

If liblarch is not in your PATH (which is usually the case without
proper packaging), you have to add it. If the liblarch folder is on the
same level as your own application level, you can do:

```python
import sys
sys.path.append("../liblarch/")
```

there are two modules you can import: liblarch and liblarch-gtk. Thus:

```python
import liblarch
```

(which contains the objects TreeNode, Tree and ViewTree)

or

```python
import liblarch-gtk
```

(which contains the object TreeView, extending gtk.TreeView)

Liblarch has an API version number in the form "1.2". The major number
changes whenever an existing method is removed or modified. The minor
number change whenever a method is added. This means that the major
version has to match your requirement but the minor number only have to
be bigger or equal to the number you've used during your development.

There's a method is_compatible() for that. You can also access the
current liblarch API version with "api".

```python
import liblarch
version_required = "1.0"
print "current liblarch version: %s" %liblarch.api
print "Compatibility: %s" %liblarch.is_compatible(version_required)
```

