from itertools import product, islice
from joblib import Parallel, delayed
import json
import requests
from requests.exceptions import ConnectionError, Timeout
from simplejson import JSONDecodeError
import string

CLIENT_ID = 'a48b4d0f6e0745e2ba68902a1f68f8d5'
URL = 'https://api.instagram.com/oembed/media/?url=http://instagram.com/p/{sc}'


def generate(length=4, start=3500000, end=4000000):
    return islice((''.join(entry) for entry in product(string.ascii_letters + string.digits, repeat=length)),
                  start, end)


def _validate(shortcode, verbose=True):
    url = URL.format(sc=shortcode)

    try:
        data = requests.get(url, timeout=60).json()
    except (IOError, TypeError, JSONDecodeError, Timeout, ConnectionError):
        return

    try:
        url, user, title = data['url'], data['author_name'], data['title']
    except KeyError:
        return

    print(user)

    return shortcode, dict(url=url, user=user, title=title)


def validate(threads=500, verbose=True):
    if verbose:
        v_int = 100
    else:
        v_int = 0

    try:
        with open('codes.json') as file:
            prev_data = json.load(file)
    except FileNotFoundError:
        prev_data = dict()

    data = Parallel(n_jobs=threads, verbose=v_int)(delayed(_validate)(shortcode=shortcode, verbose=verbose)
                                                   for shortcode in generate())

    data = [entry for entry in data if entry] + list(prev_data.items())

    with open('codes.json', 'w') as writefile:
        json.dump(dict(data), writefile, indent=4, sort_keys=True, separators=(',', ': '))


if __name__ == "__main__":
    validate()
