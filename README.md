# JellyTheme
#### A heavily modified theme for Jellyfin with a very original name /s.

This is a theme based on [JellyFlix](https://github.com/prayag17/JellyFlix), which is a Netflix-style theme for Jellyfin, so obviously credit to prayag17 for giving me the base for this theme. </br>Most changes can be made by just importing my CSS files, but things like moving the cast to be before the season list requires modification to some JavaScript files.

## Installation Instuctions - Basic
#### NOTE - BEFORE INSTALLING
Any `@import` line that you add to your CSS **must** be at the very top of your custom CSS. otherwise the file will not be imported.
### Required
Put these at the top of your custom CSS:
```
@import url("https://cdn.jsdelivr.net/gh/ShiniGandhi/JellyTheme@master/latest/JellyTheme.css");
:root {
--accent:<COLOR>!important;
}
```
**Change `<COLOR>` to an actual color before pasting, otherwise you'll have no accent color.**
### Optional
These must be added **before** the `:root {` line to work. </br>
If you want to have a cleaner UI (less options in user settings, buttons on the top bar, etc. add this as well: </br>
Feel free to look at the file to see exactly what it hides.</br>
```
@import url("https://cdn.jsdelivr.net/gh/ShiniGandhi/JellyTheme@master/latest/Cleaner-UI.css");
```
If you want Continue Watching, Next Up and the list of seasons to be smaller, as shown in my screenshots, import this:</br>
```
@import url("https://cdn.jsdelivr.net/gh/ShiniGandhi/JellyTheme@master/latest/Resize-Cards.css");
```
If your server's metadata is in Hebrew, Arabic (or any other language that is written right-to-left, import this:</br>
```
@import url("https://cdn.jsdelivr.net/gh/ShiniGandhi/JellyTheme@master/latest/RTL-Fix.css");
```

## Installation Instuctions - Advanced Extras
These require modifying some of the JavaScript files that Jellyfin generates. They will be different for every instance, and probably with different names, so make sure you back up these files before making any changes.

**TBD**


## Screenshots
#### Main page, with resized cards (optional)
![](/screenshots/Index-Resized-Cards.png)
#### Main page, no resized cards
![](/screenshots/Index.png)
#### Movie page with a single version and no trailer playing
![](/screenshots/Movie-No-Trailer_Single-Version.png)
#### Movie page with multiple versions and a trailer playing
![](/screenshots/Movie-Trailer-and-Versions.png)
#### TV show page
![](/screenshots/Show.png)
#### TV show - compact seasons list (optional)
![](/screenshots/Season-List-Compact.png)
#### TV show - episodes in season
![](/screenshots/Season.png)
#### TV show - episode entry
![](/screenshots/Episode.png)
#### Cleaner user settings (optional)
![](/screenshots/User-Settings.png)
