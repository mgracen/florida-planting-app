# Florida Planting Calendar

A single-file planting calendar for Florida gardeners. No account, no server, no build step. One HTML file you can open, host, or fork.

Florida's growing year runs backwards from most of the country. The productive season is roughly September through May, and June through August is the hard season rather than the growing season. Generic gardening apps are built around a spring-planting, frost-date model and are actively wrong here. This is an attempt to fix that for the three regions UF/IFAS Extension uses: North Florida above roughly Ocala, Central through about Sebring, and South below that.

**Live site:** https://mgracen.github.io/florida-planting-app/

---

## What's in it

**Plant now**. 229 plants across 17 segments, with planting windows for all three regions. Food garden: vegetables, herbs, sweet and hot peppers, beans, roots, heat-season tropicals, fruit trees and berries, and cover crops. Landscape: pollinator and butterfly plants, trees and shrubs, shade and foliage, bulbs and rhizomes, grasses and groundcovers, vines, water and bog plants, and succulents. 63 entries are Florida natives and can be filtered as a set. Each plant carries Florida-adapted varieties, spacing, and a note about what actually goes wrong here, plus warnings where a plant is toxic, invasive, or legally protected. Searchable across all months.

**Conditions**. Live local weather from Open-Meteo, computed into things that change what you do: soil temperature at seed depth, the warm-night count that explains why summer tomatoes won't set fruit, an irrigation gap in inches from evapotranspiration minus rainfall, freeze warnings, and fungal-disease weather.

**Pests**. 43 entries covering insects, diseases, weeds, and wildlife, including armadillos, iguanas, and the four Florida weeds that don't pull out the way people expect, with a month-by-month pressure band. Each gives what you see, what it does, and a ranked response linked to the treatment repository.

**Frost & storms**. Freeze dates by region, cold-hardiness thresholds, a six-step freeze-night procedure, hurricane preparation, and succession sowing intervals.

**Seed & harvest**. Germination temperatures, starting seedlings through a Florida summer, when to pick each crop, and seed saving.

**Soil & feeding**. Working with sand, reading nutrient deficiencies, pH lockout in South Florida limestone soils, and summer fertilizer restrictions.

**Treatments**. 38 entries in four groups: physical and cultural, biological, sprays that work, and popular remedies assessed honestly.

**Pollinators**. A Florida field reference, a crop-by-crop table of which crops actually need insects, live iNaturalist records for what's flying near you this month, and a sighting log with map and CSV export.

**Whole year**. Every planting window as a single band, with the hard season marked.

Plus a printable one-page monthly sheet for the shed.

---

## Running it

Download `index.html` and open it in a browser. That's the whole installation.

Everything except live weather, iNaturalist records, and map tiles works with no connection at all.

### Hosting it on GitHub Pages

1. Create a repository and add `index.html` to it.
2. Settings → Pages → deploy from your `main` branch, root folder.
3. Wait a minute for the first build.

Hosting works **better** than opening the file locally, because GitHub Pages serves over HTTPS. Browsers block the device-location API on `file://` URLs for security reasons, so the "Use my device" button only works on a hosted copy.

### Setting your location

Type your town and hit **Set location**. Your coordinates and region are written into the page URL, so bookmark it afterwards and it comes back next time. That's the closest thing to a login a single static file can offer.

---

## About the photos

