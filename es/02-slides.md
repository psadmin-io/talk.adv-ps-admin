!SLIDE bullets incremental

# ACM

* Automated Configuration Management
* Database Configuration
* Leverages SQL **and** PeopleCode
* Search Framework Plugins
* Configure **and** Deploy Search Indexes

!SLIDE center subsection grey

# Demo

!SLIDE supplemental guide

Tasks:

1. Configure ES Cluster
1. Clear previous ES Deployment Data
1. Redeploy ALL indexes

# ACM and Search Framework Demo

1. Use the `SEARCH_TEMPLATE` ACM plugin
1. Configure a 3 node cluster (pre-configured)
1. Remove previously deployed PTSF data

    This removes it from the PSTF* tables, but not Elasticsearch

1. Deploy ALL indexes and start a full build for each
1. Show the run controls for the builds (full and incr)

!SLIDE bullets incremental

# Understanding Callback Security

* Elasticsearch query finds all rows
* Need to filter data based on PeopleSoft security
* PeopleSoft provides a filter attribute
* Elasticsearch calls back to PS for filter attribute
* Each document in Elasticsearch has filter values
* Elasticsearch filters documents before returning results

!SLIDE bullets

# Filter Values

* `ptportalregistry`

        @@@json
        "PORTAL_SECTYPE_ORCL_ES_ACL" : [
          "1:PTDMO",
          "P:PTPT1200",
          "S:Admin"
        ]

!SLIDE bullets

# Callback URL

* `IB RESTListener URL`/`getsecurityvalues.v1`
  * `?type=`Search Definition
  * `?user=`User ID
  * `?attribute=`Filter Attribute

!SLIDE center subsection grey

# Demo

!SLIDE supplemental guide

Tasks:

1. View documents in Elasticsearch
1. Test Callback Response

# Callback Security Demo

1. View documents raw in Elasticsearch

        @@@bash
        curl -u esadmin:Passw0rd http://hr030-lnxft-1.midtier.psft.oraclevcn.com:9200/ptportalregistry_hrpum/_search?pretty=true -H 'Content-Type: application/json; encoding="UTF-8"' -H 'SearchUser: PS' | jq

1. View callback filter

        @@@bash
        curl -u PS:PS http://hr030-lnxft-1.midtier.psft.oraclevcn.com:8000/PSIGW/RESTListeningConnector/PSFT_HR/getsecurityvalues.v1/?type=ptportalregistry_hrpum?user=PS?attribute=PORTAL_SECTYPE_ORCL_ES_ACL | jq

!SLIDE bullets incremental

# Cached Security

* Callback process is expensive
* Cache user security in Elasticsearch
* Default is 120 minutes
* Configurable in Search Options


!SLIDE center subsection grey

# Demo

!SLIDE supplemental guide

Tasks:

1. Query the `orcl_es_acl` index

# Cached Security Demo

1. Use `curl` to query the `orcl_es_acl` index

        @@@bash
        curl -u esadmin:Passw0rd http://hr030-lnxft-1.midtier.psft.oraclevcn.com:9200/orcl_es_acl/_search?pretty=true&size=50

!SLIDE bullets incremental

# Full Build Tuning

* Connected Query SQL tuning
* Use Direct Transfer
* Elasticsearch Replicas
* Elasticsearch Refresh Interval

!SLIDE center subsection grey

# Demo

!SLIDE supplemental guide

Tasks:

1. Verify Direct Transfer is enabled
1. Change Refresh Interval setting
1. Reduce Replicas

# Full Build Tuning Demo

1. Under PT > Search Framework > Admin > Search Options
1. Ensure DirectTransfer is set to `Y`
1. In Cerebro, adjust the `replicas` and `refresh interval` settings for an index
1. In Kibana, use the Dev Tools for the same settings

        @@@json
        PUT /ptportalregistry_hrpum/_settings
        {
            "index" : {
                "number_of_replicas" : 0,
                "refresh_interval" : "-1"
            }
        }

1. After the Full Build

        @@@json
        PUT /ptportalregistry_hrpum/_settings
        {
            "index" : {
                "number_of_replicas" : 1,
                "refresh_interval" : "30s"
            }
        }

> [flush and refresh operations in Elasticsearch](https://qbox.io/blog/refresh-flush-operations-elasticsearch-guide)
