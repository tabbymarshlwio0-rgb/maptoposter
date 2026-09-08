# City Map Poster Generator

Generate beautiful, minimalist map posters for any city in the world.

<img src="posters/singapore_neon_cyberpunk_20260118_153328.png" width="250">
<img src="posters/dubai_midnight_blue_20260118_140807.png" width="250">

## Examples

| Country      | City           | Theme           | Poster |
|:------------:|:--------------:|:---------------:|:------:|
| USA          | San Francisco  | sunset          | <img src="posters/san_francisco_sunset_20260118_144726.png" width="250"> |
| Spain        | Barcelona      | warm_beige      | <img src="posters/barcelona_warm_beige_20260118_140048.png" width="250"> |
| Italy        | Venice         | blueprint       | <img src="posters/venice_blueprint_20260118_140505.png" width="250"> |
| Japan        | Tokyo          | japanese_ink    | <img src="posters/tokyo_japanese_ink_20260118_142446.png" width="250"> |
| India        | Mumbai         | contrast_zones  | <img src="posters/mumbai_contrast_zones_20260118_145843.png" width="250"> |
| Morocco      | Marrakech      | terracotta      | <img src="posters/marrakech_terracotta_20260118_143253.png" width="250"> |
| Singapore    | Singapore      | neon_cyberpunk  | <img src="posters/singapore_neon_cyberpunk_20260118_153328.png" width="250"> |
| Australia    | Melbourne      | forest          | <img src="posters/melbourne_forest_20260118_153446.png" width="250"> |
| UAE          | Dubai          | midnight_blue   | <img src="posters/dubai_midnight_blue_20260118_140807.png" width="250"> |
| USA          | Seattle        | emerald         | <img src="posters/seattle_emerald_20260124_162244.png" width="250"> |

## Installation

### With uv (Recommended)

