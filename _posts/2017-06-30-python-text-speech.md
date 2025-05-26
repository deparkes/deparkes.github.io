---
layout: post
title: Python Text To Speech
date: 2017-06-30 15:30:05.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- python
tags:
- audio
- python
- sapi
- text to speech
- tts
- win32
author:
  display_name: deparkes
permalink: "/2017/06/30/python-text-speech/"
---
Text to speech is a tool available in most operating systems, and helps people with reading and sight difficulties, or can be used as part of a '<a href="https://ggulati.wordpress.com/2016/02/24/coding-jarvis-in-python-3-in-2016/">Jarvis</a>' helper on your computer. Python has a few options for dealing with text to speech, generally in the form of wrappers for speech engines.
This post goes through a few of the options available for python text to speech. I've focussed on python text to speech in windows, but there are also options out there for linux and osx systems. There are already some nice <a href="https://pythonprogramminglanguage.com/text-to-speech/">summaries of python text to speech </a>available, but hopefully this one picks up a few more package options and highlights some other functionality issues.
<h4><a href="http://amzn.to/2sjBo7A">Search for Python books on Amazon</a></h4>
<h2><strong>What is text to speech?</strong></h2>
Text to speech, or <a href="https://en.wikipedia.org/wiki/Speech_synthesis">speech synthesis</a>, is a process for turning written words into audio. Text to speech systems are generaly based on a database of stored sounds which are combined together to create words and sentences. More versatile speech engines use sound elements (known as phones or dipones) which act as building blocks for whole words. These flexible speech engines can sound rather synthetic. More specialised speech engines store whole words, at the cost of some flexibility.
The processing of text into speech is done by an 'engine'. Text to speech engines work through the following steps:
<ol>
<li>
<strong>Text analysis</strong>: interpret things like numbers as words (e.g. '1' becomes 'one') and identify segments such as phrases, clauses and sentences</li>
<li>
<strong>Linguistic Analysis</strong>: such as identifying intonation and duration of speech</li>
<li>
<strong>Wave form generation</strong>: the symbolic representation of speech is converted into sound.</li>
</ol>

| ![text to speech - speech engine]({{site.baseurl}}/assets/2017/06/800px-TTS_System.svg_.png) |
|:--:|
| *text to speech - speech engine* |

Text to speech functionality often comes 'baked in' to the operating system - for example Windows uses <a href="https://en.wikipedia.org/wiki/Microsoft_Speech_API">SAPI</a>, and Linux tends to use <a href="https://en.wikipedia.org/wiki/ESpeakNG">eSpeak</a>. There are also some non-OS based text to speech engines out there. Google Translate offers an <a href="https://stackoverflow.com/questions/9893175/google-text-to-speech-api">API </a>which you can use as straight text to speech rather than translation, and the Java-based <a href="http://mary.dfki.de/">MaryTTS </a>is an open source text to speech engine that you can set up as your own text to speech client-server.
These speech engines typically offer different 'voices' which change the sound of the audio output. <a href="https://en.wikipedia.org/wiki/Microsoft_text-to-speech_voices">Windows</a>, <a href="https://support.apple.com/kb/PH18734?locale=en_US">OSX </a>and <a href="http://espeak.sourceforge.net/voices.html">Linux </a>all have a range of voices, and you can also download and install third party voices, which you can find for <a href="http://www.zero2000.com/free-text-to-speech-natural-voices.html">free </a> or for <a href="https://www.quora.com/What-is-the-best-text-to-speech-software">purchase</a>.
<h2><strong>Python Text To Speech</strong></h2>
Python implementations of text to speech typically provide a wrapper to the text to speech functionality of the operating system, or other speech engine. There is a range of packages out there which vary in scope, complexity and maturity.
A few key features or issues that you may come across are:
<ul>
<li>Compatability with python 2.7 and 3.x - some packages have not been actively developed or maintained for some time;</li>
<li>Cross-operating system support: since text-to-speech is often OS-dependent, some developers do not attempt to support all operating systems;</li>
<li>Ability to save audio outputs: some packages focus purely on the speech, while others also provide the option to save the output as an audio file.</li>
</ul>
Based on these points, I have picked out some highlights of the text to speech modules available for Python. Unfortunately, some of the fuller-featured modules are no longer maintained. I have included them here as they give a sense of what is possiblie, and might be useful in updating more recent modules.
<h2><strong>Pytts</strong></h2>
<a href="https://pypi.python.org/pypi/pyTTS/3.0">Pytts </a>is a comprehensive text to speech package for Windows. Pytts has a <a href="http://devrel.qiniucdn.com/data/20050930111327/index.html">range of features</a> including:
<ul>
<li>speak written text</li>
<li>change voices</li>
<li>save speech to a file</li>
<li>adjust pronunciation</li>
</ul>
This <a href="https://www.blog.pythonlibrary.org/2010/04/02/python-test-to-speech-making-your-pc-talk/">article </a>has some more background information about the Pytts module. Unfortunately, Pytts is <strong>no longer maintained</strong>, and is <strong>not Python 3 compatable</strong>. If these are not issues for you, then you may find that it is a good starting point, as it has features not implemented in some of these other modules.
Example:

