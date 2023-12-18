---
title: "Heaps Good Servers - Valheim Server Instructions"
date: 2023-12-02T13:16:04+10:30
toc: true
draft: false
tags: ['heaps good servers', 'valheim', 'games', 'server']
---
## Foreword

This guide serves to document how to set up Valheim with Valheim Plus and connect to the HGS Valheim Server

## Updates

If Valheim updates and stops working with Valheim Plus, check [here](https://github.com/Grantapher/ValheimPlus/releases) for newer versions (alpha and beta releases)
For Windows, you want to download the `WindowsClient.zip` file and for Steam Deck / Linux you want `UnixClient.zip`.

## Windows

1. Install Valheim
2. Download this: https://github.com/Grantapher/ValheimPlus/releases/latest/download/WindowsClient.zip
3. Extract it and move the extracted files to the Valheim directory
    - This directory is usually in `C:\Program Files(x86)\Steam\steamapps\common\Valheim`
    - If it's not there, open Steam, click Valheim > Gear icon > Manage > Browse Local Files
4. Launch the game, you should see the logo says "Valheim Plus", if not, you've done the above wrong
    - Troubleshooting 1: Do not copy the parent folder into that directory if it made one (if it did, it's probably called `WindowsClient`), you want the files inside it (the ones that are like `winhttp.dll` and `doorstop_config.ini` etc.)
5. Navigate to Multiplayer > Community - the server is called `HGS Valheim 01`

## Some Features

* First Person
    - activate with F10
* Advanced Building Mode
    - activate with F1
    - exit with F3
* Advanced Editing Mode
    - activate with Numpad 0
    - reset rotation and position with F7
    - abort with F8
    - confirm placement with Numpad Enter
* Camera Shake removed
* Teleport Prevention Disabled
* Map Progression Shared
* Player Locations on Minimap forced
* Free Placement Rotation
    - Rotate Y-axis with Left Alt
    - Rotate X-axis with C key
    - Rotate Z-axis with V key

## Mods

HGS Valheim uses the following mods:

* PlantEverything
* Clock
* Better Equipment and Quickslots

These mods can be downloaded from [here](https://drive.google.com/drive/folders/16zlHD82SPbPuU3AsSAHgPJRubU_Q6-md?usp=drive_link)

To install them, paste the files in `<valheim-install-directory>/BepInEx/plugins`

## For Admins

To control the server, go to https://valheim01.heapsgoodservers.com - message me for log in details

## Steam Deck

### Setting up SSHD on Steam Deck (recommended!)

1. On the Steam Deck, go to Desktop Mode
2. Open Konsole and run `passwd` to set a password for the `deck` user
3. Run the following: `sudo systemctl start sshd` (you may be prompted for your new password)
4. Run the following to make it so ssh is enabled whenever the steam deck is powered on: `sudo systemctl enable sshd`

### Connecting to Steam Deck via SSH (also recommended!)

1. Open a terminal (Windows or any other OS)
2. Run `ssh deck@steamdeck`, enter password set up in previous section
3. You're in (sunglasses emoji)

### Configuring Valheim+ (assumes Valheim is installed on Internal Storage rather than SD Card)

1. Install Valheim
2. Start a console session either via ssh (see above) or using Konsole on the Deck itself
3. Download Valheim Plus by running the following:

```sh
curl -OJL https://github.com/Grantapher/ValheimPlus/releases/latest/download/UnixClient.zip
```

4. Extract the zip and enter the directory by running the following:

```sh
mkdir vplus && unzip UnixClient.zip -d ./vplus && cd ./vplus
```

5. Run the following to copy V+ to your Valheim install directory:

```sh
cp -r . /home/deck/.steam/steam/steamapps/common/Valheim
```

6. Fix permissions on the files by running (Note: You may be asked for your password):

```sh
cd /home/deck/.steam/steam/steamapps/common/Valheim && sudo chmod 777 ./start_game_bepinex.sh
```

7. On your Steam Deck, navigate to Valheim > Gear icon > Properties
8. Under Launch arguments, if the option "Ask when starting game" is shown, click this and change to "Play Valheim"
9. In the text box underneath, type the following: `./start_game_bepinex.sh; echo %command%`
10. Play (you should see Valheim Plus on the title screen if it worked, otherwise you messed up somewhere)

## Epic Loot

Epic Loot is a mod that adds an RPG-like loot table to the game

The server and all clients are required to have it, and it's dependencies installed

> Note: this does not work from patch Hildir's Request onwards, will update if it's ever fixed

### Windows

1. Download this: https://github.com/RandyKnapp/ValheimMods/releases/download/v0.9.9/RandyKnapp-EpicLoot-0.9.9.zip
2. Create a folder in your BepInEx plugins directory (most likely `C:\Program Files (x86)\Steam\steamapps\common\Valheim\BepInEx\plugins`) called `EpicLoot`
3. Move the contents of the `files` directory to this newly created folder

### Steam Deck

1. Run the following to download and install the mod:

```sh
cd ~ && curl -OJL https://github.com/RandyKnapp/ValheimMods/releases/download/v0.9.9/RandyKnapp-EpicLoot-0.9.9.zip && unzip RandyKnapp-EpicLoot-0.9.9.zip -d epicloot && cd epicloot && cd files && mkdir /home/deck/.steam/steam/steamapps/common/Valheim/BepInEx/plugins/EpicLoot && cp -r . /home/deck/.steam/steam/steamapps/common/Valheim/BepInEx/plugins/EpicLoot && cd ~
```