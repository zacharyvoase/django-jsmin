# Settings

There are a few settings which `django-jsmin` will use to figure out how to build your minified JavaScript library.

`DEBUG`
:   If this is `True`, `django-jsmin` will not (by default) minify the output
    JS. This is to help with interactive debugging during development. It can be
    overridden with the options to the command-line interface; see the output of
    `djboss jsmin --help` for more information.

`JSMIN_INPUT` (required)
:   A list of [glob][] patterns or URLs which `django-jsmin` will expand to get
    a list of JavaScript filenames. For example:
      
  [glob]: http://docs.python.org/library/glob.html
    
        JSMIN_INPUT = [
            'http://ajax.googleapis.com/ajax/libs/jquery/1.3.2/jquery.js',
            'media/js/*.js',
            'apps/*/js/*.js',
        ]
    
    First, the jQuery library is downloaded from Google’s servers. The second
    item will be expanded to get a list of the JS files in the  `media/js/`
    directory. Then, any JS files in the `js/` sub-directory of each application
    will be included. Note that if a glob doesn’t match anything, it will just
    fail silently (by returning an empty list).
    
    All relative paths in globs are first resolved. `django-jsmin` will check 
    for the following settings, in this order:
    
    *   `JSMIN_ROOT`
    *   `PROJECT_DIR`
    *   `PROJECT_ROOT`
    
    Finally, if none exist, the directory containing the settings module will be
    considered the base path for resolution.

`JSMIN_OUTPUT` (required)
:   The filename to which the minified JS data will be written. Relative output
    filenames will be resolved as specified above.

`JSMIN_ROOT` (optional)
:   See the paragraph on relative glob resolution above.

`JSMIN_PROLOG` (optional)
:   A filename (relative or absolute) which contains a piece of text to include 
    at the beginning of the minified JS file. This will usually be a comment
    containing a copyright statement or license information.
