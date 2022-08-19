# rubio-radio
[![Gem Version](https://badge.fury.io/rb/rubio-radio.svg)](https://badge.fury.io/rb/rubio-radio)

Linux

![linux screenshot](screenshots/rubio-radio-linux.png)

Mac

![mac screenshot](screenshots/rubio-radio-mac.png)

Windows

![windows screenshot](screenshots/rubio-radio-windows.png)

:bowtie: Alpha

## Installation

### Requirements:

**[VLC](https://github.com/videolan/vlc)**

`rubio` uses the `vlc -I dummy` as the audio playback backend.

On Mac, it is recommended that you install VLC via [Homebrew](https://brew.sh/) to ensure the `vlc` command is added to the PATH environment variable automatically:

```
brew install vlc
```

On Windows, install VLC using the [Windows installer](https://www.videolan.org/vlc/download-windows.html), and then add the installed VLC app directory to the PATH environment variable (e.g. `C:\Program Files (x86)\VideoLAN\VLC`) to make the `vlc` command available.

### Ruby Gem:

```
gem install rubio-radio
```

## Usage

Run with this command:

```
rubio
```

The top 10,000 [Radio Browser](https://www.radio-browser.info/) stations are displayed by default. But, you can customize the count (note that currently, there are only about 32,000 [Radio Browser](https://www.radio-browser.info/) stations total).

```
rubio --count 20000
```

The stations are fetched gradually (asynchronously) from the [Radio Browser](https://www.radio-browser.info/) web API to have the app start instantly (avoid having the user wait for the app to start) no matter what the total count of stations is. But, you can avoid gradual prefetching if you prefer.

```
rubio --no-gradual
```

Default player is `vlc -I dummy`. But, you can use any command line player that can take URL of radio station as its first argument.

```
rubio --backend mpg123
```

Learn more about `rubio` options:

```
rubio --help
```

```
Usage: rubio [options]
        --vlc [STR]         use VLC interface STR on the backend [dummy]
        --mpg123            use mpg123 on the backend
    -b, --backend STR       command to use as backend player ['vlc -I dummy']
    -c, --count INT         number of stations to fetch from radio-browser [10000]
        --per-page INT      number of stations per page [20]
    -w, --width INT         main window width
    -h, --height INT        main window height
        --[no-]page-count   show/hide page count [false]
        --[no-]menu         show/hide menu [true]
        --[no-]bookmarks    show/hide bookmarks [true]
        --[no-]gradual      gradually/non-gradually fetch stations [true]
        --debug             output status of monitored threads
        --help              show this help message
        --version           show the rubio version number
```

Examples:

```
rubio --vlc              # `vlc -I rc` (interactive command line interface)
rubio --mpg123           # `rubio --backend mpg123`
rubio --count 1000       # Displays the top 1,000 Radio Browser stations
```

Minimalistic Example:

```
rubio --per-page 6 --no-margins --no-menu --no-bookmarks
```

![small screen linux screenshot](screenshots/rubio-radio-linux-example-small.png)

Page Count Example:

```
rubio --page-count
```

![page count mac screenshot](screenshots/rubio-radio-mac-example-page-count.png)

### Filtering

The filter field does AND-based filtering when you enter multiple words separated by spaces:

```
jazz smooth
```

Also, the filter field supports exact term filtering if you enter multiple words surrounded by double-quotes.

```
"bossa nova"
```

Last but not least, the filter field supports column-specific queries by including a full column name or the first few letters, followed by colon (:), followed by a single word or double-quoted multiple words for exact term matching against the column:

```
talk lang:eng
```

![advanced filtering mac screenshot](screenshots/rubio-radio-mac-example-advanced-filtering.png)

This advanced example matches the word `FM` against the name column, and language `bahasa indonesia` against the language column.

```
n:FM l:"bahasa indonesia"
```

### Menus

You can use the top menu bar to stop the currently playing radio station, bookmark, unbookmark, view only bookmarked stations, view only currently playing station, and read the about dialog.

![view book marks mac screenshot](screenshots/rubio-radio-mac-example-view-bookmarks.png)

Bookmarks are stored in `File.join(Dir.home, '.rubio-radio', 'bookmarks.yml')`

## Links

* [Ruby](https://github.com/ruby/ruby)
  * spawn
* [Radio Browser](https://www.radio-browser.info/)
  * [Radio Browser API](https://de1.api.radio-browser.info/)
* [Glimmer DSL for LibUI](https://github.com/AndyObtiva/glimmer-dsl-libui)

## Change Log

[CHANGELOG.md](CHANGELOG.md)

## LICENSE

[MIT](LICENSE.txt)
