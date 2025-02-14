## APP.ANY.RUN CLIENT [![Build Status](https://travis-ci.com/mwalkowski/anyrun.svg?branch=master)](https://travis-ci.com/mwalkowski/anyrun) [![codecov](https://codecov.io/gh/mwalkowski/anyrun/branch/master/graph/badge.svg)](https://codecov.io/gh/mwalkowski/anyrun) [![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0) [![PyPI version](https://badge.fury.io/py/anyrun.svg)](https://badge.fury.io/py/anyrun)

This is a package that allows downloading and searching malware analysis from public submissions from [app.any.run](https://app.any.run).
It is built as a websocket client application 

### Features


- Register to all public submissions
- Requirements

   - websocket_client==0.56.0
   - Python 3.5, 3.6, 3.7

### Installation


You can install django-celery-results either via the Python Package Index (PyPI)
or from source.

To install using `pip`,::

    $ pip install -U anyrun
 
### QuickStart

```
from anyrun import AnyRunClient


def callback(msg: dict) -> None:
    print(msg)


if __name__ == "__main__":
    client = AnyRunClient(
        on_message_cb=callback,
        enable_trace=False
    )
    client.connect()
    client.run_forever()

````
And as a response you should get
```
...
...
{'msg': 'added', 'collection': 'tasks', 'id': '5cf6d8005ed7525c25fe5660', 'fields': ... }
...
...
```
If You want use filters

```
from anyrun import AnyRunClient


def callback(msg: dict) -> None:
    print(msg)


if __name__ == "__main__":
    client = AnyRunClient(
        on_message_cb=callback,
        enable_trace=False
    )
    client.filter(params = {'tag':'trojan'}) #You can add any filter available in any.run
    client.connect()
    client.run_forever()

````
And as a response you should get
```
...
...
{{"msg":"added","collection":"tasks","id":"5d0ca3db1cf0363374c72d5e",...,"tags":["trojan","nanocore","rat"],... }
...
...
```

### Settings

|param|description|
|---|---|
|enable_trace| enables debug trace logs, default: False|


Testing
-------
You can run the tests by creating a Python virtual environment, installing
the requirements from `test_requirements.txt` 
```
pip install -r requirements.txt -r test_requirements.txt
```
Then:   
```
python pytest -v
```

TODO
----

- Add support for search.
- More examples.