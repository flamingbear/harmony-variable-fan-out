# variable-fan-out service

This repository contains code for the variable-fan-out-service.

This service fans out request to net2cog. It takes a request for `all` variables, and transforms it into N requests, each for a single variable, letting harmony fan it out into N parallel requests.

The basic idea for a request for all variables headed to net2cog is that the STAC Catalog's Item data asset is downloaded and net2cog's `get_all_data_variables` function is used to determine a list of variables that net2cog can process.  For every variable found, the input catalog is cloned and the Item updated with a new property `harmony:variable` whose value is the variable name.  This list of catalogs is returned to harmony, which treats them as a batch catalog and submits them to net2cog downstream.  Net2cog has been updated to look for this new `harmony:variable` property and only process the single variable found there.
