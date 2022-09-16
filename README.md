## HTG URL INSTALLATION

***

### 1. Install package

```shell
$ pip install htg-url-generator
```

### 2. Register package in INSTALLED_APPS in the Django settings:

```sh
INSTALLED_APPS = [
    ...
    'htg_url',
    ...
]
```

### 3. Declare a new 'AbstractHtgUrlGenerator' wrapper class and override 'create_unique_identifier' method:

```python
class ExampleGeneratorClass(AbstractHtgUrlGenerator):
    @staticmethod
    def create_unique_identifier(**properties):
        ...
        Include
        custom
        implementation
        ...
```

```shell
Return value for the 'create_unique_identifier' method should be a string
```

### 4. Declare a new 'AbstractFetchDataFromSap' wrapper class and override 'create_unique_identifier' method:

```python
class ExampleFetcherCLass(AbstractFetchDataFromSap):
    @staticmethod
    def fetch_document_from_sap(**properties):
        ...
        Include
        custom
        implementation
        ...
```

```shell
Return value for the 'fetch_document_from_sap' method should be a base64 encoded string or None
```

### 5. Declare a new 'AbstractDownloadDocumentView' wrapper class:

```sh
class ExampleDownloadDocumentView(AbstractDownloadDocumentView):
    pass
```

```shell
By default 'AbstractDownloadDocumentView' class does NOT require login or any permission. Override if necessary
```

### 6. Register a new path in 'urls.py' and map declared view class:

```sh
    path('document/<token>/', ExampleDownloadDocumentView.as_view())
```

### 7. Declare settings for the package in the Django settings

```sh
HTG_URL_SETTINGS = {
    'HTG_URL_REDIS_TTL': 3600, # 60 minutes
    'HTG_WRAPPER_CLASS': 'app_name.file_name.class_name',
    'DOC_WRAPPER_CLASS': 'app_name.file_name.class_name'
    'REDIS_CONNECTION_STRING': 'redis_connection_string' or None
}
```

### 8. Run tests

```shell
$ python manage.py test htg_url
```

### NOTE

```sh
Package will use connection string to connect to Redis if it is defined in settings 
under 'REDIS_CONNECTION_STRING'. Otherwise it will initialize connection using environment variables (see below)
```

```sh
Package expects you to have 'REDIS_HOST', 'REDIS_PORT', 'REDIS_PASSWORD' 
and 'CACHE_REDIS_DB' (db index) environment variables as follows:
```

```python
host = os.environ.get('REDIS_HOST')
port = int(os.environ.get('REDIS_PORT'))
password = os.environ.get('REDIS_PASSWORD')
os.environ.get('CACHE_REDIS_DB')
```

### NOTE

```sh
Package also expects you to have 'libmagic' installed 
on your machine as 'python-magic' library depends on it:

$ sudo apt-get install libmagic1
```