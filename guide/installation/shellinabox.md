---
title: ShellInABox- Terminal In Browser
description: Quick setup for shell in a box
published: true
date: 2021-10-09T16:13:21.620Z
tags: browser, terminal
editor: markdown
dateCreated: 2021-10-09T16:12:59.858Z
---

# Installation

## Ubuntu
* Package installation
`sudo apt install shellinabox openssl ca-certificates`

* Run instance

|Start service on default port | Or, start service on specific port |
|:---:|:---:|
| `sudo service shellinaboxd start` | `shellinaboxd -p 6318 &` |


# Configuration

## Ubuntu

### Customization

* Default config update 
  `$ sudo vi /etc/default/shellinabox`
    ```
    # TCP port that shellinboxd's webserver listens on
    SHELLINABOX_PORT=6175

    # specify the IP address of a destination SSH server
    SHELLINABOX_ARGS="--o-beep -s /:SSH:172.16.25.125"

    # if you want to restrict access to shellinaboxd from localhost only
    SHELLINABOX_ARGS="--o-beep -s /:SSH:172.16.25.125 --localhost-only"
    ```

* Css file add on with no hangup
  1. Create file `white-on-black.css`.
     ```
    	#vt100 #cursor.bright {
        background-color: white;
        color:            black;
      }
      
      #vt100 #cursor.dim {
        background-color: black;
        opacity:          0.2;
        -moz-opacity:     0.2;
        filter:           alpha(opacity=20);
      }
      
      #vt100 #scrollable {
        color:            #ffffff;
        background-color: #000000;
      }
      
      #vt100 #scrollable.inverted {
        color:            #000000;
        background-color: #ffffff;
      }
      
      #vt100 .ansiDef {
        color:            #ffffff;
      }
      
      #vt100 .ansiDefR {
        color:            #000000;
      }
      
      #vt100 .bgAnsiDef {
        background-color: #000000;
      }
      
      #vt100 .bgAnsiDefR {
        background-color: #ffffff;
      }
      
      #vt100 #scrollable.inverted .ansiDef {
        color:            #000000;
      }
      
      #vt100 #scrollable.inverted .ansiDefR {
        color:            #ffffff;
      }
      
      #vt100 #scrollable.inverted .bgAnsiDef {
        background-color: #ffffff;
      }
      
      #vt100 #scrollable.inverted .bgAnsiDefR {
        background-color: #000000;
      }
    	```
  1. Restart service with new file.
  	`nohup shellinaboxd -p 6318 --user-css Normal:+white-on-black.css &`

---