# Package Management — Kali Linux

## apt — Advanced Package Tool

```bash
sudo apt update                   # refresh package list
sudo apt upgrade                  # update installed packages
sudo apt install packagename      # install package
sudo apt remove packagename       # remove package
sudo apt purge packagename        # remove + config files
sudo apt autoremove               # remove unused dependencies
apt list --installed              # list installed packages
apt list --installed | grep name  # check if specific package installed
```

## Order of operations — always update before installing:

```bash
sudo apt update
sudo apt install packagename
```

## Installing from .deb file

```bash
sudo apt install ./filename.deb   # recommended (handles dependencies)
sudo dpkg -i filename.deb         # alternative (no dependency handling)
sudo apt --fix-broken install     # fix dependency errors after dpkg
```

## pip — Python Package Manager

```bash
pip install packagename                           # install
pip install -r requirements.txt                   # install from file
pip install packagename --break-system-packages   # Kali workaround
```

## Key difference: apt vs dpkg

| | apt | dpkg |
|--|-----|------|
| Handles dependencies | ✅ | ❌ |
| Installs from internet | ✅ | ❌ |
| Installs from file | ✅ | ✅ |
| Recommended | ✅ | Only when necessary |