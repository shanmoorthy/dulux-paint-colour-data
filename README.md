# Dulux Australia Colour Data

A dataset of all paint colours carried by Dulux Australia, collated by scraping the Single Page App's API.

## Background

While building a new house we had to pick out the default colour of our walls. We liked the warmth of Manorburn but wanted the lightness of Lexicon. When you browse the colours on the website, in the colour info, all colours are defined by a Red, Green and Blue tint/tone/shade strength, and a Light Reflectance Value (LRV) which indicates how bright the paint is. Using the RGB values you can quickly search for colours, and you can use the LRV filter the brightness. Mathematically choosing colours using the Dulux website is impossible, and delving into the details of each colour to see if it matches the criteria would have taken a long time.

## Example
In our instance, we knew the colour we liked was "warm" ie equal or similar amounts of red and green, and lower amounts of blue. Being a grey colour the variation between all 3 tints are minimal. Additionally we knew the colour we wanted was a light as Lexicon, so it had to have an LRV around 84.

The data can be input into a command-line JSON processor like [jq](https://stedolan.github.io/jq/), which allows you to slice, filter, map or transform the data with ease.

```sh
cat data/colours.json | jq '.colours | map(select((77 <= .lrv) and (.lrv <= 86) and (0 <= .red-.green) and (.red-.green <= 4) and (0 <= .red-.blue) and (.red-.blue <= 9))) | sort_by(.lrv) | map({name,url})'
```

Which results in:

```json
[
  {
    "name": "Amethyst Ice Quarter",
    "url": "https://www.dulux.com.au/colour/amethyst-ice-quarter"
  },
  {
    "name": "Vanilla Quake Quarter",
    "url": "https://www.dulux.com.au/colour/vanilla-quake-quarter"
  },
  {
    "name": "Brume Quarter",
    "url": "https://www.dulux.com.au/colour/brume-quarter"
  },
  {
    "name": "Mud Berry Quarter",
    "url": "https://www.dulux.com.au/colour/mud-berry-quarter"
  },
  {
    "name": "Grey Pebble Quarter",
    "url": "https://www.dulux.com.au/colour/grey-pebble-quarter"
  },
  {
    "name": "Warm Ash Quarter",
    "url": "https://www.dulux.com.au/colour/warm-ash-quarter"
  },
  {
    "name": "Slight Mushroom Quarter",
    "url": "https://www.dulux.com.au/colour/slight-mushroom-quarter"
  },
  {
    "name": "Summer Cloud",
    "url": "https://www.dulux.com.au/colour/summer-cloud"
  },
  {
    "name": "Snowy Mountains",
    "url": "https://www.dulux.com.au/colour/snowy-mountains"
  },
  {
    "name": "Casper White Half",
    "url": "https://www.dulux.com.au/colour/casper-white-half"
  },
  {
    "name": "Treble Cone Half",
    "url": "https://www.dulux.com.au/colour/treble-cone-half"
  },
  {
    "name": "Whitsunday Island",
    "url": "https://www.dulux.com.au/colour/whitsunday-island"
  },
  {
    "name": "Blissful White",
    "url": "https://www.dulux.com.au/colour/blissful-white"
  },
  {
    "name": "Mt Aspiring",
    "url": "https://www.dulux.com.au/colour/mt-aspiring"
  },
  {
    "name": "Dalmation",
    "url": "https://www.dulux.com.au/colour/dalmation"
  },
  {
    "name": "Mt Aspiring",
    "url": "https://www.dulux.com.au/colour/mt-aspiring"
  },
  {
    "name": "White Exchange Quarter",
    "url": "https://www.dulux.com.au/colour/white-exchange-quarter"
  },
  {
    "name": "Summer Cloud Half",
    "url": "https://www.dulux.com.au/colour/summer-cloud-half"
  },
  {
    "name": "Natural White™",
    "url": "https://www.dulux.com.au/colour/natural-white"
  },
  {
    "name": "Cardrona",
    "url": "https://www.dulux.com.au/colour/cardrona"
  },
  {
    "name": "Snowy Mountains Half",
    "url": "https://www.dulux.com.au/colour/snowy-mountains-half"
  },
  {
    "name": "Casper White Quarter",
    "url": "https://www.dulux.com.au/colour/casper-white-quarter"
  },
  {
    "name": "Mt Aspiring Half",
    "url": "https://www.dulux.com.au/colour/mt-aspiring-half"
  }
]
```