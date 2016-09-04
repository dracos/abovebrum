abovebrum
=========

Code that powers the [@abovebrum Twitter account](https://twitter.com/abovebrum).

There are three scripts:

* scrape – runs daily to fetch the flare/ISS times from heavens-above.com
* weather – runs hourly to fetch the latest weather from forecast.io
* twitter – runs every five minutes to see if something is coming up that needs
  to be sent to Twitter.

Installation
------------

Register an application at [https://apps.twitter.com](https://apps.twitter.com)
in order to get a consumer key and secret, and an access token and secret.
Register with [https://developer.forecast.io](forecast.io) to get an API key.

Install the needed requirements:

```
$ virtualenv venv
$ source venv/bin/activate
$ pip install -r requirements.txt
```

Clone the repository:

```
$ git clone https://github.com/dracos/abovebrum
$ cd abovebrum
$ cp config.py-example config.py
```

Now open up config.py and change the co-ordinates to wherever you want to run
the service (that's for looking up flare times). Put your tokens and
secrets in the appropriate places to enable Twitter posting access and
forecast.io lookup.

Set up cronjobs (or however you want to do it) that run `weather` every hour,
`scrape` once a day, and `twitter` every five minutes, something like:

```
2 2 * * * /home/matthew/bin/abovebrum/venv/bin/python /home/matthew/bin/abovebrum/scrape
57 * * * * /home/matthew/bin/abovebrum/venv/bin/python /home/matthew/bin/abovebrum/weather
*/5 * * * * /home/matthew/bin/abovebrum/venv/bin/python /home/matthew/bin/abovebrum/twitter
```

That should be it.
