# Guide to using CKAN for data wranglers

This guide is about adding and managing data in CKAN programmatically. This guide assumes

* You are familiar with key concepts like metadata, data etc
* You are working programmatically e.g. in one of Python, R, Javascript etc.

## Quick start

This guide currently assumes you are using Python. R and Javascript examples are coming soon.

### Prerequisites

Install the SDK for your language and configure it:

Visit the repo and follow the instructions here: https://github.com/datopian/ckan3-py-sdk#install

Create a client:

```
from ckanclient import Client

endpoint = 'https://my-ckan.com/'
token = 'xxxx'              # your CKAN API key
org_name = 'my-org'         # default organization on CKAN to add datasets to
client = Client(endpoint, token, org_name)
```

 We will also use the Frictionless library in what follows:

```
from ckanclient import f11s
```

### Upload a resource (file) (and implicitly create a new Dataset)

```python=
# loads a resource from a path
resource = f11s.load(resource_file_path)
dataset_name = 'sample-dataset'
dataset = f11s.Dataset({'name': dataset_name})
dataset.add_resource(resource)
```

### Create a new empty Dataset with metadata

```python=
dataset = f11s.Dataset({
  'name': dataset_name,
  'metadata': {'maintainer_email': 'sample@datopian.com'}}
)
client.push(dataset)
```

### Adding a resource to an existing Dataset

```python=
resource_path = 'sample.csv'

# this will upload the file and add the resource to the dataset
# NB: resource metadata e.g. name, title etc will be auto-inferred from the file
client.push_resource(
  resource_path,
  dataset='dataset-name',
  append=True
  )

# edit resource metadata before pushing ...
# TODO
```

### Edit a Dataset's metadata

WARNING: not implemented yet.

```python=
dataset = client.get_dataset(dataset_name='sample_dataset')
client.update_metadata(dataset=dataset, 'metadata': {'maintainer_email': 'sample@datopian.com'})
```

### Create the metadata for a new Dataset (prior to adding it to CKAN)

This does not involve the SDK!

template (optional)
edit
validate

You want the validation to output useful errors.

This is Frictionless stuff.

```python=

```

