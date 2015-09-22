[**Keyvaas.io**](https://www.keyvaas.io) is a free service provided by Tutum to store and retrieve key value pairs over a simple HTTP interface. In order to sign up, you just need a Tutum account.


## Authentication

Keyvaas.io authentication is the same as with Tutum's API. You can authenticate using your Tutum API key, or using the `TUTUM_AUTH` environment variable injected in containers when providing them with an API role.


## Set a key value pair

In order to store `myvalue` in the key `mykey`, perform the following HTTP call:

	curl -X PUT -d "myvalue" -H "Authorization: ApiKey username:apikey" https://keyvaas.io/username/mykey
	
Replace `username` with your Tutum username and `apikey` with your Tutum ApiKey.


## Get a key value pair

To get the key `mykey`, perform the following HTTP call:

	curl -H "Authorization: ApiKey username:apikey" https://keyvaas.io/username/mykey

Replace `username` with your Tutum username and `apikey` with your Tutum ApiKey.


## Delete a key value pair

To delete the key `mykey`, perform the following HTTP call:

	curl -X DELETE -H "Authorization: ApiKey username:apikey" https://keyvaas.io/username/mykey

Replace `username` with your Tutum username and `apikey` with your Tutum ApiKey.


## Using folders

Keys can be grouped using folders:

	curl -X PUT -d "myvalue" -H "Authorization: ApiKey username:apikey" https://keyvaas.io/username/folder/mykey1
	curl -X PUT -d "myvalue" -H "Authorization: ApiKey username:apikey" https://keyvaas.io/username/folder/mykey2

In order to get the keys within a folder, you can `GET` the folder path:

	curl -H "Authorization: ApiKey username:apikey" https://keyvaas.io/username/folder/

Which will return a recursive list of keys within that folder.

You can delete all keys within a folder recursively by performing the following HTTP call:

	curl -X DELETE -H "Authorization: ApiKey username:apikey" https://keyvaas.io/username/folder/


## Limits

The free service runs with the following limitations:

* Maximum number of keys: 256
* Maximum value size: 64 KB
* Maximum key length: 256 characters
