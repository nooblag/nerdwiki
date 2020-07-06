Nice one liner to find all the allocated IP ranges for an Automous System (ASN) given an IP address, where <ip> is address:

`whois -h whois.radb.net -i origin -T route $(whois -h whois.radb.net <ip> | grep origin: | cut -d ' ' -f 6 | head -1) | grep -w "route:" | awk '{print $NF}' |sort -n`
