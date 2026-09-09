---
icon: comment
order: 70
---

# Adjustment Notes

Adjustment Notes is a text field in the Content tab. Type what you want changed in plain English and press **Give me the Signs**; the whole street re-rolls to match. Each sign's card has its own Note field with an Apply button, for that sign only. The status bar reports what was applied and what was not understood; nothing is guessed. Adjustment Notes runs entirely on your machine, with no account and no connection. The same seed and the same note always give you the same signs.

!!!info What a note does
A note changes how likely things are across the street. To force a value on every sign, use an [Advanced row](advanced.md) or a [VEXpression](vexpression.md).
!!!

## Examples

Some notes that work, from single words to whole sentences; the full vocabulary is below.

**One word or two**

- `no icons`
- `no yellow`
- `no cables`
- `no flicker`
- `no arrows`
- `dimmer`
- `brighter`
- `rivets`
- `dark metal`
- `chunky tube`
- `hairline tube`
- `plain signs`
- `busier signs`
- `only bars`
- `english only`
- `pristine signs`
- `run down signs`
- `flickering signs`

**Style and lettering**

- `open frame signs`
- `oval signs`
- `framed signs`
- `two tone signs`
- `one word names`
- `possessive names`
- `mostly yellow`
- `crank the teal`
- `do not use red`
- `steer clear of pink`
- `avoid script fonts`
- `more stencil fonts`
- `more japanese signs`
- `only 1950s style names`
- `real sounding names`
- `one colour per sign`
- `no background decor`

**Amounts and combinations**

- `more diners and hotels`
- `neither bars nor diners`
- `a bit more decor`
- `much fewer bars`
- `could we have more bars`
- `i would like fewer diners`
- `more bars, fewer diners, all in red`

**Aimed at part of the street**

- `yellow on the bars`
- `the big signs in red`
- `red on every other sign`
- `warmer at this end`
- `run down on the rooftop signs`
- `paint the theatres yellow`
- `1960s era for the karaoke places`
- `brighter bars, dim everything else`

## Scopes need an instruction

Scopes on their own do nothing. Words like "big signs", "the rooftop ones" or "every other sign" only apply once you pair them with an instruction:

```text
red on the big signs
```

Exceptions work the same way:

```text
yellow everywhere except the bars
```

## Adjustment Notes - supported vocabulary

Every word below is recognised. Words are grouped by what they change.

### How much

Any of these sets the strength of a clause.

`additional` · `all` · `avoid` · `banish` · `barely` · `boost` · `bunch` · `chiefly` · `crank` · `curb` · `curtail` · `cut` · `cuts` · `delete` · `ditch` · `don't` · `dont` · `downplay` · `drop` · `drops` · `eliminate` · `entirely` · `every` · `exclude` · `exclusively` · `extra` · `fewer` · `forget` · `hardly` · `heaps` · `heavy` · `increase` · `just` · `kill` · `largely` · `lean` · `leaning` · `less` · `loads` · `lose` · `lots` · `mainly` · `many` · `more` · `mostly` · `neither` · `never` · `nix` · `no` · `none` · `nor` · `not` · `nothing` · `omit` · `only` · `overwhelmingly` · `plenty` · `predominantly` · `primarily` · `principally` · `prune` · `purely` · `purge` · `push` · `rare` · `rarely` · `reduce` · `remove` · `sans` · `scrap` · `seldom` · `skip` · `skips` · `sole` · `solely` · `sparing` · `sparingly` · `strictly` · `tons` · `trim` · `without` · `zero`

### Stronger / weaker

Scale whatever strength the words above chose ("a bit more", "way more").

`absolutely` · `completely` · `considerably` · `extremely` · `far` · `fractionally` · `gently` · `hugely` · `marginally` · `massively` · `max` · `maximum` · `mildly` · `much` · `properly` · `really` · `seriously` · `slight` · `slightly` · `somewhat` · `subtly` · `totally` · `utterly` · `very` · `way` · `wildly`

### Business types

`adult` · `arcade` · `arcades` · `auto` · `automotive` · `bakeries` · `bakery` · `bar` · `barbecue` · `barber` · `barbers` · `bars` · `bbq` · `books` · `bookstore` · `bookstores` · `bowling` · `burlesque` · `cafe` · `cafes` · `cantina` · `car` · `cars` · `casino` · `casinos` · `chinese` · `cinema` · `cinemas` · `club` · `clubs` · `coffee` · `corporate` · `corporations` · `corps` · `diner` · `diners` · `garage` · `garages` · `gas` · `gym` · `gyms` · `hotel` · `hotels` · `jazz` · `karaoke` · `laundromat` · `laundromats` · `laundry` · `liquor` · `media` · `mexican` · `motel` · `motels` · `nightclub` · `nightclubs` · `noodle` · `noodles` · `pawn` · `pho` · `pizza` · `pizzeria` · `pub` · `pubs` · `ramen` · `records` · `seafood` · `strip` · `stripclub` · `stripclubs` · `taco` · `tacos` · `tattoo` · `tattoos` · `tech` · `theater` · `theaters` · `theatre` · `theatres`

