# Comics Manifest

## Example

```json
{
  "@context": "http://idpf.org/epub.jsonld",

  "metadata": {
    "@type": "http://schema.org/GraphicNovel",
    "title": "La Page Blanche",
    "sort_as": "Page Blanche, La",
    "author": {
      "name": "Boulet",
      "identifier": "http://isni.org/isni/0000000120186808"
    },
    "illustrator": {
      "name": "Pénélope Bagieu",
      "sort_as": "Bagieu, Pénélope",
      "identifier": "http://isni.org/isni/0000000121313960"
    },
    "identifier": "urn:isbn:97822531670xx",
    "language": "fr",
    "modified": "2016-07-20T17:00:00Z",
    "published": "2012-01-18",
    "publisher": ["Delcourt", "Mirages"],
    "schema:license": "http://creativecommons.org/licenses/by-sa/3.0",
    "numberOfPages": 8
  },

  "links": [
    {"rel": "self", "href": "http://hadriengardeur.github.io/comics-manifest/examples/PageBlanche/manifest.json", "type": "application/comics+json"}
  ],

  "spine": [
    {"href": "cover.jpg", "type": "image/jpeg", "height": 1577, "width": 1200, "rel": "cover", "title": "Couverture"}, 
    {"href": "PageBlanche_Page_001.jpg", "type": "image/jpeg", "height": 1577, "width": 1200, "properties": "page-left"}, 
    {"href": "PageBlanche_Page_002.jpg", "type": "image/jpeg", "height": 1577, "width": 1200, "properties": "page-right", "title": "Dédicaces"}, 
    {"href": "PageBlanche_Page_003.jpg", "type": "image/jpeg", "height": 1577, "width": 1200, "properties": "page-left"}, 
    {"href": "PageBlanche_Page_004.jpg", "type": "image/jpeg", "height": 1577, "width": 1200, "properties": "page-right"}, 
    {"href": "PageBlanche_Page_005.jpg", "type": "image/jpeg", "height": 1577, "width": 1200, "title": "Commencer la lecture"}, 
    {"href": "PageBlanche_Page_006.jpg", "type": "image/jpeg", "height": 1577, "width": 1200}, 
    {"href": "PageBlanche_Page_007.jpg", "type": "image/jpeg", "height": 1577, "width": 1200}, 
    {"href": "PageBlanche_Page_008.jpg", "type": "image/jpeg", "height": 1577, "width": 1200}
  ]
}
```


## Introduction

Unlike ebooks, there is no single dominant format for comics or even a real attempt to standardize them.

The closest thing to a dominant format for comics is the CBZ format where:

- all images are contained in a ZIP archive
- the reading order is determined by the name of the images
- there is no standard document providing metadata

Compared to CBZ, the Comics Manifest provides the following additional features:

- support for comics that are either living on the Web (each image is accessible through a URI) or distributed as a single archive
- rich metadata for comics based on schema.org
- comics specific display settings such as double pages or variant covers
- provide panel by panel navigation, with support for transitions

While the Comics Manifest is technically a profile of the [Web Publication Manifest] (https://github.com/HadrienGardeur/webpub-manifest), it has its own media type and file extension in order to maximize compatibilty with dedicated comics apps:

- its media type is `application/comics+json`
- its file extension is `.comics-manifest`

## Metadata

The core metadata for the Comics Manifest are based on [the default context for the Web Publication Manifest](https://github.com/HadrienGardeur/webpub-manifest/tree/master/contexts/default) with the following additional requirements:

- ...

## Listing Images

A comics is divided into multiple images, which are all listed in the `spine` of the manifest, in reading order.

In addition to the normal requirements of a `spine`, all link objects have the following recommendations:
 
 - ...

## Cover

A manifest can also specify the cover of a comics using the "cover" relationship in either `links` or the `spine`:

```json
"links": [{
  "rel": "cover", 
  "href": "http://example.org/cover.jpeg", 
  "type": "image/jpeg", 
  "height": 300, "width": 300}]
```

> TODO: variant covers


## Container

In order to facilitate distribution, both manifest and images can also be distributed using a container.

In this case, all files (individual imagesand manifest) must be contained in a ZIP where the manifest is at the root of the zip and named `manifest.json`.

The container also has the following properties:

- its file extension must be `.comics`
- its media type must be `application/comics+zip`

When an comics is distributed in a container (instead of simply as a manifest), the manifest has the following additional restriction:

- the `spine` must strictly reference images that are present in the container