```python
import pyTTS
tts = pyTTS.Create()
tts.Speak('Hello, world!')
```

<h2><strong>Pyttsx</strong></h2>
<a href="https://github.com/RapidWareTech/pyttsx">Pyttsx </a>is similar to pytts, but is cross platform: it is compatible with Windows, OSX and Linux. <a href="http://pyttsx.readthedocs.io/en/latest/install.html">Pyttsx </a>does not seem to be as feature complete as pytts - in particular in being able to save output as a wav file, and the orignal code has not been updated in some time. There are however <a href="https://github.com/RapidWareTech/pyttsx/network">various forks</a> on Github which you may find achieve what you need. Some highlights include:
<ul>
<li>
<a href="https://github.com/RapidWareTech/pyttsx">RapidWareTech/pyttsx</a>: the original pyttsx</li>
<li>
<a href="https://github.com/jpercent/pyttsx/">jpercent/pyttsx</a>: Fixes <a href="https://stackoverflow.com/questions/24963638/import-pyttsx-works-in-python-2-7-but-not-in-python3">Python 3 compatibility</a>. You can also follow <a href="http://orcunyilmaz.com/coding-python/how-to-install-pyttsx-library-for-python-3.html">these instructions</a>.</li>
<li>
<a href="https://stackoverflow.com/questions/24963638/import-pyttsx-works-in-python-2-7-but-not-in-python3">gursimar/pyttsx:</a> a fork with some ability to save output to file (Windows only)</li>
</ul>
It doesn't look as though there is a single fork or version which has all of these updates and features in, so you may need to pick and chose depending on your usage.
Example:

```python
import pyttsx
engine = pyttsx.init()
engine.say('Greetings!')
engine.say('How are you today?')
engine.runAndWait()
```

<h2>DeepHorizon/tts</h2>
In some ways the <a href="https://github.com/DeepHorizons/tts">DeepHorizon implemenation</a> of a python tts wrapper is not as advanced as the other ones I have listed here. What it does have is the ability to both <strong>speak</strong> as the text is being read, and <strong>save</strong> the output to file. DeepHorizon tts is only compatible with Windows.
Example:

```python
import tts.sapi
voice = tts.sapi.Sapi()
voice.say("Hello")
voice.set_voice("Anna")
voice.create_recording('output.wav', "This will be in a wav file")
voice.rate(-5)
voice.say("This will be said slower")
```

<h2>pywin32</h2>
Many of the other packages here will rely on pywin32 to communicate with Windows drivers, and it is possible to work with the package itself.  You can download pywin32 from <a href="http://www.lfd.uci.edu/~gohlke/pythonlibs/#pywin32">here</a>, or see more discussion around this on <a href="https://stackoverflow.com/questions/4863056/how-to-install-pywin32-module-in-windows-7">Stackoverflow</a>.
You won't have some of the convenience features provided in the other wrappers, but using pywin32 is a simple, straightforward way to achieve python text to speech, and may also be useful for troubleshooting issues.
Example:

```python
import win32com.client
speaker = win32com.client.Dispatch("SAPI.SpVoice")
speaker.Speak("Hello, it works!")
```

<h2><strong>Mary TTS</strong></h2>
An alternative to a pure python approach is to build on the Java-based Mary TTS. This mature project works on a client-server basis. Once you have <a href="http://mary.dfki.de/download/">downloaded</a> and <a href="https://github.com/marytts/marytts/wiki/Local-MaryTTS-Server-Installation">installed the server</a> , you can <a href="https://github.com/marytts/marytts-txt2wav/tree/python">use python to pass text to the server</a> and retrieve the output.
You can also <a href="http://mary.dfki.de:59125/">try out Mary TTS online</a>.
<h2><strong>gTTS</strong></h2>
<a href="https://github.com/pndurette/gTTS">gTTS </a>uses the <a href="https://cloud.google.com/translate/docs/">Google Translate API</a> for TTS. I like the default Google translate voice, so this may be an attractive option in many cases. It does however put you at the <a href="https://techcrunch.com/2009/12/14/the-unofficial-google-text-to-speech-api/">mercy </a>of Google's control of its API, which will be of a particular concern if you are attempting a more 'serious' use of python text to speech.
It is worth noting that, unlike the other packages I have listed, gTTS is primarily for saving the audio output, rather than speaking it directly.
Example:

```python
from gtts import gTTS
tts = gTTS(text='Hello, world!, lang='en')
tts.save("good.mp3")
```

