---
title: How it Works 
layout: home
nav_order: 2
---

# How it works

<p class="text-center">
  <img src="assets/images/flow.jpg">
</p>

Under the hood this orchestrates:
1. Establishing a bi-directional audio stream of the call to the IVR flow - using [Twilio](https://www.twilio.com/)
2. Transcribing the voice responses from the flow - using [Google Speech-to-Text](https://cloud.google.com/speech-to-text)
3. Using the test to conditionally respond with DTMF tones to transcripts
