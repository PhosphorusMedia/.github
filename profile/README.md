# PhosphorusMedia

Phosphorus aims to be a multi-interface tool for streaming and downloading music from varius sources. This project took inspiration
from [Nuclear](https://github.com/nukeop/nuclear), a project that already offers all the functionalities that Phosphorus should provide, but
suffers from a heavy user experience and an excessively high response time.

Phosphorus is currently very far away from being a usable product, but [phosphorus_cli](https://github.com/PhosphorusMedia/phosphorus_cli)
already provides a primitive and experimental terminal-based interface that allows streaming and downloading content from Youtube. In fact,
right now, the only supported source is Youtube, through the [youtube_dl](https://youtube-dl.org/) tool. On the ```better_ui``` branch, a
better and more complete UI is being implemented, but neither streaming not download are available, for now.

## Project code organization
Phosphorus code is organized into 3 repositories:
* `phosphorus_core`: a repository in which all components agnostic to a particolar application or UI implementation reside. In here there are implementations for `plugin_manager`, `playlist_manager` and similar core components;
* `plugins`: in this repository simply contains the implementation of plugins. A plugin is a component responsible for accessing and retrieving content from a particular source (e.g. YouTube);
* `phosphorus_cli`: an TUI application that allows using Phosphorus components in an easy-way;

### `phosphorus_core`
Within this repository one finds the following structures:
* `Song`: a song is made of a raw part and a meta part. The first is the actual data content, so the song one can listen to. The meta part instead has decorative information like song name, artist, duration and so on;
* `QueueManager`: this is just a struct that allows managing a reproduction queue. Nothing less, nothing more
* `PlaylistManager`: as one could easily expect this struct allows handling multiple playlists, so creating and deleting them and adding or removing songs from them. However, a `PlaylistManager` is also responsible for loading and saving song and playlist meta information from and into the disk. These are represented as JSON files;
* `PluginManager`: the `PluginManager` is maybe the single most important component in Phosphorus. It's responsible for forwarding requests to the plugins and retrieving from them a response. Plugins must be registered with the PluginManager to be used.
