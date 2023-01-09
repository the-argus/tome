# tome

a file format specification for D&amp;D 5e classes, items, creatures, NPCs, and
player character sheets

## goals of tome

My goals in creating the tome file format are as follows (in order of
importance):

1. Make a barebones, easily editable representation of character sheets. I can't
deal with editing PDFs or using dndbeyond any longer.

2. Keep information about a player character's class in the same place as their
character.

3. Allow players to see where stats come from. A +5 to attack may be +1 from a
fighting style, +2 proficiency, and +2 from a feature. A standard character
sheet doesn't show that breakdown.

4. Future compatibility between various D&amp;D tools, like a GUI character
creator or a combat tracker.

## specification outline

For full specifications, check out [specification.md](./specification.md)

The structure of a tome file for a character looks something like the following.
Note this is a description of the structure and an actual tome file does not
look like this.

```txt
metadata
    name ""
    player_name ""
    alignment ""
inputs {}
    classes []
    subclasses []
    background {}
    levels []
events []
    {type: "change_value", event: "hurt", value: 10}
    {type: "change_value", event: "heal", value: 7}
    {type: "change_value", event: "xp_gain", value: 100}
    {type: "effect", event: "confuse"}
    {type: "lose_effect", event: "confuse"}
decisions []
    {
        # level 1 example decisions
        initial_ability_scores {}
            strength int
            dexterity int
            constitution int
            wisdom int
            intelligence int
            charisma int
        fighting_style ""
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
    ability_modifiers {}
    ability_scores {}
    initiative_modifier int
    hp_max int
    hp_current int
    xp_current int
    inspiration bool
    languages []
    proficiencies {}
        abilities []
        equipment []
    features []
    equipment {}
```

From there, a PDF can be generated using a tool like [dungeonsheets](https://github.com/canismarko/dungeon-sheets)
