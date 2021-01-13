# English Text to Speech Voice (kathleen)

Voice and vocoder models for [larynx](https://github.com/rhasspy/larynx) based on the [kathleen](https://github.com/rhasspy/dataset-voice-kathleen/).

Used in [Rhasspy](https://github.com/rhasspy) in the [rhasspy-tts-larynx-hermes](https://github.com/rhasspy/rhasspy-tts-larynx-hermes) service.

[Samples](samples)

## Usage

```sh
$ larynx \
    --model /path/to/tts-checkpoint.pth.tar \
    --vocoder-model /path/to/vocoder-checkpoint.pth.tar \
    --output-file /path/to/output.wav \
    'Hello world!'
```

### Docker

Run a web server at http://localhost:5002

```sh
$ docker run -it -p 5002:5002 \
    --device /dev/snd:/dev/snd \
    rhasspy/larynx:en-kathleen-1
```

Endpoints:

* `/api/tts` - returns WAV audio for text
    * `GET` with `?text=...`
    * `POST` with text body
* `/api/phonemize` - returns phonemes for text
    * `GET` with `?text=...`
    * `POST` with text body
* `/process` - compatibility endpoint to emulate [MaryTTS](http://mary.dfki.de/)
    * `GET` with `?INPUT_TEXT=...`

## Model Details

* Type: [Tacotron2](https://arxiv.org/abs/1712.05884)
* Sample rate: 24000 Hz
* Frequency range: 50-7600 Hz

See [configuration](config.json) for details.

## Vocoder Details

* Type: [Fullband MelGAN](https://arxiv.org/abs/1710.10467)
* Sample rate: 24000 Hz
* Frequency range: 50-7600 Hz

See [configuration](vocoder/config.json) for details.

## Files

Some files are split into multiple parts so that they can be uploaded to GitHub. This is done with the `split` command:

```bash
split -d -b 25M FILE FILE.part-
```

They can be recombined simply with:

```bash
cat FILE.part-* > FILE
```
