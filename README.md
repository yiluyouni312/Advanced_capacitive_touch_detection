# Advanced_capacitive_touch_detection

These capacitive touch detection library is an extension of the Arduino capacitive touch library, it offers two detection algorithms that solves two of the main problems associated with detecting capacitive touch on the Arduino. The library also allows advanced touch detections; such as, Double tap, Short press and Long press. Also featured in the library is a haptics controller, this allows you to connect and control a vibration motor as a feedback when you interact with the capacitive touch surface.

<script src="https://gist.github.com/ahmsville/5ade8dee2795402d2df029cbc7025fa4.js"></script>

The code snippet above shows how you would typically setup the library.
Line 2 is used to create a new capacitive touch object; the object is named “samplepad” but you can give any other name.
In the setup section of the code, the first line calls the function set_inputTypeThresholds(), this function is used to set the different detection levels of the four detectable capacitive touch types (single tap, short press, long press and double tap). Think of the numbers as how long your finger must be on the pad for specific touch types. For example, the code above sets 20 as the single tap threshold; this means any touch input that yields a count less than 20 will be categorized as a single tap, if the touch yields a count greater than 20 but less than 40, the touch is categorized as a short press, the same logic applies to the remaining touch types.
The second line set_detectionThreshold(); is used to set the sensitivity of the capacitive touch surface. The function accepts two integers, the touch detection threshold and the touch rejection threshold, the recommended ratio of detection to rejection threshold is 4:1. The larger the detection thresholds, the lower the pad sensitivity.
Line three is used to configure the Arduino pins connected to the resistor and the touch surfaces. The code sample uses just one pin i:e one touch pad. You can have up to 4 pads connected, all of which will share the same send pin.
Line four is used to initialize the capacitive touch, the function initialize_capTouch() accepts an integer from 1 – 4, representing the number of pads your working with.
Line five is optional, only use this function when you have a haptics circuit setup.

Detecting touch in the main program loop.

<script src="https://gist.github.com/ahmsville/e0f717f0b333d5f237a9b9ff3b2b2016.js"></script>

There are two main functions for running the touch detection algorithm, the first is the detect_touch() function. This function should be used for a low noise touch setup, the function will return an integer value from 0 – 4.
•	0 means no touch was detected.
•	1 means a single tap was detected.
•	2 means a double tap was detected.
•	3 means a short press was detected.
•	4 means a long press was detected.
The function detect_touch() should always be called with a integer value from 0 – 3, this value represents the position of the capacitive touch pad you want to run a touch detection on.
For noisy touch setups, use the detect_touchFromNoise() function instead, this function is more reliable and works in the exact same way as detect_touch(). Because this algorithm involves signal sampling, it is just a little bit slower than the alternative.
The second function update_basevalue() in the loop is used to continuously update the nominal value of the touch pad. This function is integral to making the touch detection adaptable across various touch conditions.

