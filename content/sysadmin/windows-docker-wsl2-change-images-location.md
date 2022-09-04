# Change Docker WSL2 Images Location

## References
- https://stackoverflow.com/questions/62441307/how-can-i-change-the-location-of-docker-images-when-using-docker-desktop-on-wsl2
- https://blog.codetitans.pl/post/howto-docker-over-wsl2-location/

## Archive
- https://web.archive.org/web/20220325152401/https://blog.codetitans.pl/post/howto-docker-over-wsl2-location/


## Steps I followed with success in 2022

Mostly followed 'Coding with Titans' recipe, recommend following those steps.

1. Shutdown Docker
2. Exit all running WSL and confirm all shutdown
```powershell
PS wsl --list -v
```
3. Shutdown all WSL 'distributions' just to make sure
```sh
$ wsl --shutdown
```

2. Export (can take some time)
```powershell
PS wsl --export docker-desktop-data "D:\Docker\wsl\data\docker-desktop-data.tar"
```
3. Import
```powershell
PS  wsl --import docker-desktop-data "D:\Docker\wsl\data" "D:\Docker\wsl\data\docker-desktop-data.tar" --version 2
```
4. Restart Docker
5. Profit!

