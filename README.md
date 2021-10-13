# time-agnostic-browser

**time-agnostic-browser** is a browser application to execute time-travel queries on RDF datasets through a graphical user interface. It is based on the Python package **time-agnostic-library**, whose documentation can be viewed on [https://github.com/opencitations/time-agnostic-library](https://github.com/opencitations/time-agnostic-library).

## Table of Contents

- [User's guide](#users-guide)
  * [Requirements](#requirements)
  * [How to run the application](#how-to-run-the-application)
  * [Configuration files](#configuration-files)
    * [Config library](#config-library)  
    * [Config browser](#config-browser) 

## User's guide

### Requirements

  1. Have Python &ge; 3.7 installed.
  2. Have the Python package time-agnostic-library installed. Otherwise, run the following terminal command:
  ```bash
    pip install time-agnostic-library
  ```

### How to run the application

To launch the application, do the following:
  1. Clone the repository.
  2. Compile the configuration file in [time-agnostic-browser/config_library.json](https://github.com/opencitations/time-agnostic-browser/blob/main/time-agnostic-browser/config_library.json). For more information on how to set it, see [Config library](config-library). 
  3. From the root directory, run the following terminal command:
  ```bash
    python time-agnostic-browser/app.py
  ```
  4. Visit the address [http://127.0.0.1:5000/](http://127.0.0.1:5000/).

### Configuration files

There are two configuration files. The first one is in [time-agnostic-browser/config_library.json](https://github.com/opencitations/time-agnostic-browser/blob/main/time-agnostic-browser/config_library.json) and setting it is mandatory for the proper functioning of the application. The second one is located in [time-agnostic-browser/config_browser.json](https://github.com/opencitations/time-agnostic-browser/blob/main/time-agnostic-browser/config_browser.json) and it improves the user experience. Let’s see them one at a time. 

### Config library

The [config_library.json](https://github.com/opencitations/time-agnostic-browser/blob/main/time-agnostic-browser/config_library.json) file is mainly used to indicate where data and provenance are. In addition, some optional values can be set to make executions faster and more efficient.

- **dataset** (required)
  - **triplestore_urls**: Specify a list of triplestore URLs containing data.  
  - **file_paths**: Specify a list of paths of files containing data.   
- **provenance** (required)
  - **triplestore_urls**: Specify a list of triplestore URLs containing provenance metadata.    
  - **file_paths** Specify a list of paths of files containing provenance metadata.      
- **blazegraph_full_text_search** (optional): Specify an affirmative Boolean value if Blazegraph was used as a triplestore, and a textual index was built to speed up queries. For more information, see [https://github.com/blazegraph/database/wiki/Rebuild_Text_Index_Procedure](https://github.com/blazegraph/database/wiki/Rebuild_Text_Index_Procedure). The allowed values are "true", "1", 1, "t", "y", "yes", "ok", or "false", "0", 0, "n", "f", "no".
- **cache_triplestore_url** (optional): Specifies the triplestore URL to use as a cache to make queries faster.

``` python
# TEMPLATE
{
    "dataset": {
        "triplestore_urls": ["TRIPLESTORE_URL_1", "TRIPLESTORE_URL_2", "TRIPLESTORE_URL_N"],
        "file_paths": ["PATH_1", "PATH_2", "PATH_N"]
    },
    "provenance": {
        "triplestore_urls": ["TRIPLESTORE_URL_1", "TRIPLESTORE_URL_2", "TRIPLESTORE_URL_N"],
        "file_paths": ["PATH_1", "PATH_2", "PATH_N"]
    },
    "blazegraph_full_text_search": "no",
    "cache_triplestore_url": "TRIPLESTORE_URL"
}

# USAGE EXAMPLE
{
    "dataset": {
        "triplestore_urls": ["http://localhost:9999/blazegraph/sparql"],
        "file_paths": []
    },
    "provenance": {
        "triplestore_urls": [],
        "file_paths": ["./provenance.json"],
    },
    "blazegraph_full_text_search": "yes",
    "cache_triplestore_url": "http://localhost:19999/blazegraph/sparql"
}
```

### Config browser

The [config_browser.json](https://github.com/opencitations/time-agnostic-browser/blob/main/time-agnostic-browser/config_browser.json) file allows specifying the dataset’s base URIs: only entities containing those URIs are shown as links, and those URIs are omitted for improved readability. In addition, the [config_browser.json](https://github.com/opencitations/time-agnostic-browser/blob/main/time-agnostic-browser/config_browser.json) file enables the user to customize the properties' order. 

- **base_uris** (optional): a list of base URIs. This information compresses entity names and only shows them as links, while other URIs are displayed as plain text. If this field is left blank, the entity names are reported in extended format, and URIs not corresponding to entities appear clickable. 
- **rules_on_properties_order** (optional): a dictionary whose keys are resources types. Each type’s value is a list, and the items’ order is respected in the interface for the entities of that type.

```python
# TEMPLATE
{
    "base_uris": [BASE_URL_1, BASE_URL_2, BASE_URL_N],
    "rules_on_properties_order": {
        TYPE_1: [PROPERTY_1, PROPERTY_2, PROPERTY_N],
        TYPE_2: [PROPERTY_1, PROPERTY_2, PROPERTY_N],
        TYPE_N: [PROPERTY_1, PROPERTY_2, PROPERTY_N],
    }
}

# USAGE EXAMPLE
{
    "base_urls": ["https://github.com/arcangelo7/time_agnostic/"],
    "rules_on_properties_order": {
        "http://purl.org/spar/datacite/Identifier": [
            "http://www.w3.org/1999/02/22-rdf-syntax-ns#type",
            "http://purl.org/spar/datacite/usesIdentifierScheme",
            "http://www.essepuntato.it/2010/06/literalreification/hasLiteralValue"
        ]
    }
}
```

