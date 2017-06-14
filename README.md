# libwebrtc-android

Prebuilt WebRTC library for Android, available via gradle.

Built against the 'stable' release branches used in Chrome for Android (currently M59).

I will endevour to add the latest stable releases as and when they are released. (Release Schedule: https://www.chromium.org/developers/calendar)

Usage is demonstrated in the AppRTC sample app which I have mirrored and setup to use this library:
https://github.com/deano2390/AppRTC

# Gradle

[![](https://jitpack.io/v/deano2390/libwebrtc-android.svg)](https://jitpack.io/#deano2390/libwebrtc-android)

Add the jitpack repo to your your project's build.gradle at the end of repositories

/build.gradle
```groovy
allprojects {
	repositories {
		jcenter()
		maven { url "https://jitpack.io" }
	}
}
```

Then add the dependency to your module's build.gradle:

/app/build.gradle
```groovy
	dependencies {
	        compile 'com.github.deano2390:libwebrtc-android:59-vanilla'
	}

```

# Noise Suppressor
I needed access to the Software Noise Suppressor in WebRTC in my Java code so I wrote a small JNI wrapper to expose it. You can access this using the alternative branch release:
```groovy
	dependencies {
	        compile 'com.github.deano2390:libwebrtc-android:59-NS'
          }

```

Example usage:
```java
import org.webrtc.NoiseSuppressor;

// setup
int samplingRate = 16000; // 16Khz
int mode = 2; // (0 = mild, 1 = medium, 2 = aggressive)
NoiseSuppressor noiseSuppressor = new NoiseSuppressor(samplingRate, mode);

// usage - inBuffer contains your frasmes of audio sample
// the WebRTC noise suppressor uses a strict frame size of 160 samples

short[] inBuffer = new short[160]; // copy input samples into here
short[] outBuffer = new short[160]; // your de-noised audio frame will appear in outBuffer

noiseSuppressor.processAudioFrame(inBuffer, outBuffer, (short) inBuffer.length);

// teardown
softNoiseSuppressor.close();
                
```

# License
```yaml
Copyright (c) 2011, The WebRTC project authors. All rights reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are
met:

  * Redistributions of source code must retain the above copyright
    notice, this list of conditions and the following disclaimer.

  * Redistributions in binary form must reproduce the above copyright
    notice, this list of conditions and the following disclaimer in
    the documentation and/or other materials provided with the
    distribution.

  * Neither the name of Google nor the names of its contributors may
    be used to endorse or promote products derived from this software
    without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS
"AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT
LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR
A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT
HOLDER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL,
SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT
LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE,
DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY
THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
(INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
```
