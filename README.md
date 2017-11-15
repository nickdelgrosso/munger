# munger

This python package prefixes all your variable names with another name (underscore, by default).  It was an idle experiment to play with python's importlib, inspect standard modules and to get a deeper understanding of the Python language model.

*THIS IS FOR DEMONSTRATION PURPOSES ONLY.*

Please note that this package breaks all of your variable names, producing some fairly tough-to-debug errors.  As such, it could be considered malware.  So be careful with it!

## Lessons learned

The key function here is the *munge()* function.  Here's the code for the lazy::
```python
    import importlib
    def munge(namespace='__main__', prefix='_'):
        """Precedes all names in 'namespace' with 'prefix'."""
        module = importlib.import_module(namespace)
        for name, val in vars(module).items():
            if len(name) >= prefix) and name[:len(prefix)] != prefix:
                setattr(module, prefix + name, val)
                delattr(module, name)
```

Originally, I thought the globals() or inspect module would be needed, especially to back out to the calling namespace (the __main__ namespace being the most interesting), but that turned out to be unnecessary, since the namespace can be directly imported from anywhere.  That key realization made it all simple!


## More devious ideas

If you wanted things to be even more confusing, why leave it at just prefixes?  Python's dictionary-based naming system would let you, say, randomly reassign every variable name to each others' values, producing random and extremely hard-to-debug errors!   Or why not make every number a string?  Or add an auto-importing line to the Python startup file, so all future Python code is munged?  Yep, there are certainly a multitude of potential problems that could be created...

## Explicit is better than Implicit

Python is a wonderful language that gives you the flexibility to do what you will, with a community that encourages readable code as part of good practices.  As Python becomes more popular, more malicious code is appearing in the repository.  Be sure to vet out the packages you are using, and start new projects in virtual environments in order to keep from breaking your system.  Finally, we need even more automated tools to keep malicious code from entering the community in the first place.  As always, work is ongoing.  Anyway, keep up the great work! :-)