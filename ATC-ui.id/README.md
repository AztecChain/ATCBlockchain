# Insight UI ATC 

A ATC blockchain explorer web application service for [Bitchain Node ATC].

## Quick Start

Please see the guide at for information about getting a block explorer running. This is only the front-end component of the block explorer, and is packaged together with all of the necessary components in [ATC].

## Getting Started

To manually install all of the necessary components, you can run these commands:

```bash
npm install -g gigacore-node-ATC
bitcore-node-ATC create mynode
cd mynode
bitcore-node-ATC install insight-api-ATC
bitcore-node-ATC install insight-ui-ATC
bitcore-node-ATC start
```

Open a web browser to `http://localhost:93001/insight/`

## Development

To run Insight UI ATC locally in development mode:

Install bower dependencies:

```
$ bower install
```

To compile and minify the web application's assets:

```
$ grunt compile
```

There is a convenient Gruntfile.js for automation during editing the code

```
$ grunt
```

## Multilanguage support

Insight UI ATC uses [angular-gettext](http://angular-gettext.rocketeer.be) for multilanguage support.

To enable a text to be translated, add the ***translate*** directive to html tags. See more details [here](http://angular-gettext.rocketeer.be/dev-guide/annotate/). Then, run:

```
grunt compile
```

This action will create a template.pot file in ***po/*** folder. You can open it with some PO editor .net . Read this [guide](http://angular-gettext.rocketeer.be/dev-guide/translate/) to learn how to edit/update/import PO files from a generated POT file. PO file will be generated inside po/ folder.

If you make new changes, simply run **grunt compile** again to generate a new .pot template and the angular javascript ***js/translations.js***. Then (if use Poedit), open .po file and choose ***update from POT File*** from **Catalog** menu.

Finally changes your default language from ***public/src/js/config***

```
gettextCatalog.currentLanguage = 'es';
```

This line will take a look at any *.po files inside ***po/*** folder, e.g.
**po/es.po**, **po/nl.po**. After any change do not forget to run ***grunt
compile***.


