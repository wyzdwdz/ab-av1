# ab-av1
AV1 re-encoding using _ffmpeg_, _svt-av1_ & _vmaf_.

## auto-encode
Automatically determining the best crf & use it to encode a video.

Two phases:
* [crf-search](#crf-search) to determine the best --crf value
* ffmpeg & SvtAv1EncApp to encode using the settings

```
ab-av1 auto-encode [OPTIONS] -i <INPUT> --preset <PRESET>
```

## crf-search
Pseudo binary search using [sample-encode](#sample-encode) to find the best 
crf value delivering **min-vmaf** & **max-encoded-percent**.

Outputs:
* Best crf value
* Mean sample VMAF score
* Predicted full encode size
* Predicted full encode time

```
ab-av1 crf-search [OPTIONS] -i <INPUT> --preset <PRESET>
```

## sample-encode
Encode short video samples of an input using provided **crf** & **preset**. 
This is much quicker than full encode/vmaf run. 

Outputs:
* Mean sample VMAF score
* Predicted full encode size
* Predicted full encode time

```
ab-av1 sample-encode [OPTIONS] -i <INPUT> --crf <CRF> --preset <PRESET>
```

## encode
Simple invocation of ffmpeg & SvtAv1EncApp to reencode a video.

```
ab-av1 encode [OPTIONS] -i <INPUT> --crf <CRF> --preset <PRESET>
```

## vmaf
Simple full calculation of VMAF score distorted file vs original file.

```
ab-av1 vmaf --original <ORIGINAL> --distorted <DISTORTED>
```
