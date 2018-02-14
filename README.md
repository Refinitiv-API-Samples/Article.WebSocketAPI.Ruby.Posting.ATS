# The Elektron WebSocket API Posting example with Ruby

## Overview

[Elektron WebSocket API](https://developers.thomsonreuters.com/websocket-api) enables easy integration into a multitude of client technology environments such as scripting and web.  This API runs directly on your TREP infrastructure or the Thomson Reuters platform and presents data in an open (JSON) readable format. The API supports all Thomson Reuters Elektron data models and can be integrated into multiple client technology standards e.g. JavaScript, Python, R, .Net etc.

This article covers how to implement the Elektron WebSocket client application to create, update market price data/field and delete ATS server contribution RIC via ADS 3.2 with Posting feature. 

The example application is implemented with Ruby language, but the main concept and JSON post message structures are the same for all technologies. 

## Prerequisite 
1. ADS server 3.2 with WebSocket connection and connects to ATS server
2. The ADS server 3.2 must contain the ATS fields definition in the RDMFieldDictionary file.
```
X_RIC_NAME                "RIC NAME"                    -1      NULL    ALPHANUMERIC    32  RMTES_STRING    32
```
3. [Ruby](https://www.ruby-lang.org/en/) compiler and runtime
4. Ruby [websocket-client-simple](https://rubygems.org/gems/websocket-client-simple) library 
5. Ruby [ipaddress](https://rubygems.org/gems/ipaddress) library 
6. Ruby [http](https://rubygems.org/gems/http) library 

## How to run this example application
1. Unzip or download the example project folder into a directory of your choice 
2. Install required Ruby libraries via the following commands
```
gem install websocket-client-simple
gem install ipaddress
gem install http
```
3. If you are using Windows, you can download Ruby Installer via [Ruby Installer](https://rubyinstaller.org/downloads/) web site. 
4. If you are using Windows, you need to install [MSYS2](http://www.msys2.org/) toolkit (bundled with Ruby Installer) development toolchain in order to install Ruby [http](https://rubygems.org/gems/http) library via the following steps
    - run the ```ridk install``` command in console
    - Select 1 **MSYS2 base installation** to install MSYS2 toolkit

    ![windows installation](images/msys2_2.png "install MSYS2 toolkit")
    - Then select 3 **MSYS2 and MINGW development toolchain** to install required development libraries. 

    ![windows installation](images/msys2_6.png "install MSYS2 development toolchain")

## How to run this example application
1. Unzip or download the example project folder into a directory of your choice 
2. Open command prompt and go to **&gt;project>&lt;src** folder and run the following command

```
$> ruby market_price_postapp.rb [--hostname hostname ] [--port WebSocket port] [--app_id appID] [--user user] [--action {{create, addfields, removefields, delete, update}}]
```

## Create ATS contribution RIC example JSON message
```
{
  "ID": 1, 
  "Type": "Post",
  "Domain": "MarketPrice",
  "Ack": true,
  "PostID": 1,
  "PostUserInfo": {
    "Address": "<Machine IP Address>",
    "UserID": <USER ID>
  },
  "Key": {
    "Name": "ATS_INSERT_S", # RIC name for create ATS server contribution RIC
    "Service": <ADS Service ID that connects to ATS server>
  },
  "Message": {
    "ID": 0,
    "Type": "Refresh",
    "Domain": "MarketPrice",
    "Fields": {
      "X_RIC_NAME": "<Contribution RIC name>",
      "BID": 12,
      "ASK": 15
    }
  }
}
```
## Update market price data to contribution RIC example
```
{
  "ID": 1,
  "Type": "Post",
  "Domain": "MarketPrice",
  "Ack": true,
  "PostID": 1,
  "PostUserInfo": {
    "Address": "<Machine IP Address>",
    "UserID": <USER ID>
  },
  "Key": {
    "Name": "<Contribution RIC name>",
    "Service": <ADS Service ID that connects to ATS server>
  },
  "Message": {
    "ID": 0,
    "Type": "Update",
    "Domain": "MarketPrice",
    "Fields": {
      "BID": 43,
      "ASK": 46
    }
  }
}
```
## Implementation Detail

Please see [Implementation Note file](./note.md) for more detail.

## References
For further details, please check out the following resources:
* [Elektron WebSocket API](https://developers.thomsonreuters.com/websocket-api) page on the [Thomson Reuters Developer Community](https://developers.thomsonreuters.com/) web site.
* [Developer Webinar Recording: Introduction to Electron Websocket API](https://www.youtube.com/watch?v=CDKWMsIQfaw)
* [WebSocket technology](https://www.websocket.org/index.html) web site.

For any question related to this article or Elektron WebSocket API page, please use the Developer Community [Q&A Forum](https://community.developers.thomsonreuters.com/).