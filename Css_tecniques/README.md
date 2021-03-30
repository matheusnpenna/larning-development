# Centralization tricks without flex and rows
````
father with: position relative
child with: position absolute
child with:
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
````
# Grow up aways proportionaly
````
father with: position relative
child with: position absolute
child with:
    height 0;
    width: 100%;
    padding-bottom: 50%, 100%, etc
````

# Translate without crash on responsive
````
    use translate with percent values
````

# Configure purgecss in gulp // Why bootstrap/css feature not working because the class is injected by js of bootstrap
````
    - Add then on scss gulp pipe
    - Add watcher to export and make gulp watch htmls
    - If any feature not working (ex: a modal show and hide) because is injected by Javascript the purge will not add css, for fix this, add find the class that not working and add then in template-*.html on diet folder for force purgecss load the class

    Examples that happen's: Bootstrap modal, bootstrap accordion, dropdowns, etc..
````