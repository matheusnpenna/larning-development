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