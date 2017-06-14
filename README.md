# Set up host with latest flatpak

```
sudo apt-get remove flatpak
sudo add-apt-repository ppa:alexlarsson/flatpak
sudo apt update
sudo apt install flatpak
sudo apt install flatpak-builder
```

# Add SDK and runtime

```
flatpak remote-add --from gnome https://sdk.gnome.org/gnome.flatpakrepo
flatpak remote-add --from gnome-apps https://sdk.gnome.org/gnome-apps.flatpakrepo
flatpak install gnome org.gnome.Platform//3.24 org.gnome.Sdk//3.24
```

# Install and poke about in some of the standard apps

```
flatpak install gnome-apps org.gnome.gedit
flatpak run org.gnome.gedit
flatpak run --devel --command=bash org.gnome.gedit
```

# Build nip2

```
flatpak-builder --repo=nip2-repo nip2 org.vips.nip2.json
```

# Exporting the package

```
flatpak build-export repo nip2
flatpak --user remote-add --no-gpg-verify --if-not-exists nip2-repo repo
flatpak --user install nip2-repo org.vips.nip2
flatpak run org.vips.nip2
```

# Links

http://docs.flatpak.org/en/latest/

# Removed

Might not be necessary? It adds a lot of stuff. 

```
    {
      "name": "popplerdata",
      "no-autogen": true,
      "make-install-args": ["prefix=/app"],
      "sources": [
        {
          "type": "archive",
          "url": "http://poppler.freedesktop.org/poppler-data-0.4.7.tar.gz",
          "sha256": "e752b0d88a7aba54574152143e7bf76436a7ef51977c55d6bd9a48dccde3a7de"
        }
      ]
    },
```
