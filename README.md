builtin:kubernetes.pods:last:filter(and(or(not(existskey(pod_status)), ne(pod_status, Terminating)),eq(pod_phase, Running))):splitBy("dt.entity.cloud_application_namespace","dt.entity.kubernetes_cluster"):sum:sort(value(sum,descending))
{
  "metadata": {
    "configurationVersions": [
      7
    ],
    "clusterVersion": "1.303.42.20241021-231645"
  },
  "id": "9ec33d06-2f39-4c8d-85db-c77038b284b8",
  "dashboardMetadata": {
    "name": "Kubernetes cluster overview",
    "shared": true,
    "owner": "anthony.su@dynatrace.com",
    "tags": [
      "Kubernetes"
    ],
    "preset": true,
    "popularity": 1,
    "dynamicFilters": {
      "filters": [
        "KUBERNETES_CLUSTER"
      ],
      "genericTagFilters": []
    },
    "hasConsistentColors": true
  },
  "tiles": [
    {
      "name": "Markdown",
      "tileType": "MARKDOWN",
      "configured": true,
      "bounds": {
        "top": 0,
        "left": 0,
        "width": 684,
        "height": 38
      },
      "tileFilter": {},
      "isAutoRefreshDisabled": false,
      "markdown": "## Cluster overview"
    },
    {
      "name": "",
      "tileType": "HOSTS",
      "configured": true,
      "bounds": {
        "top": 38,
        "left": 342,
        "width": 342,
        "height": 304
      },
      "tileFilter": {
        "timeframe": "-5m"
      },
      "isAutoRefreshDisabled": false,
      "filterConfig": {
        "type": "HOST",
        "customName": "Full-Stack Kubernetes nodes",
        "defaultName": "Full-Stack Kubernetes nodes",
        "chartConfig": {
          "legendShown": true,
          "type": "TIMESERIES",
          "series": [],
          "resultMetadata": {}
        },
        "filtersPerEntityType": {}
      },
      "chartVisible": true
    },
    {
      "name": "Markdown",
      "tileType": "MARKDOWN",
      "configured": true,
      "bounds": {
        "top": 684,
        "left": 0,
        "width": 1672,
        "height": 38
      },
      "tileFilter": {
        "timeframe": "-5m"
      },
      "isAutoRefreshDisabled": false,
      "markdown": "## Node resources"
    },
    {
      "name": "Markdown",
      "tileType": "MARKDOWN",
      "configured": true,
      "bounds": {
        "top": 0,
        "left": 722,
        "width": 228,
        "height": 38
      },
      "tileFilter": {
        "timeframe": "-5m"
      },
      "isAutoRefreshDisabled": false,
      "markdown": "## Pods overview"
    },
    {
      "name": "Markdown",
      "tileType": "MARKDOWN",
      "configured": true,
      "bounds": {
        "top": 342,
        "left": 0,
        "width": 342,
        "height": 38
      },
      "tileFilter": {
        "timeframe": "-5m"
      },
      "isAutoRefreshDisabled": false,
      "markdown": "## Cluster resources"
    },
    {
      "name": "Markdown",
      "tileType": "MARKDOWN",
      "configured": true,
      "bounds": {
        "top": 0,
        "left": 950,
        "width": 418,
        "height": 38
      },
      "tileFilter": {},
      "isAutoRefreshDisabled": false,
      "markdown": "Find more insights on our [Workload overview dashboard](#dashboard;id=6b38732e-d26b-45c7-b107-ed85e87ff288)."
    },
    {
      "name": "Markdown",
      "tileType": "MARKDOWN",
      "configured": true,
      "bounds": {
        "top": 0,
        "left": 1368,
        "width": 304,
        "height": 38
      },
      "tileFilter": {},
      "isAutoRefreshDisabled": false,
      "markdown": "## [📝We'd love your feedback!](https://dt-url.net/k8scod)"
    },
    {
      "name": "Memory requests in % of allocatable",
      "nameSize": "",
      "tileType": "DATA_EXPLORER",
      "configured": true,
      "bounds": {
        "top": 380,
        "left": 1254,
        "width": 418,
        "height": 304
      },
      "tileFilter": {
        "timeframe": "-5m"
      },
      "isAutoRefreshDisabled": false,
      "customName": "Memory available",
      "queries": [
        {
          "id": "B",
          "spaceAggregation": "AUTO",
          "timeAggregation": "DEFAULT",
          "splitBy": [
            "dt.entity.kubernetes_cluster"
          ],
          "metricSelector": "(builtin:kubernetes.node.requests_memory:last:splitBy(\"dt.entity.kubernetes_cluster\"):sum / builtin:kubernetes.node.memory_allocatable:last:splitBy(\"dt.entity.kubernetes_cluster\"):sum * 100):setUnit(Percent):sort(value(sum,descending))",
          "rate": "NONE",
          "enabled": true
        }
      ],
      "visualConfig": {
        "type": "TOP_LIST",
        "global": {
          "hideLegend": false
        },
        "rules": [
          {
            "matcher": "B:",
            "unitTransform": "Percent",
            "valueFormat": "0",
            "properties": {
              "color": "DEFAULT",
              "seriesType": "LINE"
            },
            "seriesOverrides": []
          }
        ],
        "axes": {
          "xAxis": {
            "displayName": "",
            "visible": true
          },
          "yAxes": [
            {
              "displayName": "",
              "visible": true,
              "min": "0",
              "max": "100",
              "position": "LEFT",
              "queryIds": [
                "B"
              ],
              "defaultAxis": true
            }
          ]
        },
        "heatmapSettings": {
          "yAxis": "VALUE"
        },
        "thresholds": [
          {
            "axisTarget": "LEFT",
            "rules": [
              {
                "value": 0,
                "color": "#7dc540"
              },
              {
                "value": 90,
                "color": "#f5d30f"
              },
              {
                "color": "#dc172a"
              }
            ],
            "queryId": "",
            "visible": true
          }
        ],
        "tableSettings": {
          "isThresholdBackgroundAppliedToCell": false,
          "hiddenColumns": []
        },
        "graphChartSettings": {
          "connectNulls": false
        },
        "honeycombSettings": {
          "showHive": true,
          "showLegend": true,
          "showLabels": false
        }
      },
      "queriesSettings": {
        "resolution": ""
      },
      "metricExpressions": [
        "resolution=null&((builtin:kubernetes.node.requests_memory:last:splitBy(\"dt.entity.kubernetes_cluster\"):sum/builtin:kubernetes.node.memory_allocatable:last:splitBy(\"dt.entity.kubernetes_cluster\"):sum*100):setUnit(Percent):sort(value(sum,descending))):limit(100):names:fold(auto)"
      ]
    },
    {
      "name": "CPU requests in % of allocatable",
      "nameSize": "",
      "tileType": "DATA_EXPLORER",
      "configured": true,
      "bounds": {
        "top": 722,
        "left": 418,
        "width": 418,
        "height": 304
      },
      "tileFilter": {
        "timeframe": "-5m"
      },
      "isAutoRefreshDisabled": false,
      "customName": "Memory available",
      "queries": [
        {
          "id": "B",
          "spaceAggregation": "AUTO",
          "timeAggregation": "DEFAULT",
          "splitBy": [
            "dt.entity.kubernetes_node",
            "dt.entity.kubernetes_cluster"
          ],
          "metricSelector": "(\n  builtin:kubernetes.node.requests_cpu:last:splitBy(\"dt.entity.kubernetes_node\",\"dt.entity.kubernetes_cluster\"):sum \n  / builtin:kubernetes.node.cpu_allocatable:last:splitBy(\"dt.entity.kubernetes_node\",\"dt.entity.kubernetes_cluster\"):sum \n  * 100\n):setUnit(Percent):sort(value(sum,descending))",
          "rate": "NONE",
          "enabled": true
        }
      ],
      "visualConfig": {
        "type": "TOP_LIST",
        "global": {
          "hideLegend": false
        },
        "rules": [
          {
            "matcher": "B:",
            "unitTransform": "auto",
            "valueFormat": "0",
            "properties": {
              "color": "DEFAULT",
              "seriesType": "LINE"
            },
            "seriesOverrides": []
          }
        ],
        "axes": {
          "xAxis": {
            "displayName": "",
            "visible": true
          },
          "yAxes": [
            {
              "displayName": "",
              "visible": true,
              "min": "0",
              "max": "100",
              "position": "LEFT",
              "queryIds": [
                "B"
              ],
              "defaultAxis": true
            }
          ]
        },
        "heatmapSettings": {
          "yAxis": "VALUE"
        },
        "thresholds": [
          {
            "axisTarget": "LEFT",
            "rules": [
              {
                "value": 0,
                "color": "#7dc540"
              },
              {
                "value": 90,
                "color": "#f5d30f"
              },
              {
                "color": "#dc172a"
              }
            ],
            "queryId": "",
            "visible": true
          }
        ],
        "tableSettings": {
          "isThresholdBackgroundAppliedToCell": false,
          "hiddenColumns": []
        },
        "graphChartSettings": {
          "connectNulls": false
        },
        "honeycombSettings": {
          "showHive": true,
          "showLegend": true,
          "showLabels": false
        }
      },
      "queriesSettings": {
        "resolution": ""
      },
      "metricExpressions": [
        "resolution=null&((builtin:kubernetes.node.requests_cpu:last:splitBy(\"dt.entity.kubernetes_node\",\"dt.entity.kubernetes_cluster\"):sum/builtin:kubernetes.node.cpu_allocatable:last:splitBy(\"dt.entity.kubernetes_node\",\"dt.entity.kubernetes_cluster\"):sum*100):setUnit(Percent):sort(value(sum,descending))):limit(100):names:fold(auto)"
      ]
    },
    {
      "name": "Memory requests in % of allocatable",
      "nameSize": "",
      "tileType": "DATA_EXPLORER",
      "configured": true,
      "bounds": {
        "top": 722,
        "left": 1254,
        "width": 418,
        "height": 304
      },
      "tileFilter": {
        "timeframe": "-5m"
      },
      "isAutoRefreshDisabled": false,
      "customName": "Memory available",
      "queries": [
        {
          "id": "B",
          "spaceAggregation": "AUTO",
          "timeAggregation": "DEFAULT",
          "splitBy": [
            "dt.entity.kubernetes_node",
            "dt.entity.kubernetes_cluster"
          ],
          "metricSelector": "(builtin:kubernetes.node.requests_memory:last:splitBy(\"dt.entity.kubernetes_node\",\"dt.entity.kubernetes_cluster\"):sum / builtin:kubernetes.node.memory_allocatable:last:splitBy(\"dt.entity.kubernetes_node\",\"dt.entity.kubernetes_cluster\"):sum * 100):setUnit(Percent):sort(value(sum,descending))",
          "rate": "NONE",
          "enabled": true
        }
      ],
      "visualConfig": {
        "type": "TOP_LIST",
        "global": {
          "hideLegend": false
        },
        "rules": [
          {
            "matcher": "B:",
            "unitTransform": "Percent",
            "valueFormat": "0",
            "properties": {
              "color": "DEFAULT",
              "seriesType": "LINE"
            },
            "seriesOverrides": []
          }
        ],
        "axes": {
          "xAxis": {
            "displayName": "",
            "visible": true
          },
          "yAxes": [
            {
              "displayName": "",
              "visible": true,
              "min": "0",
              "max": "100",
              "position": "LEFT",
              "queryIds": [
                "B"
              ],
              "defaultAxis": true
            }
          ]
        },
        "heatmapSettings": {
          "yAxis": "VALUE"
        },
        "thresholds": [
          {
            "axisTarget": "LEFT",
            "rules": [
              {
                "value": 0,
                "color": "#7dc540"
              },
              {
                "value": 90,
                "color": "#f5d30f"
              },
              {
                "color": "#dc172a"
              }
            ],
            "queryId": "",
            "visible": true
          }
        ],
        "tableSettings": {
          "isThresholdBackgroundAppliedToCell": false,
          "hiddenColumns": []
        },
        "graphChartSettings": {
          "connectNulls": false
        },
        "honeycombSettings": {
          "showHive": true,
          "showLegend": true,
          "showLabels": false
        }
      },
      "queriesSettings": {
        "resolution": ""
      },
      "metricExpressions": [
        "resolution=null&((builtin:kubernetes.node.requests_memory:last:splitBy(\"dt.entity.kubernetes_node\",\"dt.entity.kubernetes_cluster\"):sum/builtin:kubernetes.node.memory_allocatable:last:splitBy(\"dt.entity.kubernetes_node\",\"dt.entity.kubernetes_cluster\"):sum*100):setUnit(Percent):sort(value(sum,descending))):limit(100):names:fold(auto)"
      ]
    },
    {
      "name": "Pods by phase",
      "tileType": "DATA_EXPLORER",
      "configured": true,
      "bounds": {
        "top": 38,
        "left": 1026,
        "width": 342,
        "height": 304
      },
      "tileFilter": {
        "timeframe": "-5m"
      },
      "isAutoRefreshDisabled": false,
      "customName": "Pods",
      "queries": [
        {
          "id": "C",
          "spaceAggregation": "AUTO",
          "timeAggregation": "DEFAULT",
          "splitBy": [
            "pod_phase"
          ],
          "metricSelector": "builtin:kubernetes.node.pods:last:splitBy(pod_phase):sum:sort(value(sum,descending))",
          "rate": "NONE",
          "enabled": true
        }
      ],
      "visualConfig": {
        "type": "PIE_CHART",
        "global": {
          "hideLegend": false
        },
        "rules": [
          {
            "matcher": "C:",
            "unitTransform": "auto",
            "valueFormat": "auto",
            "properties": {
              "color": "DEFAULT",
              "seriesType": "LINE"
            },
            "seriesOverrides": [
              {
                "name": "Running",
                "color": "#5ead35"
              },
              {
                "name": "Pending",
                "color": "#7c38a1"
              },
              {
                "name": "Failed",
                "color": "#f5d30f"
              },
              {
                "name": "Succeeded",
                "color": "#008cdb"
              }
            ]
          }
        ],
        "axes": {
          "xAxis": {
            "displayName": "",
            "visible": true
          },
          "yAxes": []
        },
        "heatmapSettings": {
          "yAxis": "VALUE"
        },
        "thresholds": [
          {
            "axisTarget": "LEFT",
            "rules": [
              {
                "color": "#7dc540"
              },
              {
                "color": "#f5d30f"
              },
              {
                "color": "#dc172a"
              }
            ],
            "queryId": "",
            "visible": true
          }
        ],
        "tableSettings": {
          "isThresholdBackgroundAppliedToCell": false,
          "hiddenColumns": []
        },
        "graphChartSettings": {
          "connectNulls": false
        },
        "honeycombSettings": {
          "showHive": true,
          "showLegend": true,
          "showLabels": false
        }
      },
      "queriesSettings": {
        "resolution": ""
      },
      "metricExpressions": [
        "resolution=null&(builtin:kubernetes.node.pods:last:splitBy(pod_phase):sum:sort(value(sum,descending))):limit(100):names:fold(auto)"
      ]
    },
    {
      "name": "Top 10 CPU usage",
      "tileType": "DATA_EXPLORER",
      "configured": true,
      "bounds": {
        "top": 1026,
        "left": 0,
        "width": 418,
        "height": 304
      },
      "tileFilter": {},
      "isAutoRefreshDisabled": false,
      "customName": "CPU usage % ",
      "queries": [
        {
          "id": "A",
          "spaceAggregation": "AUTO",
          "timeAggregation": "DEFAULT",
          "splitBy": [
            "dt.entity.host"
          ],
          "metricSelector": "builtin:host.cpu.usage:filter(and(in(\"dt.entity.host\",entitySelector(\"type(host),softwaretechnologies(~\"KUBERNETES~\")\")))):splitBy(\"dt.entity.host\"):sort(value(avg,descending)):limit(10)",
          "rate": "NONE",
          "enabled": true
        }
      ],
      "visualConfig": {
        "type": "GRAPH_CHART",
        "global": {
          "hideLegend": false
        },
        "rules": [
          {
            "matcher": "A:",
            "unitTransform": "Percent",
            "valueFormat": "0",
            "properties": {
              "color": "DEFAULT",
              "seriesType": "LINE"
            },
            "seriesOverrides": []
          }
        ],
        "axes": {
          "xAxis": {
            "displayName": "",
            "visible": true
          },
          "yAxes": [
            {
              "displayName": "",
              "visible": true,
              "min": "0",
              "max": "100",
              "position": "LEFT",
              "queryIds": [
                "A"
              ],
              "defaultAxis": true
            }
          ]
        },
        "heatmapSettings": {
          "yAxis": "VALUE"
        },
        "thresholds": [
          {
            "axisTarget": "LEFT",
            "rules": [
              {
                "color": "#7dc540"
              },
              {
                "value": 90,
                "color": "#f5d30f"
              },
              {
                "color": "#dc172a"
              }
            ],
            "queryId": "",
            "visible": true
          }
        ],
        "tableSettings": {
          "isThresholdBackgroundAppliedToCell": false,
          "hiddenColumns": []
        },
        "graphChartSettings": {
          "connectNulls": false
        },
        "honeycombSettings": {
          "showHive": true,
          "showLegend": true,
          "showLabels": false
        }
      },
      "queriesSettings": {
        "resolution": ""
      },
      "metricExpressions": [
        "resolution=null&(builtin:host.cpu.usage:filter(and(in(\"dt.entity.host\",entitySelector(\"type(host),softwaretechnologies(~\"KUBERNETES~\")\")))):splitBy(\"dt.entity.host\"):sort(value(avg,descending)):limit(10)):limit(100):names"
      ]
    },
    {
      "name": "Top 10 memory usage",
      "tileType": "DATA_EXPLORER",
      "configured": true,
      "bounds": {
        "top": 1026,
        "left": 418,
        "width": 418,
        "height": 304
      },
      "tileFilter": {},
      "isAutoRefreshDisabled": false,
      "customName": "Memory usage % ",
      "queries": [
        {
          "id": "A",
          "spaceAggregation": "AUTO",
          "timeAggregation": "DEFAULT",
          "splitBy": [
            "dt.entity.host"
          ],
          "metricSelector": "builtin:host.mem.usage:filter(and(in(\"dt.entity.host\",entitySelector(\"type(host),softwaretechnologies(~\"KUBERNETES~\")\")))):splitBy(\"dt.entity.host\"):sort(value(avg,descending)):limit(10)",
          "rate": "NONE",
          "enabled": true
        }
      ],
      "visualConfig": {
        "type": "GRAPH_CHART",
        "global": {
          "hideLegend": false
        },
        "rules": [
          {
            "matcher": "A:",
            "unitTransform": "Percent",
            "valueFormat": "0",
            "properties": {
              "color": "DEFAULT",
              "seriesType": "LINE"
            },
            "seriesOverrides": []
          }
        ],
        "axes": {
          "xAxis": {
            "displayName": "",
            "visible": true
          },
          "yAxes": [
            {
              "displayName": "",
              "visible": true,
              "min": "0",
              "max": "100",
              "position": "LEFT",
              "queryIds": [
                "A"
              ],
              "defaultAxis": true
            }
          ]
        },
        "heatmapSettings": {
          "yAxis": "VALUE"
        },
        "thresholds": [
          {
            "axisTarget": "LEFT",
            "rules": [
              {
                "color": "#7dc540"
              },
              {
                "value": 90,
                "color": "#f5d30f"
              },
              {
                "color": "#dc172a"
              }
            ],
            "queryId": "",
            "visible": true
          }
        ],
        "tableSettings": {
          "isThresholdBackgroundAppliedToCell": false,
          "hiddenColumns": []
        },
        "graphChartSettings": {
          "connectNulls": false
        },
        "honeycombSettings": {
          "showHive": true,
          "showLegend": true,
          "showLabels": false
        }
      },
      "queriesSettings": {
        "resolution": ""
      },
      "metricExpressions": [
        "resolution=null&(builtin:host.mem.usage:filter(and(in(\"dt.entity.host\",entitySelector(\"type(host),softwaretechnologies(~\"KUBERNETES~\")\")))):splitBy(\"dt.entity.host\"):sort(value(avg,descending)):limit(10)):limit(100):names"
      ]
    },
    {
      "name": "Top 10 disk usage",
      "tileType": "DATA_EXPLORER",
      "configured": true,
      "bounds": {
        "top": 1026,
        "left": 836,
        "width": 418,
        "height": 304
      },
      "tileFilter": {},
      "isAutoRefreshDisabled": false,
      "customName": "Disk usage % ",
      "queries": [
        {
          "id": "A",
          "spaceAggregation": "AUTO",
          "timeAggregation": "DEFAULT",
          "splitBy": [
            "dt.entity.host",
            "dt.entity.disk"
          ],
          "metricSelector": "builtin:host.disk.usedPct:filter(and(in(\"dt.entity.host\",entitySelector(\"type(host),softwaretechnologies(~\"KUBERNETES~\")\")))):splitBy(\"dt.entity.host\",\"dt.entity.disk\"):avg:sort(value(avg,descending)):limit(10)",
          "rate": "NONE",
          "enabled": true
        }
      ],
      "visualConfig": {
        "type": "GRAPH_CHART",
        "global": {
          "hideLegend": false
        },
        "rules": [
          {
            "matcher": "A:",
            "unitTransform": "Percent",
            "valueFormat": "0",
            "properties": {
              "color": "DEFAULT",
              "seriesType": "LINE"
            },
            "seriesOverrides": []
          }
        ],
        "axes": {
          "xAxis": {
            "displayName": "",
            "visible": true
          },
          "yAxes": [
            {
              "displayName": "",
              "visible": true,
              "min": "0",
              "max": "100",
              "position": "LEFT",
              "queryIds": [
                "A"
              ],
              "defaultAxis": true
            }
          ]
        },
        "heatmapSettings": {
          "yAxis": "VALUE"
        },
        "thresholds": [
          {
            "axisTarget": "LEFT",
            "rules": [
              {
                "color": "#7dc540"
              },
              {
                "value": 90,
                "color": "#f5d30f"
              },
              {
                "color": "#dc172a"
              }
            ],
            "queryId": "",
            "visible": true
          }
        ],
        "tableSettings": {
          "isThresholdBackgroundAppliedToCell": false,
          "hiddenColumns": []
        },
        "graphChartSettings": {
          "connectNulls": false
        },
        "honeycombSettings": {
          "showHive": true,
          "showLegend": true,
          "showLabels": false
        }
      },
      "queriesSettings": {
        "resolution": ""
      },
      "metricExpressions": [
        "resolution=null&(builtin:host.disk.usedPct:filter(and(in(\"dt.entity.host\",entitySelector(\"type(host),softwaretechnologies(~\"KUBERNETES~\")\")))):splitBy(\"dt.entity.host\",\"dt.entity.disk\"):avg:sort(value(avg,descending)):limit(10)):limit(100):names"
      ]
    },
    {
      "name": "Top 10 traffic in/out",
      "tileType": "DATA_EXPLORER",
      "configured": true,
      "bounds": {
        "top": 1026,
        "left": 1254,
        "width": 418,
        "height": 304
      },
      "tileFilter": {},
      "isAutoRefreshDisabled": false,
      "customName": "Traffic in/out",
      "queries": [
        {
          "id": "A",
          "spaceAggregation": "AUTO",
          "timeAggregation": "DEFAULT",
          "splitBy": [
            "dt.entity.host"
          ],
          "metricSelector": "builtin:host.net.nic.trafficIn:avg:filter(and(in(\"dt.entity.host\",entitySelector(\"type(host),softwaretechnologies(~\"KUBERNETES~\")\")))):splitBy(\"dt.entity.host\"):sum:auto:sort(value(sum,descending)):limit(10)",
          "rate": "NONE",
          "enabled": true
        },
        {
          "id": "B",
          "spaceAggregation": "AUTO",
          "timeAggregation": "DEFAULT",
          "splitBy": [
            "dt.entity.host"
          ],
          "metricSelector": "builtin:host.net.nic.trafficOut:avg:filter(and(in(\"dt.entity.host\",entitySelector(\"type(host),softwaretechnologies(~\"KUBERNETES~\")\")))):splitBy(\"dt.entity.host\"):sum:auto:sort(value(sum,descending)):limit(10)",
          "rate": "NONE",
          "enabled": true
        }
      ],
      "visualConfig": {
        "type": "GRAPH_CHART",
        "global": {
          "hideLegend": false
        },
        "rules": [
          {
            "matcher": "A:",
            "unitTransform": "auto",
            "valueFormat": "auto",
            "properties": {
              "color": "BLUE",
              "seriesType": "LINE"
            },
            "seriesOverrides": []
          },
          {
            "matcher": "B:",
            "unitTransform": "auto",
            "valueFormat": "auto",
            "properties": {
              "color": "ORANGE",
              "seriesType": "LINE"
            },
            "seriesOverrides": []
          }
        ],
        "axes": {
          "xAxis": {
            "displayName": "",
            "visible": true
          },
          "yAxes": [
            {
              "displayName": "",
              "visible": true,
              "min": "AUTO",
              "max": "AUTO",
              "position": "LEFT",
              "queryIds": [
                "A",
                "B"
              ],
              "defaultAxis": true
            }
          ]
        },
        "heatmapSettings": {
          "yAxis": "VALUE"
        },
        "thresholds": [
          {
            "axisTarget": "LEFT",
            "rules": [
              {
                "color": "#7dc540"
              },
              {
                "color": "#f5d30f"
              },
              {
                "color": "#dc172a"
              }
            ],
            "queryId": "",
            "visible": true
          }
        ],
        "tableSettings": {
          "isThresholdBackgroundAppliedToCell": false,
          "hiddenColumns": []
        },
        "graphChartSettings": {
          "connectNulls": false
        },
        "honeycombSettings": {
          "showHive": true,
          "showLegend": true,
          "showLabels": false
        }
      },
      "queriesSettings": {
        "resolution": ""
      },
      "metricExpressions": [
        "resolution=null&(builtin:host.net.nic.trafficIn:avg:filter(and(in(\"dt.entity.host\",entitySelector(\"type(host),softwaretechnologies(~\"KUBERNETES~\")\")))):splitBy(\"dt.entity.host\"):sum:auto:sort(value(sum,descending)):limit(10)):limit(100):names,(builtin:host.net.nic.trafficOut:avg:filter(and(in(\"dt.entity.host\",entitySelector(\"type(host),softwaretechnologies(~\"KUBERNETES~\")\")))):splitBy(\"dt.entity.host\"):sum:auto:sort(value(sum,descending)):limit(10)):limit(100):names"
      ]
    },
    {
      "name": "Running pods",
      "tileType": "DATA_EXPLORER",
      "configured": true,
      "bounds": {
        "top": 38,
        "left": 722,
        "width": 304,
        "height": 304
      },
      "tileFilter": {
        "timeframe": "-5m"
      },
      "isAutoRefreshDisabled": false,
      "customName": "Running pods",
      "queries": [
        {
          "id": "B",
          "spaceAggregation": "AUTO",
          "timeAggregation": "DEFAULT",
          "splitBy": [
            "dt.entity.cloud_application_namespace",
            "dt.entity.kubernetes_cluster"
          ],
          "metricSelector": "builtin:kubernetes.pods:last:filter(and(or(not(existskey(pod_status)), ne(pod_status, Terminating)),eq(pod_phase, Running))):splitBy(\"dt.entity.cloud_application_namespace\",\"dt.entity.kubernetes_cluster\"):sum:sort(value(sum,descending))",
          "rate": "NONE",
          "enabled": true
        }
      ],
      "visualConfig": {
        "type": "TOP_LIST",
        "global": {
          "hideLegend": false
        },
        "rules": [
          {
            "matcher": "B:",
            "properties": {
              "color": "DEFAULT"
            },
            "seriesOverrides": []
          }
        ],
        "axes": {
          "xAxis": {
            "displayName": "",
            "visible": true
          },
          "yAxes": []
        },
        "heatmapSettings": {
          "yAxis": "VALUE"
        },
        "thresholds": [
          {
            "axisTarget": "LEFT",
            "rules": [
              {
                "value": 0,
                "color": "#5ead35"
              },
              {
                "color": "#f5d30f"
              },
              {
                "color": "#dc172a"
              }
            ],
            "queryId": "",
            "visible": true
          }
        ],
        "tableSettings": {
          "isThresholdBackgroundAppliedToCell": false,
          "hiddenColumns": []
        },
        "graphChartSettings": {
          "connectNulls": false
        },
        "honeycombSettings": {
          "showHive": true,
          "showLegend": true,
          "showLabels": false
        }
      },
      "queriesSettings": {
        "resolution": ""
      },
      "metricExpressions": [
        "resolution=null&(builtin:kubernetes.pods:last:filter(and(or(not(existsKey(pod_status)),ne(pod_status,Terminating)),eq(pod_phase,Running))):splitBy(\"dt.entity.cloud_application_namespace\",\"dt.entity.kubernetes_cluster\"):sum:sort(value(sum,descending))):limit(100):names:fold(auto)"
      ]
    },
    {
      "name": "CPU requests in % of allocatable",
      "nameSize": "",
      "tileType": "DATA_EXPLORER",
      "configured": true,
      "bounds": {
        "top": 380,
        "left": 418,
        "width": 418,
        "height": 304
      },
      "tileFilter": {
        "timeframe": "-5m"
      },
      "isAutoRefreshDisabled": false,
      "customName": "Memory available",
      "queries": [
        {
          "id": "B",
          "spaceAggregation": "AUTO",
          "timeAggregation": "DEFAULT",
          "splitBy": [
            "dt.entity.kubernetes_cluster"
          ],
          "metricSelector": "(builtin:kubernetes.node.requests_cpu:last:splitBy(\"dt.entity.kubernetes_cluster\"):sum / builtin:kubernetes.node.cpu_allocatable:last:splitBy(\"dt.entity.kubernetes_cluster\"):sum * 100):sort(value(sum,descending))",
          "rate": "NONE",
          "enabled": true
        }
      ],
      "visualConfig": {
        "type": "TOP_LIST",
        "global": {
          "hideLegend": false
        },
        "rules": [
          {
            "matcher": "B:",
            "unitTransform": "%",
            "valueFormat": "0",
            "properties": {
              "color": "DEFAULT",
              "seriesType": "LINE"
            },
            "seriesOverrides": []
          }
        ],
        "axes": {
          "xAxis": {
            "displayName": "",
            "visible": true
          },
          "yAxes": [
            {
              "displayName": "",
              "visible": true,
              "min": "0",
              "max": "100",
              "position": "LEFT",
              "queryIds": [
                "B"
              ],
              "defaultAxis": true
            }
          ]
        },
        "heatmapSettings": {
          "yAxis": "VALUE"
        },
        "thresholds": [
          {
            "axisTarget": "LEFT",
            "rules": [
              {
                "value": 0,
                "color": "#7dc540"
              },
              {
                "value": 90,
                "color": "#f5d30f"
              },
              {
                "color": "#dc172a"
              }
            ],
            "queryId": "",
            "visible": true
          }
        ],
        "tableSettings": {
          "isThresholdBackgroundAppliedToCell": false,
          "hiddenColumns": []
        },
        "graphChartSettings": {
          "connectNulls": false
        },
        "honeycombSettings": {
          "showHive": true,
          "showLegend": true,
          "showLabels": false
        }
      },
      "queriesSettings": {
        "resolution": "",
        "foldTransformation": "LAST_VALUE"
      },
      "metricExpressions": [
        "resolution=null&((builtin:kubernetes.node.requests_cpu:last:splitBy(\"dt.entity.kubernetes_cluster\"):sum/builtin:kubernetes.node.cpu_allocatable:last:splitBy(\"dt.entity.kubernetes_cluster\"):sum*100):sort(value(sum,descending))):limit(100):names:last"
      ]
    },
    {
      "name": "Number of nodes",
      "tileType": "DATA_EXPLORER",
      "configured": true,
      "bounds": {
        "top": 38,
        "left": 0,
        "width": 342,
        "height": 304
      },
      "tileFilter": {
        "timeframe": "-5m"
      },
      "isAutoRefreshDisabled": false,
      "customName": "Cluster nodes",
      "queries": [
        {
          "id": "C",
          "spaceAggregation": "AUTO",
          "timeAggregation": "DEFAULT",
          "splitBy": [
            "dt.entity.kubernetes_cluster"
          ],
          "metricSelector": "builtin:kubernetes.nodes:last:splitBy(\"dt.entity.kubernetes_cluster\"):sum:sort(value(sum,descending))",
          "rate": "NONE",
          "enabled": true
        }
      ],
      "visualConfig": {
        "type": "PIE_CHART",
        "global": {
          "hideLegend": false
        },
        "rules": [
          {
            "matcher": "C:",
            "properties": {
              "color": "DEFAULT"
            },
            "seriesOverrides": []
          }
        ],
        "axes": {
          "xAxis": {
            "visible": true
          },
          "yAxes": []
        },
        "heatmapSettings": {
          "yAxis": "VALUE"
        },
        "thresholds": [
          {
            "axisTarget": "LEFT",
            "rules": [
              {
                "color": "#7dc540"
              },
              {
                "color": "#f5d30f"
              },
              {
                "color": "#dc172a"
              }
            ],
            "queryId": "",
            "visible": true
          }
        ],
        "tableSettings": {
          "isThresholdBackgroundAppliedToCell": false,
          "hiddenColumns": []
        },
        "graphChartSettings": {
          "connectNulls": false
        },
        "honeycombSettings": {
          "showHive": true,
          "showLegend": true,
          "showLabels": false
        }
      },
      "queriesSettings": {
        "resolution": ""
      },
      "metricExpressions": [
        "resolution=null&(builtin:kubernetes.nodes:last:splitBy(\"dt.entity.kubernetes_cluster\"):sum:sort(value(sum,descending))):limit(100):names:fold(auto)"
      ]
    },
    {
      "name": "Failed pods",
      "tileType": "DATA_EXPLORER",
      "configured": true,
      "bounds": {
        "top": 38,
        "left": 1368,
        "width": 304,
        "height": 152
      },
      "tileFilter": {
        "timeframe": "-5m"
      },
      "isAutoRefreshDisabled": false,
      "customName": "Pods",
      "queries": [
        {
          "id": "C",
          "spaceAggregation": "AUTO",
          "timeAggregation": "DEFAULT",
          "splitBy": [
            "k8s.namespace.name",
            "dt.entity.kubernetes_cluster"
          ],
          "metricSelector": "builtin:kubernetes.pods:last:filter(eq(\"pod_phase\", \"Failed\")):splitBy(\"k8s.namespace.name\",\"dt.entity.kubernetes_cluster\"):sum:sort(value(sum,descending))",
          "rate": "NONE",
          "enabled": true
        }
      ],
      "visualConfig": {
        "type": "TOP_LIST",
        "global": {
          "hideLegend": false
        },
        "rules": [
          {
            "matcher": "C:",
            "unitTransform": "auto",
            "valueFormat": "0",
            "properties": {
              "color": "DEFAULT",
              "seriesType": "LINE"
            },
            "seriesOverrides": [
              {
                "name": "Select series",
                "color": "#5ead35"
              },
              {
                "name": "Select series",
                "color": "#f5d30f"
              },
              {
                "name": "Select series",
                "color": "#c41425"
              },
              {
                "name": "Select series",
                "color": "#008cdb"
              }
            ]
          }
        ],
        "axes": {
          "xAxis": {
            "visible": true
          },
          "yAxes": []
        },
        "heatmapSettings": {
          "yAxis": "VALUE"
        },
        "thresholds": [
          {
            "axisTarget": "LEFT",
            "rules": [
              {
                "color": "#7dc540"
              },
              {
                "value": 0,
                "color": "#f5d30f"
              },
              {
                "color": "#dc172a"
              }
            ],
            "queryId": "",
            "visible": true
          }
        ],
        "tableSettings": {
          "isThresholdBackgroundAppliedToCell": false,
          "hiddenColumns": []
        },
        "graphChartSettings": {
          "connectNulls": false
        },
        "honeycombSettings": {
          "showHive": true,
          "showLegend": true,
          "showLabels": false
        }
      },
      "queriesSettings": {
        "resolution": ""
      },
      "metricExpressions": [
        "resolution=null&(builtin:kubernetes.pods:last:filter(eq(pod_phase,Failed)):splitBy(\"k8s.namespace.name\",\"dt.entity.kubernetes_cluster\"):sum:sort(value(sum,descending))):limit(100):names:fold(auto)"
      ]
    },
    {
      "name": "Pending pods",
      "tileType": "DATA_EXPLORER",
      "configured": true,
      "bounds": {
        "top": 190,
        "left": 1368,
        "width": 304,
        "height": 152
      },
      "tileFilter": {
        "timeframe": "-5m"
      },
      "isAutoRefreshDisabled": false,
      "customName": "Pods",
      "queries": [
        {
          "id": "C",
          "spaceAggregation": "AUTO",
          "timeAggregation": "DEFAULT",
          "splitBy": [
            "k8s.namespace.name",
            "dt.entity.kubernetes_cluster"
          ],
          "metricSelector": "builtin:kubernetes.pods:last:filter(eq(\"pod_phase\",\"Pending\")):splitBy(\"k8s.namespace.name\",\"dt.entity.kubernetes_cluster\"):sum:sort(value(sum,descending))",
          "rate": "NONE",
          "enabled": true
        }
      ],
      "visualConfig": {
        "type": "TOP_LIST",
        "global": {
          "hideLegend": false
        },
        "rules": [
          {
            "matcher": "C:",
            "unitTransform": "auto",
            "valueFormat": "0",
            "properties": {
              "color": "DEFAULT",
              "seriesType": "LINE"
            },
            "seriesOverrides": [
              {
                "name": "Select series",
                "color": "#5ead35"
              },
              {
                "name": "Select series",
                "color": "#f5d30f"
              },
              {
                "name": "Select series",
                "color": "#c41425"
              },
              {
                "name": "Select series",
                "color": "#008cdb"
              }
            ]
          }
        ],
        "axes": {
          "xAxis": {
            "visible": true
          },
          "yAxes": []
        },
        "heatmapSettings": {
          "yAxis": "VALUE"
        },
        "thresholds": [
          {
            "axisTarget": "LEFT",
            "rules": [
              {
                "color": "#7dc540"
              },
              {
                "value": 0,
                "color": "#7c38a1"
              },
              {
                "color": "#dc172a"
              }
            ],
            "queryId": "",
            "visible": true
          }
        ],
        "tableSettings": {
          "isThresholdBackgroundAppliedToCell": false,
          "hiddenColumns": []
        },
        "graphChartSettings": {
          "connectNulls": false
        },
        "honeycombSettings": {
          "showHive": true,
          "showLegend": true,
          "showLabels": false
        }
      },
      "queriesSettings": {
        "resolution": ""
      },
      "metricExpressions": [
        "resolution=null&(builtin:kubernetes.pods:last:filter(eq(pod_phase,Pending)):splitBy(\"k8s.namespace.name\",\"dt.entity.kubernetes_cluster\"):sum:sort(value(sum,descending))):limit(100):names:fold(auto)"
      ]
    },
    {
      "name": "Allocatable CPU",
      "tileType": "DATA_EXPLORER",
      "configured": true,
      "bounds": {
        "top": 380,
        "left": 0,
        "width": 418,
        "height": 304
      },
      "tileFilter": {
        "timeframe": "-5m"
      },
      "isAutoRefreshDisabled": false,
      "customName": "Cluster nodes",
      "queries": [
        {
          "id": "C",
          "spaceAggregation": "AUTO",
          "timeAggregation": "DEFAULT",
          "splitBy": [
            "dt.entity.kubernetes_cluster"
          ],
          "metricSelector": "builtin:kubernetes.node.cpu_allocatable:last:splitBy(\"dt.entity.kubernetes_cluster\"):sum:sort(value(sum,descending))",
          "rate": "NONE",
          "enabled": true
        }
      ],
      "visualConfig": {
        "type": "PIE_CHART",
        "global": {
          "hideLegend": false
        },
        "rules": [
          {
            "matcher": "C:",
            "unitTransform": "Cores",
            "valueFormat": "0,0",
            "properties": {
              "color": "DEFAULT",
              "seriesType": "LINE"
            },
            "seriesOverrides": []
          }
        ],
        "axes": {
          "xAxis": {
            "visible": true
          },
          "yAxes": []
        },
        "heatmapSettings": {
          "yAxis": "VALUE"
        },
        "thresholds": [
          {
            "axisTarget": "LEFT",
            "rules": [
              {
                "color": "#7dc540"
              },
              {
                "color": "#f5d30f"
              },
              {
                "color": "#dc172a"
              }
            ],
            "queryId": "",
            "visible": true
          }
        ],
        "tableSettings": {
          "isThresholdBackgroundAppliedToCell": false,
          "hiddenColumns": []
        },
        "graphChartSettings": {
          "connectNulls": false
        },
        "honeycombSettings": {
          "showHive": true,
          "showLegend": true,
          "showLabels": false
        }
      },
      "queriesSettings": {
        "resolution": ""
      },
      "metricExpressions": [
        "resolution=null&(builtin:kubernetes.node.cpu_allocatable:last:splitBy(\"dt.entity.kubernetes_cluster\"):sum:sort(value(sum,descending))):limit(100):names:fold(auto)"
      ]
    },
    {
      "name": "Allocatable Memory",
      "tileType": "DATA_EXPLORER",
      "configured": true,
      "bounds": {
        "top": 380,
        "left": 836,
        "width": 418,
        "height": 304
      },
      "tileFilter": {
        "timeframe": "-5m"
      },
      "isAutoRefreshDisabled": false,
      "customName": "Cluster nodes",
      "queries": [
        {
          "id": "C",
          "spaceAggregation": "AUTO",
          "timeAggregation": "DEFAULT",
          "splitBy": [
            "dt.entity.kubernetes_cluster"
          ],
          "metricSelector": "builtin:kubernetes.node.memory_allocatable:last:splitBy(\"dt.entity.kubernetes_cluster\"):sum:sort(value(sum,descending))",
          "rate": "NONE",
          "enabled": true
        }
      ],
      "visualConfig": {
        "type": "PIE_CHART",
        "global": {
          "hideLegend": false
        },
        "rules": [
          {
            "matcher": "C:",
            "unitTransform": "GibiByte",
            "valueFormat": "0,0",
            "properties": {
              "color": "DEFAULT",
              "seriesType": "LINE"
            },
            "seriesOverrides": []
          }
        ],
        "axes": {
          "xAxis": {
            "visible": true
          },
          "yAxes": []
        },
        "heatmapSettings": {
          "yAxis": "VALUE"
        },
        "thresholds": [
          {
            "axisTarget": "LEFT",
            "rules": [
              {
                "color": "#7dc540"
              },
              {
                "color": "#f5d30f"
              },
              {
                "color": "#dc172a"
              }
            ],
            "queryId": "",
            "visible": true
          }
        ],
        "tableSettings": {
          "isThresholdBackgroundAppliedToCell": false,
          "hiddenColumns": []
        },
        "graphChartSettings": {
          "connectNulls": false
        },
        "honeycombSettings": {
          "showHive": true,
          "showLegend": true,
          "showLabels": false
        }
      },
      "queriesSettings": {
        "resolution": ""
      },
      "metricExpressions": [
        "resolution=null&(builtin:kubernetes.node.memory_allocatable:last:splitBy(\"dt.entity.kubernetes_cluster\"):sum:sort(value(sum,descending))):limit(100):names:fold(auto)"
      ]
    },
    {
      "name": "Allocatable Memory",
      "tileType": "DATA_EXPLORER",
      "configured": true,
      "bounds": {
        "top": 722,
        "left": 836,
        "width": 418,
        "height": 304
      },
      "tileFilter": {
        "timeframe": "-5m"
      },
      "isAutoRefreshDisabled": false,
      "customName": "Cluster nodes",
      "queries": [
        {
          "id": "C",
          "spaceAggregation": "AUTO",
          "timeAggregation": "DEFAULT",
          "splitBy": [
            "dt.entity.kubernetes_node",
            "dt.entity.kubernetes_cluster"
          ],
          "metricSelector": "builtin:kubernetes.node.memory_allocatable:last:splitBy(\"dt.entity.kubernetes_node\", \"dt.entity.kubernetes_cluster\"):sum:sort(value(sum,descending))",
          "rate": "NONE",
          "enabled": true
        }
      ],
      "visualConfig": {
        "type": "PIE_CHART",
        "global": {
          "hideLegend": false
        },
        "rules": [
          {
            "matcher": "C:",
            "unitTransform": "GibiByte",
            "valueFormat": "0,0",
            "properties": {
              "color": "DEFAULT",
              "seriesType": "LINE"
            },
            "seriesOverrides": []
          }
        ],
        "axes": {
          "xAxis": {
            "visible": true
          },
          "yAxes": []
        },
        "heatmapSettings": {
          "yAxis": "VALUE"
        },
        "thresholds": [
          {
            "axisTarget": "LEFT",
            "rules": [
              {
                "color": "#7dc540"
              },
              {
                "color": "#f5d30f"
              },
              {
                "color": "#dc172a"
              }
            ],
            "queryId": "",
            "visible": true
          }
        ],
        "tableSettings": {
          "isThresholdBackgroundAppliedToCell": false,
          "hiddenColumns": []
        },
        "graphChartSettings": {
          "connectNulls": false
        },
        "honeycombSettings": {
          "showHive": true,
          "showLegend": true,
          "showLabels": false
        }
      },
      "queriesSettings": {
        "resolution": ""
      },
      "metricExpressions": [
        "resolution=null&(builtin:kubernetes.node.memory_allocatable:last:splitBy(\"dt.entity.kubernetes_node\",\"dt.entity.kubernetes_cluster\"):sum:sort(value(sum,descending))):limit(100):names:fold(auto)"
      ]
    },
    {
      "name": "Allocatable CPU",
      "tileType": "DATA_EXPLORER",
      "configured": true,
      "bounds": {
        "top": 722,
        "left": 0,
        "width": 418,
        "height": 304
      },
      "tileFilter": {
        "timeframe": "-5m"
      },
      "isAutoRefreshDisabled": false,
      "customName": "Cluster nodes",
      "queries": [
        {
          "id": "C",
          "spaceAggregation": "AUTO",
          "timeAggregation": "DEFAULT",
          "splitBy": [
            "dt.entity.kubernetes_node",
            "dt.entity.kubernetes_cluster"
          ],
          "metricSelector": "builtin:kubernetes.node.cpu_allocatable:last:splitBy(\"dt.entity.kubernetes_node\", \"dt.entity.kubernetes_cluster\"):sum:sort(value(sum,descending))",
          "rate": "NONE",
          "enabled": true
        }
      ],
      "visualConfig": {
        "type": "PIE_CHART",
        "global": {
          "hideLegend": false
        },
        "rules": [
          {
            "matcher": "C:",
            "unitTransform": "Cores",
            "valueFormat": "0,0",
            "properties": {
              "color": "DEFAULT",
              "seriesType": "LINE"
            },
            "seriesOverrides": []
          }
        ],
        "axes": {
          "xAxis": {
            "visible": true
          },
          "yAxes": []
        },
        "heatmapSettings": {
          "yAxis": "VALUE"
        },
        "thresholds": [
          {
            "axisTarget": "LEFT",
            "rules": [
              {
                "color": "#7dc540"
              },
              {
                "color": "#f5d30f"
              },
              {
                "color": "#dc172a"
              }
            ],
            "queryId": "",
            "visible": true
          }
        ],
        "tableSettings": {
          "isThresholdBackgroundAppliedToCell": false,
          "hiddenColumns": []
        },
        "graphChartSettings": {
          "connectNulls": false
        },
        "honeycombSettings": {
          "showHive": true,
          "showLegend": true,
          "showLabels": false
        }
      },
      "queriesSettings": {
        "resolution": ""
      },
      "metricExpressions": [
        "resolution=null&(builtin:kubernetes.node.cpu_allocatable:last:splitBy(\"dt.entity.kubernetes_node\",\"dt.entity.kubernetes_cluster\"):sum:sort(value(sum,descending))):limit(100):names:fold(auto)"
      ]
    }
  ]
}
