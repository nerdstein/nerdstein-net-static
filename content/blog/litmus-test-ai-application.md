---
title: "A litmus test of an AI application"
date: 2024-10-31
slug: "litmus-test-ai-application"
tags: ["development"]
description: "A one-hour prototype that cost six cents — what building a conversational AI chatbot taught me about how fast this space has moved."
draft: false
---

Two years ago, if you had asked me to build a conversational chatbot that leveraged AI, I would have been discussing hundreds of thousands of dollars to build and run it. Today, I built a prototype in one hour that cost me six cents of a SaaS service. It is astonishing to know how far this space has come in such a short timeframe. While it's rare I blog at this point, I want to share more about this experience.

## The approach

I started with a simple Google search on conversational AI chatbots. This led me to Python, as all of the examples I found seemed to leverage it. Most examples leveraged OpenAI for the core of the model connectivity, model serving, microservices, and available libraries. Converting the speech to text and parsing the results to speech leveraged various tools like Google Cloud's text2speech and even more OpenAI services. To summarize and simplify: I focused on a Python based application that leveraged only OpenAI's services. 

## Key findings

I was surprised how much I enjoyed working on this. I don't code very often and I thought I was entering into a difficult task upfront. I was wrong.

**Finding 1: none of the code samples worked out of the box.** This space seems to be moving so fast that even blog posts and documentation cannot keep up (yes, even from the service providers!). This may sound bad but the code samples were helpful to get started and it was fairly straightforward to remediate.

**Finding 2: there was no free trial**. I had to pay to even do a proof of concept. I was surprised because even the system said "free trial" when I made an account. It's unclear if I was trying to leverage services that had no free trial and the error messages were opaque at best.

**Finding 3: OpenAI is trying to be "way more" than just model serving. **I was surprised to find it had a bunch of common utilities that seem adjacent to interacting with AI models, like speech to text conversion. I assume this could apply to other use cases where relevant.

**Finding 4: this was way easier than I expected**. I was shocked how seamless and easy it was to create this example. I was anticipating more immaturity in the tools, the libraries, and even the services. I had the code cobbled together from several of the examples I found within about 30 minutes. I was able to work through the errors and changes to the library within another 30 minutes. I barely consider myself a Python developer but the developer experience around this was far more straightforward than I anticipated.

**Finding 5: Python itself was up to task**. AI related use cases seem to compliment all of the various statistical, charting, and natural language processing capabilities that Python already had. The existing libraries, already hardened and matured, integrated perfectly into the AI use cases.

**Finding 6: this was way cheaper and faster than I expected**. I recognize pricing of SaaS vendors can change at any point in time. I ran at least 20 tests to get the PoC working properly. I loaded $15 into my OpenAI account and used $0.06 of it. Given the cost of GPUs, I thought it would be way more. And, the whole application ran in seconds; not minutes, hours, or even days. I recognize I was not doing any model training, but it was still impressive in terms of both the cost and performance demonstrated.

**Finding 7: stick to best practices**. I was pleased to see that OpenAI stuck to common best practices, like microservice-based APIs. Some AI tooling I have explored seem to introduce patterns, like hard-coding connections to models, that have already been improved upon in other problem spaces and don't scale. OpenAI, through microservices, is a more intuitive abstraction for developers, is more language-agnostic, and can promote better decoupling of application architecture. Other AI-related capabilities should slow down just enough to make wise choices that their adopters don't later regret.

## The code

Given I did not see one working example, the code may be helpful. It also may rot within minutes of posting this :)

```

from openai import OpenAI
import io
import sounddevice as sd
from scipy.io.wavfile import write
import os
from pathlib import Path
import warnings

```

```

# Ignore DeprecationWarning
warnings.filterwarnings("ignore", category=DeprecationWarning)

client = OpenAI(api_key = 'xxxxxxxxxxxxxxx')

def transcribe_audio(audio_file_path):
    audio_file= open(audio_file_path, "rb")
    transcription = client.audio.transcriptions.create(
        model="whisper-1",
        file=audio_file
    )
    return transcription.text
```

```

def generate_response(prompt):
    completion = client.chat.completions.create(
        model="gpt-4o-mini",
        messages=[
            {
                "role": "user",
                "content": [
                    {
                        "type": "text",
                        "text": prompt
                    }
                ]
            },
        ],
    )
    return completion.choices[0].message.content

def synthesize_speech(text, output_file_path):
    response = client.audio.speech.create(
        model="tts-1",
        voice="alloy",
        input=text
    )
    response.stream_to_file(output_file_path)

# settings
fs = 4800  # Sample rate
seconds = 3  # Duration of recording
channels = 1

# file names
input_file = Path(__file__).parent / "conversational-chatbot-recording.wav"
output_file = Path(__file__).parent / "conversational-chatbot-output.mp3"

# clean existing files
if os.path.exists(input_file):
  os.remove(input_file)
else:
  print("The recording file does not exist")

if os.path.exists(output_file):
  os.remove(output_file)
else:
  print("The output file does not exist")

# produce recording
print("Start recording now")
myrecording = sd.rec(int(seconds * fs), samplerate=fs, channels=channels)
sd.wait()  # Wait until recording is finished
print("End recording")
write(input_file, fs, myrecording)  # Save as WAV file

# transcribe the recording into text
transcribed_text = transcribe_audio(input_file)
print("Wrote recording to file")

# get a response back from openAPI
user_query = transcribed_text
response_text = generate_response(user_query)
print("Response text >>> " + response_text)

# make a recording of the speech
synthesize_speech(response_text, output_file)
print("Wrote response to file")
```

## Conclusion

For someone who doesn't do code every day, I was pleasantly surprised by the experience leveraging Python and OpenAI to develop a simple conversational chatbot. While I didn't see any working end-to-end examples, this suggests the space is innovating rapidly and I still did not find it difficult to address gaps I found. It was more affordable than I expected to run a third-party service and they offered interfaces I natively understood. I expected much more friction in getting this done and glad to be able to share more positive findings.