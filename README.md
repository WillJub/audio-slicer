# Audio Slicer with Path Support for ffmpeg

This is a fork from <https://github.com/AliAryanTech/audio-slicer/>.
All this fork do is adding the ability to set the path of ffmpeg.

Credits to AliAryanTech for the functionalities and the original README.

## Installation

Before using the `audio-slicer-with-path` module, you must have the package `@ffmpeg-installer/ffmpeg` installed in your app. You can install `audio-slicer-with-path` using npm or yarn:

```sh
npm install audio-slicer-with-path
```

```javascript
 dotenv = require('dotenv');
dotenv.config();

```

To set the path of ffmpeg, you can use the following code in your project:

```javascript
import dotenv from 'dotenv';
const ffmpeg = require('@ffmpeg-installer/ffmpeg');
dotenv.config();
process.env.FFMPEG_PATH = ffmpeg.path;
```

### Usage

The `audio-slicer-with-path` module provides two functions:

#### 1. `audioToSlice(buffer, seconds, video)`

- `buffer` (required): The audio data buffer you want to slice. This should be a Buffer containing the audio content you want to split.
- `seconds` (required): The duration of each segment in seconds.
- `video` (optional, default is false): A boolean indicating whether the media is video (true) or audio (false).

Here's an example usage:

```js
const { audioToSlice } = require('audio-slicer-with-path')
const { readFile } = require('fs-extra')

(async () => {
  try {
    // Read the media file as a buffer (can be audio or video)
    const media = await readFile('./media.mp4')
    // Specify segment duration in seconds (e.g., 60 seconds)
    const seconds = 60
    // Specify whether it's video (true) or audio (false)
    const video = true
    // Call the mediaToSlice function
    const buffers = await audioToSlice(media, seconds, video)
    console.log(`Sliced into ${buffers.length} segments.`)
  } catch (error) {
    console.error('Error slicing media:', error.message)
  }
})()
```

#### 2. `audioMerge(audios)`

- `audios` (required): An array of audio buffers to merge.

Here's an example usage:

```js
const { audioMerge } = require('audio-slicer-with-path')
const { readFile } = require('fs-extra')

(async () => {
  try {
    // Read multiple audio files as buffers
    const audio1 = await readFile('./audio1.mp3')
    const audio2 = await readFile('./audio2.mp3')
    const audio3 = await readFile('./audio3.mp3')

    // Create an array of audio buffers
    const audioBuffers = [audio1, audio2, audio3]

    // Call the audioMerge function
    const mergedBuffer = await audioMerge(audioBuffers)

    // Handle the merged audio buffer as needed
    console.log('Merged audio buffer:', mergedBuffer)
  } catch (error) {
    console.error('Error merging audio:', error.message)
  }
})()
```

### Credits

The `audio-slicer` module is created and maintained by [AliAryanTech](https://github.com/AliAryanTech).
The `audio-slicer-with-path` module is a fork of `audio-slicer` with the addition of setting the path of ffmpeg.
