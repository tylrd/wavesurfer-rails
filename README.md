# Wavesurfer-rails

[Wavesurfer Homepage](http://wavesurfer-js.org/)

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'wavesurfer-rails'
```

And then execute:

    $ bundle

In `app/assets/javascripts/application.js` put the following:

```javascript
//= require wavesurfer
```

If you want the wavesurfer plugins:

```javascript
//= require wavesurfer-plugins
```

## Usage

From the wavesurfer documentation:

```javascript
var wavesurfer = Object.create(WaveSurfer);

wavesurfer.init({
    container: document.querySelector('#wave'),
    waveColor: 'violet',
    progressColor: 'purple'
});

wavesurfer.on('ready', function () {
    wavesurfer.play();
});

wavesurfer.load('example/media/demo.mp3');
```

## WaveSurfer Options

| option | type | default | description |
| --- | --- | --- | --- |
| `audioContext` | object | _none_ | Use your own previously initialized `AudioContext` or leave blank. |
| `audioRate` | float | `1` | Speed at which to play audio.  Lower number is slower. |
| `backend` | string | `WebAudio` | `WebAudio` or `MediaElement`. In most cases you don't have to set this manually. `MediaElement` is a fallback for unsupported browsers. |
| `barWidth` | number | _none_ | If specified, the waveform will be drawn like this: ▁ ▂ ▇ ▃ ▅ ▂ |
| `container` | mixed | _none_ | CSS-selector or HTML-element where the waveform should be drawn. This is the only required parameter. |
| `cursorColor` | string | `#333` | The fill color of the cursor indicating the playhead position. |
| `cursorWidth` | integer | `1` | Measured in pixels. |
| `fillParent` | boolean | `true` | Whether to fill the entire container or draw only according to `minPxPerSec`. |
| `height` | integer | `128` | The height of the waveform.  Measured in pixels. |
| `hideScrollbar` | boolean | `false` | Whether to hide the horizontal scrollbar when one would normally be shown. |
| `interact` | boolean | `true` | Whether the mouse interaction will be enabled at initialization.  You can switch this parameter at any time later on. |
| `minPxPerSec` | integer | `50` | Minimum number of pixels per second of audio. |
| `normalize` | boolean | `false` | If `true`, normalize by the maximum peak instead of 1.0. |
| `pixelRatio` | integer | `window.devicePixelRatio` | Can be set to `1` for faster rendering. |
| `progressColor` | string | `#555` | The fill color of the part of the waveform behind the cursor. |
| `scrollParent` | boolean | `false` | Whether to scroll the container with a lengthy waveform. Otherwise the waveform is shrunk to the container width (see `fillParent`). |
| `skipLength` | float | `2` | Number of seconds to skip with the `skipForward()` and `skipBackward()` methods. |
| `waveColor` | string | `#999` | The fill color of the waveform after the cursor. |

## WaveSurfer Methods

All methods are intentionally public, but the most readily available are the following:

 * `init(options)` – Initializes with the options listed above.
 * `destroy()` – Removes events, elements and disconnects Web Audio nodes.
 * `empty()` – Clears the waveform as if a zero-length audio is loaded.
 * `getCurrentTime()` – Returns current progress in seconds.
 * `getDuration()` – Returns the duration of an audio clip in seconds.
 * `isPlaying()` – Returns true if currently playing, false otherwise.
 * `load(url)` – Loads audio from URL via XHR. Returns XHR object.
 * `loadBlob(url)` – Loads audio from a `Blob` or `File` object.
 * `on(eventName, callback)` – Subscribes to an event.  See [WaveSurfer Events](#wavesurfer-events) section below for a list.
 * `un(eventName, callback)` – Unsubscribes from an event.
 * `unAll()` – Unsubscribes from all events.
 * `pause()` – Stops playback.
 * `play([start[, end]])` – Starts playback from the current position.  Optional `start` and `end` measured in seconds can be used to set the range of audio to play.
 * `playPause()` – Plays if paused, pauses if playing.
 * `seekAndCenter(progress)` – Seeks to a progress and centers view `[0..1]` (0 = beginning, 1 = end).
 * `seekTo(progress)` – Seeks to a progress `[0..1]` (0=beginning, 1=end).
 * `setFilter(filters)` - For inserting your own WebAudio nodes into the graph.  See [Connecting Filters](#connecting-filters) below.
 * `setPlaybackRate(rate)` – Sets the speed of playback (`0.5` is half speed, `1` is normal speed, `2` is double speed and so on).
 * `setVolume(newVolume)` – Sets the playback volume to a new value `[0..1]` (0 = silent, 1 = maximum).
 * `skip(offset)` – Skip a number of seconds from the current position (use a negative value to go backwards).
 * `skipBackward()` - Rewind `skipLength` seconds.
 * `skipForward()` - Skip ahead `skipLength` seconds.
 * `stop()` – Stops and goes to the beginning.
 * `toggleMute()` – Toggles the volume on and off.
 * `toggleInteraction()` – Toggle mouse interaction.
 * `toggleScroll()` – Toggles `scrollParent`.
 * `zoom(pxPerSec)` – Horiontally zooms the waveform in and out. The
   parameter is a number of horizontal pixels per second of audio. It
   also changes the parameter `minPxPerSec` and enables the
   `scrollParent` option.

## Credits

Initial idea by [Alex Khokhulin](https://github.com/xoxulin). Many
thanks to
[the awesome contributors](https://github.com/katspaugh/wavesurfer.js/contributors)!

## License

![cc-by](http://i.creativecommons.org/l/by/3.0/88x31.png)

This work is licensed under a
[Creative Commons Attribution 3.0 Unported License](http://creativecommons.org/licenses/by/3.0/deed.en_US).
