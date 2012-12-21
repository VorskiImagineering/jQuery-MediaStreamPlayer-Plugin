### Status: Planning
# jQuery MediaStreamPlayer Plugin implementation architecture

## Overview

The basic idea is very simple. The MediaStreamPlayer calls next() on a MediaStream getting items to be played.
For each item it uses a MediaPlayer to display the videos. In order to create a smooth viewing experience 
transitions are used when switching between players. 

## Questions
* what about handling of resizing? 

## Classes

### interface MediaStream
Returns an endless stream of MediaItems... Could also have some sort of a push
registration mechanism so it can push items to the MediaStreamPlayer?

### class MediaStreamPlayer

The main class, it does a slideshow of MediaPlayers based on the MediaStream it gets...

Pre-loads players 
Uses a MediaPlayerPool to re-use MediaPlayers as much as possible.
 
### interface MediaItem
A MediaItem interface some set of media, could be one video, could be a set of photos, could be a live video stream. Only useful if there is a MediaPlayer which knows how to play this MediaItem.

### interface MediaPlayer
Knows how to play a MediaItem into a DOM element.

A specific implementation of this exists for each video (photo, etc.) site we support.

### interface Transition

Does a transition between two MediaPlayers

### class SlideTransition

### class FadeTransition

MediaPlayerPool
 Manages a pool of MediaPlayers, up to two per media type. Automatically creates MediaPlayers if there are not sufficient ones.

Question: how do we manage this? do we require an explicit returnPlayer() to return the player to be available? Or for the first implementation do we just go with two players always returned in order 1,2,1,2...

### class RandomMediaStream

A helper class, takes an array of MediaItems and returns them in random order forever, however making sure that the same item is never played twice in a row. 

### class LoopMediaStream

A helper class, takes an array of MediaItems and returns them in order forever, looping around to start when it gets to the end.

### class CrossMediaStream

A helper class, **composition of multiple media streams**, takes a set of MediaStreams and returns MediaItems from them in random order.


### class YouTubeMediaItem

A  media item implementation for youtube.

### class YouTubeMediaPlayer

A player for YouTube movies.


## Implementation ideas.

```
/* A Media stream is an endless iterator over MediaItems. 

Note that a MediaStream is endless, next() always returns
a valid item. 
*/
MediaStream {
/* Returns the next MediaItem in the stream.*/
	function next();
}

/*
	Allows registering a player factory for a certain media item type
*/
RegisterPlayerFactory(MediaItemType, PlayerFactory) 

Just use new PlayerFactory(‘youtube’)

VV: Does this code make sense in Javascript? How do you do the factory pattern in Javascript?
AL: Look  http://www.joezimjs.com/javascript/javascript-design-patterns-factory/

/* Factory MediaPlayer instances */
PlayerFactory(ItemType) class:

properties:
	/* List of allowed players */
MediaItemTypes Enum: 
	
methods:
/* creates a instance of media player related to item type. */ 
	createPlayer(ItemType): MediaPlayer:

events:
	/* Event on create media player */
	onCreate(MediaPlayer) 


/*  A MediaItem models some set of media, could be one video, could be a set of photos, could be a live video stream. Only useful if there is a MediaPlayer which knows how to play this MediaItem. */

MediaItem extend Backbone.Models {

/* Type of media item */
var mediaType = ‘’;

/* Duration in seconds, 0 - static item (photo), -1 - stream item. */
var duration = 0;

/* Source url /*
var src =’’;

/* Media title */
	var title = ‘’;

	/* Media description */
	var description = ‘’;

	/* Validator required properties and theirs types */
	function validator() {}
}

	
 
	
/* 
This is the class which does the work of playing a MediaItem onto the screen by the MediaItemList. What doing this actually involves depends completely on the MediaItem in question. 

MediaPlayers are developed for each type of source media site we work with.

*/

MediaPlayer interface extend Backbone: {
	/* Constructor, the MediaPlayer is passed the DOM element
it should bind itself into.

Question: how will resizing work? The MediaPlayer should auto-resize to the DOM element?
*/
	function init(domelement) {}

/* Loads media item into the player. 

Video does not start playing until the play() method is called.

If an MediaItem is already being played it is dropped and the loading process begins.

When loading is completed XXXX event is launched.

If loading fails -- event???
*/
	function load(MediaItem) {}

/* Plays the currently loaded MediaItem. 

If no item loaded - ???

If item not yet ready - queue the play request?

*/
	function play() {}

	/* Media type served movies by that player */
var mediaType = ‘’;

	/* Player mode */
var mode = array(‘on-screen’,  ‘off-screen’)
	/* Volume value */
	var volume = 70;
	/* Is muted? */
	var muted = false;
	/* Is paused? */
	var paused = false;
	/* Is ended? */
	var ended = false;
	/* currentTime */
	var currentTime;
	/* link to playing MediaItem object */
	var item = {MediaItem object};

	/* Player controls settings */
		var controls = {‘hide’: ‘all’, ‘mouse’: 0, ‘keyboard’: 0};

	/* Get currentTime property value */
	function getCurrentTime() {}

	/* Set muted property value */ 
	function setMute() {}
	/* Get muted property value */ 
	function getMute() {}

	/* Set volume property value */ 
	function setVolume(0...100) {}
	/* Get volume property value */
	function getVolume() {}

	/* Get mode property value 

	What’s the mode?
*/
	function getMode() {}
	/* Get mode property value */
	function setMode() {}

	/* Get paused property value */
	function getPaused() {}

	/* Get ended property value */
	function getEnded() {}

	/* Set controls property value */
	function setControls() {}

Events:
loadeddata - Movie loaded and ready for play
	progress - Movie loading
	canplay - Movie can be played
	play - On start play movie
	playing - On movie playing
	pause - On pause
	ended - On movie end
	volumechange - On volume change
}

/* A pool of MediaPlayers. 

Question: how do we manage this? do we require an explicit returnPlayer() to return the player to be available? Or for the first implementation do we just go with two 
*/
MediaPlayerPool {

	/* Return true if player registered for media type,
otherwise - false 
*/
	function getPlayer(MediaType) {}
}

/* 
Plays the videos from a MediaStream one by one using MediaPlayers.
Manages a pool of MediaPlayers for different media types it encounters. 
*/

MediaStreamPlayer extend Backbone.View:

properties:

	/* media list on items */
	itemsList: MediaItemsCollection

	playerPool: PlayersPool

		/* Mute property */	
	mute:
	/* Volume level 0 - 100, default 70 */
	volume: 70
	/* Player mode */
	mode
	/* Debug mode. */
	debug: false
	/ Items views counter */
	views: integer

methods:
	/* Start playing media items from position in media stream (0 - first item in the sream)
	start(position = 0): null;
	/*  Play next media item by related player*/
	next(): null

	/*Factory method create player’s instance 
	default options from player settings: {mute, volume, mode}
*/
getPlayer(MediaItem [,options]): MediaPlayer
	mute() - allows muting the sound (ensures all the players it creates are also muted)
	unMute() - restores to volume level before mute
	getMute() - boolean mute setting
	setVolume(0...1) - allows setting the volume (all players it creates are also muted)
	getVolume() - returns the current volume setting
events:
	onStart();
	onNext()
	onTime()
/* If player return error we should make some action, ex.: delete problem item from collection and go to the next it */
	onError(errorType) - 
	
```

## Debugging
For debugging use something like this backbone.debug.js