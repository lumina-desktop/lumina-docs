#Lumina Style 

###A similar style to trueos_style with some unique theming for Lumina.

**In order to use the lumina_style theme, there are some adjustments to make to the _src-qt/docs/conf.py_ file:**

* Revise this value from 'classic' or something else, to 'lumina_style' prior to generating docs:
```
  html_theme = 'lumina_style'
```
* Comment out any html_options lines as the options don't exist and/or aren't used right now:
```
   #    "stickysidebar": "true",
   #    "rightsidebar": "false",
   #    "sidebarwidth" : "240",
   #    "headbgcolor" : "#fff",
   #    "relbarbgcolor" : "#696969",
   #    "sidebarbgcolor" : "#696969",
   #    "bgcolor" : "#fff"
```
* Add or adjust this statement below to match, it is for _additional_ places to search:
```
  html_theme_path = ['themes']
```
#Adjusted for Lumina with theme changes and added guilabel directive support.
