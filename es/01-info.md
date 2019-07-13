!SLIDE bullets incremental

# ACM

* Automated Configuration Management
* Database Configuration
* Leverages SQL **and** PeopleCode
* Search Framework Plugins
* Configure **and** Deploy Search Indexes

!SLIDE bullets

# ACM Demo

1. Configure ES Cluster
1. Clear previous ES Deployment Data
1. Redeploy ALL indexes

!SLIDE supplemental guide

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

!SLIDE bullets

# Callback Security Demo

1. View documents in Elasticsearch
1. Test Callback Response

!SLIDE supplemental guide

# Callback Security Demo

1. View documents raw in Elasticsearch

        @@@bash
        curl -u esadmin:Passw0rd! http://localhost:9200/ptportalregistry_psftdb/_search?pretty=true -H 'Content-Type: application/json; encoding="UTF-8"' -H 'SearchUser: PS' | jq

1. View callback filter

        @@@bash
        curl -u PS:PS http://ec2-3-82-138-233.compute-1.amazonaws.com:8000/PSIGW/RESTListeningConnector/PSFT_HR/getsecurityvalues.v1/?type=ptportalregistry_psftdb?user=PS?attribute=PORTAL_SECTYPE_ORCL_ES_ACL | jq

!SLIDE bullets incremental

# Cached Security

* Callback process is expensive
* Cache user security in Elasticsearch
* Default is 120 minutes
* Configurable in Search Options

!SLIDE bullets

# Cached Security Demo

1. Query the `orcl_es_acl` index

!SLIDE supplemental guide

# Cached Security Demo

1. Use `curl` to query the `orcl_es_acl` index

        @@@bash
        curl -u esadmin:Passw0rd! http://ec2-34-239-103-132.compute-1.amazonaws.com:9200/orcl_es_acl/_search?pretty=true&size=50

!SLIDE bullets incremental

# Full Build Tuning

* Connected Query SQL tuning
* Use Direct Transfer
* Elasticsearch Replicas
* Elasticsearch Refresh Interval

!SLIDE bullets

# Full Build Tuning Demo

1. Verify Direct Transfer is enabled
1. Change Refresh Interval setting
1. Reduce Replicas

!SLIDE supplemental guide

# Full Build Tuning Demo

1. Under PT > Search Framework > Admin > Search Options
1. Ensure DirectTransfer is set to `Y`
1. In Cerebro, adjust the `replicas` and `refresh interval` settings for an index
1. In Kibana, use the Dev Tools for the same settings

        @@@json
        PUT /pt_portalregistry_psftdb/_settings
        {
            "index" : {
                "number_of_replicas" : 0,
                "refresh_interval" : "-1"
            }
        }

1. After the Full Build

        @@@json
        PUT /pt_portalregistry_psftdb/_settings
        {
            "index" : {
                "number_of_replicas" : 1,
                "refresh_interval" : "30s"
            }
        }

> [flush and refresh operations in Elasticsearch](https://qbox.io/blog/refresh-flush-operations-elasticsearch-guide)
