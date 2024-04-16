# Overlay for displaying current song name and artist

This overlay supports horizontal scrolling for long song names. It's setup to automatically refresh every 10 seconds, so it might take a few seconds after starting/finishing song for it to appear.

![overlay](image.png)

## Installation

1. Copy the contents of `SongNameOverlay/resources` folder from this repository into the `Ragnarock` folder in your Streamer.bot folder (create it if it doesn't exist there).
    
    ![ragnarock folder](ragnarock_folder.png)
2. Import `RagnarockSongNameOverlay.bot` into Streamer.bot to add the actions necessary to update the overlay.
![alt text](import.png)
3. In OBS, create a new Browser source for the `Ragnarock/ragnarock_overlay.html` local file in your Streamer.bot installation folder, with `400` width, `200` height. You can set it to refresh browser when scene becomes active as well.
![obs source](obs.png)