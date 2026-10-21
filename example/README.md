# Command line examples


This directory contains a sample input catalog that points to an [EEDTEST granule](https://harmony.uat.earthdata.nasa.gov/service-results/harmony-uat-eedtest-data/C1256108792-EEDTEST/SMAP_L4_SM_lmc_00000000T000000_Vv6030_001.h5) for SPL4SMLM data that has 39 net2cog processible variables in it.  The following requests invoke the service from the commandline demonstrating the mechanism used by the service.

## Directory structure





## Fan Out Example


To make a URL request to Harmony that demonstrates fan out behavior you would use:

`{HARMONY_HOST_URL}/C1256108792-EEDTEST/ogc-api-coverages/1.0.0/collections/parameter_vars/coverage/rangeset?forceAsync=true&label=net2cog-test&granuleId=G1256108793-EEDTEST&format=image%2Ftiff&maxResults=1&variable=all`

where the `HARMONY_HOST_URL` depends on your environment.


Running the command below will invoke the adapter the same way locally.  It uses a message with no input variables and the sample catalog. The output catalogs are written to `fanned-out-output`


```shell
SHARED_SECRET_KEY= STAGING_BUCKET=unused STAGING_PATH=unused \
uv run python -m variable_fan_out \
  --harmony-action invoke \
  --harmony-input "$(jq -c --arg t "$UAT_BEARER" '.accessToken = $t' example/fan-out-message.json)" \
  --harmony-sources example/input-catalog/catalog0.json \
  --harmony-metadata-dir example/fanned-out-output
```



## Explicit Variables

A request that contains one or more variables explicitly requested will not fan out but pass through unchnaged. A Harmony URL request would look like:

`{HARMONY_HOST_URL}/C1256108792-EEDTEST/ogc-api-coverages/1.0.0/collections/parameter_vars/coverage/rangeset?forceAsync=true&label=net2cog-test&granuleId=G1256108793-EEDTEST&format=image%2Ftiff&maxResults=1&variable=%2FLand-Model-Constants_Data%2Fmwrtm_rghhmin&variable=cell_lon`

```shell
SHARED_SECRET_KEY= STAGING_BUCKET=unused STAGING_PATH=unused \
uv run python -m variable_fan_out \
  --harmony-action invoke \
  --harmony-input "$(jq -c --arg t "$UAT_BEARER" '.accessToken = $t' example/explicit-variable-message.json)" \
  --harmony-sources example/input-catalog/catalog0.json \
  --harmony-metadata-dir example/explicit-variable-output
```
