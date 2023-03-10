# tome filetype specifications

Tome is just a set of naming and structure conventions for JSON. So, use JSON
highlighting and linting. At the root of the JSON object is a dictionary,
containing four keys: [``metadata``](#metadata), [``inputs``](#inputs),
``events`` and ``decisions``.

## page

A ``.page`` file is a partial tome: it contains only some of the keys mentioned
in the above section. This allows for a class author to define [``decision_trees``](#decision-trees)
and distribute that as a page file for players to use in their characters.

___

## metadata

Dictionary containing the following keys and value types:

``character_name    : string``
``player_name       : string``
``alignment         : string``

___

## inputs

Dictionary containing the following keys and value types:

[``classes          : list``](#classes)
[``subclasses       : list``](#subclasses)
``background        : string``

### classes

List of dictionaries which contain keys ``name`` and ``level``, like so:

```json
{
    "classes": [
        {
            "name": "Barbarian",
            "level": 4
        }
    ]
}
```

### subclasses

A list of strings. Example:

```json
{
    "subclasses": [
        "Gloom Stalker",
        "Beastmaster"
    ]
}
```
