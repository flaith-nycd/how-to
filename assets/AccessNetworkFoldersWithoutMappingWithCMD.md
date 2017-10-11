# Access network folders with cmd commands without mapping it to a network drive (from [SuperUser](https://superuser.com/a/399885))

You have a UNC path and you want to access it under windows like `cd //NICOLAS-SPRO/linux_home`, 
but you'll have this in return:
```
The system cannot find the path specified.
```

## How to access to the UNC path (short for [Uniform Naming Convention](https://en.wikipedia.org/wiki/Path_(computing)#Uniform_Naming_Convention))?
If you use `pushd` and `popd` instead of `cd` you won't get that UNC error.

```
pushd <UNC path> will create a temporary virtual drive and get into it.
popd will delete the temporary drive and get you back to the path you were when you entered pushd.
```

Example with the UNC path __\\NICOLAS-SPRO\linux_home__:
```
E:\Projects> pushd \\NICOLAS-SPRO\linux_home\projects
```
__A temporary Z: virtual drive has been created__
```
Z:\projects> ls
40hrs/  berkeleyDB/  cron/  database/  electron/   fonts/  github/   lazarus/  lumen/  php/    purebasic/
apple/  cobol/       d/     dev/       enthalpya/  games/  laravel/  linux/    nginx/  prose/  python/
```
```
Z:\projects> popd
```
__The Z: drive has been deleted__
```
E:\Projects> 
```

Using `pushd` creates a drive mapping to the network share and then changes into a path relative to the share it creates. 
`popd` disconnects the share.
