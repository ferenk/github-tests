<div align="center" class="not_on_gh-pages">
  <br>
  <a href="https://github.com/ferenk/obsidian-tokenz">
    <img alt="tokenz poster" src="https://ferenk.github.io/github-tests/docs/img/tokenz_poster.jpg" width="830">
  </a>
</div>
<div>
</div>
<div style="text-align: center;">
<img alt="GitHub manifest version" src="https://img.shields.io/github/manifest-json/v/ferenk/obsidian-tokenz?style=flat&logo=github" height=32px>
<img alt="Obsidian downloads" src="https://img.shields.io/github/downloads/ferenk/obsidian-tokenz/main.js?style=flat&logo=obsidian" height=32px>
</div>
<div align="center" class="not_on_gh-pages">
  <h1>Obsidian / Tokenz</h1>
</div>

Use your favourite symbols, special characters and frequently used snippets with ease!
You can insert it to your document using short code mappings:

- **Built-in** short code maps:  
	- **emojis**, like ``:smile:`` 🙂 or ``:wink:`` 😉 (1800+ installed by default),  
		and the classic, good old  
	- **smileys**, like **``:-)``** 🙂, **``8-D``** 😎 (installed by default)
- **User defined** short code maps. You can use any format you'd like:
	``/prog-50``  ▋, ``.success`` 🏆,  ``!movie`` 🎥
	For further explanation and a short configuration guide see [2. User defined code maps](#2-user-defined-code-maps) .  

Demo video showing the features:<br>
<img align="center" src="https://github.com/user-attachments/assets/6e20d9ea-bb23-4082-ba0b-686987a4d989">
<br><br><br>
## Configuration

### 1. Installation
#### 1.1 From Obsidian's Community plugin collection
**Suggested method**, the easiest way to install:
1. Open settings (Gear icon)
2. Click **Options / Community plugins / Community plugins, Browse...** button
3. Search for "Tokenz"
4. Install and Enable
5. Start typing some pre-installed token, e.g. ``:)``
#### 1.2 From sources
It's also possible to install it manually:  
1. Get the sources: ``git clone https://github.com/ferenk/obsidian-tokenz``  
2. Init the sources folder: ``cd obsidian-tokenz; npm install``  
3. Build the plugin: ``npm run build``  
4. Create a folder in your Obsidian wallet: ``mkdir <your wallet's path>/.obsidian/plugins/tokenz``  
5. Copy the plugin's files **main.js**, **manifest.json**, **styles.css** into the folder just created  
6. Restart Obsidian and enable the "Tokenz" plugin  
7. Start typing ``:)``

### 2. User defined code maps
It's easy to define your own code maps. You can choose any format for your short codes (tokens). But you can also mix different formats (see 4.).  
1. Choose a name for your code map, e.g **my code map**  
2. Create a folder named **data** in <Your wallet's path>/.obsidian/plugins/tokenz
3. Create an index file of the code maps in the data folder just created. It's name must be **maps.lst**.  
   Example ***data/maps.lst:***
   ```
   my_code_map.json
   ```
4. Create your own code map file. Its structure is very simple, for example here are are the codes for our sample paragraph<br>(it also demonstrates the mixed usage of different token formats)  
   Example ***my_code_map.json*** to enter the sample lines
   ```
   {
       "/prog-20":         "▎",
       "/prog-50":         "▋",
       "/prog-80":         "▉",
       ".success":        "🏆",
       ".idea":           "💡",
       "|tv_episode|":    "📺",
       "!movie":          "🎥"
   }
   ```

And now you can insert these symbols to your document this way:

| Format          | Short code example                           |   Result               |
| --------------- | -------------------------------------------- | ---------------------- |
| IRC style       | ``/prog-20 20%, /prog-50 /prog-90 90%``      | => ▎ 20%, ▋ 50%, █ 90% |
| CSS class       | ``.idea, .success``                          | => 💡, 🏆              |
| Any crazy style | ``\|tv_episode\|``                           | => 📺                  |

### 3. Settings
#### Highlighting
Token text highlighting is enabled for all kind of code blocks by default, but you enable/disable any sets of block names with rulesets.
Format of these rulesets:
```{+|-}<block name pattern>, ...```

The rules are separated by commas, and all rules are applied in the order of appearance.
You can use the wildcard character ``*`` to match any character sequence (even "") and the ``?`` character to match any single character.
Some examples:

- ``+*``: Enable highlighting for all block names
- ``-?*``: Disable highlighting for named blocks but still enable it for unnamed blocks (``?*`` means: a name with at least one character)
- ``-*, +html``: Enable html block highlighting, all others are disabled
- ``-*, +*js*``: Enable highlighting for all block names containing "js" (e.g 'dataviewjs' blocks), all others are disabled

And a final example with the explanation of how it is applied:

``-*, +*js*, +javascript, -*json*``

0. (<font color="green">``+*``</font>) - (Hidden rule)This is the default starting state, every evaluation starts with this. It enables highlighting for all block names.
  This is a practical starting state for negative rules.
1. <font color="red">``-*``</font> - You can use this rule to start with the opposite starting state. Now all block names are disabled, even the empty ones (use ``-?*`` to keep them enabled).
  This is ideal for positive rules.
2. <font color="green">``+*js*``</font> - This rule re-enables highlighting for all block names containing "js"
3. <font color="green">``+javascript``</font> - Enable "javascript", too
4. <font color="red">``-*json*``</font> - This rule disables highlighting for all block names containing "json"

So finally the <font color="red">empty block name</font> will be *disabled*, <font color="green">"**js**"</font> and <font color="green">"dataview**js**"</font> (for example) will be *enabled*, <font color="green">"**javascript**"</font> will be *enabled*, too.  But <font color="red">"**json**"</font> will be *disabled*.
Note that the order of the rules is important. Rule 4 has to be after rule 2, because *"json"* more specific than *"js"*, so only the rule with *"js"* would erase the effect of the *"json"* rule.

