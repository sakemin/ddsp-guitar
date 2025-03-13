# DDSP Guitar

A neural guitar synthesizer that converts MIDI to realistic guitar audio using Differentiable Digital Signal Processing.

## Overview

This repository contains code for generating realistic guitar audio from string-wise MIDI input using DDSP (Differentiable Digital Signal Processing). The implementation is based on the research paper [*DDSP-based Neural Waveform Synthesis of Polyphonic Guitar Performance from String-wise MIDI Input*](https://arxiv.org/abs/2309.07658).

Listen to audio examples on our [project page](https://erl-j.github.io/neural-guitar-web-supplement/).

## Features

- Convert MIDI files to realistic guitar audio
- String-wise MIDI processing
- Multiple control options:
  - Pitch correction
  - Pitch offset adjustment
  - Legato/staccato articulation
- Pretrained unified model

## Installation

```bash
git clone https://github.com/sakemin/ddsp-guitar.git
cd ddsp-guitar
pip install -r requirements.txt
```

## Usage

Render a MIDI file with the pretrained unified model:

```bash
python render_midi.py --midi_path midi.mid --output_path out.wav
```

### Command Line Options

- `--midi_path`: Path to input MIDI file (required)
- `--output_path`: Path for output WAV file (defaults to input filename with .wav extension)
- `--crop-seconds`: Limit rendering to specified duration in seconds
- `--device`: Computation device (default: "cuda:0")
- `--pitch-correction`: Replace predicted pitch with MIDI pitch on active notes (default: True)
- `--pitch-offset`: Adjust MIDI pitch by semitones (default: 0)
- `--legato`: Use legato articulation (default: False, uses staccato on subsequent notes on same string)

## How It Works

The system processes string-wise MIDI input through a neural network that generates synthesis parameters for a differentiable synthesizer. The model:

1. Reads MIDI files and converts them to frame-wise pitch and velocity representations
2. Processes these through a trained neural network
3. Generates audio using a DDSP synthesizer with harmonic and noise components

The pretrained unified model is automatically downloaded from Hugging Face on first use.

## Acknowledgements

This work is supported by:
- MUSAiC: Music at the Frontiers of Artificial Creativity and Criticism (ERC-2019-COG No. 864189)
- JST CREST Grants (JPMJCR18A6 and JPMJCR20D3)
- MEXT KAKENHI Grants (21K17775, 21H04906, 21K11951, 22K21319)

Code bases:
- DDSP implementation based on [magenta's ddsp](https://github.com/magenta/ddsp) and [ddsp_pytorch](https://github.com/acids-ircam/ddsp_pytorch)
- Dilated convolutions code from @ljuvela

## Citation

If you use this code in your research, please cite:
```
@article{ddsp-guitar,
  title={DDSP-based Neural Waveform Synthesis of Polyphonic Guitar Performance from String-wise MIDI Input},
  author={Jonason, Erik Rutger and Wang, Xin and Cooper, Erica and Juvela, Lauri and Sturm, Bob L. T. and Yamagishi, Junichi},
  journal={arXiv preprint arXiv:2309.07658},
  year={2023}
}
```