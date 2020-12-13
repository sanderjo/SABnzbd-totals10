# SABnzbd totals10.sab

SABnzbd puts download statistics in `totals10.sab`.
The format of the file is "pickle".

It's easy to pretty-print-dump the contents of the pickle file `totals10.sab`:

```
#!/usr/bin/env python3
import pickle, pprint
with open('totals10.sab', 'rb') as handle:
	b = pickle.load(handle)
	pprint.pprint(b)
```

First lines:


```
(1607861442.0529296,
 {'127.0.0.1': 6696,
  'client.newshosting.com': 6232,
  'eunews2.frugalusenet.com': 271619083506,
  'europe.newsgroupdirect.com': 173302492687,
  'newsreader.eweka.nl': 114201200429,
  'newszilla6.xs4all.nl': 393230556},
 {'127.0.0.1': 0,
  'client.newshosting.com': 0,
  'eunews2.frugalusenet.com': 77402352,
  'europe.newsgroupdirect.com': 33215484,
  'newsreader.eweka.nl': 0,
  'newszilla6.xs4all.nl': 0},
 {'127.0.0.1': 0,
  'client.newshosting.com': 0,
  'eunews2.frugalusenet.com': 613525290,
  'europe.newsgroupdirect.com': 450941169,
  'newsreader.eweka.nl': 0,
  'newszilla6.xs4all.nl': 0},
 {'127.0.0.1': 0,
  'client.newshosting.com': 0,
  'eunews2.frugalusenet.com': 14920413939,
  'europe.newsgroupdirect.com': 1798882828,
  'newsreader.eweka.nl': 21462016,
  'newszilla6.xs4all.nl': 18500684},
 1607900399.0,
 1607900399.0,
 1609455599.0,
```
Specifically eweka:

```
~/.sabnzbd/admin$ ./dump_totals10.sab.py | grep eweka
  'newsreader.eweka.nl': 114201200429,
  'newsreader.eweka.nl': 0,
  'newsreader.eweka.nl': 0,
  'newsreader.eweka.nl': 21462016,
```
Comparing with the WebGUI of SABnzbd, those lines mean:
- Total
- Today
- This week
- This month

A hackey way to see the bytes downloaded on 2020-11-11 per newsserver:

```
~/.sabnzbd/admin$ ./dump_totals10.sab.py | grep -e '2020-11-11' -e ": {" 
 {'127.0.0.1': {'2020-06-01': 6696,
                '2020-11-11': 0,
  'client.newshosting.com': {'2020-03-29': 1312,
                             '2020-11-11': 0,
  'eunews2.frugalusenet.com': {'2020-05-08': 12682506360,
                               '2020-11-11': 3886526638,
  'europe.newsgroupdirect.com': {'2020-05-02': 106572501,
                                 '2020-11-11': 479925295,
  'newsreader.eweka.nl': {'2020-03-28': 5762662081,
                          '2020-11-11': 21488221,
  'newszilla6.xs4all.nl': {'2020-03-28': 374479189,
                           '2020-11-11': 0,
```
or
```
~/.sabnzbd/admin$ ./dump_totals10.sab.py | grep -e '2020-11-11' -e ": {"  | sed -e 's/{.*//g' 
 
                '2020-11-11': 0,
  'client.newshosting.com': 
                             '2020-11-11': 0,
  'eunews2.frugalusenet.com': 
                               '2020-11-11': 3886526638,
  'europe.newsgroupdirect.com': 
                                 '2020-11-11': 479925295,
  'newsreader.eweka.nl': 
                          '2020-11-11': 21488221,
  'newszilla6.xs4all.nl': 
                           '2020-11-11': 0,
```




