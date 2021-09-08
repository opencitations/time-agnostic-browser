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

Ci sono due file di configurazione. Il primo si trova in [time-agnostic-browser/config_library.json](https://github.com/opencitations/time-agnostic-browser/blob/main/time-agnostic-browser/config_library.json) e la sua compilazione è obbligatoria per il corretto funzionamento dell'applicazione. Il secondo si trova in [time-agnostic-browser/config_browser.json](https://github.com/opencitations/time-agnostic-browser/blob/main/time-agnostic-browser/config_browser.json) e serve per migliore l'esperienza utente. Vediamoli uno alla volta. 

### Config library

The configuration file is mainly used to indicate where data and provenance are. In addition, some optional values can be set to make executions faster and more efficient.

- **dataset** (required)
  - **triplestore_urls**: Specify a list of triplestore URLs containing data.  
  - **file_paths**: Specify a list of paths of files containing data.   
- **provenance** (required)
  - **triplestore_urls**: Specify a list of triplestore URLs containing provenance metadata.    
  - **file_paths** Specify a list of paths of files containing provenance metadata.      
- **blazegraph_full_text_search** (optional): Specify an affirmative Boolean value if Blazegraph was used as a triplestore, and a textual index was built to speed up queries. For more information, see [https://github.com/blazegraph/database/wiki/Rebuild_Text_Index_Procedure](https://github.com/blazegraph/database/wiki/Rebuild_Text_Index_Procedure). The allowed values are "true", "1", 1, "t", "y", "yes", "ok", or "false", "0", 0, "n", "f", "no".
- **cache_triplestore_url** (optional): Specifies the triplestore URL to use as a cache to make queries faster.

``` json
  {
      "dataset": {
          "triplestore_urls": ["TRIPLESTORE_URL_1", "TRIPLESTORE_URL_2", "TRIPLESTORE_URL_N"],
          "file_paths": ["PATH_1", "PATH_2", "PATH_N"]
      },
      "provenance": {
          "triplestore_urls": ["TRIPLESTORE_URL_1", "TRIPLESTORE_URL_2", "TRIPLESTORE_URL_N"],
          "file_paths": ["PATH_1", "PATH_2", "PATH_N"]
      },
      "blazegraph_full_text_search": "yes",
      "cache_triplestore_url": "TRIPLESTORE_URL"
  }
```

### Config browser


