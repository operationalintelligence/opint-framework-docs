# Feedback Mechanism

A basic feedback mechanism has been implemented to give the app developers the posibility to record feedback.

This feature requires a database to be configured in the freamework to be used.


## Schema

The schema of the Feedback model is the following:
```python
class Feedback(models.Model):
    """
    Feedback object.
    """

    model = models.CharField(max_length=512)
    object_pk = models.CharField(max_length=512)
    url = models.CharField(max_length=512, blank=True)
    comment = models.TextField(blank=True)
    extra_data = models.TextField(blank=True)
    created = models.DateTimeField(auto_now=True)
``` 

`model`: That is the name of the entity that the feedback is recorded for (e.g. Error, Classification, ProposedAction)

`object_pk`: The specific object that the feedback concerns.

`url`: A url to some external source (e.g. JIRA or GGUS ticket, Github Issue etc). This field can be left blank.

`comment`: A comment for the feedback. This field can be left blank.

`extra_data`: A free-text field that can be populated by any other data (e.g. a JSON blob). This field can be left blank.

`created`: The date the feedback has been recorded in the database,

## API

There is an API provided to fetch recorded feedback and record feedback into the system.


The following examples consider `http://127.0.0.1:8000/` as the domain name.

### GET API example

The followin call would return a list of all the feedback items.

```bash
curl http://127.0.0.1:8000/core/api/feedback/
```

#### Example return: 
The return is paginated at every 100 results. 
```json
{
    "count": 2,
    "next": null,
    "previous": null,
    "results": [
        {
            "id": 1,
            "model": "ExampleModel",
            "object_pk": "1",
            "url": "aurls.com",
            "comment": "",
            "extra_data": "",
            "created": "2020-05-19T14:53:12.112352Z"
        },
        {
            "id": 2,
            "model": "ExampleModel",
            "object_pk": "2",
            "url": "",
            "comment": "This is a comment",
            "extra_data": "{'comment_id': 12}",
            "created": "2020-05-19T14:53:28.765564Z"
        }
    ]
}
```


### POST API example

The following call would create a new feedback item:

```bash
curl -d '{ "model": "ExampleModel", "object_pk": "1", "url": "aurls.com"}'  -H 'Content-Type: application/json' http://127.0.0.1:8000/core/api/feedback/
```

#### Example return: 

```json
{"id":1,"model":"ExampleModel","object_pk":"1","url":"aurls.com","comment":"","extra_data":"","created":"2020-05-19T14:53:12.112352Z"}%
```