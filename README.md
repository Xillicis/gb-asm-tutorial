
# gb-asm-tutorial v2

Re-doing GB ASM Tutorial, and this time, until the end.

## Adding a translation

1.  Create a new directory under `tutorial` (e.g. `fr`)
2.  Add an entry in `_config.yml`'s `defaults` array:
    ```yaml
      - scope:
          path: "tutorial/fr"
        values:
          locale: fr-FR
      ## ADD NEW TRANSLATIONS ABOVE THIS LINE
    ```
3.  Add an entry in `_data/pages.json`:
    ```json
    "fr": {
        "name": "Français 🇫🇷",
        "pages": [
        ]
    },
    ```
4.  Start translating pages (the originals in the `_tutorial/en` directory).
    Once a page has been translated, add it to the `pages` array in `_data/pages.json` you created just above.
    Don't include the `tutorial/<lang>/` part, however!

    Begin with `part1/setup.md`, as this is the page that will be linked to by the language selection.
