For Linux
https://syncthing.net/

For android
https://github.com/researchxxl/syncthing-android

Install
```
sudo curl -L -o /etc/apt/keyrings/syncthing-archive-keyring.gpg https://syncthing.net/release-key.gpg
cat /etc/apt/keyrings/syncthing-archive-keyring.gpg
ls -l /etc/apt/keyrings/
echo "deb [signed-by=/etc/apt/keyrings/syncthing-archive-keyring.gpg] https://apt.syncthing.net/ syncthing stable-v2" | sudo tee /etc/apt/sources.list.d/syncthing.list
cat /etc/apt/sources.list.d/syncthing.list

sudo apt install syncthing
```

Then setup in the WebGUI
https://127.0.0.1:8384/
