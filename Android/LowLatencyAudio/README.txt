PGLowLatencyAudio plugin for PhoneGap/Apache Cordova
Developed by Andrew Trice - http://tricedesigns.com

THIS SOFTWARE IS PROVIDED BY ANDREW TRICE "AS IS" AND ANY EXPRESS OR
IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF
MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO
EVENT SHALL ANDREW TRICE OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT,
INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING,
BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE,
DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF
LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE
OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF
ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

You can read more about this plugin at:
http://www.tricedesigns.com/2012/01/25/low-latency-polyphonic-audio-in-phonegap/

The low latency audio plugin is designed to enable low latency and polyphonic audio from PhoneGap applications, using a very simple and basic API.

Getting started:
Add the following files to your JAVA project, keeping the folder structure:
com/phonegap/PGLowLatencyAudio.java
com/phonegap/PGLowLatencyAudioAsset.java
com/phonegap/PGPolyphonicVoice.java

Add the following file to your www directory, and add to index.html:
PGLowLatencyAudio.js

Add the following to your phonegap plugins.xml file:
<plugin name="PGLowLatencyAudio" value="com.phonegap.PGLowLatencyAudio" />

Usage:
1) Preload the audio asset
2) Play the audio asset
3) When done, unload the audio asset

API methods:
preloadFX: function ( id, assetPath, success, fail)
	params: ID - string unique ID for the audio file
			assetPath - the relative path to the audio asset within the www directory
			success - success callback function
			fail - error/fail callback function
	detail:	
			The preloadFX function loads an audio file into memory.  Assets that are loaded using preloadFX are managed/played using the Android SoundPool class.   These are very low-level audio methods and have minimal overhead.   These assets should be short.   Sound files longer than 5 seconds may have errors including (not playing, clipped content, not looping) - all will fail silently on the device (debug output will be visible if connected to debugger).  These assets are fully concurrent and polyphonic.
			
preloadAudio: function ( id, assetPath, voices, success, fail) 
	params: ID - string unique ID for the audio file
			assetPath - the relative path to the audio asset within the www directory
			voices - the number of polyphonic voices available
			success - success callback function
			fail - error/fail callback function
	detail:	
			The preloadAudio function loads an audio file into memory.  Assets that are loaded using preloadAudio are managed/played using the Android MediaPlayer.   These have more overhead than assets laoded via preloadFX, and can be looped/stopped.   By default, there is a single "voice" - only one instance that will be stopped & restarted when you hit play.  If there are multiple voices (number greater than 0), it will cycle through voices to play overlapping audio.
		
play: function (id, success, fail) 	
	params: ID - string unique ID for the audio file
			success - success callback function
			fail - error/fail callback function
	detail:	
			Plays an audio asset
		
loop: function (id, success, fail) 	
	params: ID - string unique ID for the audio file
			success - success callback function
			fail - error/fail callback function
	detail:	
			Loops an audio asset infinitely - this only works for assets loaded via preloadAudio
		
stop: function (id, success, fail) 	
	params: ID - string unique ID for the audio file
			success - success callback function
			fail - error/fail callback function
	detail:	
			Stops an audio file - this only works for assets loaded via preloadAudio
		
unload: function (id, success, fail) 	
	params: ID - string unique ID for the audio file
			success - success callback function
			fail - error/fail callback function
	detail:	
			Unloads an audio file from memory
			
			
			
