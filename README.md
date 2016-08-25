# httsleep

httsleep is a powerful polling library for Python.

[![Build Status](https://travis-ci.org/kopf/httsleep.svg?branch=master)](https://travis-ci.org/kopf/httsleep)

[![Coverage Status](https://coveralls.io/repos/github/kopf/httsleep/badge.svg?branch=master)](https://coveralls.io/github/kopf/httsleep?branch=master)

## Idea

```
   until = {
       'status_code': 200,
       'jsonpath': [{'expression': 'status', 'value': 'OK'}]
   }
   alarms = [
       {'json': {'status': 'ERROR'}},
       {'jsonpath': [{'expression': 'status', 'value': 'UNKNOWN'},
                     {'expression': 'owner', 'value': 'Chris'}],
       'callback': is_job_really_failing},
       {'status_code': 404}
   ]
   httsleep('http://myendpoint/jobs/1', until, alarms=alarms,
            max_retries=20)
```

Translated into English, this means:

* Poll ``http://myendpoint/jobs/1`` -- at most 20 times -- until
    * it returns a status code of ``200``
    * AND the ``status`` key in its response has the value ``OK``
* but raise an error if
    * the ``status`` key has the value ``ERROR``
    * OR the ``status`` key has the value ``UNKNOWN`` AND the ``owner`` key has the value ``Chris`` AND the function ``is_job_really_dying`` returns ``True``
    * OR the status code is 404

## Documentation 

(TODO: Link here once doc is published)

## Installing

```
pip install httsleep
```

## Testing

```
pip install -e .
pip install -r test-requirements.txt
py.test
```
