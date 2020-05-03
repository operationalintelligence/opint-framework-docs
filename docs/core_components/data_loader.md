# BaseLoader

The BaseLoader is the base skeleton implementation of the frameworks data loaders

It provides basic caching and abstract classes for other loaders to inherit and use.

Example of usage can be found at the [HDFSLoader](data_loader_hdfs.md)

## Methods

### fetch_data

`fetch_data` makes the connection to external source and fetches the data.\
This method should be completely overwritten by the parent.

```python
fetch_data(cls, **kwargs)
```
:return: (data fetched from source)

### translate_data

`translate_data` translates the data from the source format to any desired format.\
This method can be overwritten by the parent

```python
translate_data(cls, data, **kwargs)
```
:return: (data translated to desired format)

### load_data

`load_data` is the method that initialises `fetch_data` pipelines them through `translate_data` and stores them to a cache file (if a cache argument is provided).\

This method shouldn't be overwritten by the parent.

```python
load_data(cls, **kwargs)
```

optional 'parameter' `cache`: file path to cache return of loader\
:return: (data loaded from url, etag)
