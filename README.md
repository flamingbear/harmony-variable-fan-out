# variable-fan-out service

This repository contains code for the harmony-variable-fan-out-service.

This service takes a single request for `all` variables, and transforms it into N requests for a single variable, Fanning it out into a parallelizable set of requests for a single variable.

The high-level overview of how the service works:

- Read the incoming stac Catalog
- Discover all variables
- For each variable:
  - Clone the catalog
  - Add the variable to a custom property in the catalog so a downstream service can find it.
- Return this list of amended catalogs to harmony.
- Harmony submits all of the catalogs to the next service in parallel.

##