Make sure [uv](https://docs.astral.sh/uv/) is installed. Running the script by prepending `uv run` automatically creates and manages a virtual environment.

```bash
# First run will automatically install dependencies
uv run ./create_map_poster.py --city "Paris" --country "France"

# Or sync dependencies explicitly first (using locked versions)
uv sync --locked
uv run ./create_map_poster.py --city "Paris" --country "France"
```

### With pip + venv

```bash
python -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

## Usage

### Generate Poster

If you're using `uv`:

```bash
uv run ./create_map_poster.py --city <city> --country <country> [options]
```

Otherwise (pip + venv):

```bash
python create_map_poster.py --city <city> --country <country> [options]
```

### Required Options

| Option | Short | Description |
|--------|-------|-------------|
| `--city` | `-c` | City name (used for geocoding) |
| `--country` | `-C` | Country name (used for geocoding) |

### Optional Flags

| Option | Short | Description | Default |
|--------|-------|-------------|---------|
| **OPTIONAL:** `--latitude` | `-lat` | Override latitude center point (use with --longitude) | |
| **OPTIONAL:** `--longitude` | `-long` | Override longitude center point (use with --latitude) | |
| **OPTIONAL:** `--country-label` | | Override country text displayed on poster | |
| **OPTIONAL:** `--theme` | `-t` | Theme name | terracotta |
| **OPTIONAL:** `--distance` | `-d` | Map radius in meters | 18000 |
| **OPTIONAL:** `--list-themes` | | List all available themes | |
| **OPTIONAL:** `--all-themes` | | Generate posters for all available themes | |
| **OPTIONAL:** `--width` | `-W` | Image width in inches | 12 (max: 20) |
| **OPTIONAL:** `--height` | `-H` | Image height in inches | 16 (max: 20) |

### Multilingual Support - i18n

Display city and country names in your language with custom fonts from google fonts:

| Option | Short | Description |
|--------|-------|-------------|
| `--display-city` | `-dc` | Custom display name for city (e.g., "東京") |
| `--display-country` | `-dC` | Custom display name for country (e.g., "日本") |
| `--font-family` | | Google Fonts family name (e.g., "Noto Sans JP") |

**Examples:**

```bash
# Japanese
python create_map_poster.py -c "Tokyo" -C "Japan" -dc "東京" -dC "日本" --font-family "Noto Sans JP"

# Korean
python create_map_poster.py -c "Seoul" -C "South Korea" -dc "서울" -dC "대한민국" --font-family "Noto Sans KR"

# Arabic
python create_map_poster.py -c "Dubai" -C "UAE" -dc "دبي" -dC "الإمارات" --font-family "Cairo"
```

**Note**: Fonts are automatically downloaded from Google Fonts and cached locally in `fonts/cache/`.

### Resolution Guide (300 DPI)

Use these values for `-W` and `-H` to target specific resolutions:

| Target | Resolution (px) | Inches (-W / -H) |
|--------|-----------------|------------------|
| **Instagram Post** | 1080 x 1080 | 3.6 x 3.6 |
| **Mobile Wallpaper** | 1080 x 1920 | 3.6 x 6.4 |
| **HD Wallpaper** | 1920 x 1080 | 6.4 x 3.6 |
| **4K Wallpaper** | 3840 x 2160 | 12.8 x 7.2 |
| **A4 Print** | 2480 x 3508 | 8.3 x 11.7 |

### Usage Examples

#### Basic Examples

```bash
# Simple usage with default theme
python create_map_poster.py -c "Paris" -C "France"

# With custom theme and distance
python create_map_poster.py -c "New York" -C "USA" -t noir -d 12000
```

#### Multilingual Examples (Non-Latin Scripts)

Display city names in their native scripts:

```bash
# Japanese
python create_map_poster.py -c "Tokyo" -C "Japan" -dc "東京" -dC "日本" --font-family "Noto Sans JP" -t japanese_ink

# Korean
python create_map_poster.py -c "Seoul" -C "South Korea" -dc "서울" -dC "대한민국" --font-family "Noto Sans KR" -t midnight_blue

# Thai
python create_map_poster.py -c "Bangkok" -C "Thailand" -dc "กรุงเทพมหานคร" -dC "ประเทศไทย" --font-family "Noto Sans Thai" -t sunset

# Arabic
python create_map_poster.py -c "Dubai" -C "UAE" -dc "دبي" -dC "الإمارات" --font-family "Cairo" -t terracotta

# Chinese (Simplified)
python create_map_poster.py -c "Beijing" -C "China" -dc "北京" -dC "中国" --font-family "Noto Sans SC"

# Khmer
python create_map_poster.py -c "Phnom Penh" -C "Cambodia" -dc "ភ្នំពេញ" -dC "កម្ពុជា" --font-family "Noto Sans Khmer"
```

#### Advanced Examples

```bash
# Iconic grid patterns
python create_map_poster.py -c "New York" -C "USA" -t noir -d 12000           # Manhattan grid
python create_map_poster.py -c "Barcelona" -C "Spain" -t warm_beige -d 8000   # Eixample district

# Waterfront & canals
python create_map_poster.py -c "Venice" -C "Italy" -t blueprint -d 4000       # Canal network
python create_map_poster.py -c "Amsterdam" -C "Netherlands" -t ocean -d 6000  # Concentric canals
python create_map_poster.py -c "Dubai" -C "UAE" -t midnight_blue -d 15000     # Palm & coastline

# Radial patterns
python create_map_poster.py -c "Paris" -C "France" -t pastel_dream -d 10000   # Haussmann boulevards
python create_map_poster.py -c "Moscow" -C "Russia" -t noir -d 12000          # Ring roads

# Organic old cities
python create_map_poster.py -c "Tokyo" -C "Japan" -t japanese_ink -d 15000    # Dense organic streets
python create_map_poster.py -c "Marrakech" -C "Morocco" -t terracotta -d 5000 # Medina maze
python create_map_poster.py -c "Rome" -C "Italy" -t warm_beige -d 8000        # Ancient layout

# Coastal cities
python create_map_poster.py -c "San Francisco" -C "USA" -t sunset -d 10000    # Peninsula grid
python create_map_poster.py -c "Sydney" -C "Australia" -t ocean -d 12000      # Harbor city
python create_map_poster.py -c "Mumbai" -C "India" -t contrast_zones -d 18000 # Coastal peninsula

# River cities
python create_map_poster.py -c "London" -C "UK" -t noir -d 15000              # Thames curves
python create_map_poster.py -c "Budapest" -C "Hungary" -t copper_patina -d 8000  # Danube split

# Override center coordinates
python create_map_poster.py --city "New York" --country "USA" -lat 40.776676 -long -73.971321 -t noir

# List available themes
python create_map_poster.py --list-themes

# Generate posters for every theme
python create_map_poster.py -c "Tokyo" -C "Japan" --all-themes
```

### Distance Guide

| Distance | Best for |
|----------|----------|
| 4000-6000m | Small/dense cities (Venice, Amsterdam center) |
| 8000-12000m | Medium cities, focused downtown (Paris, Barcelona) |
| 15000-20000m | Large metros, full city view (Tokyo, Mumbai) |

## Themes

17 themes available in `themes/` directory:

| Theme | Style |
|-------|-------|
| `gradient_roads` | Smooth gradient shading |
| `contrast_zones` | High contrast urban density |
| `noir` | Pure black background, white roads |
| `midnight_blue` | Navy background with gold roads |
| `blueprint` | Architectural blueprint aesthetic |
| `neon_cyberpunk` | Dark with electric pink/cyan |
| `warm_beige` | Vintage sepia tones |
| `pastel_dream` | Soft muted pastels |
| `japanese_ink` | Minimalist ink wash style |
| `emerald`      | Lush dark green aesthetic |
| `forest` | Deep greens and sage |
| `ocean` | Blues and teals for coastal cities |
| `terracotta` | Mediterranean warmth |
| `sunset` | Warm oranges and pinks |
| `autumn` | Seasonal burnt oranges and reds |
| `copper_patina` | Oxidized copper aesthetic |
| `monochrome_blue` | Single blue color family |

## Output

Posters are saved to `posters/` directory with format:

```text
{city}_{theme}_{YYYYMMDD_HHMMSS}.png
```

## Adding Custom Themes

Create a JSON file in `themes/` directory:

```json
{
  "name": "My Theme",
  "description": "Description of the theme",
  "bg": "#FFFFFF",
  "text": "#000000",
  "gradient_color": "#FFFFFF",
  "water": "#C0C0C0",
  "parks": "#F0F0F0",
  "road_motorway": "#0A0A0A",
  "road_primary": "#1A1A1A",
  "road_secondary": "#2A2A2A",
  "road_tertiary": "#3A3A3A",
  "road_residential": "#4A4A4A",
  "road_default": "#3A3A3A"
}
```

## Project Structure

```text
map_poster/
├── create_map_poster.py    # Main script
├── font_management.py      # Font loading and Google Fonts integration
├── themes/                 # Theme JSON files
├── fonts/                  # Font files
│   ├── Roboto-*.ttf        # Default Roboto fonts
│   └── cache/              # Downloaded Google Fonts (auto-generated)
├── posters/                # Generated posters
└── README.md
```


## Hacker's Guide

Quick reference for contributors who want to extend or modify the script.

### Contributors Guide

- Bug fixes are welcomed
- Don't submit user interface (web/desktop)
- Don't Dockerize for now
- If you vibe code any fix please test it and see before and after version of poster
- Before embarking on a big feature please ask in Discussions/Issue if it will be merged

### Architecture Overview

```text
┌─────────────────┐     ┌──────────────┐     ┌─────────────────┐
│   CLI Parser    │────▶│  Geocoding   │────▶│  Data Fetching  │
│   (argparse)    │     │  (Nominatim) │     │    (OSMnx)      │
└─────────────────┘     └──────────────┘     └─────────────────┘
                                                     │
                        ┌──────────────┐             ▼
                        │    Output    │◀────┌─────────────────┐
                        │  (matplotlib)│     │   Rendering     │
                        └──────────────┘     │  (matplotlib)   │
                                             └─────────────────┘
```

### Key Functions

| Function | Purpose | Modify when... |
|----------|---------|----------------|
| `get_coordinates()` | City → lat/lon via Nominatim | Switching geocoding provider |
| `create_poster()` | Main rendering pipeline | Adding new map layers |
| `get_edge_colors_by_type()` | Road color by OSM highway tag | Changing road styling |
| `get_edge_widths_by_type()` | Road width by importance | Adjusting line weights |
| `create_gradient_fade()` | Top/bottom fade effect | Modifying gradient overlay |
| `load_theme()` | JSON theme → dict | Adding new theme properties |
| `is_latin_script()` | Detects script for typography | Supporting new scripts |
| `load_fonts()` | Load custom/default fonts | Changing font loading logic |

### Rendering Layers (z-order)

```text
z=11  Text labels (city, country, coords)
z=10  Gradient fades (top & bottom)
z=3   Roads (via ox.plot_graph)
z=2   Parks (green polygons)
z=1   Water (blue polygons)
z=0   Background color
```

### OSM Highway Types → Road Hierarchy

```python
# In get_edge_colors_by_type() and get_edge_widths_by_type()
motorway, motorway_link     → Thickest (1.2), darkest
trunk, primary              → Thick (1.0)
secondary                   → Medium (0.8)
tertiary                    → Thin (0.6)
residential, living_street  → Thinnest (0.4), lightest
```

### Typography & Script Detection

The script automatically detects text scripts to apply appropriate typography:

- **Latin scripts** (English, French, Spanish, etc.): Letter spacing applied for elegant "P  A  R  I  S" effect
- **Non-Latin scripts** (Japanese, Arabic, Thai, Korean, etc.): Natural spacing for "東京" (no gaps between characters)

Script detection uses Unicode ranges (U+0000-U+024F for Latin). If >80% of alphabetic characters are Latin, spacing is applied.

### Adding New Features

**New map layer (e.g., railways):**

```python
# In create_poster(), after parks fetch:
try:
    railways = ox.features_from_point(point, tags={'railway': 'rail'}, dist=dist)
except:
    railways = None

# Then plot before roads:
if railways is not None and not railways.empty:
    railways = railways.to_crs(g_proj.graph["crs"])
    railways.plot(ax=ax, color=THEME['railway'], linewidth=0.5, zorder=2.5)
```

**New theme property:**

1. Add to theme JSON: `"railway": "#FF0000"`
2. Use in code: `THEME['railway']`
3. Add fallback in `load_theme()` default dict

### Typography Positioning

All text uses `transform=ax.transAxes` (0-1 normalized coordinates):

```text
y=0.14  City name (spaced letters for Latin scripts)
y=0.125 Decorative line
y=0.10  Country name
y=0.07  Coordinates
y=0.02  Attribution (bottom-right)
```

### Useful OSMnx Patterns

```python
# Get all buildings
buildings = ox.features_from_point(point, tags={'building': True}, dist=dist)

# Get specific amenities
cafes = ox.features_from_point(point, tags={'amenity': 'cafe'}, dist=dist)

# Different network types
G = ox.graph_from_point(point, dist=dist, network_type='drive')  # roads only
G = ox.graph_from_point(point, dist=dist, network_type='bike')   # bike paths
G = ox.graph_from_point(point, dist=dist, network_type='walk')   # pedestrian
```

### Performance Tips

- Large `dist` values (>20km) = slow downloads + memory heavy
- Cache coordinates locally to avoid Nominatim rate limits
- Use `network_type='drive'` instead of `'all'` for faster renders
- Reduce `dpi` from 300 to 150 for quick previews


## 🌐 Web Resources & Interactive Index
- [CATEGORY PUZZLE 9](https://mindconvert.pages.dev/category-puzzle-9.html)
- [JUNGLE SOLITAIRE](https://ieduquests.web.app/jungle-solitaire.html)
- [ZOMBIES AND GUNS](https://eduquestsjp.pages.dev/zombies-and-guns.html)
- [CATCH THIEF](https://quizzesarena.onrender.com/catch-thief.html)
- [CATEGORY BIKE 2](https://eduquestsfr.pages.dev/category-bike-2.html)
- [BRAIN PUZZLES QUESTS](https://quizzesarena.web.app/brain-puzzles-quests.html)
- [BOBBLEHEAD BALL](https://eduquestspt.pages.dev/bobblehead-ball.html)
- [SUDOBLOCK DAILY](https://brainquestspt.pages.dev/sudoblock-daily.html)
- [FASHIONISTA CHRISTMAS EVE PARTY](https://learnaction.netlify.app/fashionista-christmas-eve-party.html)
- [FOOD TRUCK CHEF COOKING](https://eduquestsjp.pages.dev/food-truck-chef-cooking.html)
- [CATEGORY CARE](https://eduquests.pages.dev/category-care.html)
- [CLASSIC MAHJONG](https://brainquestspt.pages.dev/classic-mahjong.html)
- [VOLLEY BEANS VOLLEYBALL GAME](https://quizzesarena.onrender.com/volley-beans-volleyball-game.html)
- [COOL SUPERCARS STUNTS PVP](https://brainquests.pages.dev/cool-supercars-stunts-pvp.html)
- [CATEGORY FASHION105](https://learnaction.netlify.app/category-fashion105.html)
- [AVOID THE SPIKES](https://quizzesarena.onrender.com/avoid-the-spikes.html)
- [WATER SORT PUZZLE 3](https://brainquestspt.pages.dev/water-sort-puzzle-3.html)
- [ROMANTIC MATCH TACTICS](https://quizzesarena.onrender.com/romantic-match-tactics.html)
- [SANDWICH RUNNER](https://eduquestspt.pages.dev/sandwich-runner.html)
- [CATEGORY BATTLE ROYALE25](https://quizzesarena.web.app/category-battle-royale25.html)
- [STICK VS MONSTER SCHOOL 2](https://brainquests.pages.dev/stick-vs-monster-school-2.html)
- [ELEMENTAL MONSTERS MERGE EVOLUTION](https://brainquestspt.pages.dev/elemental-monsters-merge-evolution.html)
- [CATEGORY FUN MAKEUP GAMES](https://quizzesarena.web.app/category-fun-makeup-games.html)
- [STICK COLOR WAR](https://brainquests.pages.dev/stick-color-war.html)
- [INDEX30](https://eduquestspt.pages.dev/index30.html)
- [HEXAMATCH](https://brainquests.pages.dev/hexamatch.html)
- [BRAWL STARS BRAVE ADVENTURE](https://quizzesarena.onrender.com/brawl-stars-brave-adventure.html)
- [OBBY CLIMB RACING](https://brainquests.pages.dev/obby-climb-racing.html)
- [ARTILLERY VS TANKS](https://quizzesarena.onrender.com/artillery-vs-tanks.html)
- [ARROWS PUZZLE ESCAPE](https://brainquests.pages.dev/arrows-puzzle-escape.html)
- [PUSH IT 3D](https://eduquestsjp.pages.dev/push-it-3d.html)
- [CHRISTMAS BLIND BOX](https://brainquests.pages.dev/christmas-blind-box.html)
- [CATEGORY TITANIUM NETWORK](https://quizzesarena.web.app/category-titanium-network.html)
- [CATEGORY CLASSIC98](https://quizzesarena.web.app/category-classic98.html)
- [CAR CARE REPAIR DUDU MECHANIC](https://brainquests.pages.dev/car-care-repair-dudu-mechanic.html)
- [ANTS PARTY](https://quizzesarena.onrender.com/ants-party.html)
- [CATEGORY MAKEUP51](https://quizzesarena.onrender.com/category-makeup51.html)
- [BRAWL STARS SOUND](https://brainquests.pages.dev/brawl-stars-sound.html)
- [SKIBIDI SURVIVOR RUSH](https://brainquests.pages.dev/skibidi-survivor-rush.html)
- [CATEGORY GITHUB IO](https://eduquests.pages.dev/category-github-io.html)
- [JUMP BALL CLASSIC](https://brainquests.pages.dev/jump-ball-classic.html)
- [ASOKA MAKEUP INDIAN BRIDE](https://brainquests.pages.dev/asoka-makeup-indian-bride.html)
- [WAFFLE WORDS](https://brainquests.pages.dev/waffle-words.html)
- [KNOTS](https://brainquestspt.pages.dev/knots.html)
- [FIGHT TRIVIA](https://quizzesarena.web.app/fight-trivia.html)
- [CATEGORY SHOP49](https://welearnaction.onrender.com/category-shop49.html)
- [CATEGORY WAR137](https://welearnaction.onrender.com/category-war137.html)
- [BASKET SPORT STARS](https://welearnaction.onrender.com/basket-sport-stars.html)
- [JOIN CLASH COLOR BUTTON](https://brainquestspt.pages.dev/join-clash-color-button.html)
- [TAP OUT PUZZLE](https://eduquestspt.pages.dev/tap-out-puzzle.html)
- [WAVE CHIC OCEAN FASHION FRENZY](https://quizzesarena.web.app/wave-chic-ocean-fashion-frenzy.html)
- [ROLLING BALLS SEA RACE](https://brainquestspt.pages.dev/rolling-balls-sea-race.html)
- [CHESSFIELD](https://eduquestspt.pages.dev/chessfield.html)
- [GEM DEEP DIGGER](https://brainquests.pages.dev/gem-deep-digger.html)
- [CAT RESCUE](https://brainquests.pages.dev/cat-rescue.html)
- [CATEGORY STICKMAN](https://quizzesarena.web.app/category-stickman.html)
- [GOO GOO GAGA CLICKER](https://brainquestspt.pages.dev/goo-goo-gaga-clicker.html)
- [DUCK LUCK](https://quizzesarena.onrender.com/duck-luck.html)
- [CRAFT OF WARS](https://quizzesarena.web.app/craft-of-wars.html)
- [CATEGORY BIKE 2](https://quizzesarena.web.app/category-bike-2.html)
- [BLOCK PUZZLE CATS](https://eduquestspt.pages.dev/block-puzzle-cats.html)
- [CATEGORY DEFENSE176](https://eduquests.onrender.com/category-defense176.html)
- [OBBY GYM SIMULATOR ESCAPE](https://brainquests.pages.dev/obby-gym-simulator-escape.html)
- [HILL STATION BUS SIMULATOR](https://quizzesarena.onrender.com/hill-station-bus-simulator.html)
- [DROP KICK WORLD CUP 2018](https://eduquestspt.pages.dev/drop-kick-world-cup-2018.html)
- [CATEGORY MANAGEMENT GAME](https://quizzesarena.onrender.com/category-management-game.html)
- [CATEGORY SOCCER](https://brainquestspt.pages.dev/category-soccer.html)
- [CHICKEN BLAST](https://brainquests.pages.dev/chicken-blast.html)
- [FURRY KUNG FU](https://brainquestspt.pages.dev/furry-kung-fu.html)
- [TOWER OF FALL](https://ieduquests.web.app/tower-of-fall.html)
- [2 3 4 PLAYER GAMES](https://brainquests.pages.dev/2-3-4-player-games.html)
- [HAPPY ASMR CARE](https://eduquests.onrender.com/happy-asmr-care.html)
- [ROBBERIES 3D](https://quizzesarena.web.app/robberies-3d.html)
- [PEOPLE PLAYGROUND 3D](https://eduquestsjp.pages.dev/people-playground-3d.html)
- [CATEGORY MOUSE1 697](https://eduquests.netlify.app/category-mouse1-697.html)
- [CATEGORY ANIMAL](https://eduquests.pages.dev/category-animal.html)
- [CATEGORY DESTROY256](https://eduquests.netlify.app/category-destroy256.html)
- [CATEGORY THIRD PERSON SHOOTER80](https://brainquestspt.pages.dev/category-third-person-shooter80.html)
- [SCREW PUZZLE](https://eduquests.netlify.app/screw-puzzle.html)
- [CATEGORY BASKETBALL 3](https://quizzesarena.onrender.com/category-basketball-3.html)
- [STICK HERO FIGHT](https://brainquests.pages.dev/stick-hero-fight.html)
- [INFINITE CRAFT](https://eduquests.onrender.com/infinite-craft.html)
- [CATEGORY SOLITAIRE](https://quizzesarena.onrender.com/category-solitaire.html)
- [CATEGORY IDLE445](https://welearnaction.onrender.com/category-idle445.html)
- [CATEGORY MAKEUP51](https://welearnaction.onrender.com/category-makeup51.html)
- [ITILEZEN SORT PUZZLE](https://ieduquests.web.app/itilezen-sort-puzzle.html)
- [BOMBER FRIENDS](https://quizzesarena.onrender.com/bomber-friends.html)
- [ANIME COUPLE AVATAR MAKER](https://brainquests.pages.dev/anime-couple-avatar-maker.html)
- [COLOR CARGO PUZZLE RUSH](https://eduquests.onrender.com/color-cargo-puzzle-rush.html)
- [FARM MATCH SEASONS 2](https://eduquestspt.pages.dev/farm-match-seasons-2.html)
- [JENNYS MATH PUZZLE](https://eduquestspt.pages.dev/jennys-math-puzzle.html)
- [FAR ORION NEW WORLDS](https://welearnaction.onrender.com/far-orion-new-worlds.html)
- [HERO FIGHT CLASH](https://quizzesarena.web.app/hero-fight-clash.html)
- [FANTASY MADNESS](https://quizzesarena.onrender.com/fantasy-madness.html)
- [STAR ATTACK 3D](https://brainquests.pages.dev/star-attack-3d.html)
- [GTA CAR RUSH](https://brainquestspt.pages.dev/gta-car-rush.html)
- [CATEGORY AGILITY](https://quizzesarena.onrender.com/category-agility.html)
- [INDEX5](https://brainquestspt.pages.dev/index5.html)
- [CATEGORY RPG80](https://eduquestspt.pages.dev/category-rpg80.html)
- [POPPING CANDIES](https://quizzesarena.onrender.com/popping-candies.html)
- [DOG MERGE MANIA](https://quizzesarena.onrender.com/dog-merge-mania.html)
- [GUN CRAFT RUN WEAPON FIRE](https://quizzesarena.web.app/gun-craft-run-weapon-fire.html)
- [HOME DESIGN SMALL HOUSE](https://welearnaction.onrender.com/home-design-small-house.html)
- [ROYAL JIGSAW](https://brainquests.pages.dev/royal-jigsaw.html)
- [BOMB EVOLUTION](https://eduquestspt.pages.dev/bomb-evolution.html)
- [TOP HOG](https://brainquestspt.pages.dev/top-hog.html)
- [THREAD MATCH](https://quizzesarena.web.app/thread-match.html)
- [GRUKKLE ONSLAUGHT](https://quizzesarena.onrender.com/grukkle-onslaught.html)
- [CARD QUEST 10 MINUTE ADVENTURE](https://quizzesarena.web.app/card-quest-10-minute-adventure.html)
- [INDEX3](https://eduquests.pages.dev/index3.html)
- [ONU LIVE](https://eduquests.netlify.app/onu-live.html)
- [MADNESS DRIVER VERTIGO CITY](https://brainquestspt.pages.dev/madness-driver-vertigo-city.html)
- [MAHJONG SLIDE PUZZLE](https://eduquests.netlify.app/mahjong-slide-puzzle.html)
- [SPRUNKI SPACE CHALLENGE](https://brainquests.pages.dev/sprunki-space-challenge.html)
- [QUIZ X](https://brainquests.pages.dev/quiz-x.html)
- [CATEGORY FASHION105](https://eduquestspt.pages.dev/category-fashion105.html)
- [CATEGORY COLLECT565](https://eduquests.pages.dev/category-collect565.html)
- [TOWER GUARDIAN EPIC DEFENSE](https://brainquestspt.pages.dev/tower-guardian-epic-defense.html)
- [NUMBER MASTER RUN AND MERGE](https://quizzesarena.onrender.com/number-master-run-and-merge.html)
- [BACKGAMMON DUEL](https://brainquestspt.pages.dev/backgammon-duel.html)
- [POLITON](https://brainquestspt.pages.dev/politon.html)
- [RUSH CAR DRIVING RACE MASTER](https://brainquests.pages.dev/rush-car-driving-race-master.html)
- [CATEGORY MAHJONG](https://quizzesarena.onrender.com/category-mahjong.html)
- [ULTIMATE DESTRUCTION SIMULATOR](https://eduquestspt.pages.dev/ultimate-destruction-simulator.html)
- [CATEGORY STRATEGY](https://quizzesarena.onrender.com/category-strategy.html)
- [CATEGORY TOWER DEFENSE 2](https://eduquests.onrender.com/category-tower-defense-2.html)
- [MEME CHALLENGEIO](https://brainquests.pages.dev/meme-challengeio.html)
- [BLACK PINK STPATRICKS DAY CONCERT](https://learnaction.netlify.app/black-pink-stpatricks-day-concert.html)
- [TOPSY TURVY](https://quizzesarena.onrender.com/topsy-turvy.html)
- [INDEX18](https://eduquests.netlify.app/index18.html)
