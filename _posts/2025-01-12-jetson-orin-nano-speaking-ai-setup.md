---
layout: post
title: "Nvidia Jetson Orin Super Nano 8GB — setup and demo"
date: 2025-01-12
tags: [edge-ai, tutorial]
original_url: https://medium.com/@ori.nachum_22849/jetson-orin-nano-8gb-speaking-ai-setup-606c7871a7e0
---

Quickly set up your Orin Nano unit for a Hearing-Thinking-Speaking (HTS) bot.

## Agenda

- Goal
- Device preparation
  - JetPack 6.1+
  - System configuration Wizard
  - Bonus: useful applications
- Install GPU libraries
  - Install torch
  - Install CTranslate2
  - Install torchaudio
- Test your system
- Run the HTS bot
- Statistics
- Demo video of "baby-tau"
- Acknowledgments
- Links

## Goal

At the end of this guide, your Jetson Orin Nano Super 8GB ("JONS") will run VAD, STT, LLM, and TTS for speech detection, speech to text, LLM for thinking, and text to speech, respectively.

Your JONS will have basic packages, configuration, and everything necessary to make the above work properly.

### Note

There are many alternatives, and for this guide, I've chosen:

- VAD: SileroVAD
- STT: FasterWhisper (small)
- LLM: Ollama (Llama 3.2 3B, 4Q_K_M, 2GB)
- TTS:
  - PiperTTS (High, 218mb, 1 ms for 'hello world')
  - KokoroTTS (643mb, 470ms for 'hello world', edit: not utilizing GPU here. An improvement in progress, track this guide to see the update)

## Prerequisites

1. Nvidia Jetson Orin Nano Super 8GB / Jetson Orin Nano 8GB with upgraded firmware (Which is the same)
2. Display port cable + screen (Or any alternative). I recommend a big screen here — any PC or laptop-sized screen is excellent.
3. A microphone and speakers. I tried two setups:
   - ReSpeaker 2.0 4-mic array with connected speaker.
   - Waveshare USB-to-Audio with a matching pair of speakers.
   - A Bluetooth headset with a microphone built-in. ReSpeaker is the better microphone option of the first two, and the USB-to-Audio provides a louder volume. I haven't tried option 3.
4. SD Card with JetPack 6.1 (JP6.1) or alternative (NVMe with JP6.1 and a flag to boot from NVMe)
5. A working internet connection.

## Device preparation

### JetPack 6.1

Install JetPack 6.1 per Nvidia's guide. If this doesn't work for you, you have an old firmware. In that case, install JetPack 5.1.3 per Nvidia's guide and let it auto-update the firmware until you reach a black screen. Per the guide, switch back to JetPack 6.1, and everything should work now.

### System Configuration wizard

You should expect to find the System Configuration wizard screen on startup — a wizard guiding you for initial configuration.

After you've gone through the wizard, you should have a username and password. You've also set your region, keyboard, and internet connection.

I have rolled with their APP Partition recommendation and set up Chromium for convenience. (Chromium can be installed later as well)

### Bonus: Essential applications

It's not strictly necessary, but it's very handy. Click the "9 dots" icon to the bottom left, write and run the "Software" app, and install some essentials:

- Chromium / Firefox / any preferred browser
- Codium — a stripped-down version of VSCode. It's a good development IDE and manages git credentials for you.

### Python virtual environments

Install virtual environment for python:

```bash
sudo apt install python-3.10-venv -y
```

## Install GPU libraries

This part can be solved with dusty-nv's jetson-containers GitHub repository. It provides all the necessary components, using a "mix and deploy" approach, as docker containers to fulfill your project's requirements.

At the time of this post, JetPack 6.1 was not supported, and I went lower to install the libraries manually. To my content, dusty-nv also provided the wheels from which his system builds the containers and had already supported JetPack 6.x there.

### Install torch

Install torch from Nvidia's wheel. You can get the links here:

```bash
mkdir git ; cd git
git clone https://github.com/OriNachum/autonomous-intelligence
cd autonomous-intelligence/jetson-super
cat setup.sh
```

The above script has code for:

- Set up path for CUDA + set it on system start (~/.bashrc)
- Download and unpack cusparselt compiled for JONS by Nvidia
- Install portaudio19-dev, python-all-dev, python3-all-dev
- Install python3-pip, python3-dev, python3-setuptools
- Download and install torch 2.5.0 compiled for JONS by Nvidia (Must happen after cusparselt unpack!)

Check your cuda version with the below. Reboot if needed.

Test torch:

```bash
nvidia-smi --version
nvcc --version
```

### Install CTranslate2

Initially, use the wheels from `https://pypi.jetson-ai-lab.dev/jp6/cu126`

I got an error and needed to provide a missing file.

#### Troubleshoot

I was missing `libctranslate2.so.4`. I got it with:

Build CTranslate2 from pip page manual installation:

```bash
git clone https://github.com/OpenNMT/CTranslate2
cd CTranslate2
git submodule update --init --recursive
mkdir build && cd build
cmake -DWITH_CUDA=ON -DWITH_CUDNN=ON -DWITH_MKL=OFF
make -j4
```

Add full path of `libctranslate2.so.4` to `LD_LIBRARY_PATH`:

```bash
export LD_LIBRARY_PATH="/home/<username>/git/CTranslate2/build:$LD_LIBRARY_PATH"
```

(Also add to `~/.bashrc` at the bottom to maintain the configuration)

### Install Torchaudio

Use the wheels from `https://pypi.jetson-ai-lab.dev/jp6/cu126`

## Test your system

### Run the HTS bot

```bash
# If not done yet:
mkdir git ; cd git
git clone https://github.com/OriNachum/autonomous-intelligence
cd autonomous-intelligence/baby-tau
```

This is my demo app for hearing-thinking-speaking system.

Run `init_env.sh` with source:

```bash
source init_env.sh
```

It is required to enable the environment and keep it enabled for your session.

This installs:

- requests
- python-dotenv
- faster_whisper
- numpy==1.26.4
- piper-tts (for piperTTS)
- kokoro-onnx (for kokoroTTS, then uninstall onnxruntime, reinstall onnxruntime from wheel)
- pyaudio

Remember: If you installed kokoro-onnx, uninstall onnxruntime, and reinstall onnxruntime from wheel for CUDA.

Then run:

```bash
python3 main.py -audio
```

Wait for it to load and start speaking.

## Acknowledgments

- Dustin Franklin, GitHub, for their significant work on jetson-containers repo and compiled libraries that greatly simplified the installation.
- JohnnyNuñez, GitHub, LinkedIn, for his assistance with the setup.

## Thank you

Found errors? Please comment with corrections so I can fix them.

Did you like it, or did it benefit you? Please support me with claps (Up to 50), and add a star to my [GitHub repository](https://github.com/OriNachum/autonomous-intelligence).

Please hop into Dusty's repo, [jetson-containers](https://github.com/dusty-nv/jetson-containers), and give it a star — this repository is gold.

## Links

- [Official Jetson AI Lab Research Group Community Discord Server](https://discord.gg/jetson-ai-lab)
- [jetson-containers GitHub repository](https://github.com/dusty-nv/jetson-containers)
- [jetson-containers prebuilt wheels](https://pypi.jetson-ai-lab.dev/jp6/cu126)
