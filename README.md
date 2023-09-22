# Grafana Azure Plus Datasource

![Build & Publish](https://github.com/DFE_Digital/grafana-azure-datasource/workflows/Build%20&%20Publish/badge.svg?branch=master)

Grafana **Azure plus** datasource plugin provides additional azure capabilities to grafana. For examples and screenshots, refer [here](https://github.com/DFE_Digital/grafana-azure-datasource/issues/5).

## Features

* Azure Resource Graph
* Azure Cost Analysis
* Azure Service Health

### Azure Cost Analysis

![image](https://user-images.githubusercontent.com/153843/82420435-9d5b1800-9a77-11ea-818e-7b57b0f6353c.png)

### Azure Resource Graph

![image](https://user-images.githubusercontent.com/153843/82420772-178b9c80-9a78-11ea-8294-2d0500aa3592.png)

## Installation

There are multiple ways to install this plugin

#### Download and extract zip file

Download the zip file from [github](https://github.com/DFE_Digital/grafana-azure-datasource/archive/master.zip) and extract into your grafana plugin folder. Then restart Grafana.

#### Using grafana-cli

If you are using grafana-cli, execute the following command to install the plugin

```
grafana-cli --pluginUrl https://github.com/DFE_Digital/grafana-azure-datasource/archive/master.zip plugins install DFE_Digital-azure-datasource
```
#### Using helm chart

If you use help chart to provision grafana, use the following config to install the plugin

```
plugins:
  - https://github.com/DFE_Digital/grafana-azure-datasource/archive/master.zip;DFE_Digital-azure-datasource
```

## Configuration

Configuration of the plugin requires Tenant ID, Client ID and Client Secret.

#### Provisioning via file

If you want to use the grafana provisioning feature, use the following yaml

```
apiVersion: 1

datasources:
- name: <Datasource Name>
  type: DFE_Digital-azure-datasource
  access: proxy
  isDefault: false
  jsonData:
       cloudName: azuremonitor
       clientId: <Azure SPN ID>
       tenantId: <Azure Tenant ID>
  secureJsonData:
       clientSecret: <Azure SPN Secret>
  version: 1
  readOnly: false
```

#### Azure Permissions / Roles 

The client which connects to azure should have the following permissions.

* [Monitoring Reader](https://docs.microsoft.com/en-us/azure/role-based-access-control/built-in-roles#monitoring-reader) OR [Reader](https://docs.microsoft.com/en-us/azure/role-based-access-control/built-in-roles#reader)

In case, if you are using the cost analysis services alone, provide only the following roles to the client

* [Cost Management Reader](https://docs.microsoft.com/en-us/azure/role-based-access-control/built-in-roles#cost-management-reader)

## Dashboards Included

For convenience, following sample dashboards are included in the plugin

* Azure Cost - By Subscription

If you want to share your dashboards to the community, Create a pull request with the dashboard json.

## Template Variables

Following template variable queries are supported

- `Subscriptions()`
- `ResourceGraph(YOUR RESOURCE GRAPH QUERY GOES HERE)`

If the Resource graph query return two column, first column will be considered as display value and the second column will be considered as actual value. 

Sample template variable queries are given [here](https://github.com/DFE_Digital/grafana-azure-datasource/issues/5#issuecomment-666500009).