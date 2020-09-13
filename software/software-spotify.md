# Cache getting too large
After some time spotify stores a bunch of data under $HOME/.cache/spotify/Data or $HOME/.cache/spotify/Storage.

First quit spotify then edit $HOME/.config/spotify/prefs and add/update the following line:
```
storage.size=512
```

Then restart spotify, it will automatically shrink the cache.
