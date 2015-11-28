Meteor Remote DDP
=================

When building an app with decoupled client-code and server-code (say a mobile version of an existing app), your client connects via DDP to its own server by default. 

This package allows you to specify a remote DDP server for Accounts, subscriptions and Meteor methods.

This package is quite brittle. It relies heavily on private APIs and monkey patching and has been
tested by the author on **Meteor 1.1**. Bug reports welcome.

Usage
-----

1. `meteor add budgie:remote-ddp`

	If you use accounts-base, or any dependant package, you must edit `.meteor/packages` to move `budgie:remote-ddp` above any such packages.

1. Add the remote to your settings JSON file:

	``` json
	{
	  "public": {
		"remoteDdpUrl": "http://localhost:5000"
	  }
	}
	```

1. In your client code, before doing anything that uses DDP, initialise RemoteDDP:

	``` javascript
	RemoteDDP.monkeyPatch();
	```
	
	*Note that the `Accounts` package uses DDP as it is initialised, but this package works around that as a special case (see step 1.).*

1. Launch Meteor using your settings file:

	``` sh
	meteor --settings settings.json
	```


Contributing
------------

Please send Issues and Pull Requests to <https://github.com/BudgieInWA/meteor-remote-ddp>.

Notes
-----  

- Based on [gwendall:remote-ddp](https://github.com/gwendall/meteor-remote-ddp).
- The author is not convinced that the `Mongo.Collection` support is bulletproof.
- Does not work in Cordova. To access a different server, use the `--mobile-server` flag instead.
