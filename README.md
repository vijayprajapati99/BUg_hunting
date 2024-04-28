# BUg_hunting

#!/bin/bash

# Discover subdomains
subfinder -d <target_domain> -silent | tee subdomains.txt

# Discover URLs from the web archive
cat subdomains.txt | waybackurls | tee urls.txt

# Scan for XSS vulnerabilities
cat urls.txt | dalfox pipe | tee xss_results.txt

# Test XSS filters
cat xss_results.txt | noxss | tee filtered_results.txt

# Test for reflected XSS
cat filtered_results.txt | xsstrike.py -m GET --random-agent | tee reflected_xss_results.txt

# Test for stored XSS
cat filtered_results.txt | xsstrike.py -m POST --random-agent | tee stored_xss_results.txt
