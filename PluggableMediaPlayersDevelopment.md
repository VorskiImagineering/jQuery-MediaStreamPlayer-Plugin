### Status: Planning
# Developing MediaPlayer plugins for the MediaStreamPlayer


## MediaPlayer

A media player just knows how to take an ID of a video and plays it into the DOM.

* URL translation&munging is not done in the player, so the player needs to get a well formatted ID of a video


## PlayerFactory
This is just a simple class which creates a MediaPlayer on demand.

## Plugin
- plugin registers a player factory for a media type it knows about
