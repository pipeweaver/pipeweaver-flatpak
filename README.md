# Pipeweaver Flatpak Generation

This repository is primarily a way to test an isolated Flatpak generation, as well as be the base for future flathub
contributions. If it works here, it'll work on flathub.

By Default, this will build the latest `main` revision from the [PipeWeaver](https://github.com/pipeweaver/pipeweaver)
repository.

### First time setup
Firstly, install the `flatpak-builder` package for your distribution.

Create a Python Environment to work with, then activate it:
```shell 
python -m venv ~/.python_pipeweaver/
source ~/.python_pipeweaver/bin/activate
```

Perform the First Build
```shell
flatpak-builder --repo=pipeweaver-repo --install-deps-from=flathub --force-clean build-dir io.github.pipeweaver.yml
```

Create a local flatpak remote, and install our built app to it
```shell
flatpak --user remote-add --no-gpg-verify pipeweaver-repo pipeweaver-repo
flatpak install --user pipeweaver-repo io.github.pipeweaver
```

### Future Builds
To update the installed package run the following:
```shell
source ~/.python_pipeweaver/bin/activate
flatpak-builder --repo=pipeweaver-repo --install-deps-from=flathub --force-clean build-dir io.github.pipeweaver.yml
flatpak update
```

### Cleaning Up
To remove all flatpak files, run the following:
```shell
rm -rf ~/.python_pipeweaver/
flatpak remote-delete pipeweaver-repo
rm -rf ~/.local/share/flatpak/pipeweaver-repo/
```
