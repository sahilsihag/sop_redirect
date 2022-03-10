# Same Origin Policy (SOP) and Redirects  
A question popped up during discussion:  
> If I load `http://example.com/2.html` (which auto redirects to https) in an iframe from `https://example.com/1.html`, am I allowed to read content of `2.html`? Because initially origins don't match for these 2 web pages.

This repository is demo Implementation for same. To get answers, visit: https://sahilsihag.github.io/sop_redirect/attacker.html

### Repository Information:
- `attacker.html`: Loads 4 iframes:  
  1. (To Check:) `benign1.html` with `http` URL, redirects to `https`  
  2. Same origin: `benign2.html` with `https` URL for comparison
  3. Cross origin: `https://cms.cispa.saarland/system/courses` which does not allow framing  
  4. Cross origin: `https://de.wikipedia.org/wiki/Wikipedia:Hauptseite` which allows framing

- `doIt` function overwrites `h1` tag if iframe is accessible.

### Results
- Google Chrome:
  1. Does not allow loading first iframe. Reason: `Mixed Content: The page at 'https://sahilsihag.github.io/sop_redirect/attacker.html' was loaded over HTTPS, but requested an insecure frame 'http://sahilsihag.github.io/sop_redirect/benign1.html'. This request has been blocked; the content must be served over HTTPS.`
  2. Allows loading from second iframe. Reason: Same Origin.  
  3.  Does not allow loading third iframe. Reason: cross-origin frame  
  4.  Does not allow loading third iframe. Reason: cross-origin frame  

- Mozilla Firefox:
  1. Allows loading from first iframe. Reason: (Probably) considers it same origin since it was finally fetched over `https`
  2. Allows loading from second iframe. Reason: Same Origin.  
  3.  Does not allow loading third iframe. Reason: cross-origin frame  
  4.  Does not allow loading third iframe. Reason: cross-origin frame  

### Reporting Errors:
- Create pull request to notify about error.