### Trade groups

`companies` · `company` · `drink` · `drinking` · `eateries` · `eating` · `entertainment` · `food` · `lodging` · `nightlife` · `restaurant` · `restaurants` · `retail` · `service` · `services` · `shop` · `shops` · `store` · `stores`

### Colours

`amber` · `amethyst` · `apricot` · `aqua` · `aquamarine` · `azure` · `blue` · `blush` · `chartreuse` · `cherry` · `coral` · `crimson` · `cyan` · `emerald` · `fuchsia` · `garnet` · `gold` · `golden` · `grape` · `green` · `honey` · `hotpink` · `ice` · `indigo` · `ivory` · `jade` · `lavender` · `lilac` · `lime` · `magenta` · `navy` · `orange` · `peach` · `pink` · `plum` · `purple` · `red` · `rose` · `ruby` · `salmon` · `sapphire` · `scarlet` · `seafoam` · `silver` · `snow` · `tangerine` · `teal` · `turquoise` · `violet` · `white` · `yellow`

### Colour families

`acid` · `cool` · `cooler` · `jewel` · `pastel` · `warm` · `warmer`

### Scripts

`arab` · `arabic` · `cantonese` · `cyrillic` · `hanzi` · `hiragana` · `japanese` · `kanji` · `katakana` · `mandarin` · `russian` · `soviet`

### Name forms

`acronym` · `acronyms` · `attested` · `categories` · `category` · `coined` · `evocative` · `historical` · `initials` · `invented` · `nonsense` · `partnership` · `partnerships` · `placename` · `placenames` · `possessive` · `possessives` · `prefixed` · `suffixed` · `toponym` · `toponyms` · `whimsical` · `whimsy` · `family name` · `founder` · `genuine sounding` · `made up` · `made-up` · `one word` · `one-word` · `plausible names` · `real sounding` · `real-sounding` · `short names` · `shorter names` · `single word` · `surname`

### Eras

`1900s` · `1910s` · `1920s` · `1930s` · `1940s` · `1950s` · `1960s` · `1970s` · `1980s` · `1990s` · `2000s` · `atomic` · `disco` · `eighties` · `fifties` · `forties` · `millennium` · `modern` · `noughties` · `postwar` · `prewar` · `prohibition` · `psychedelic` · `seventies` · `sixties` · `spaceage` · `twenties` · `wartime` · `y2k` · `yuppie`

### Themes and moods

`americana` · `brash` · `classy` · `cyber` · `cyberpunk` · `detective` · `dystopian` · `flashy` · `futurist` · `gaudy` · `glamorous` · `glitzy` · `hardboiled` · `highttech` · `midcentury` · `minimal` · `minimalist` · `moody` · `neotokyo` · `noir` · `nostalgic` · `restrained` · `roadside` · `scandinavian` · `scifi` · `shady` · `showgirl` · `showy` · `sleazy` · `sleek` · `smalltown` · `tasteful` · `understated` · `upmarket` · `vegas`

### Font styles

Usable on their own, or with the word "fonts".

`army` · `bold` · `cursive` · `deco` · `elegant` · `futuristic` · `geometric` · `handwritten` · `industrial` · `military` · `modern` · `monoline` · `neon` · `retro` · `rounded` · `sans` · `script` · `serif` · `stencil` · `tall` · `techno` · `thin` · `urban` · `vintage`

### Decor

`arrow` · `arrows` · `badge` · `badges` · `border` · `borders` · `bulb` · `bulbs` · `bunting` · `buntings` · `cartouche` · `cartouches` · `chevron` · `chevrons` · `crest` · `crests` · `decor` · `decoration` · `decorations` · `emblem` · `emblems` · `flag` · `flags` · `flourish` · `flourishes` · `frame` · `frames` · `grid` · `grids` · `heraldic` · `heraldry` · `lattice` · `lattices` · `marquee` · `ornament` · `ornamentation` · `ornaments` · `oval` · `ovals` · `pennant` · `pennants` · `rays` · `ribbon` · `ribbons` · `scallop` · `scallops` · `seal` · `seals` · `shield` · `shields` · `slash` · `slashes` · `squiggle` · `squiggles` · `star` · `starburst` · `stars` · `sunburst` · `swoosh` · `swooshes` · `underline` · `underlines` · `wave` · `waves` · `wavy`

### Decor density

`bare bones` · `busier` · `busiest` · `busy` · `cluttered` · `fussy` · `minimal signs` · `ornate` · `plain signs` · `simpler` · `simplest` · `spare signs` · `sparse` · `stripped back` · `uncluttered`

### Tube gauge

`beefy` · `bolder` · `boldest` · `bulky` · `chunkier` · `chunky` · `delicate` · `fat` · `fatter` · `fine` · `finest` · `hairline` · `hefty` · `meatier` · `skinny` · `slender` · `slim` · `spindly` · `stout` · `thick` · `thicker` · `thickest` · `thin` · `thinner` · `thinnest` · `wispy`

### Brightness

