Centrifuge with Django
======================

Simple demo site to display events on Google map in real-time.

To run demo

1) Clone this repo

2) Install requirements

```bash
pip install -r requirements.txt
```

3) Add your Centrifuge (must be already running) parameters in `settings.py`:

```python
CENTRIFUGE_ADDRESS = 'http://localhost:8000'
CENTRIFUGE_PROJECT_ID = '1d88332ec09e4ed3805fc1999379bcfd'
CENTRIFUGE_PROJECT_SECRET = '1ee93d4ac83e4ccf87d2bbd0e447275b'
CENTRIFUGE_TIMEOUT = 5
```

4) Run server

```bash
python manage.py runserver 0:8080
```

5) Go to http://localhost:8080


You will see a map and you can start sending events into `map` channel. For example:

```bash
echo '{"channel": "map", "data": {"lat": 33, "long": 55, "content": "I am testing Centrifuge"}}'|cent map publish
```

After this all connected clients will see new event on map.