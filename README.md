# MMM-Sonos

<p>
<a href="https://github.com/jishi/node-sonos-http-api"><img src="https://img.shields.io/badge/Sonos-API-orange.svg" alt="API"></a>
<a href="http://choosealicense.com/licenses/mit"><img src="https://img.shields.io/badge/license-MIT-blue.svg" alt="License"></a>
</p>

This is an adaption and modification of of [Vaggan's](https://github.com/Vaggan) [MagicMirror-SonosModule](https://github.com/Vaggan/MagicMirror-SonosModule) and [CFenner's](https://github.com/CFenner) [MagicMirror-SonosModule](https://github.com/CFenner/MagicMirror-Sonos-Module). It was modified to get some enhancements in visualisation an configuration. Also the module hides itself when not playing now.

Note from Snille: I'm new to the MagicMirror world and Node.js, this is my first attempt to modify a module. There are probably lot's of things that could have been done better. :)

When starting the Mirror:

![Sonos Module Loading](https://github.com/Snille/MMM-Sonos/blob/master/.github/Sonos-Loading.png)

Module on the Left side of the Mirror:

![Sonos Module Left](https://github.com/Snille/MMM-Sonos/blob/master/.github/Sonos-Left.png)

Module in the Center of the Mirror:

![Sonos Module Center](https://github.com/Snille/MMM-Sonos/blob/master/.github/Sonos-Center.png)

Module on the Right side of the Mirror:

![Sonos Module Right](https://github.com/Snille/MMM-Sonos/blob/master/.github/Sonos-Right.png)

This is my own mirrors view (Top Center) using some addition in the custom.css [see below](#custom-css)

![Sonos Module Custom CSS](https://github.com/Snille/MMM-Sonos/blob/master/.github/Sonos-Custom-CSS.png)


## Usage

_Prerequisites_

- requires MagicMirror v2.0.0
- install and [run](https://github.com/MichMich/MagicMirror/wiki/Auto-Starting-MagicMirror) [node-sonos-http-api](https://github.com/jishi/node-sonos-http-api)

### Installation

In your terminal, go to your MagicMirror's Module folder:

```
cd ~/MagicMirror/modules
```

Clone this repository:

```
git clone https://github.com/Snille/MMM-Sonos.git
```

Add some [config entries](#configuration) to your config.js file. After that the content will be added to your mirror.

### Configuration

To run the module properly, you need to add the following data to your config.js file.

```
{
	module: 'MMM-Sonos',
	header: "Playing on SONOS",
	position: "top_center", // Any of the zones on the mirror.
	classes: "default everyone",
	config: {
		// Configuration options below goes in here...
	}
}
```

Here are the options to configure the module.

| Option | Description |
|---|---| 
|`showStoppedRoom`|Trigger the visualization of stopped rooms.<br><br>**Default value:** `true`|
|`showAlbumArt`|Trigger the visualization of the album art.<br><br>**Default value:** `true`|
|`showRoomName`|Trigger the visualization of the room name.<br><br>**Default value:** `true`|
|`preRoomText`|Text to be displayed before the zone name.<br><br>**Default value:** `Zone: `|
|`preArtistText`|Text to be displayed before the artist name.<br><br>**Default value:** `Artist: `|
|`preTrackText`|Text to be displayed before the track name.<br><br>**Default value:** `Track: `|
|`preTypeText`|Text to be displayed before the source name.<br><br>**Default value:** `Source: `|
|`animationSpeed`|Lenght of the fade animation.<br><br>**Default value:** `1000`|
|`updateInterval`|Update interval.<br><br>**Default value:** `0.5`|
|`apiBase`|http link to the SONOS API.<br><br>**Default value:** `http://localhost'`|
|`apiPort`|SONOS API port.<br><br>**Default value:** `5005`|
|`apiEndpoint`|Link to the "zones" information on the SONOS API.<br><br>**Default value:** `zones`|
|`exclude`|Zones names to exclude ["Secret-Room","Greenhouse"].<br><br>**Default value:** `[]`|

### Custom-CSS

Here is my CSS settings for the module that I have added to my custom.css to give it the exta special look. :)

```
/* Sonos --------------------------------------------*/
.sonos ul .type {
    font-size: 12px;
	padding: 0px 0px;
	line-height: 12px;
	width: 260px;
}
.sonos ul .room {
    font-size: 16px;
	padding: 0px 0px;
	line-height: 16px;
	width: 260px;
}
.sonos ul .song {
	padding: 0px 0px;
	position: relative;
}
.sonos ul .art img {
    height: 60px;
    width: 60px;
	border-radius: 50%;
	margin: 0px 0px;
	border: 2px solid #FFF;
}
.sonos ul .name {
    width: 200px;
    font-size: 16px;
	padding: 0px 4px;
	line-height: 16px;
}
/*****************************************************/
```

### Known Issues

The module may not be able to access the data of the sonos API due to a Cross-Origin Resource Sharing (CORS) issue. This could be solved by adding the following lines to the `sonos-http-api.js` just before `res.write(new Buffer(jsonResponse));` in the sonos api. Remember to restart the service after the change.

```
  res.setHeader("Access-Control-Allow-Origin", "http://localhost");
  res.setHeader("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
```
