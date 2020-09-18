Linux has two clipboard buffers: PRIMARY and CLIPBOARD. Basic idea is that selecting text copies it to PRIMARY, it can then be pasted with a middle-click or using Shift+Insert. Copy/paste functions in most GUI applications mostly use CLIPBOARD.

Some more advanced testing:

- Copying:
  - lastpass browser extension: clipboard
  - pass: clipboard (or primary depending on config)
  - ctrl+c in firefox: clipboard and primary
  - selection in firefox: primary
  - ctrl+insert in firefox: clipboard and primary
  - ctrl+c in gedit: clipboard and primary
  - selection in gedit: primary
  - ctrl+insert in gedit: clipboard and primary
  - selection in rxvt: primary
  - selection in rxvt w/ selection-to-clipboard extension: clipboard and primary
  - ctrl+insert in rxvt: (same as selection)
- Pasting:
  - ctrl+v in firefox: clipboard
  - shift+insert in firefox: clipboard
  - ctrl+v in gedit: clipboard
  - shift+insert in gedit: clipboard
  - shift+insert in rxvt: primary
  - ctrl+alt+v in rxvt: clipboard

To check their content:
```
xclip -o -selection clipboard
xclip -o -selection primary
```

To set their content:
```
echo -n 'foo' | xclip -i -selection clipboard
echo -n 'bar' | xclip -i -selection primary
```
