# tome

a file format specification for D&amp;D 5e classes, items, creatures, NPCs, and
player character sheets

## goals of tome

My goals in creating the tome file format are as follows (in order of
importance):

1. Make a barebones, easily editable representation of character sheets. I can't
deal with editing PDFs or using dndbeyond any longer.

2. Remove redundant stats: you should not have to define, for example, both your
ability score and your ability modifiers.

3. Keep information about a player character's class in the same place as their
character. (see the [``page`` filetype](./specification.md#page) for a version
of tome which contains these elements separately)

4. Future compatibility between various D&amp;D tools, like a GUI character
creator or a combat tracker.

## specification outline

For full specifications, check out [specification.md](./specification.md)

A tome is a JSON file structured something like the following. Note this is a
description of the structure and an actual tome file does not look like this.

```txt
metadata
    name : ""
    player_name : ""
    alignment : ""
decision_trees : {}
    Archer : {}
        type : ""
            "class"
        outputs : {}
            # outputs are unique to classes
            charisma : {}
                type : ""
                    "stat"
                range : {}
                    max : int
                        20
                    min : int
                        0
            dexterity : {}
                # ... etc
        decisions : []
            {
                initial_ability_scores : {}
                    charisma : {}
                        default : int
                            10
                    # and so on...
                feat : {}
                    
                # etc ...
            }
            # a lot of stuff would go here...
    Actor : {}
        type : ""
            "feat"
        effects : []
            {
                type : ""
                    "increment_stat"
                stats : []
                    "charisma"
                # no "prompt" key, meaning the effect is always applied
            }
            {
                type : ""
                    "advantage"
                stats : []
                    "deception"
                    "performance"
                prompt : ""
                    "when trying to pass yourself off as a different person."
            }
            {
                type : ""
                    "text"
                text : ""
                    "You can mimic the speech of another person or the sounds
                    made by other creatures. You must have heard the person
                    speaking, or heard the creature make the sound, for at least
                    1 minute. A successful Wisdom (Insight) check contested by
                    your Charisma (Deception) check allows a listener to
                    determine that the effect is faked."
            }
inputs : {}
    classes : []
        "Archer"
    subclasses : []
    background : {}
    levels : []
events : []
    # this is formatted differently than the rest of this example just because
    # I didn't want to take up a ton of space
    {type: "change_value", event: "hurt", value: 10}
    {type: "change_value", event: "heal", value: 7}
    {type: "change_value", event: "xp_gain", value: 100}
    {type: "effect", event: "confuse"}
    {type: "lose_effect", event: "confuse"}
decisions : []
    {
        # level 1 example decisions
        initial_ability_scores : {}
            charisma : int
                14
            # etc...
        feat : ""
            "Actor"
        fighting_style : ""
            "Two-Weapon Fighting"
    }
    {
        # level 2 decisions...
    }
```

Using this file, you can determine what equipment your character has, features,
etc. For example, you could use the first file to build an output file like
this:

```txt
outputs
    ability_modifiers : {}
    ability_scores : {}
    initiative_modifier : int
    hp_max : int
    hp_current : int
    xp_current : int
    inspiration : bool
    languages : []
    proficiencies : {}
        abilities : []
        equipment : []
    features : []
    equipment : {}
```

From there, a PDF can be generated using a tool like [dungeonsheets](https://github.com/canismarko/dungeon-sheets)
