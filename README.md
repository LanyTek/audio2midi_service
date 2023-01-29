# LanyTek Audio2Midi Transcription

Our service allows users to easily convert music audio files or YouTube links into MIDI and PDF files of the corresponding sheet music.

Whether you’re a musician looking to transcribe your own performances, or a music educator looking to create sheet music for your students, our service makes it easy to get the files you need.

Our state-of-the-art AI algorithms are able to accurately transcribe even the most complex pieces of music, and our user-friendly interface makes it simple for anyone to use.

We’re excited for you to try it out, and we’re confident that you’ll be impressed with the results!

## Usage

### Transcribe from Youtube URL

```
import time

import requests

X_RAPIDAPI_KEY = "<YOUR_RAPID_API_KEY"

url = "https://lanytek-audio2midi.p.rapidapi.com/audios/gen-from-youtube"

querystring = {
    "url": "https://www.youtube.com/watch?v=lRVTVB94zTg&ab_channel=Passenger"
}

headers = {
    "content-type": "application/json",
    "X-RapidAPI-Key": X_RAPIDAPI_KEY,
    "X-RapidAPI-Host": "lanytek-audio2midi.p.rapidapi.com",
}

# submit translation request
response = requests.request("POST", url, json={}, headers=headers, params=querystring)

request_id = response.json()["requestId"]
print(f"request_id: {request_id}")

# wait for translation to be ready
while True:
    time.sleep(10)

    url = "https://lanytek-audio2midi.p.rapidapi.com/audios"

    querystring = {"req_id": request_id}

    headers = {
        "X-RapidAPI-Key": X_RAPIDAPI_KEY,
        "X-RapidAPI-Host": "lanytek-audio2midi.p.rapidapi.com",
    }

    response = requests.request("GET", url, headers=headers, params=querystring)
    if response.status_code == 200:
        data = response.json()
        music_sheet_pdf_url = data["pdf"]
        midi_url = data["midi"]

        print(f"music_sheet_pdf_url: {music_sheet_pdf_url}")
        print(f"midi_url: {midi_url}")
        break

    print(response.json()["detail"])
```

The script demonstrated above allows you to submit a YouTube URL and receive URLs to download both the MIDI file and a PDF file of the corresponding music sheet.

### Transcribe from local file
```
import time

import requests

X_RAPIDAPI_KEY = "YOUR_RAPID_API_KEY"
FILE_PATH = "PATH_TO_AUDIO_FILE"

url = "https://lanytek-audio2midi.p.rapidapi.com/audios/gen-from-file"

payload = open(FILE_PATH, "rb").read()

headers = {
    "X-RapidAPI-Key": X_RAPIDAPI_KEY,
    "X-RapidAPI-Host": "lanytek-audio2midi.p.rapidapi.com",
}

response = requests.request("POST", url, files={"file": payload}, headers=headers)

request_id = response.json()["requestId"]
print(f"request_id: {request_id}")

# wait for translation to be ready
while True:
    time.sleep(10)

    url = "https://lanytek-audio2midi.p.rapidapi.com/audios"

    querystring = {"req_id": request_id}

    headers = {
        "X-RapidAPI-Key": X_RAPIDAPI_KEY,
        "X-RapidAPI-Host": "lanytek-audio2midi.p.rapidapi.com",
    }

    response = requests.request("GET", url, headers=headers, params=querystring)
    if response.status_code == 200:
        data = response.json()
        music_sheet_pdf_url = data["pdf"]
        midi_url = data["midi"]

        print(f"music_sheet_pdf_url: {music_sheet_pdf_url}")
        print(f"midi_url: {midi_url}")
        break

    print(response.json()["detail"])

```
The code example above demonstrates how to submit a local audio file (with a maximum size of 25 MB) and receive URLs to download the corresponding MIDI file and PDF music sheet.

## Feedback
We welcome any feedback you may have. 

If you'd like to share your thoughts with us, please feel free to send us an email at lanytek@gmail.com. 

We appreciate your input and look forward to hearing from you!
