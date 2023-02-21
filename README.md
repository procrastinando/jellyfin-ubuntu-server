# A way to install JellyFin on ubuntu server and setup the paths locations

## 1. Install requirements:
```
sudo rm /etc/apt/sources.list.d/jellyfin.list
sudo apt install curl gnupg
sudo add-apt-repository universe
```
## 2. Add the Jellyfin repository:
```
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://repo.jellyfin.org/jellyfin_team.gpg.key | sudo gpg --dearmor -o /etc/apt/keyrings/jellyfin.gpg
```
```
cat <<EOF | sudo tee /etc/apt/sources.list.d/jellyfin.sources
Types: deb
URIs: https://repo.jellyfin.org/$( awk -F'=' '/^ID=/{ print $NF }' /etc/os-release )
Suites: $( awk -F'=' '/^VERSION_CODENAME=/{ print $NF }' /etc/os-release )
Components: main
Architectures: $( dpkg --print-architecture )
Signed-By: /etc/apt/keyrings/jellyfin.gpg
EOF
```
## 3. Install Jellyfin:
```
sudo apt update
sudo apt install jellyfin
```
## 4. Add storage permisions:
Supposing that your media files are in `/media/ubuntu/external/`:
```
sudo chown -R jellyfin /media/ubuntu/external
```
## 5. Install plugins:
After the first setup, in Dashboard/Plugins install:
* Fanart
* OpenSubtitles
* Reports
After that, restart Jellyfin:
```
sudo /etc/init.d/jellyfin restart
```
