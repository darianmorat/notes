## How to remove extra dependencies when uninstalling a package

After installing a package that pulls in a lot of dependencies, the correct way to remove it is NOT
using `-Rsc PKGNAME`. Instead, remove the package with `-R PKGNAME` then remove any orphaned dependencies with:

```
pacman -Qdtq | sudo pacman -Rns -
```
