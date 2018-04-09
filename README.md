# DwebTransports
General transport library for Decentralized Web handles multiple underlying transports.

## Background
This library is part of a general project at the Internet Archive (archive.org) 
to support the decentralized web.  

###Goals
* to allow a single API that can be used for most basic interactions with 
decentralized transports. 
* to support multiple URLs, on different transports, so that the (current) underlying unreliability
 is hidden. 

### Node Installation
* Clone this repo. 
* Until this is in npm, add the line
`"dweb-transports": "git+https://git@github.com/mitra42/dweb-transports.git",`
to your package.json file in the dependencies section. 
* (TODO Note location above will change to an internetarchive repo)
* `npm install dweb-transports`  will install the dependencies including IPFS & WebTorrent

`const DwebTransports = require(dweb-transport)` will add all Transports to a Javascript file.
* TODO writeup how to require only some of the transports.
* Then see usage API below

### Installation and usage in the Browser
* TODO installation of dev dependencies
* Install npm & node
* Clone this repo and cd to it.
* `npm bundle` will create dist/dweb_transports_bundle.js
* Add `<SCRIPT type="text/javascript" src="dweb_transports_bundle.js"></SCRIPT>` to your `<HEAD>`

Then code like this should work. 

```
async function main(url) {
    try {
        // and if not found will use the defaulttransports specified here.
        await DwebTransports.p_connect({
            statuselement: document.getElementById("statuselement"),    // Where to build status indicator
            defaulttransports: ["HTTP","IPFS"],                         // Default transports if not specified
            transports: searchparams.getAll("transport")    // Allow override default from URL parameters
        }, verbose);                                        // Pass verbose global parameter from command line
        // Any code you want to run after connected to transports goes here.
    } catch(err) {
        console.log("App Error:", err);
        alert(err.message);
    }
}
var searchparams = new URL(window.location.href).searchParams;
// Allow specifying ?verbose=true in URL to get debugging, and transport=HTTP etc
var verbose = searchparams.get("verbose") || false;
```

See [example_block.html](./example_block.html) for an example of connecting, storing and retrieving.


