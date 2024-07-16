# Facets

## Primary Facets

```javascript
// with facetGroup 'style_group' and facetValue 'Bohemian'
const url = `https://service.cnstrc.com/browse/style_group/Bohemian`;


// with facetGroup 'shape' and facetValue 'Round'
const url = `https://service.cnstrc.com/browse/shape/Round`;


// with facetGroup 'group_id' and facetValue '1'
const url = `https://service.cnstrc.com/browse/group_id/1`;

```

All requests must include a primary facet in the URL, which consists of its `facetGroup` and `facetValue`

### HTTP Request

`GET https://service.cnstrc.com/browse/<facetGroup>/<facetValue>`

Facet Group | Facet Values
--------- | -------
style_group | `Outdoor` `Kitchen & Bath` `Animal Artistry` `Animal Prints` `Oriental & Persian` `Shags` `Kids & Novelty` `Vintage` `Coastal` `Country & Floral` `Farmhouse` `Geometric` `Southwestern` `Contemporary` `Sports Fan` `Moroccan` `Traditional` `Autumn Harvest` `Bohemian` `Casuals` `Solids & Stripes` `Natural Fibers` `Dorm & Classroom` `Transitional` `Washable` `Reversible` `One of a Kind`
color_grp | `Tans & Ivories` `Blues` `Blacks & Grays` `Reds` `Pinks` `Greens` `Yellows & Golds` `Purples` `Oranges` `Browns` `Multi` `Burgundies`
size_grp | `Runner` `8x10` `Oversize` `9x12` `4x6` `3x5` `5x8` `10x14` `2x3` `Swatch`
room_grp | `Bathroom` `Kitchen` `Living Room` `Bedroom` `Outdoor/Patio` `Kids Room` `Dining Room` `Entryway` `Hallway` `Office`
shape | `Round` `Stair Tread` `Square` `Oval` `Rectangle` `Oval Runner` `Oval Stair Tred` `Kidney` `Octagon` `Hearth` `Football` `Shaped` `Round Chair Pad` `Square Chair Pad` `Star` `Bone` `Heart`
material_cat | `Jute & Sisal` `Wool` `Cotton` `Silk` `Leather` `Synthetics`
weave_cat | `Braided` `Hand tufted` `Hand Hooked` `Hand Knotted` `Flatweave` `Machine Made`
group_id | `1` `10000` `20000` `40000`

The `group_id` facet is an important parameter that controls the product type being returned in the results. It changes based on the search url

url | group_id | product type
--------- | ----------- | -----
search-rugs | 10000 | RUGS
search-keywords | 1 | ANY TYPE
search-lighting | 20000 | LIGHTING
search-furniture | 40000 | FURNITURE

A `group_id` facet with value `1` returns all product types; it is equivalent to not filtering results by their product type. Every searchable product has two group_ids, `group_id=1` and `group_id=<type_specific_id>`. Filtering by `group_id` equal to `1` will therefore return all product types.

## Secondary Parameters

Secondary parameters are added as query parameters. More than one secondary parameter can be added, and some are required

> Request with primary and secondary facet

```javascript
// primary: bohemian style
// secondary: round shape
const url = `https://service.cnstrc.com/browse/style_group/Bohemian?filter[shape]=Round`;

// primary: RUG product type
// secondary: API key / stock status / USD 
const url = `https://service.cnstrc.com/browse/group_id/10000?key=api-public-key&filters[Stock Status]=Y&filters[Currency]=USD`;

// primary: washable style
// secondary: API key / in stock / USD / 60 results / page 1 / RUG product type / sort by relevance / order by descending / cio session #2 / cio user id
const url = `https://service.cnstrc.com/browse/style_group/Washable?key=api-public-key&filters[Stock Status]=Y&filters[Currency]=USD&num_results_per_page=60&page=1&filters[group_id]=10000&sort_by=relevance&sort_order=descending&s=226&i=1130efed-2ad1-1a9b-9414-71e65cfd7f51`;

```

### HTTP Request

`GET https://service.cnstrc.com/browse/<facetGroup>/<facetValue>?<parameter>=<parameterValue>`

<aside class="notice">
Aside from the key, <code>Required</code> fields are required in the sense that they are needed to get relevant results
</aside>

Parameter | Required | Values | Description
--------- | ----------- | ---- | -----
key | true | `<api-public-key>`| API key
group_id | true | `1` `10000` `20000` `40000` | Must be included either as a primary or secondary facet 
filter[Stock Status] | true | `Y` `N` | Stock status of results
filter[Currency] | true | `USD` `CAD` | set to `USD` for .com, set to `CAD` for .ca
filter[`<facetGroup>`] | false | `<facetValue>` | same facetGroup and facetValues listed in primary facets 
s | true | `<ConstructorioID_session_id>` | user-specific session id from cookie
i | true | `<ConstructorioID_client_id>` | user-specific client id from cookie; used to get personalized results
sort_by | false | `relevance` `price` `bestseller` `min_age` | sort by
sort_order | false | `descending` `ascending` | sort order
page | false | `<integer>` | defaults to 1. controls pagination
num_results_per_page | false | `<integer>` | defaults to 60

