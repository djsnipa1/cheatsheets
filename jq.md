

```shell
cat history.json | jq '.items[0]'
```

```yaml
{
  "track": {
    "album": {
      "album_type": "album",
      "artists": [
        {
          "external_urls": {
            "spotify": "https://open.spotify.com/artist/3190LZw4ThYKXI7rkkmpYl"
          },
          "href": "https://api.spotify.com/v1/artists/3190LZw4ThYKXI7rkkmpYl",
          "id": "3190LZw4ThYKXI7rkkmpYl",
          "name": "Melting Point (INT)",
          "type": "artist",
          "uri": "spotify:artist:3190LZw4ThYKXI7rkkmpYl"
        }
              ]  
          }
       }
}
```
---

```shell
cat history.json | jq '.items[0] .track'
```

```yaml

{
  "album": {
    "album_type": "album",
    "artists": [
      {
        "external_urls": {
          "spotify": "https://open.spotify.com/artist/3190LZw4ThYKXI7rkkmpYl"
        },
        "href": "https://api.spotify.com/v1/artists/3190LZw4ThYKXI7rkkmpYl",
        "id": "3190LZw4ThYKXI7rkkmpYl",
        "name": "Melting Point (INT)",
        "type": "artist",
        "uri": "spotify:artist:3190LZw4ThYKXI7rkkmpYl"
      }
    ],
    "available_markets": [
      "AD",
      "AE",
      "AR",
      "AT",
      "AU",
      "BE",
      "BG",
      "BH",
      "BO",
      "BR",
      "CA",
      "CH",
      "CL",
      "CO",
      "CR",
      "CY",
      "CZ",
      "DE",
      "DK",
      "DO",
      "DZ",
      "EC",
      "EE",
      "EG",
      "ES",
      "FI",
      "FR",
      "GB",
      "GR",
      "GT",
      "HK",
      "HN",
      "HU",
      "ID",
      "IE",
      "IL",
      "IN",
      "IS",
      "IT",
      "JO",
      "JP",
      "KW",
      "LB",
      "LI",
      "LT",
      "LU",
      "LV",
      "MA",
      "MC",
      "MT",
      "MX",
      "MY",
      "NI",
      "NL",
      "NO",
      "NZ",
      "OM",
      "PA",
      "PE",
      "PH",
      "PL",
      "PS",
      "PT",
      "PY",
      "QA",
      "RO",
      "SA",
      "SE",
      "SG",
      "SK",
      "SV",
      "TH",
      "TN",
      "TR",
      "TW",
      "US",
      "UY",
      "VN",
      "ZA"
    ],
    "external_urls": {
      "spotify": "https://open.spotify.com/album/2RoyeRuaMNiagmnsWFsHCy"
    },
    "href": "https://api.spotify.com/v1/albums/2RoyeRuaMNiagmnsWFsHCy",
    "id": "2RoyeRuaMNiagmnsWFsHCy",
    "images": [
      {
        "height": 640,
        "url": "https://i.scdn.co/image/e3e9e8c9cb11e9349f80fd122b79e70994f54eda",
        "width": 640
      },
      {
        "height": 300,
        "url": "https://i.scdn.co/image/3087211927e8eb8307238a79d971b27b23aa0c02",
        "width": 300
      },
      {
        "height": 64,
        "url": "https://i.scdn.co/image/c81b343856e9d1356595f521c2eabc717ff45aed",
        "width": 64
      }
    ],
    "name": "Tales from Within",
    "release_date": "2019-11-25",
    "release_date_precision": "day",
    "total_tracks": 9,
    "type": "album",
    "uri": "spotify:album:2RoyeRuaMNiagmnsWFsHCy"
  },
  "artists": [
    {
      "external_urls": {
        "spotify": "https://open.spotify.com/artist/3190LZw4ThYKXI7rkkmpYl"
      },
      "href": "https://api.spotify.com/v1/artists/3190LZw4ThYKXI7rkkmpYl",
      "id": "3190LZw4ThYKXI7rkkmpYl",
      "name": "Melting Point (INT)",
      "type": "artist",
      "uri": "spotify:artist:3190LZw4ThYKXI7rkkmpYl"
    }
  ],
  "available_markets": [
 // junk
 ],
  "disc_number": 1,
  "duration_ms": 390620,
  "explicit": false,
  "external_ids": {
    "isrc": "GBLV61916705"
  },
  "external_urls": {
    "spotify": "https://open.spotify.com/track/5kIC4aCkybIRK7kawX15SC"
  },
  "href": "https://api.spotify.com/v1/tracks/5kIC4aCkybIRK7kawX15SC",
  "id": "5kIC4aCkybIRK7kawX15SC",
  "is_local": false,
  "name": "Vortex",
  "popularity": 13,
  "preview_url": "https://p.scdn.co/mp3-preview/0df6d596bd16957d1edf214939b44f7aefaa15f3?cid=774b29d4f13844c495f206cafdad9c86",
  "track_number": 2,
  "type": "track",
  "uri": "spotify:track:5kIC4aCkybIRK7kawX15SC"
}
```

---

```shell
cat history.json | jq '.items[0] .track.name'
```

```json
"Vortex"
```
---

```shell
cat history.json | jq '.items[] .track.name'
```

```yaml
"Vortex"
"Our World"
"Our World"
"Zenith"
"One Among Many"
"Here I Come"
"Here I Come"
"Freedom"
"Black Bagels"
"Artificial Effects"
"Dialogue of the Machine - Original"
"Complete Awakening - Original"
"Through the Storm"
"Alternative Realities"
"Next Destination - Mindsurfer Remix"
"Black Bagels"
"Artificial Effects"
"Decipher - Arhetip Remix"
"THC"
"Visions of Digital Vibes"
"Two Types of Dream"
"Acid Prove (Diamond Remix)"
"Acid Prove"
"Super Mantra"
"Acid Prove (Diamond Remix)"
"We Are Future Minds"
"Syncfloor"
"Future Tribes"
"Walk It Talk"
"Futura"
"Reactor - Yestermorrow Remix"
"Thirteen Days"
"Psychedelix - NoFace Remix"
"Visions"
"Nocturnal - Aioaska & Gipsy Soul Remix"
"Zero - Outsiders Remix"
"Free from the Others"
"Life Frequency"
"Human Heart"
"One of Those Ways"
"Rickety Reked - Original mix"
"Tale of Trance - Kalki Remix"
"Power of Magic - Original Mix"
"Rise"
"Funk Pollo"
"Pandorum"
"Morning Star"
"Insidious - Electric Universe Remix"
"The Godz Planet (feat. Deadroom Professor)"
"Chicken vs Turkey Meat"
```
