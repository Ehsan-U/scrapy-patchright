# scrapy-patchright: Patchright integration for Scrapy

## Installation

`scrapy-patchright` is available on PyPI and can be installed with `pip`:

```
pip install scrapy-patchright
```

`patchright` is defined as a dependency so it gets installed automatically,
however it might be necessary to install the specific browser(s) that will be
used:

```
playwright install
```

It's also possible to install only a subset of the available browsers:

```
playwright install chromium
```

## Changelog

See the [changelog](docs/changelog.md) document.


## Activation

### Download handler

Replace the default `http` and/or `https` Download Handlers through
[`DOWNLOAD_HANDLERS`](https://docs.scrapy.org/en/latest/topics/settings.html):

```python
# settings.py
DOWNLOAD_HANDLERS = {
    "http": "scrapy_patchright.handler.ScrapyPatchrightDownloadHandler",
    "https": "scrapy_patchright.handler.ScrapyPatchrightDownloadHandler",
}
```

Note that the `ScrapyPatchrightDownloadHandler` class inherits from the default
`http/https` handler. Unless explicitly marked (see [Basic usage](#basic-usage)),
requests will be processed by the regular Scrapy download handler.


### Twisted reactor

[Install the `asyncio`-based Twisted reactor](https://docs.scrapy.org/en/latest/topics/asyncio.html#installing-the-asyncio-reactor):

```python
# settings.py
TWISTED_REACTOR = "twisted.internet.asyncioreactor.AsyncioSelectorReactor"
```

This is the default in new projects since [Scrapy 2.7](https://github.com/scrapy/scrapy/releases/tag/2.7.0).
