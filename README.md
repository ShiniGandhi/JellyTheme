# JellyTheme
### A heavily modified theme for Jellyfin with a very original name /s.

This is a theme based on [JellyFlix](https://github.com/prayag17/JellyFlix), which is a Netflix-style theme for Jellyfin, so obviously credit to **prayag17** for providing the base for this theme. </br>Most changes can be made by just importing my CSS files, but things like moving the cast to be before the season list requires modification to some JavaScript files.

The theme is optimized for 1080p, but it should work well on 720p, 768p, 1440p and 4K. </br>
1440p might be okay, but for best results zoom 125% should be used.</br>
4K is needs to be at 125% or 150% zoom. </br>
I'm still looking into solutions for that.

## Installation Instuctions - Basic
#### NOTE - BEFORE INSTALLING
Any `@import` line that you add to your CSS **must** be at the very top of your custom CSS. otherwise the file will not be imported.

#### Theme Versions
Since this is my personal theme, it might change however I see fit. If you don't want these changes to affect you, please use the CSS files in the `static` directory, rather than `latest`.</br> All fixes will be applied to both, but changes to how the interface looks will only be made to the files under `latest`.

### Required
Put these at the top of your custom CSS:
```
@import url("https://cdn.jsdelivr.net/gh/ShiniGandhi/JellyTheme@latest/latest/JellyTheme.css");
:root {
--accent:<COLOR>!important;
}
```
**Change `<COLOR>` to an actual color before pasting, otherwise you'll have no accent color.**
If you want a slightly cleaner UI, with no backdrop in the main menu and a few more things, use `JellyTheme-Cleaner.css` rather than `JellyTheme.css`.

If you don't use video backdrops, add this line to display a poster on mobile:
```
.layout-mobile .primaryImageWrapper > img {
display:block!important;
}
```

### Optional
These must be added **before** the `:root {` line to work. </br>

#### Cleaner UI
If you want to have a cleaner UI, add this:</br>
The following is removed: </br>
 - Play trailer button </br>
 - Rotten tomatoes rating </br>
 - User icon </br>
 - Cast button (still displayed on mobile) </br>
 - Display and Home Preferences in User Settings
```
@import url("https://cdn.jsdelivr.net/gh/ShiniGandhi/JellyTheme@latest/latest/Cleaner-UI.css");
```

#### Resize Some Elements

If you want Continue Watching, Next Up and the list of seasons to be smaller, as shown in my screenshots, import this:</br>
```
@import url("https://cdn.jsdelivr.net/gh/ShiniGandhi/JellyTheme@latest/latest/Resize-Cards.css");
```
**Keep in mind that for this to work your home screen order must be as follow:**
* Section 1: My Media
* Section 2: Continue Watching
* Section 3 and under: Irrelevant


#### Right-to-Left Support

If your server's metadata is in Hebrew, Arabic (or any other language that is written right-to-left, import this:</br>
```
@import url("https://cdn.jsdelivr.net/gh/ShiniGandhi/JellyTheme@latest/latest/RTL-Fix.css");
```

#### Revamped video player

If you want the revamped video player, optimized for most screen resolutions and scales, (screenshot below), import this:</br>
```
@import url("https://cdn.jsdelivr.net/gh/ShiniGandhi/JellyTheme@latest/latest/PlayerRevamp.css");
```
![](/screenshots/PlayerRevamp.png)

#### Trimmed Quality Section

If you want to have less bitrate options (screenshot below), import this:</br>
```
@import url("https://cdn.jsdelivr.net/gh/ShiniGandhi/JellyTheme@latest/latest/TrimmedQualitySection.css");
```
![](/screenshots/TrimmedQualitySection.png)
</br><b>NOTE: This removes every bitrate over 8Mbps and changes the names of everything as shown in the screenshot. Use this only if you're sure that's what you want.</b>

#### Slim Active Devices

If you want slimmer Active Devices entries like here (At the moment this ~~only looks good in 1080p~~ looks great in 4K and 1440p, but not perfect in 1080p (how the turntables huh), still working on scaling it), Import this: </br>
![ ](/screenshots/Slim-ActiveDevices.png)</br>
```
@import url("https://cdn.jsdelivr.net/gh/ShiniGandhi/JellyTheme@latest/latest/Slim-ActiveDevices.css");
``` 
</br>
NOTE: The logo will be pretty low resolution because it's generating a low resolution image to begin with. If you want better quality logos, perform the following:</br>

1. Open your `dashboard-dashboard.********************.bundle.js` file (asterisks are replaced with something specific to your instance, but this never changes after initial setup).
2. Find `tag:a.ParentLogoImageTag` and set the values of `maxHeight` and `maxWidth` to `500`.
3. Clear browser cache.</br>

## Installation Instuctions - Advanced Extras
These require modifying some of the JavaScript files that Jellyfin generates. They will be different for every instance, and probably with different names, so make sure you back up these files before making any changes. </br>
These work best if you're running Jellyfin inside a Docker container, so you can make sure the files won't get overwritten (which can cause issues if something major changes in Jellyfin). </br>
All files related to this section are located in `/usr/share/jellyfin/web/` if using a Docker container. I'm not sure where they are if using other types of installations.

**NOTE: If using a Docker container, you must copy these files to your filesystem and then add them as "read-only volumes" in your container configuration**</br>
Example in a docker-compose file:
```
    volumes:
      - ./custom/main.********************.bundle.js:/usr/share/jellyfin/web/main.********************.bundle.js:ro
      - ./custom/itemDetails-index-html.********************.bundle.js:/usr/share/jellyfin/web/itemDetails-index-html.********************.bundle.js:ro
```
Keep in mind that if the file is not read-only Jellyfin might overwrite it at some point, which is why I suggest using Docker.


#### Force Backdrops
1. Open your `main.********************.bundle.js` file (asterisks are replaced with something specific to your instance, but this never changes after initial setup).
2. Find `enableBackdrops:function() {return _}` and change the `_` to `x`.
3. Clear browser cahce.

#### Force Video Backdrops
Before you do this, you **must** have a directory called `backdrops` with a video file in every movie or show you want to have a backdrop, otherwise Jellyfin won't know what to play.
1. Open your `main.********************.bundle.js` file (asterisks are replaced with something specific to your instance, but this never changes after initial setup).
2. Find `enableThemeVideos:function(){return _}` and change the `_` to 'x'.
3. Clear browser cache.

#### Cast List Position
1. Open your `itemDetails-index-html.********************.bundle.js` file (asterisks are replaced with something specific to your instance, but this never changes after initial setup).
2. Find the following line:
```
<div id="castCollapsible" class="verticalSection detailVerticalSection hide"> <h2 id="peopleHeader" class="sectionTitle sectionTitle-cards padded-right">${HeaderCastAndCrew}</h2> <div is="emby-scroller" class="padded-top-focusscale padded-bottom-focusscale" data-centerfocus="true"> <div id="castContent" is="emby-itemscontainer" class="scrollSlider focuscontainer-x itemsContainer"></div> </div> </div>
```
4. Cut it from the file and paste it before `<div id="childrenCollapsible" class="hide verticalSection`.
5. Add the following code to your CSS:
```
.layout-desktop div#castCollapsible {
margin-bottom:6em;
margin-top:-22vh;
width:68vw;
}

.layout-desktop div#childrenCollapsible {
margin-top:4em;
}

.layout-tv div#castCollapsible {
margin-top:-22vh;
width:68vw;
}
```
7. Clear browser cache.


#### Hide Details While Watching Backdrop
If you want item details to hide after a certain amount of time while watching a video backdrop as shown below, do the following:</br>
![ ](/screenshots/IdleHide.png)</br>
1. Open your `itemDetails-index-html.********************.bundle.js` file (asterisks are replaced with something specific to your instance, but this never changes after initial setup).
2. Add the code from lines 10 to 21 located in [IdleHIde.css](https://github.com/ShiniGandhi/JellyTheme/blob/main/latest/IdleHide.css)
3. Set `idle`to your preferred time in milliseconds (20 seconds by default)
4. import the following to your custom CSS:
```
@import url("https://cdn.jsdelivr.net/gh/ShiniGandhi/JellyTheme@latest/latest/IdleHide.css");
```
5. Clear browser cache.

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
