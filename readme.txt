TEMmod - TEdgeMask modified for Avisynth2.6x

TEMmod is an Avisynth plugin which based on TEdgeMask written by Kevin Stone
(a.k.a. tritical) and was written from scratch.


Info:
    Creates an edgemask using gradient vector magnitude.
    Only planar formats are supported.


Requirement:
    Avisynth 2.6 alpha 4 or later.
    Visual C++ Redistributable Package for Visual Studio 2019
    SSE2 capable CPU


Syntax:

    TEMmod(clip c, float "threshY", float "threshC", int "type", int "link",
           int "chroma", bool "invert", bool "preblur", float "scale")


    threshY:
        Set the magnitude thresholds for Y-plane.
        If over this value then a sample will be considered an edge, and the
        output mask will be binarizeto by 0 and 255.
        Set this to 0 means output a magnitude mask instead of binary mask.

        default: 8.0 (float)

    threshC:
        Set the magnitude thresholds for U-plane and V-plane.
        Others are same as threshY.

        default: 8.0 (float)

    type:
        Sets the type of first order partial derivative approximation that is used.
        possible values:

            1 - 2 pixel (floating point arithmetic, almost same as original)
            2 - 4 pixel (floating point arithmetic, almost same as original)
            3 - 2 pixel (type1 with SSE2 integer arithmetic, a bit incorrect but faster)
            4 - 4 pixel (type2 with SSE2 integer arithmetic, a bit incorrect but faster)
            5 - 6 pixel (Sobel operator with SSE2 integer arithmetic)

        default: 4 (int)

    link:
        Specifies whether luma to chroma linking, no linking, or linking of every
        plane to every other plane is used.

            0 - no linking
            1 - luma to chroma linking
            2 - every plane to every other plane

        default: 1 (int)

    chroma:
        This control how chroma(U-plane and V-plane) is processed.
        Set to 0 to not process and never touch.
        Set to 1 to process chroma.
        Set to 2 to not process and all samples are fill to zero.

        default: 1 (int)

    invert:
        If this set to True, the output mask will be inverted.

        default: False (bool)

    preblur:
        Indicates whether to apply a 3x3 guassian blur to the input image
        prior to generating the edge map.

        default: False (bool)

    scale:
        If output is a magnitude mask(threshY=0), it is scaled by this value.
        Set this to 0 means output is adjusted automatically and scaled onto
        0-255 range.

        default: 0

Note:
    type5 is more edge sensitive than the others.
    Therefore, you should raise thresholds to others about 150%.

Source code:
    https://github.com/chikuzen/TEMmod/


Author:
    Oka Motofumi (chikuzen.mo at gmail dot com)