`blazing` · `blinding` · `bright` · `brighter` · `brightest` · `calmer` · `darker` · `dim` · `dimmer` · `dimmest` · `faint` · `feeble` · `fierce` · `gentler` · `glaring` · `glow` · `glowing` · `hotter` · `livelier` · `louder` · `loudest` · `muted` · `punchier` · `punchiest` · `punchy` · `quieter` · `quietest` · `searing` · `sedate` · `soft` · `softer` · `softest` · `subtle` · `vivid` · `washed` · `weak` · `blown out` · `cranked up`

### Wear and flicker

`abandoned` · `aged` · `battered` · `blinking` · `broken` · `busted` · `buzzing` · `crumbling` · `decayed` · `decaying` · `derelict` · `dilapidated` · `faded` · `failing` · `flicker` · `flickering` · `flickery` · `fresh` · `grimy` · `guttering` · `immaculate` · `maintained` · `mint` · `neglected` · `peeling` · `pristine` · `refurbished` · `repaired` · `restored` · `rundown` · `rusted` · `rusty` · `scruffy` · `seedy` · `shabby` · `spotless` · `stable` · `steady` · `stuttering` · `tired` · `unblemished` · `unflickering` · `weathered` · `working` · `worn` · `run down` · `falling apart` · `worse for wear` · `beaten up` · `past its best` · `brand new` · `just installed` · `like new`

### Rig and mounting

`backboard` · `cable` · `cables` · `panel` · `panels` · `plate` · `rivet` · `rivets` · `scaffolding` · `skeleton` · `spacers` · `standoff` · `standoffs` · `trussed` · `band plate` · `bottom plate` · `bright metal` · `clean mounts` · `cross braced` · `cross frame` · `dark metal` · `deep frame` · `driver brick` · `electrical box` · `evenly spaced standoffs` · `exposed frame` · `fitted backing` · `generous margin` · `inset edge` · `junction box` · `ladder frame` · `led panel box` · `left plate` · `legs to the wall` · `minimal runs` · `no backing` · `one run` · `open frame` · `outset edge` · `pale metal` · `pipe grid` · `plate behind the text` · `purlins` · `right plate` · `rim frame` · `roof bracing` · `roof frame` · `shallow frame` · `spine frame` · `square edge` · `square section` · `standoffs in pairs` · `standoffs to the wall` · `three runs` · `tidy mounts` · `tight margin` · `top plate` · `two runs`

### Title typography

`a backdrop` · `angled` · `background decor` · `fat gauge` · `fill the sign` · `fine gauge` · `heaviest gauge` · `leave the title alone` · `level titles` · `lightest gauge` · `looser lettering` · `medium gauge` · `nudge the title down` · `nudge the title left` · `nudge the title right` · `nudge the title up` · `slanted` · `spaced out` · `straight titles` · `thicker decor lines` · `thin decor lines` · `tight tracking` · `tighter lettering` · `tilted` · `wider tracking`

### Colour policy and letter swaps

`every letter` · `every word` · `first letter` · `letter for an icon` · `letter swap` · `multicolored` · `multicoloured` · `one color per sign` · `one colour per sign` · `one colour titles` · `rainbow lettering` · `single color` · `single colour` · `swap a letter` · `two tone` · `word by word`

### Composition

`badge layout` · `bordered` · `catchphrase` · `framed` · `icon only` · `just the name` · `name only` · `subtitle` · `subtitles` · `symbol only` · `tagline` · `title only` · `underlined` · `with borders`

### Layout

The last few need a "more"/"fewer" to tell them apart from the scopes below.

`across in one` · `one line` · `single line` · `stack the text` · `stacked text` · `taller signs` · `vertical layout` · `vertical lettering` · `wide layout` · `wider signs` · `horizontal signs` · `upright signs` · `vertical signs`

### One palette for the street

`consistent` · `all the same` · `all match` · `them all match` · `uniform` · `cohesive` · `matching colours` · `matching colors` · `one palette` · `same colour` · `same color`

### Aiming at part of the street

Put one of these WITH an instruction - "red on the big signs". On their own they do nothing.

`alternate signs` · `big signs` · `biggest` · `down low` · `down the street` · `every other one` · `every other sign` · `every second sign` · `far end` · `high signs` · `in the middle` · `landscape signs` · `large signs` · `little signs` · `low signs` · `middle of the street` · `near end` · `portrait signs` · `small signs` · `smallest` · `the big ones` · `the far end` · `the first few` · `the high ones` · `the last few` · `the low ones` · `the middle` · `the ones in the middle` · `the small ones` · `the vertical ones` · `the wide ones` · `this end` · `up high` · `vertical signs` · `wide signs` · `blade signs` · `marquee signs` · `plaque signs` · `rooftop signs` · `storefront signs` · `the blade ones` · `the marquee ones` · `the plaque ones` · `the rooftop ones` · `the storefront ones`

### Everything but

"yellow everywhere except the bars".

`except` · `apart from` · `other than` · `besides` · `but not` · `aside from` · `excluding` · `save for`
