# Translations

Every language is a plain UTF-8 text file in [`lang/`](../lang): English on the left, the translation on the right.

```
@code = it
@name = Italiano
Refresh now = Aggiorna ora
{name} is at {percent}% = {name} è al {percent}%
```

- **Use your own language right away:** choose *Language → Add your own language...* in the menu. It opens `%APPDATA%\WirelessBattery\lang` with `_template.txt`, which lists every phrase. Copy it to e.g. `it.txt`, fill in `@code`, `@name` and the translations, and the language appears in the menu (no restart needed). A file there with the same `@code` as a built-in language replaces its phrases, so you can also fix a single word locally.
- **Share it with everyone:** send the file as a pull request to [`lang/`](../lang). The build includes every file in that folder automatically; no code change is needed.
- Keep `{placeholders}` as they are, and add `@rtl = 1` for right-to-left scripts. Phrases left empty stay English, so a partial translation is fine.
- The `--list` and `--dump` output stays English on purpose: it is pasted into GitHub issues.
