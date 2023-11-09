

**Important:** The maintainers(s) of this repository are not affiliated or connected with the original version of VoiceFixer.

**Note:** We are actively accepting contributions! Please check the To Do list for how you can contribute!

# <img src="https://github.com/fakerybakery/voicefixer/assets/76186054/499b358d-0063-45bc-925b-d4136c05af34" width="50"> VoiceFixer 2

Welcome to VoiceFixer 2, the next generation of VoiceFixer. VoiceFixer is a general speech restoration tool, using AI to remove background noise, fix degraded speech, enhance audio quality from old recordings, upscale low resolution, and more, all in one model!

VoiceFixer aims to restore human speech, regardless of how seriously degraded it is. It can handle noise, reverberation, low resolution, and clipping effect within one model!

## What’s different from the original VoiceFixer?

The [original version of VoiceFixer](https://github.com/haoheliu/voicefixer) continues to be updated with minor changes and bug fixes, however if one tries to install it and run it out of the box, one would encounter several errors that require modifying installed packages to fix.

**What’s the problem? How does this fix it?** VoiceFixer requires an old version of the `librosa` library, which is incompatible with new versions of the `numpy` library. We’ve fixed this issue by fixing the old version of `librosa` and `voicefixer`. We also added several new features.

### New features in VoiceFixer 2

We’ve added the following features in VoiceFixer 2:

* We’ve added MPS support, which means you can use GPU acceleration on M1 macs. You can enable this by setting the `cuda` parameter to `True`. It’s automatically enabled when using the command line interface (CLI).
* More features coming soon!
## To-Do
Here's what we still need to do - feel free to contribute:
* Implement .mp3 support (currently only supports .wav) - probably won't be that hard - just need to use pydub. good beginner contribution!
* Add TQDM progress bar - crucial for longer conversions - maybe a beginner contribution?
* Fine-tune model for better results (this one requires $$$/compute :) - see [this](https://github.com/haoheliu/voicefixer_main) training repo)
* Use latest version of librosa (probably pretty important)
* Publish to pip (plz don't contribute on this one - I'll do it eventually but I have a certain workflow + system I like to use :) thanks!)
## Demo

[Check out the demos to see what VoiceFixer can do!](https://haoheliu.github.io/demopage-voicefixer/)

## Installation

PyPi package coming soon!

```bash
pip install git+https://github.com/fakerybakery/voicefixer
```

## Usage

**Important:** VoiceFixer can only process files in the `wav` format. We recommend using `ffmpeg` library to convert `mp3`s to `wav`s. We’re working on supporting this.

### Command Line

Process a file:

```bash
voicefixer --infile test/utterance/original/original.wav
```

Process all files in a directory:

```bash
voicefixer --infolder /path/to/input --outfolder /path/to/output
```

Change modes (default 0):

```bash
voicefixer --infile /path/to/input.wav --outfile /path/to/output.wav --mode 1
```

Run all modes:

```bash
voicefixer --infile /path/to/input.wav --outfile /path/to/output.wav --mode all
```

For more information:

```bash
voicefixer -h
```

### Python API

```python
from voicefixer import VoiceFixer
voicefixer = VoiceFixer()
# Mode 0: Original Model (suggested by default)
# Mode 1: Add preprocessing module (remove higher frequency)
# Mode 2: Train mode (might work sometimes on seriously degraded real speech)
for mode in [0,1,2]:
    print("Testing mode",mode)
    voicefixer.restore(input=os.path.join(git_root,"test/utterance/original/original.flac"), # low quality .wav/.flac file
                       output=os.path.join(git_root,"test/utterance/output/output_mode_"+str(mode)+".flac"), # save file path
                       cuda=False, # GPU acceleration
                       mode=mode)
    if(mode != 2):
        check("output_mode_"+str(mode)+".flac")
    print("Pass")
```

## License

The original version of VoiceFixer was licensed under the permissive MIT license, available [here](VOICEFIXER_LIC_MIT).

VoiceFixer 2 is licensed under the New Open-Source "Copyleft" License (Commercial Edition), Version 2.0 (NOSCL-C-2.0), available [here](LICENSE). The NOSCL license family is a permissive ("weak") copyleft license. The NOSCL-C-2.0 license allows for commercial use, with a few restrictions. Although NOSCL-C-2.0 requires derivatives to have the same license, it allows software that "links" to this library to be licensed under different license. For example, if you reference this library in your software, you can redistribute your software under a different license, as long as you don't bundle the library into your software (this is not a replacement for the license, and there are more restrictions). More details can be found [here](LICENSE).

The main reason why I decided to switch is because I didn't want something as restrictive as GPL/LGPL but BSD/MIT felt too weak. If you want an exception, its probably fine but please contact me first. Thanks!
