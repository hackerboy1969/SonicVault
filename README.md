SONICVAULT
==========
Hide it in sound. Lock it with a key.

SonicVault is a browser-based audio toolkit in a single HTML file. It can hide
text inside a WAV audio file, recover it again, and protect audio files with a
password. Everything runs locally in your browser. Nothing is uploaded, and
there is no analytics or tracking.


FEATURES
--------
1. Encode message
   Turns text into a WAV file using two audio tones.
   1000 Hz = bit 0, 2000 Hz = bit 1.

2. Decode signal
   Reads a SonicVault WAV file and recovers the hidden text using Goertzel
   tone detection.

3. Encrypt / decrypt files
   Protects audio files (MP3, WAV, M4A, OGG, FLAC and others) with a password
   using AES-256-GCM. Keys are derived with PBKDF2 (SHA-256). Encrypted files
   are saved with the .aenc extension.

4. Recipe and operations library
   Transform text before encoding or after decoding with operations such as
   Hex, Base64, Binary, ROT13, XOR, Vigenere, Morse, MD5 and SHA.

5. Light and dark themes, responsive layout, works offline.


HOW TO USE
----------
1. Open index.html in a modern browser (Chrome, Edge, Firefox, Safari).
   No installation, build step or server is needed.

2. To hide a message:
   - Open the "Encode message" tab.
   - Type your message and, if you want, add recipe steps.
   - Check the Payload panel, then click "Generate WAV" and download the file.

3. To read a message:
   - Open the "Decode signal" tab.
   - Drop in the WAV file. The recovered text appears in the result panel.
   - Add recipe steps to transform it, then use Copy or Export .txt.

4. To protect an audio file:
   - Open the "Encrypt / decrypt files" tab.
   - Choose a file, enter a password (at least 8 characters) and encrypt.
   - To restore it, choose the .aenc file and enter the same password.


RECIPE
------
A recipe is an ordered list of operations that transforms your text. Each step
takes the output of the step before it.

- On the Encode tab, the recipe changes your message before it becomes audio.
- On the Decode tab, the recipe changes the recovered message.
- To undo a recipe, apply the reverse operations in reverse order.
  Example: To Base64 then ROT13 when encoding; ROT13 then From Base64 when
  decoding.
- Steps can be reordered or removed, and some take parameters such as a key.
- If a step fails, it is highlighted and the error message names the step.
- With no steps, the text is used as it is.


PAYLOAD
-------
The payload is the exact text that is encoded into sound: your message after
the recipe has run. It is shown on the Encode tab so you can check it first.

- The panel shows size in bytes and bits, and the estimated audio length.
- Each character takes about 8.4 seconds of audio, so keep payloads short.
- The payload is limited to 2,400 characters after the recipe. Operations such
  as To Hex or To Base64 make text longer.
- "Generate WAV" encodes the payload, not the original message.


SIGNAL FORMAT
-------------
2 second lead tone (2000 Hz)
Then each byte, most significant bit first:
   1 second tone per bit (1000 Hz = 0, 2000 Hz = 1) plus a 50 ms gap
2 second end tone (2000 Hz)

Audio is 44.1 kHz, mono, 16-bit PCM WAV. Text is encoded as UTF-8.


IMPORTANT NOTES
---------------
- Use the original WAV file for decoding. MP3, AAC and other compressed
  formats, or files re-sent through messaging apps, can distort the tones and
  make decoding fail.
- If you lose the password for an .aenc file, it cannot be recovered.
- The encoding in "Encode message" hides text in sound but is NOT encryption.
  Anyone with the right decoder can read it unless you add recipe steps or
  encrypt the file.
- Only some operations in the library are runnable. The others are listed in
  the catalogue and shown greyed out.


PRIVACY
-------
All processing happens in your browser. No files, messages or passwords are
sent anywhere.


LICENSE
-------
Add your license here (for example MIT).


CREDITS
-------
Created by Yaswanth Maruthi.
