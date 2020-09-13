# Privacy browser extenions
- Privacy badger
- uBlock Origin
- Canvas blocker
- Smart HTTPS or HTTPS Everywhere

# Smart HTTPS vs HTTPS Everywhere
- HTTPS Everywhere use a very extensive set of rules for redirecting to HTTPS.
  - The upside is that it's certain a rule will work (site might break between updates, but it's rare) and it can do "complex" redirects (IE http://www.example.com to https://secure.example.com).
  - The downside is that if a site support HTTPS but it's not in the ruleset it will not work.
- Smart HTTPS just tries to load the HTTPS version of every site, and it doesn't work it will fail back to the HTTP version.
  - Downsides is that it won't do "complex" redirect, and that some sites might break (for the extension, "break" only mean that the site won't load. If the https version is not serving the same content, or it's serving broken content, it will still be considered valid).
