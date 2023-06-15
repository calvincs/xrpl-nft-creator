## Archived / No longer supported

# XRP Ledger Non Fungible Token Creator
 - Proof Of Concept NFT token builder for the XRP ledger
 - Not production ready, only an example for demonstration
 - XRP Ledger Testnet only
 - Please feel free to fork this, alter this, go build amazing things :-)

 - Watch Video Demo:  https://www.youtube.com/watch?v=0aNBpp-2R1w


## Build & Run

`npm install`

`node index.js`

 - Ensure you've configured the setup.yml
 - Follow along with the prompts
 - You can use Xumm w/ the QR codes to help add and send funds to your TEST wallets Ref Xumm for setup of Testnet
 - All interactions with the script, including QR codes, are logged to the creation.log file
 - The creation.log may contain secrets used during the build process!
 - You have the option of using IPFS, Pinata Cloud, WebHosting via S3/Spaces, Torrents.
 - The resulting hashes will be added to the XRP wallets Domain field


### input folder
  Place all the content you want to include in your NFT in this directory.
  - These folders will serve as the templates for your projects build
  - They should contain the following folders/files (See included examples) in your main project folder
   1. content  -> this is all the data you want to package
   2. make.yml -> this is the instructions used to make your package
   3. viewer.html -> this is the html template that's populated during the build
  
  - I removed bunny.mp4 & sintel.mp4 from the GitRepo due to size, check the readme.md in each project folder for the IPFS hash for download.

  This index.html file is generated base on the make.yml & view.html files
  
  It is recommended your viewer.html file be as generic as possible, as adding to many js libraries to your work may not work well in the future.
  
  As an example, browsers which support jQuery x.0.0 may not support jQuery x.0.0 in the future.  
  
  You should preview the index.html file before publishing, and the script allows you to do this, its a built-in step.
  
  - If you develop a fantastic template to show off your NFT, please let us see it! Share on Twitter and please tag me. I would love to see it!


### ouput folder
  Your generated content will be located in this folder.
  Some important notes here:
  1.  You will need to seed the Torrent after the build completes.  It is assumed your using IPFS as your primary seeding source.
  2.  If you need to re-distribute your IPFS data, remove the .torrent file from the output directory.  Then proceed to add the entire built folder into IPFS.  The hash SHOULD be exactly the same keeping it compatible with whats already been built/set in the XRP wallet.
  3.  If you want to use WebTorrents, you NEED to seed the Torrent via a compatible WRTC enabled client, like WebTorrent Desktop client.  You can validate the WebTorrent is working by testing the magnet url on https://instant.io.
  4.  Using an external pinning service will greatly improve the availability of your packaged content.
  5.  I recommend the use of DigitalOcean Spaces to helping ensure your content is easily accessible.
  6.  On first creation, your content may take some time to propagate!


### make.yml and setup.yml files
  The make.yml and setup.yml files are well documented with comments.
  
  Please validate all the settings in the yml files before generating your content.
  
  The script will ask you multiple times to validate the configured settings.

  - make.yml is located in your input project folder, for each project build
  - setup.yml is located in the main script folder, used for all project builds


### make.yml
 - settings.contentFolder : the project folder you want to package (default of 'content')
 - settings.templateFile : the file you want to use as an HTML template to build the index.html file (default viewer.html)
 - settings.tempateHtmlEscape : should we escape any html found in the make.yml configuration file? (default false)
 - settings.makeTorrent : should we create a .torrent package from the output content?  (default true)
 - settings.useIPFSWebSeed : if we build a torrent, should we include IPFS webseeds? (default true) 
 - settings.meta.webHostingURI : this is the BASE url were all your nft content will be located at: ex https://nft.xrpfs.com/buckbunny1617650420008/ is the contents NFT, and https://nft.xrpfs.com/ is the base url.
 - settings.meta.honorDynamicILPAddress : this tells the viewer of the meta.json code to honor the ILP address in the XRP wallet Domain field IF found over the preset ILP value, IF configured.
 - settings.meta.staticILPAddress : this is the payment pointer given during the build, that is included in the index.html page.
 - settings.meta.author {} : infomation about the author.
 - settings.meta.details {} : information on the packaged content.


### setup.yml
 - webbucket
    Allows user to upload NFT content to an online storage system (Amazon S3 / DigitalOcean Spaces)

    timeout : how long to wait before timeout of connection for uploads.  (default 10 minutes)

    disableSyncUpload: if you have a large file, the script will wait for the content to upload to ensure it completes before the end of the script.  If the file(s) are large, this can take some time.  You can make this activity Async by disabling the auto Sync nature of large file uploads.  (default false)

 -  pinatacloud
    Allows user to pin a hash on build creation to Pinata Cloud.  This can take some time to propagate, so I recommend local pinning to IPFS desktop to ensure remote pinning completes.

