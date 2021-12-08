## INSTALLATION

***


### 1. Install package

```sh
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

```sh
class HtgUrlGenerator(AbstractHtgUrlGenerator):
    @staticmethod
    def create_unique_identifier(**properties):
        ...
        Include custom implementation
        ...
```

### 4. Declare a new 'AbstractFetchDataFromSap' wrapper class and override 'create_unique_identifier' method:

```sh
class FetchDataFromSap(AbstractFetchDataFromSap):
    @staticmethod
    def fetch_document_from_sap(**properties):
        ...
        Include custom implementation
        ...
```

### 5. Declare a new 'AbstractDownloadDocumentView' wrapper class:

```sh
class DownloadDocumentView(AbstractDownloadDocumentView):
    pass
```


### 6. Register a new path in 'urls.py' and map declared view class:
```sh
    path('document/<token>/', DownloadDocumentView.as_view())
```

### 7. Declare settings for the package in the Django settings
```sh
HTG_URL_SETTINGS = {
    'HTG_URL_REDIS_TTL': 216000,
    'HTG_WRAPPER_CLASS': 'app_name.file_name.class_name',
    'DOC_WRAPPER_CLASS': 'app_name.file_name.class_name'
}
```