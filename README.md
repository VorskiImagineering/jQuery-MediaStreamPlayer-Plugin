# Status: Planning
# jQuery MediaStreamPlayer Plugin

Open source jQuery plugin for the continuous slideshow of media (videos, photos, live streams, etc.)  
with pluggable media modules including: youtube, vimeo, 

Other projects implement plugins for playing media streams such as:
instagram, flickr, facebook-photo, ustream.


## Demo
We've got a handy demo up at http://vorski.com/MediaStreamPlayer/

## Getting Started
Download "Cowboy" Ben Alman's [JavaScript Linkify - v0.3](https://raw.github.com/cowboy/javascript-linkify/master/ba-linkify.min.js).

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

## Contributing
This project generally follows [Idiomatic.js](https://github.com/rwldrn/idiomatic.js) from Rick Waldron, take care to maintain the existing coding style. 

## Release History

* 2012/12/21 - v0.0.1 - Planning begins.

## License
Copyright (c) 2012 Vorski Imagineering  
Licensed under the LGPL license http://www.gnu.org/licenses/lgpl-3.0.txt

## Dependencies...

jQuery... 

This project is built with "Cowboy" Ben Alman's [Grunt](https://github.com/cowboy/grunt).

## Authors

* [Andrey Lebedev](http://github.com/alebedev80)
* [Victor Vorski](http://github.com/vvorski)
