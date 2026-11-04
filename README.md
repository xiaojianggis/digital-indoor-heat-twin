# Philadelphia Indoor Heat Twin

An interactive digital twin that predicts indoor air temperature in a two-story Philadelphia house from outdoor air temperature, solar radiation, building typology, orientation, window placement and size, roof insulation and roof color.

Everything runs in the browser (`index.html`). There's no server and no build step.

## What you can change

- **Site:** any of 159 Philadelphia neighborhoods, plus the urban heat island offset for day and night.
- **Weather:** month (a typical day built from 1991–2020 PHL normals), a 3-day heat wave or cold snap, and sky condition.
- **Building:** rowhouse, twin or detached; envelope era (pre-1940 brick → IECC 2021 → deep retrofit); which way the front faces; footprint size; street canyon H/W; interior thermal mass.
- **Roof:** flat or pitched with a ventilated attic; insulation R-value; solar absorptance (cool vs. dark roof).
- **Windows:** area per façade and floor, U-value, SHGC and interior blinds.
- **Operation:** infiltration, window-opening strategy, internal gains, and optional heating and cooling.

## Model

A lumped resistance–capacitance thermal network, integrated at 60-second steps over 10 days (7 to settle, 3 shown):

- **Each floor** has an air node, an interior-mass node and an exterior-wall node. Party walls count as mass.
- **The roof** is either a flat roof-deck node or a deck → ventilated attic → ceiling-insulation chain.
- **Sun position** uses the NOAA/Spencer equations. Clear-sky sunlight (Haurwitz) is scaled to Philadelphia's monthly mean, then split into beam and diffuse with the Erbs correlation. Each surface gets beam, sky diffuse and ground-reflected light.
- **Sol-air temperatures** drive heat flow through opaque walls and the roof.
- **Window solar gain** uses SHGC, an incidence-angle modifier and the blind setting, plus shading from the opposite row of the street canyon.

## Limitations

- The neighborhood urban heat island offsets are an illustrative distance-to-City-Hall proxy, not measurements. Import your own CSV (`name,uhi_day,uhi_night`) in the app to replace them.
- Weather is a single typical day per month (no TMY/AMY).
- There's no wind- or stack-driven airflow model.
- The model hasn't been calibrated against measured indoor temperatures.

Neighborhood boundaries come from [OpenDataPhilly open-geo-data](https://github.com/opendataphilly/open-geo-data).