Plant photos are fetched live from the [iNaturalist](https://www.inaturalist.org/) API by scientific name, lazily as cards scroll into view, and cached for the session. Each photo displays its photographer credit and licence, and there is an On/Off toggle for anyone on a metered connection or working offline. Cards with no photo show a botanical placeholder tinted to their segment colour.

**Only freely licensed photographs are shown.** Photos come from two sources, iNaturalist and Wikimedia Commons, and are restricted to public domain, CC0 and plain CC BY. Both allow any use, commercial included, and CC BY simply requires credit, which appears on every photo along with the licence. Non-commercial, no-derivatives and share-alike licences are excluded deliberately, so that nobody using this project or forking it has a licence question to answer.

iNaturalist's default setting for a new account is all rights reserved, and displaying a credit does not grant a licence, so anything outside the permitted set is rejected. When a taxon's own photo does not qualify, the app searches observations filtered to open licences instead. If nothing qualifying exists for a plant, the card keeps its placeholder rather than showing an image the project has no right to use.

Food-garden plants query Wikimedia Commons first, because iNaturalist records wild organisms and cultivated varieties are not separate taxa there, so every pepper cultivar resolves to the same species photo. Landscape plants and natives query iNaturalist first, which is where it is strongest. Either source can serve as the other's fallback.

There is also a `PHOTO_FIX` map near the top of the photo code for pinning a specific taxon, choosing a different photo from a gallery, or pointing an entry at your own image file.

The practical cost is coverage: this is a strict filter and a fair number of plants will show a placeholder rather than a photo. That is the intended trade. Filling those gaps with your own photographs is the reliable long-term fix, and it also solves the accuracy problem, since your pictures will show your region and your cultivars.

**These matches are automated and unverified.** 217 of the 229 plants carry a scientific name for lookup; the remaining twelve are multi-species groupings such as "Oregano & thyme" or non-plants such as "Solarization fallow", and they keep the placeholder by design. An automatic name-to-photo match can return the wrong organism, a different cultivar, or an unrepresentative specimen.

That matters more here than in most plant apps, because this collection includes plants that are lethal (gloriosa lily, Carolina jessamine), toxic unless cooked (chaya, elderberry, taro), easily confused with edible lookalikes (gotu kola and dollarweed), and native species routinely mislabelled in the nursery trade (native firebush versus the African one, native versus nonnative porterweed, native Aristolochia versus the giant pipevine that kills the butterfly larvae it attracts).

So every auto-matched photo is labelled **unverified** until a human checks it. As you confirm one, add the plant name to the `VERIFIED` set near the top of the photo code and the badge disappears for that entry:

```js
const VERIFIED = new Set([
  "Datil pepper",
  "Muhly grass",
]);
```

This is a genuinely good task to crowdsource through issues and pull requests, since verification needs someone who can recognise the plant.

If you would rather not depend on an external service, the alternative is to photograph plants yourself and swap the fetch for local image files. Slower, but the photos then match your region, your cultivars, and your actual garden, and the app keeps working with no connection at all.

## About the data

Planting windows are adapted from UF/IFAS Extension's *Florida Vegetable Gardening Guide* and *Florida Gardening Calendar*, condensed into three regional bands and rewritten. Pest timings follow UF/IFAS pest and disease guidance.

**Treat every window's edges as approximate.** A mile inland versus coastal, a raised bed versus in-ground, or a warm autumn can move them by weeks. Your county Extension office is the tiebreaker, and it's free. They also run plant diagnostic clinics and handle soil sample submission to the UF/IFAS soil testing lab.

Some deliberate editorial choices worth knowing about:

- **Companion planting** is presented honestly. Trap crops, insectary plants, and shade partners have evidence behind them. The classic plant-pairing charts largely don't, and the app says so.
- **Popular home remedies** get verdicts rather than silent omission. Hydrogen peroxide is a good sanitiser and not a foliar fungicide. Epsom salt doesn't fix blossom end rot. Dish detergent is not insecticidal soap.
- **"Natural" is not treated as a synonym for "safe."** Spinosad, neem, and pyrethrin all kill bees on contact while wet.
- **Marginal crops are labelled marginal.** Brussels sprouts, pomegranate, olive, lavender, and dooryard citrus all carry honest expectations rather than encouragement.
- **Invasive and protected species are flagged.** Prohibited aquatic plants, invasive sword fern and strawberry guava, and legally protected sea oats and gopher tortoises are all called out where they come up.

Nothing here is a substitute for identifying a problem before treating it, and it isn't horticultural, medical, or legal advice.

---

## Limitations

- **No persistence.** There's no server and no account. Your pollinator sighting log does not survive a page refresh. Export the CSV before closing. Location persists only because it lives in the URL.
- **API-dependent tabs need a connection.** Weather, iNaturalist, and map tiles fail gracefully with an explanation rather than an endless spinner.
- **Regional bands are coarse.** Three regions for a state spanning USDA zones 8a to 11a is a compromise.

---

## Contributing

Corrections are the most valuable contribution, particularly from people growing in a specific county. If a planting window is off by a few weeks where you are, or a variety recommendation doesn't hold up, open an issue and say which region and what you observed.

The file is plain HTML, CSS, and vanilla JavaScript with no build step and no dependencies beyond Leaflet, loaded from a CDN only when the map is used. Plant data lives in the `CROPS` array, pests in `PESTS`, and treatments in `TREATMENTS`. Adding an entry means adding one object.

Forking it for another state or region is welcome and is a good reason this is MIT-licensed. The structure is not Florida-specific even though all the content is.

---

## License and attribution

Code and written content are released under the [MIT License](LICENSE).

Third-party services and libraries used:

- Weather data from [Open-Meteo](https://open-meteo.com/) (CC BY 4.0), no API key required
- Observation records and plant photographs from [iNaturalist](https://www.inaturalist.org/) contributors, under the licences shown on each photo
- Plant photographs from [Wikimedia Commons](https://commons.wikimedia.org/) contributors, under the licences shown on each photo
- Map tiles © [OpenStreetMap](https://www.openstreetmap.org/copyright) contributors
- [Leaflet](https://leafletjs.com/) mapping library (BSD 2-Clause)
- Fonts from Google Fonts: Fraunces, Karla, Archivo Narrow (SIL Open Font License)

Horticultural guidance adapted from UF/IFAS Extension publications. This project is not affiliated with or endorsed by the University of Florida.
