# Status: Planning
# jQuery MediaStreamPlayer Plugin

Open source jQuery plugin for the continuous slideshow of media (videos, photos, live streams, etc.)  
with pluggable media modules including: youtube, vimeo, 

Other projects implement plugins for playing media streams such as:
instagram, flickr, facebook-photo, ustream.

## Features
* fills specified DOM element
* supports resize
* Auto adjust to DOM element size when DOM element resizes
* Pluggable media players eventually including:
	* youtube
	* vimeo
	* dailymotion
	* instagram
	* flickr
	* facebook - photo
	* PluggableMediaPlayers - Additional Media players can be developed in separate projects 
* No player Chrome - the plugin does not create any chrome of it’s own and players disable other site chrome in so far as possible

## Getting Started

Download the [production version][min] or the [development version][max] of jQuery.MediaStreamPlayer.

[min]: https://raw.github.com/VorskiImagineering/jQuery-MediaStreamPlayer-Plugin/master/dist/jquery.mediastreamplayer.min.js
[max]: https://raw.github.com/VorskiImagineering/jQuery-MediaStreamPlayer-Plugin/master/dist/jquery.mediastreamplayer.js

In the browser:

```
<script src="http://code.jquery.com/jquery.js"></script>
<script src="jquery.mediastreamplayer.min.js"></script>
<script src="jquery.mediastreamplayer.vimeo.min.js"></script>
<script>
	/* Create a media stream. The RandomMediaStream just returns the items
	it was passed in, in random order forever. */
	var mediaStream = new RandomMediaStream([new YouTubeMediaItem(“id1”), new VimeoMediaItem(“id2”)]);

    $('player').mediastreamplayer(mediastream)
</script>
```
## YouTube MediaPlayer Plugin
The YouTube media player allows you to create media 


## Demo
We've got a handy demo up at http://vorski.com/MediaStreamPlayer/


## Contributing
This project generally follows [Idiomatic.js](https://github.com/rwldrn/idiomatic.js) from Rick Waldron, take care to maintain the existing coding style. 

## Release History

* 2012/12/21 - v0.0.1 - Planning begins.

## License
Copyright (c) 2012 Vorski Imagineering  
Licensed under the LGPL license http://www.gnu.org/licenses/lgpl-3.0.txt

## Dependencies...

jQuery... 


## Authors

* [Andrey Lebedev](http://github.com/alebedev80)
* [Victor Vorski](http://github.com/vvorski)
