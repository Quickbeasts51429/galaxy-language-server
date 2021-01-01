# Galaxy Language Server

[![Actions Status](https://github.com/davelopez/galaxy-language-server/workflows/Language%20Server%20CI/badge.svg)](https://github.com/davelopez/galaxy-language-server/actions)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
![PyPI - Python Version](https://img.shields.io/pypi/pyversions/galaxy-language-server)
[![PyPI version](https://badge.fury.io/py/galaxy-language-server.svg)](https://badge.fury.io/py/galaxy-language-server)

The aim of this project is to implement the [Language Server Protocol](https://microsoft.github.io/language-server-protocol/) to assist in the development of [Galaxy tool wrappers](https://docs.galaxyproject.org/en/latest/dev/schema.html) inside modern code editors.

> The idea is to provide realtime XML validation, code completion, help/documentation and other *smart* features to help in following best practices during the development process of XML tool wrappers for Galaxy.

This repository contains both the [server](https://github.com/davelopez/galaxy-language-server/tree/master/server) implementation in [Python](https://www.python.org/) and the [client](https://github.com/davelopez/galaxy-language-server/tree/master/client) implementation of a [Visual Studio Code](https://code.visualstudio.com/) [extension](https://marketplace.visualstudio.com/VSCode) in [Node.js](https://nodejs.org/en/).

> Please note this is still a work in progress so **bugs and issues are expected**. If you find any, you are welcome to open a new [issue](https://github.com/galaxyproject/galaxy-language-server/issues).

## Features
### Tag and attribute auto-completion 

![Demo feature auto-completion](../assets/feature.autocompletion.gif)

The tags and attributes are suggested based on the [Galaxy.xsd](https://github.com/galaxyproject/galaxy/blob/dev/lib/galaxy/tool_util/xsd/galaxy.xsd) schema. They will appear in the same order that they are declared in the schema, so they can comply with the best practices recommendations defined in the [Galaxy IUC Standards Style Guide](https://galaxy-iuc-standards.readthedocs.io/en/latest/best_practices/tool_xml.html?#coding-style).


### Documentation on Hover

![Demo feature hover documentation](../assets/feature.hover.documentation.gif)

The documentation of tags and attributes is retrieved from the [Galaxy.xsd](https://github.com/galaxyproject/galaxy/blob/dev/lib/galaxy/tool_util/xsd/galaxy.xsd) schema.
>Please note that some elements in the schema are still missing documentation. This will probably be improved over time.


### Document validation

![Demo feature validation](../assets/feature.validation.png)

The tools are also validated against the [Galaxy.xsd](https://github.com/galaxyproject/galaxy/blob/dev/lib/galaxy/tool_util/xsd/galaxy.xsd) schema.


### Document auto-formatting

![Demo feature auto-formatting](../assets/feature.autoformat.gif)

When the tool file is saved it gets auto-formatted to maintain a consistent format with the [Galaxy IUC Standards Style Guide](https://galaxy-iuc-standards.readthedocs.io/en/latest/best_practices/tool_xml.html?#coding-style).

### Tag auto-closing

![Demo feature auto-close tags](../assets/autoCloseTag.gif)

Whenever you write a closing ``>`` the corresponding closing tag will be inserted. You can also type ``/`` in an open tag to close it.


### Snippets

![Demo snippets](../assets/snippets.gif)

Snippets can be really helpful to speed up your tool wrapper development. They allow to quickly create common blocks and let you enter just the important information by pressing ``tab`` and navigating to the next available value.
>If you want to add more snippets check the [guide](./docs/CONTRIBUTING.md#adding-snippets) in the contribution guidelines.

---

# Getting Started
If you just want to use the Galaxy Language Server, the easiest option is to install the VSCode extension from the [Market](https://marketplace.visualstudio.com/items?itemName=davelopez.galaxy-tools) or the [Open VSX registry](https://open-vsx.org/extension/davelopez/galaxy-tools). Additionally you can download the VSIX package from the [releases](https://github.com/galaxyproject/galaxy-language-server/releases) and install it manually.

If you are considering contributing, please read the [contribution guide](docs/CONTRIBUTING.md).

To setup your development environment you can read [this guide](docs/CONTRIBUTING.md#getting-started).


## How to manually run the server
Usually, the [client](../client) will be in charge of running the server when it is needed, but, in case you want to run it manually for some reason, you can use the following (let's assume a clean start):

````sh
git clone https://github.com/galaxyproject/galaxy-language-server.git
cd galaxy-language-server/server
python3 -m venv myenv
source ./myenv/bin/activate
python3 -m pip install -r ./requirements.txt

python3 -m galaxyls
````

By default, the server uses IO pipes to communicate with the client. If you want to use TCP, you can pass additional parameters, for example:

````sh
python3 -m galaxyls --tcp --host=127.0.0.1 --port=2087
````

To check if everything went ok, you can look at the content of the server log file (``galaxy-language-server.log``) that should contain the following lines:
````
INFO:pygls.server:Starting server on 127.0.0.1:2087
INFO:pygls.server:Shutting down the server
INFO:pygls.server:Closing the event loop.
````
