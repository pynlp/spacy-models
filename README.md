<a href="https://explosion.ai"><img src="https://explosion.ai/assets/img/logo.svg" width="125" height="125" align="right" /></a>

# spaCy models
This repository contains [releases](https://github.com/explosion/spacy-models/releases)
of models for the [spaCy](https://github.com/explosion/spaCy) NLP library. For
more info on how to download, install and use the models, see the
[models documentation](https://spacy.io/usage/models).

> **⚠️ Important note:** Because the models can be very large and consist mostly
> of binary data, we can't simply provide them as files in a GitHub repository.
> Instead, we've opted for adding them to
> [releases](https://github.com/explosion/spacy-models/releases) as `.tar.gz`
> files. This allows us to still maintain a public release history.

## Quickstart

To install a specific model, run the following command with the model name
(for example `en_core_web_sm`):

```bash
python -m spacy download [model]
```

* [spaCy v2.x models directory](https://alpha.spacy.io/models/)
* [spaCy v2.x model comparison](https://alpha.spacy.io/models/comparison)
* [Individual release notes](https://github.com/explosion/spacy-models/releases)

For the spaCy v1.x models, [see here](#spacy-v1x-releases).

## Model naming conventions

In general, spaCy expects all model packages to follow the naming convention of
`[lang]_[name]`. For our models, we also chose to divide the name into three
components:

* **type**: Model capabilities (e.g. `core` for general-purpose model with vocabulary, syntax, entities and word vectors, or `depent` for only vocab, syntax and entities)
* **genre**: Type of text the model is trained on (e.g. `web` for web text, `news` for news text)
* **size**: Model size indicator (`sm`, `md` or `lg`)

For example, `en_depent_web_md` is a medium-sized English model trained on
written web text (blogs, news, comments), that includes vocabulary, syntax and
entities.

### Model versioning

Additionally, the model versioning reflects both the compatibility with spaCy,
as well as the major and minor model version. A model version `a.b.c`
translates to:

* `a`: **spaCy major version**. For example, `2` for spaCy v2.x.
* `b`: **Model major version.** Models with a different major version can't be loaded by the same code. For example, changing the width of the model, adding hidden layers or changing the activation changes the model major version.
* `c`: **Model minor version.** Same model structure, but different parameter values, e.g. from being trained on different data, for different numbers of iterations, etc.

For a detailed compatibility overview, see the [`compatibility.json`](compatibility.json).
This is also the source of spaCy's internal compatibility check, performed when you
run the `download` command.

### Support for older versions

If you're using an older version (v1.6.0 or below), you can still download and
install the old models from within spaCy using `python -m spacy.en.download all`
or `python -m spacy.de.download all`. The `.tar.gz` archives are also
[attached to the v1.6.0 release](https://github.com/explosion/spaCy/tree/v1.6.0).
To download and install the models manually, unpack the archive, drop the
contained directory into `spacy/data` and load the model via `spacy.load('en')`
or `spacy.load('de')`.

## Downloading models

To increase transparency and make it easier to use spaCy with your own models,
all data is now available as direct downloads, organised in
[individual releases](https://github.com/explosion/spacy-models/releases). spaCy
1.7 also supports installing and loading models as **Python packages**. You can
now choose how and where you want to keep the data files, and set up "shortcut
links" to load models by name from within spaCy. For more info on this, see the
new [models documentation](https://spacy.io/usage/models).

```bash
# download best-matching version of specific model for your spaCy installation
python -m spacy download en_core_web_sm

# out-of-the-box: download best-matching default model
python -m spacy download en

# pip install .tar.gz archive from path or URL
pip install /Users/you/en_core_web_sm-2.1.0.tar.gz
pip install https://github.com/explosion/spacy-models/releases/download/en_core_web_sm-2.1.0/en_core_web_sm-2.1.0.tar.gz
```

## Loading and using models

To load a model, use `spacy.load()` with the model name, a shortcut link or
a path to the model data directory.

```python
import spacy
nlp = spacy.load("en_core_web_sm")
doc = nlp(u"This is a sentence.")
```

If you've installed a model via pip, you can also `import` it directly and
then call its `load()` method with no arguments. This should also work for
older models in previous versions of spaCy.

```python
import spacy
import en_core_web_sm

nlp = en_core_web_sm.load()
doc = nlp(u"This is a sentence.")
```

## Manual download and installation

In some cases, you might prefer downloading the data manually, for example to
place it into a custom directory. You can download the model via your browser from
the [latest releases](https://github.com/explosion/spacy-models/releases), or
configure your own download script using the URL of the archive file. The archive
consists of a model directory that contains another directory with the model data.

```yaml
└── en_core_web_sm-2.0.0.tar.gz       # downloaded archive
    ├── meta.json                     # model meta data
    ├── setup.py                      # setup file for pip installation
    └── en_core_web_md                # model directory
        ├── __init__.py               # init for pip installation
        ├── meta.json                 # model meta data
        └── en_core_web_sm-2.0.0      # model data
```

You can place the model data directory anywhere on your local file system. To
use it with spaCy, simply assign it a name by creating a shortcut link for the 
data directory.

**📖 For more info and examples, check out the [models documentation](https://spacy.io/usage/models).**

## spaCy v1.x Releases

| Date | Model | Version | Dep | Ent | Vec | Size | License | | |
| --- | --- | --- | :---: | :---: | :---: | ---: | --- | --- | --- |
| `2017-06-06` | `es_core_web_md` | 1.0.0 | X | X | X | 377 MB | CC BY-SA | [![][i]][i-es_core_web_md-1.0.0] | [![][dl]][es_core_web_md-1.0.0]
| `2017-04-26` | `fr_depvec_web_lg` | 1.0.0 | X | | X | 1.33 GB | CC BY-NC | [![][i]][i-fr_depvec_web_lg-1.0.0] | [![][dl]][fr_depvec_web_lg-1.0.0]
| `2017-03-21` | `en_core_web_md` | 1.2.1 | X | X | X | 1 GB | CC BY-SA | [![][i]][i-en_core_web_md-1.2.1] | [![][dl]][en_core_web_md-1.2.1]
| `2017-03-21` | `en_depent_web_md` | 1.2.1 | X | X | | 328 MB | CC BY-SA | [![][i]][i-en_depent_web_md-1.2.1] | [![][dl]][en_depent_web_md-1.2.1]
| `2017-03-17` | `en_core_web_sm` | 1.2.0 | X | X | X | 50 MB | CC BY-SA | [![][i]][i-en_core_web_sm-1.2.0] | [![][dl]][en_core_web_sm-1.2.0]
| `2017-03-17` | `en_core_web_md` | 1.2.0 | X | X | X | 1 GB | CC BY-SA | [![][i]][i-en_core_web_md-1.2.0] | [![][dl]][en_core_web_md-1.2.0]
| `2017-03-17` | `en_depent_web_md` | 1.2.0 | X | X | | 328 MB | CC BY-SA | [![][i]][i-en_depent_web_md-1.2.0] | [![][dl]][en_depent_web_md-1.2.0]
| `2016-05-10` | `de_core_news_md` | 1.0.0 | X | X | X | 645 MB | CC BY-SA | [![][i]][i-de_core_news_md-1.0.0] | [![][dl]][de_core_news_md-1.0.0]
| `2016-03-08` | `en_vectors_glove_md` | 1.0.0 | | | X | 727 MB | CC BY-SA | [![][i]][i-en_vectors_glove_md-1.0.0] | [![][dl]][en_vectors_glove_md-1.0.0]

[es_core_web_md-1.0.0]: https://github.com/explosion/spacy-models/releases/download/es_core_web_md-1.0.0/es_core_web_md-1.0.0.tar.gz
[fr_depvec_web_lg-1.0.0]: https://github.com/explosion/spacy-models/releases/download/fr_depvec_web_lg-1.0.0/fr_depvec_web_lg-1.0.0.tar.gz
[en_core_web_md-1.2.1]: https://github.com/explosion/spacy-models/releases/download/en_core_web_md-1.2.1/en_core_web_md-1.2.1.tar.gz
[en_depent_web_md-1.2.1]: https://github.com/explosion/spacy-models/releases/download/en_depent_web_md-1.2.1/en_depent_web_md-1.2.1.tar.gz
[en_core_web_sm-1.2.0]: https://github.com/explosion/spacy-models/releases/download/en_core_web_sm-1.2.0/en_core_web_sm-1.2.0.tar.gz
[en_core_web_md-1.2.0]: https://github.com/explosion/spacy-models/releases/download/en_core_web_md-1.2.0/en_core_web_md-1.2.0.tar.gz
[en_depent_web_md-1.2.0]: https://github.com/explosion/spacy-models/releases/download/en_depent_web_md-1.2.0/en_depent_web_md-1.2.0.tar.gz
[de_core_news_md-1.0.0]: https://github.com/explosion/spacy-models/releases/download/de_core_news_md-1.0.0/de_core_news_md-1.0.0.tar.gz
[en_vectors_glove_md-1.0.0]: https://github.com/explosion/spacy-models/releases/download/en_vectors_glove_md-1.0.0/en_vectors_glove_md-1.0.0.tar.gz

[i-es_core_web_md-1.0.0]: https://github.com/explosion/spacy-models/releases/es_core_web_md-1.0.0
[i-fr_depvec_web_lg-1.0.0]: https://github.com/explosion/spacy-models/releases/fr_depvec_web_lg-1.0.0
[i-en_core_web_md-1.2.1]: https://github.com/explosion/spacy-models/releases/en_core_web_md-1.2.1
[i-en_depent_web_md-1.2.1]: https://github.com/explosion/spacy-models/releases/en_depent_web_md-1.2.1
[i-en_core_web_sm-1.2.0]: https://github.com/explosion/spacy-models/releases/en_core_web_sm-1.2.0
[i-en_core_web_md-1.2.0]: https://github.com/explosion/spacy-models/releases/en_core_web_md-1.2.0
[i-en_depent_web_md-1.2.0]: https://github.com/explosion/spacy-models/releases/en_depent_web_md-1.2.0
[i-de_core_news_md-1.0.0]: https://github.com/explosion/spacy-models/releases/de_core_news_md-1.0.0
[i-en_vectors_glove_md-1.0.0]: https://github.com/explosion/spacy-models/releases/en_vectors_glove_md-1.0.0

[dl]: http://i.imgur.com/gQvPgr0.png
[i]: http://i.imgur.com/OpLOcKn.png

## Issues and bug reports

To report an issue with a model, please open an issue on the
[spaCy issue tracker](https://github.com/explosion/spaCy).
Please note that no model is perfect. Because models are statistical, their
expected behaviour **will always include some errors**. However, particular
errors can indicate deeper issues with the training feature extraction or
optimisation code. If you come across patterns in the model's performance that
seem suspicious, please do file a report.
