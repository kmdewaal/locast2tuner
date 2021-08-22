# Remapping
In case you override multiple zip codes, Emby and Plex will sort channels by channel number, which means channels from different locations might be intermingled. In order circumvent this, you can remap channels.  `locast2tuner` offers two ways of remapping channels. Note that these two options are mutually exclusive, but both can appear in a config file. If both appear, then the `--remap` option takes precedence.

> ❗ Remapping only works when using `multiplex`.

The easiest way is to use `--remap` option. This causes `locast2tuner` to rewrite the channel number based on the amount of instances there are. Locast will remap a "channel_number" to "channel_number + (100 * instance_number)", where the instance_number starts at 0. E.g. you override 3 zip codes, then the channels from the first location will be untouched (since 100 * 0 == 0). The stations for the second location will start at 100 (e.g. 2.1 CBS becomes 102.1 CBS) and the stations for the third location will start at 200 (e.g. 13.2 WWFF becomes 213.2 WWFF).

Another way to do remapping is to use the `--remap_file <filename>` option. You can specify a JSON file containing your remappings. To get your current mappings, you can go to `http://PORT:IP/map.json`. Copy that content to a JSON file (you'll want to pretty it up too to make it easier to work with) and you can edit that JSON file, save it, and then use `--remap_file <filename>` to load those remappings the next time you run `locast2tuner`. You will need to restart `locast2tuner` in order to see any changes you made (and you may need to recreate your tuner/EPG setup to have Plex or Emby reflect the right channels).

>This is currently a manual edit process, so if you want to go this route, please be sure that the JSON content is valid JSON before trying to use it. A web-based remap editor is in the works.
