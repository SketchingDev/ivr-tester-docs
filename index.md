---
title: Home
layout: home
nav_order: 1
---

# IVR Tester: Automate the testing of IVRs

IVR Tester automates the testing of IVR flows by calling them, interpreting prompts and replying with DTMF tones based
on fluent test definitions.

<p class="text-center">
  <img src="assets/images/cli/demo.gif">
</p>

Features:
* Fully automates testing call flows
* Test multiple scenarios in parallel
* Expressive test definitions help document call flow
* Record audio of tests
* Record transcriptions of tests
* Supports Google Speech-to-Text and AWS Transcript for transcribing calls
* Open-source

```typescript
const config = { transcriber: googleSpeechToText({ languageCode: "en-GB" }) };

new IvrTester(config).run(
  { from: "0123 456 789", to: "0123 123 123" },
  {
    name: "Customer is provided a menu after their account number confirmed",
    steps: [
      {
        whenPrompt: similarTo("Please enter your account number"),
        then: press("184748"),
        silenceAfterPrompt: 3000,
        timeout: 6000,
      },
      {
        whenPrompt: similarTo(
          "press 1 for booking a repair or 2 for changing your address"
        ),
        then: hangUp(),
        silenceAfterPrompt: 3000,
        timeout: 6000,
        },
     ],
  }
);
```