- system
    Generic system-related things. Allows you to exit the script after a set period of time.
    Enabled by default to exitEnabled: true and will exit the script after 30 minutes


### meta.json
  The meta.json file contains details linking the IPFS file contents to the NFT wallet and the creators/artists wallet.
  
  This is generated during the build process.
  
  Example output:
  ```json
{
    "webHostingURI": "nft.xrpfs.com",
    "honorDynamicILPAddress": true,
    "staticILPAddress": "$ilp.uphold.com/ZQ9a44qFAxLk",
    "author": {
        "wallet": "X7ART2fww9nxR1xWxM9WjQzY3j3C7eVaquLorx4aMio6UL8",
        "name": "Calvin",
        "email": "calvin [@] example [.] com",
        "twitter": "@calcs9 ",
        "website": "http://some.example.com/",
        "payId": "example$example.com",
        "bio": "Autodidact, driven by possibilities, passionate about Technology, Security, Personal Finance, Blockchain, Real Estate, Science\nDev: Python,JS,Go,Rust,Java,etc\nFind me on Twitter @calcs9"
    },
    "details": {
        "title": "Big Buck Bunny",
        "description": "When Big Bucks day gets turned upside down by the loss of his favorite butterflies via some rotten rodents, he takes to the offensive to avenge his friends. This is a short animated, comedic, and light-hearted movie that has stood the test of time.\nCode-named \"Project Peach\" by the Blender Institute, the film was made using a free and open-source software application called Blender.\n\nThis short film was released in 2008 under the Creative Commons Attribution 3.0 license.\n\nThis NFT is a distribution of that original work.  By releasing this work as an NFT, I hope to accomplish the following:\n1) Preserve the work of this media on a decentralized platform\n2) Bring awareness to XRPs ability to create NFTs on the ledger easily and efficiently\n3) Show the benefits of having an XRP wallet as the NFT vs a \"token\"\n4) Raise money for some great open source projects/foundations\n\nClick the above floating BigBuckBunny to watch a short film if you have an IPFS enabled browser.",
        "cover": "bunny.png",
        "link": "bunny.mp4",
        "legal": "The works contained in this package are protected by U.S. and International copyright laws\nCreative Commons Attribution 3.0 license\n(c) copyright 2008, Blender Foundation / www.bigbuckbunny.org",
        "NFTWalletAddress": "rPu3t9CND35sm2waACwKhABtAZhr9g3KW8",
        "NFTWalletXAddress": "XVkwcJoq3RzAP6jcNr6krmPJCHgTWjA4C4BZ4PmeQk7uN4p"
    },
    "hashes": [
        {
            "file": "/buckbunny1617650420008/bunny.mp4",
            "cid": "QmNT6isqrhH6LZWg8NeXQYTD9wPjJo2BHHzyezpf9BdHbD",
            "sha256": "20b80994904d40acbf6224024097a2ce5a1ea7130478e57162a38af1b876dfce"
        },
        {
            "file": "/buckbunny1617650420008/bunny.png",
            "cid": "QmRe6bYHv4XtsA8oXJeNSY6NqmDYa9Q3JBhUtZCEAC6yDQ",
            "sha256": "7ef51475fe83169530a16403a9941afde156fc87aa058a8500131a23de600f9a"
        }
    ],
    "created": 1617650420008,
    "framework": "https://github.com/calvincs/xrpl-nft-creator"
}
  ```


#### Why use an XRP wallet?
 Here are a few reasons I believe XRP wallets are an excellent choice for NFTs

 - Multiple people can control/own a single asset via MultiSign
 - Wallets can be easily transferred between users by updating the Regular Signers Key
 - Adding a pointer from the XRP wallet to a decentralized data store aka IPFS is straight forward
 - XRP + IPFS allows an easily traceable path of ownership of an NFT and the original creator/artist
 - While a Wallet does require a 20 XRP funding minimum, future TXs are relatively inexpensive as compared to some other solutions
 - Having access to the Wallet allows for exciting features that are difficult to implement in a Token alone.
    - Some examples:
        Wallets can sign data
        
        Wallets can receive and send payments.
        
        Wallets using Xumm can authenticate to other services ;-)
        
        Hooks?
        
        Xmpl.Cloud?
        

 # Enjoy
