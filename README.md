# variable-fan-out service

This service image is placed as a shim before a service to transform requests with a harmony message that requests `all` for a variable into a batch catalog of the same input stac but extended with a custom extension with one stac catalog per variable.  This allows harmony to fan-out a single request to a single pod into a request per variable allowing mulitple pods to work a granules's variables at once.
