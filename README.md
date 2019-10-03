
# Welcome to the Scava documentation

This repository contains all the documentation pertaining to the [Eclipse Scava project](https://projects.eclipse.org/projects/technology.scava).

[![Documentation Status](https://readthedocs.org/projects/scava-docs/badge/?version=latest)](https://scava-docs.readthedocs.io/en/latest/?badge=latest)

The documentation system used for Scava relies on Markdown files, stored in the `docs/` directory.
These can be converted to a full static web site using [mkdocs](https://www.mkdocs.org). The configured output directory for html files is `site/`, which can then be served directly by any web server.

The intended deployment site is:

* ReadTheDocs: [https://scava-docs.readthedocs.io](https://scava-docs.readthedocs.io)

## Building the web site

Simply execute the following command at the root of the directory.

```
boris@kadath:gh_crossminer_scava-docs$ mkdocs build --clean
INFO    -  Cleaning site directory
INFO    -  Building documentation to directory: /home/boris/Projects/gh_crossminer_scava-docs/site
boris@kadath:gh_crossminer_scava-docs$
```


## About Scava

* Eclipse Scava project page: https://projects.eclipse.org/projects/technology.scava
* Scava official repository for code: https://github.com/crossminer/scava
* Scava Official repository for documentation: https://scava-docs.readthedocs.io
* Licencing for this repository: EPL v2, as described in the [LICENSE.txt](LICENSE.txt)
