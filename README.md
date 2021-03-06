# npdoc.py

I do a lot of work entirely in an IPython notebook and it can be annoying to switch back and forth from a browser to the command line to look up function usage.  I therefore wrote this little utility.  Given a numpy function name, it will look up the function's source on GitHub, and parse the usage comment at the top of the function.

This code requires the BeautifulSoup 4 library, which is readily pip'd.

Here's an example:

```
>> import npdoc

>> npd('meshgrid')

>> Return coordinate matrices from coordinate vectors.

   Make N-D coordinate arrays for vectorized evaluations of
   N-D scalar/vector fields over N-D grids, given
   one-dimensional coordinate arrays x1, x2,..., xn.

   .. versionchanged:: 1.9
      1-D and 0-D cases are allowed.

...
```
(Not showing the full output because there's a lot)

You can also specify to only see the first or last lines with the ```nl``` argument.  A positive argument gives the first N lines:
```
>> import npdoc

>> npd('meshgrid', nl = 4)

>> Return coordinate matrices from coordinate vectors.

   Make N-D coordinate arrays for vectorized evaluations of
   N-D scalar/vector fields over N-D grids, given
```

And a negative argument gives the last N lines:
```
>> import npdoc

>> npd('meshgrid', nl = -4)

>>  >>> y = np.arange(-5, 5, 0.1)
    >>> xx, yy = np.meshgrid(x, y, sparse=True)
    >>> z = np.sin(xx**2 + yy**2) / (xx**2 + yy**2)
    >>> h = plt.contourf(x,y,z)
```

Note:  in the case of the base NumPy functions, like ```np.array```, the source is more difficult to get to and to parse (those functions are written in C, too), so in that case, ```npd()``` will just open a browser with the formatted webpage.  If you just want to go straight to the formatted webpage anyway, just do ```npd('meshgrid', browser = True)```.
