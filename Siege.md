## Siege

Strength-test/benchmark a webserver.

First generate a list of URLs by spidering the site to test. Log `wget`'s output, to build the list, then clean it up with `sed`.

```
wget --spider --recursive --no-verbose --output-file=wgetlog.txt https://example.com
sed -n "s@.\+ URL:\([^ ]\+\) .\+@\1@p" wgetlog.txt | sed "s@&@\&amp;@" > sedlog.txt
```


Then

```
siege --verbose --internet --concurrent 100 --reps 1 --file sedlog.txt
```
