

# Make a `.tar.gz` file of each directory

```bash
find . -maxdepth 1 -mindepth 1 -type d -exec tar cvzf {}.tar.gz {}  \;
```

