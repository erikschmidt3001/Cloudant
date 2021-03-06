---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-27"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

<!-- Acrolinx: 2018-05-31 -->

# Advanced
{: #advanced}

These endpoints provide information about the state of the cluster,
details about revision history,
and other miscellaneous tasks.
{:shortdesc}

## `GET /`
{: #-get-}

-	**Method**: `GET`
-	**Path**: `/`
-	**Response**: Welcome message and version

Accessing the root endpoint `/` returns meta information about the cluster.
The response is a JSON object that contains a welcome message and the version of the server.
The `version` field contains the CouchDB version the server is compatible with.
The `vendor.version` field contains the build number of {{site.data.keyword.cloudantfull}}'s CouchDB implementation.

For {{site.data.keyword.cloudant_short_notm}} versions before 2.0.0,
you might see a `cloudant_build` field in the response,
rather than a `vendor.version` field.
In each case,
the field contains the build number of {{site.data.keyword.cloudant_short_notm}}'s CouchDB implementation.
{: tip}

_Example request to get server meta information,by using HTTP:_

```HTTP
GET / HTTP/1.1
HOST: $ACCOUNT.cloudant.com
```
{:codeblock}

_Example request to get server meta information, by using the command line:_

```sh
curl https://$ACCOUNT.cloudant.com/
```
{:codeblock}

<!--

_Example request to get server meta information, by using Javascript:_

```javascript
var nano = require('nano');
var account = nano('https://$ACCOUNT:$PASSWORD@$ACCOUNT.cloudant.com');
account.request({
	path: '/'
}, function (err, body) {
	if (!err) {
		console.log(body);
	}
});
```
{:codeblock}

-->

_Example JSON response for {{site.data.keyword.cloudant_short_notm}} version 2.0.0:_

```json
{
	"couchdb": "Welcome",
	"version": "2.0.0",
	"vendor": {
		"name": "IBM Cloudant",
		"version": "5638",
		"variant": "paas"
	},
	"features": [
		"geo"
	]
}
```
{:codeblock}

_Example JSON response for an older {{site.data.keyword.cloudant_short_notm}} version 1.0.2:_

```json
{
	"couchdb": "Welcome",
	"version": "1.0.2",
	"cloudant_build": "2660"
}
```
{:codeblock}

## `GET /_db_updates`
{: #-get-_db_updates-}

This endpoint is only available to customers with dedicated system accounts.
{: tip}

The `/_db_updates` endpoint returns a list of changes to databases,
similar to a global [changes feed](database.html#get-changes).
Changes can be either updates to an existing database,
creation of a new database,
or deletion of a database.
Like the changes feed,
the `/_db_updates` endpoint is not guaranteed to return changes in the correct order,
and might contain changes more than once.
Polling modes for this endpoint work like the polling modes for
[the changes feed](database.html#get-changes).


Argument | Description | Optional | Type | Default | Supported Values
---------|-------------|----------|------|---------|-----------------
descending | Determines that results are returned in descending order, in other words the most recent event appears first. By default, the oldest event is returned first. | yes | boolean | false | 
feed | Type of feed | yes | string | normal | `continuous`: Continuous (non-polling) mode, `longpoll`: Long polling mode, `normal`: default polling mode
heartbeat | Time in milliseconds after which an empty line is sent during longpoll or continuous if no changes occurred | yes | numeric | 60000 | 
limit | Maximum number of results to return | yes | numeric | none |  
since | Start the results from changes immediately after the specified sequence number. If since is 0 (the default), the request returns all changes since the feature was activated. | yes | string | 0 | 
timeout | Number of milliseconds to wait for data in a `longpoll` or `continuous` feed before the response is terminated. If both `heartbeat` and `timeout` are suppled, `heartbeat` supersedes `timeout`. | yes | numeric |  | 

_Example request to get a list of changes to the database, by using HTTP:_

```HTTP
GET /_db_updates HTTP/1.1
```
{:codeblock}

_Example request to get a list of changes to the database, by using the command line:_

```sh
curl https://$ACCOUNT.cloudant.com/_db_updates \
	-u $ACCOUNT
```
{:codeblock}

<!--

_Example request to get a list of changes to the database, using Javascript:_

```javascript
var nano = require('nano');
var account = nano('https://$ACCOUNT:$PASSWORD@$ACCOUNT.cloudant.com');
account.request({
	path: '_db_updates'
}, function (err, body) {
	if (!err) {
		console.log(body);
	}
});
```
{:codeblock}

-->

_Example response:_

```json
{
	"results": [{
		"dbname": "$DATABASE_NAME",
		"type": "created",
		"account": "$ACCOUNT",
		"seq": "673-g1AAAAJAeJyN0Et..."
	}],
	"last_seq": "673-g1AAAAJAeJyN0Et..."
}
```
{:codeblock}

## `GET /$DATABASE/_shards`
{: #-get-database-_shards-}

The `/$DATABASE/_shards` endpoint returns information about the shards in the cluster,
specifically what nodes contain what hash ranges.

The `shards` field in the response contains an object with keys that are the hash value range for each shard.
Each value is the array of nodes that contain that a copy of that shard.

_Example request, by using HTTP:_

```HTTP
GET /$DATABASE/_shards HTTP/1.1
```
{:codeblock}

_Example request, by using the command line:_

```sh
curl https://$ACCOUNT.cloudant.com/$DATABASE/_shards \
	-u $ACCOUNT
```
{:codeblock}

<!--

_Example request, using Javascript:_

```javascript
var nano = require('nano');
var account = nano('https://$ACCOUNT:$PASSWORD@$ACCOUNT.cloudant.com');
account.request({
	database: $DATABASE,
	path: '_shards'
}, function (err, body) {
	if (!err) {
		console.log(body);
	}
});
```
{:codeblock}

-->

_Example response:_

```json
{
	"shards": {
		"00000000-3fffffff": [
			"dbcore@db1.mead.cloudant.net",
			"dbcore@db2.mead.cloudant.net",
			"dbcore@db3.mead.cloudant.net"
		],
		"40000000-7fffffff": [
			"dbcore@db1.mead.cloudant.net",
			"dbcore@db2.mead.cloudant.net",
			"dbcore@db3.mead.cloudant.net"
		],
		"80000000-bfffffff": [
			"dbcore@db1.mead.cloudant.net",
			"dbcore@db2.mead.cloudant.net",
			"dbcore@db3.mead.cloudant.net"
		],
		"c0000000-ffffffff": [
			"dbcore@db1.mead.cloudant.net",
			"dbcore@db2.mead.cloudant.net",
			"dbcore@db3.mead.cloudant.net"
		]
	}
}
```
{:codeblock}

## `GET /$DATABASE/_missing_revs`
{: #-get-database_missing_revs-}

When supplied with a list of document revisions, 
the `/$DATABASE/_missing_revs` endpoint returns a list of the document revisions that do not exist in the database.

The list of document revisions is supplied in a JSON document,
similar to the following example:

```json
{
	"$DOCUMENT_ID": [
		"$REV_1",
		"$REV_2"
	]
}
```
{:codeblock}

_Example request, by using HTTP:_

```HTTP
GET /$DATABASE/_missing_revs HTTP/1.1
Content-Type: application/json
```
{:codeblock}

_Example request, by using the command line:_

```sh
curl https://$ACCOUNT.cloudant.com/$DATABASE/_missing_revs \
	 -X POST \
	 -u "$ACCOUNT:$PASSWORD" \
	 -H "Content-Type: application/json" \
	 -d @request-body.json
```
{:codeblock}

<!--

_Example request, using Javascript:_

```javascript
var nano = require('nano');
var account = nano('https://$ACCOUNT:$PASSWORD@$ACCOUNT.cloudant.com');
account.request({
	database: $DATABASE,
	path: '_missing_revs',
	method: 'POST',
	body: '$JSON'
},
function (err, body) {
	if (!err) {
		console.log(body);
	}
});
```
{:codeblock}

-->

_Example response:_

```json
{
	"missed_revs":{
		"$DOCUMENT_ID": [
			"$REV_1"
		]
	}
}
```
{:codeblock}

## `POST /$DATABASE/_revs_diff`
{: #-post-database-_revs_diff-}

When supplied with a set of document revision IDs, 
the `/$DATABASE/_revs_diff` endpoint returns a subset of those document revision IDs that do not correspond to revisions stored in the database.

The list of document revision IDs is supplied in a JSON document,
similar to the following example:

```json
{
	"190f721ca3411be7aa9477db5f948bbb": [
		"3-bb72a7682290f94a985f7afac8b27137",
		"4-10265e5a26d807a3cfa459cf1a82ef2e",
		"5-067a00dff5e02add41819138abb3284d"
	]
}
```
{:codeblock}

_Example request, by using HTTP:_

```HTTP
POST /$DATABASE/_revs_diff HTTP/1.1
Content-Type: application/json
```
{:codeblock}

_Example request, from the command line:_

```sh
curl https://$ACCOUNT.cloudant.com/$DATABASE/_revs_diff \
	-X POST \
	-u $ACCOUNT \
	-d "$JSON"
```
{:codeblock}

<!--

_Example request, using Javascript:_

```javascript
var nano = require('nano');
var account = nano('https://$ACCOUNT:$PASSWORD@$ACCOUNT.cloudant.com');
account.request({
	database: $DATABASE,
	path: '_revs_diff',
	method: 'POST',
	body: '$JSON'
}, function (err, body) {
	if (!err) {
		console.log(body);
	}
});
```
{:codeblock}

-->

_Example response:_

```json
{
	"190f721ca3411be7aa9477db5f948bbb": {
		"missing": [
			"3-bb72a7682290f94a985f7afac8b27137",
			"5-067a00dff5e02add41819138abb3284d"
		],
		"possible_ancestors": [
			"4-10265e5a26d807a3cfa459cf1a82ef2e"
		]
	}
}
```
{:codeblock}

## `GET /$DATABASE/_revs_limit`
{: #-get-database-_revs_limit-}

Gets the number of past revisions of a document that {{site.data.keyword.cloudant_short_notm}} retains.

Although the documents that are associated with past revisions are automatically removed,
"tombstones" remain with the `_rev` value for that revision.
If a document has more revisions than the value of `_revs_limit`,
{{site.data.keyword.cloudant_short_notm}} deletes the tombstones of the oldest revisions.
{: tip}

_Example request, by using HTTP:_

```HTTP
GET /$DATABASE/_revs_limit HTTP/1.1
```
{:codeblock}

_Example request, by using the command line:_

```sh
curl https://$ACCOUNT.cloudant.com/$DATABASE/_revs_limit \
	-X GET \
	-u "$ACCOUNT:$PASSWORD"
```
{:codeblock}

<!--

_Example request, using Javascript:_

```javascript
var nano = require('nano');
var account = nano('https://$ACCOUNT:$PASSWORD@$ACCOUNT.cloudant.com');
account.request({
	path: '_revs_limit'
}, function (err, body) {
	if (!err) {
		console.log(body);
	}
});
```
{:codeblock}

-->

_Example response:_

```
1000
```
{:codeblock}

## `PUT /$DATABASE/_revs_limit`
{: #-put-database-_revs_limit-}

Sets the maximum number of past revisions of a document that {{site.data.keyword.cloudant_short_notm}} retains.

Although the documents that are associated with past revisions are automatically removed,
"tombstones" remain with the `_rev` value for that revision.
If a document has more revisions than the value of `_revs_limit`,
{{site.data.keyword.cloudant_short_notm}} deletes the tombstones of the oldest revisions.
{: tip}

_Example request, by using HTTP:_

```HTTP
PUT /$DATABASE/_revs_limit HTTP/1.1
```
{:codeblock}

_Example request, by using the command line:_

```sh
curl https://$ACCOUNT.cloudant.com/_revs_limit \
	-u $ACCOUNT \
	-X PUT \
	-d 500
```
{:codeblock}

<!--

_Example request, using Javascript:_

```javascript
var nano = require('nano');
var account = nano('https://$ACCOUNT:$PASSWORD@$ACCOUNT.cloudant.com');
account.request({
	path: '_revs_limit',
	body: '500',
	method: 'PUT'
}, function (err, body) {
	if (!err) {
		console.log(body);
	}
});
```
{:codeblock}

-->

_Example response:_

```json
{
	"ok": true
}
```
{:codeblock}

## `GET /_membership`
{: #-get-_membership-}

This endpoint returns the names of nodes in the cluster.
Currently, active clusters are indicated in the `cluster_nodes` field.
The `all_nodes` field lists all the nodes,
regardless of whether they are active or not.

-   **Method**: `GET`
-   **Path**: `/_membership`
-   **Response**: JSON document that lists cluster nodes and all nodes
-   **Roles permitted**: _admin

_Example request to list nodes in the cluster, by using HTTP:_

```http
GET /_membership HTTP/1.1
```
{:codeblock}

_Example request to list nodes in the cluster, by using the command line:_

```sh
curl https://$ACCOUNT.cloudant.com/_membership \
	-u $ACCOUNT
```
{:codeblock}

<!--

_Example request to list nodes in the cluster, using Javascript:_

```javascript
var nano = require('nano');
var account = nano('https://$ACCOUNT:$PASSWORD@$ACCOUNT.cloudant.com');
account.request({
	path: '_membership'
}, function (err, body) {
	if (!err) {
		console.log(body);
	}
});
```
{:codeblock}

-->

### Response structure
{: #response-structure}

Field name      | Description
----------------|------------------------------------------------------------------
`cluster_nodes` | Array of node names (strings) of the active nodes in the cluster.
`all_nodes`     | Array of nodes names (strings) of all nodes in the cluster.

_Example response:_

```json
{
	"cluster_nodes": [
		"dbcore@db1.testy004.cloudant.net",
		"dbcore@db2.testy004.cloudant.net",
		"dbcore@db3.testy004.cloudant.net"
	],
	"all_nodes": [
		"dbcore@db1.testy004.cloudant.net",
		"dbcore@db2.testy004.cloudant.net",
		"dbcore@db3.testy004.cloudant.net"
	]
}
```
{:codeblock}

## `GET /_uuids`
{: #-get-_uuids-}

This endpoint is a general utility requests one or more Universally Unique Identifiers (UUIDs).
The response is a JSON object that provides a list of UUIDs.

-   **Method**: `GET`
-   **Path**: `/_uuids`
-   **Response**: JSON document that contains a list of UUIDs

Argument | Description               | Optional | Type
---------|---------------------------|----------|------------------------------------------------------------------
`count`  | Number of UUIDs to return | yes      | Positive integer, greater than 0 and less than or equal to 1,000.

_Example request for a single UUID, by using HTTP:_

```HTTP
GET /_uuids HTTP/1.1
```
{:codeblock}

_Example request for a single UUID, by using the command line:_

```sh
curl https://$ACCOUNT.cloudant.com/_uuids \
	-u $ACCOUNT
```
{:codeblock}

<!--

_Example request for a single UUID, using Javascript:_

```javascript
var nano = require('nano');
var account = nano('https://$ACCOUNT:$PASSWORD@$ACCOUNT.cloudant.com');
account.request({
	path: '_uuids'
}, function (err, body) {
	if (!err) {
		console.log(body);
	}
});
```
{:codeblock}

-->

_Example response to a request for a single UUID:_

```json
{
	"uuids" : [
		"7e4b5a14b22ec1cf8e58b9cdd0000da3"
	]
}
```
{:codeblock}

_Example request for five UUIDs, by using HTTP:_

```HTTP
GET /_uuids?count=5 HTTP/1.1
```
{:codeblock}

_Example request for five UUIDs, by using the command line:_

```sh
curl https://$ACCOUNT.cloudant.com/_uuids?count=5 \
	-u $ACCOUNT
```
{:codeblock}

<!--

_Example request for five UUIDs, using Javascript:_

```javascript
var nano = require('nano');
var account = nano('https://$ACCOUNT:$PASSWORD@$ACCOUNT.cloudant.com');
account.request({
	path: '_uuids?count=5'
}, function (err, body) {
	if (!err) {
		console.log(body);
	}
});
```
{:codeblock}

-->

_Example response to a request for five UUIDs:_

```json
{
	"uuids" : [
		"c9df0cdf4442f993fc5570225b405a80",
		"c9df0cdf4442f993fc5570225b405bd2",
		"c9df0cdf4442f993fc5570225b405e42",
		"c9df0cdf4442f993fc5570225b4061a0",
		"c9df0cdf4442f993fc5570225b406a20"
	]
}
```
{:codeblock}
