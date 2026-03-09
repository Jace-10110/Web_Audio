# Web Audio Lab

A small experimental tool for exploring how browsers decode, route, and downmix audio using the Web Audio API.

This project demonstrates the different ways audio can enter the Web Audio pipeline and how browsers handle multichannel audio.

The application can load both standalone audio files and media containers (video/audio), route them through a Web Audio graph, and visualise channel activity using analyser meters.

The goal is to explore:

- browser decoding behaviour
- multichannel audio handling (2.0 / 4.0 / 5.1 / 7.1)
- automatic browser downmixing
- Web Audio graph routing (only a channel splitter was used for AnalyserNode metering, no attempt has been made to route or mix audio beyond the hardware default capabilities)


## Features

![Web Audio Lab Screenshot](static/audio/Screenshot.jpg)

- Load audio files using `decodeAudioData()`
- Load video/audio containers using `MediaElementSource`
- Visualise individual channel activity using analyser nodes
- Inspect decoded file metadata
- Display the Web Audio routing graph
- Compare browser behaviour across different codecs and channel layouts, .wav, .flac, .vob, .mp4


## Observations

Tested on Safari and Chrome only:

- Safari and Chrome successfully decodes multichannel WAV and FLAC files using `AudioContext.decodeAudioData`.
- Chrome passes multichannel using `AudioContext.decodeAudioData`, but does not automatically downmix beyond 2.0. Merger Node may be needed for stereo monitoring.
- Safari passes multichannel using `AudioContext.decodeAudioData`, but does not automatically downmix beyond 5.1. Merger Node may be needed for stereo monitoring. 
- Wider browser codec support for media elements via `AudioContext.createMediaElementSource` . Automatic downmix seems to be the default. Chrome does not support VOB (MPEG-2/AC3)
- Both loading mechanisms can handle H.264/AAC .mp4 containers in Safari and Chrome


  ## Running the Project 

Requirements:

- Python 3
- pip install flask

Start the local server:

```bash
python server.py
