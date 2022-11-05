# OpenStreetMap

> TODO delete or reestructure this page

- https://www.wikidata.org/wiki/Wikidata:OpenStreetMap
- https://www.wikidata.org/wiki/Property:P8253

## Temp

```sparql
SELECT DISTINCT ?item ?itemLabel WHERE {
  ?item p:P31/ps:P31/wdt:P279* wd:Q56695738 .
  SERVICE wikibase:label { bd:serviceParam wikibase:language "en". }
}

```

[Run it on Wikidata](https://query.wikidata.org/#SELECT%20DISTINCT%20%3Fitem%20%3FitemLabel%20%3Fcoord%20%3FcountryLabel%20%3FshortCountry%20%3Fcity%20%20WHERE%20%7B%0A%20%20%3Fitem%20p%3AP31%2Fps%3AP31%2Fwdt%3AP279%2a%20wd%3AQ56695738%20.%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22.%20%7D%0A%7D%0A)

### OpenStreetMap Data items

```
== TL;DR OpenStreetMap Data Items ==
* https://wiki.openstreetmap.org/wiki/Data_items
** https://wiki.openstreetmap.org/wiki/Special:ListProperties
** https://wiki.openstreetmap.org/wiki/Special:ListDatatypes
** https://wiki.openstreetmap.org/wiki/SPARQL_examples
** https://wiki.openstreetmap.org/wiki/SPARQL_examples#Data_items
** Response example
*** https://wiki.openstreetmap.org/w/api.php?action=wbgetentities&sites=wiki&titles=Key:bridge:movable&languages=en%7Cfr
*** https://wiki.openstreetmap.org/wiki/Special:EntityData/Q2.ttl
*** https://wiki.openstreetmap.org/wiki/Special:EntityData/Q2.json

```

### Umapped places

- Discussions/code/etc
  - https://wiki.openstreetmap.org/wiki/Unmappedplaces
    - https://github.com/openstreetmap/svn-archive/blob/main/applications/utils/gary68/unmappedplaces.pl
  - https://github.com/hfs/unmapped-census
  - https://forum.openstreetmap.org/viewtopic.php?id=70649
  - https://neis-one.org/2016/06/unmapped-places-osm/
    - http://resultmaps.neis-one.org/unmapped#2/23.7/3.5


Overpass
```
/*
This has been generated by the overpass-turbo wizard.
The original search was:
“healthcare=hospital”
*/
[out:json][timeout:25];
// gather results
(
  // query part for: “healthcare=hospital”
  node["healthcare"="hospital"]({{bbox}});
  way["healthcare"="hospital"]({{bbox}});
  relation["healthcare"="hospital"]({{bbox}});
);
//rel(around:1000)["name"="Porto Alegre"];
// print results
out body;
>;
out skel qt;
```

```
/*
This has been generated by the overpass-turbo wizard.
The original search was:
“healthcare=hospital”
*/
[out:json][timeout:25];
// gather results
(
  // query part for: “healthcare=hospital”
  node["healthcare"="hospital"]({{bbox}});
  //way["healthcare"="hospital"]({{bbox}});
  //relation["healthcare"="hospital"]({{bbox}});
);
//rel(around:1000)["name"="Porto Alegre"];
// print results
out body;
>;
out skel qt;
```

https://wiki.openstreetmap.org/wiki/Overpass_API/Overpass_QL#Relative_to_other_elements_(around)

```
area[name="Bonn"];
node(area)[highway=bus_stop]->.bus_stops;
( 
  way(around.bus_stops:100)[amenity=cinema];
  node(around.bus_stops:100)[amenity=cinema];
);
(._;>;);
out meta;
```

### TODO remove these toy examples
#### Hospitais a 100m de cinemas
```
[out:json][timeout:25];
//(
//  node["healthcare"="hospital"]({{bbox}});
//  way["healthcare"="hospital"]({{bbox}});
//  relation["healthcare"="hospital"]({{bbox}});
//)->.hospitals;

(
  node["amenity"="cinema"]({{bbox}});
  way["amenity"="cinema"]({{bbox}});
  relation["amenity"="cinema"]({{bbox}});
)->.cinemas;

(
  way(around.cinemas:1000)[healthcare=hospital];
  node(around.cinemas:1000)[healthcare=hospital];
  relation(around.cinemas:1000)[healthcare=hospital];
);

(._;>;);
out body;
```