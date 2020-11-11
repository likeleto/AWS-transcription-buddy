# Transcription Buddy

Transcription buddy is an interactive transcript editor.

See a live demo here: https://samfredlumley.github.io/AWS-transcription-buddy/

## why?

Manual transcription has the advantage of the listener getting close to the material, but it can take a long time. Automated transcription is fast and cheap, but it isn't perfect, and you lose the insights from going through the manual transcription process.

Transcription buddy aims to provide a best of both worlds. It uses the brute force of automated transcription to start things off and provides an interactive editor to easily correct the transcript in real time by listening to the original audio. 

I couldn't find another service which was cheap, quick and easy to edit, but there is lots of other good stuff out there. For completely manual transcription, try [oTranscribe](https://otranscribe.com/). For paid, automatic transcription try [Trint](https://trint.com/). For a deeper overview of options see this [Medium article](https://medium.com/journalism-innovation/the-best-new-ways-to-transcribe-c4c342abf172).

## Amazon Transcribe features

*  Solid automatic transcription of audio
*  Punctuation
*  Speaker identification
*  Custom volcabularies 
*  Custom word removal

## Editor features

*  Linked audio and text
*  Autoscroll
*  Visualise confidence score for each word
*  Autosave
*  Highlight word on click 
*  Audio control via keybaord shortcuts

## Workflow

To use the app, you'll run jobs through the Amazon Web Services (AWS), download the output, and run the output through the app. The process could take 15 minutes or so minutes to set up, so it's probably not worth it if you have less than an hour of audio. Right now, the process also requires you to enter a few commands in your computer's terminal.

Amazon Transcribe is not free. It costs $1.44 per hour. So 10 hours costs $14.40. More pricing info [here](https://aws.amazon.com/transcribe/pricing/).

## Getting started

If this all sounds good, the following instructions will guide you through using the Amazon Transcribe and getting a copy of the project up and running.

### Prerequisites

1. Get an [Amazon Web Servives](https://aws.amazon.com/) account 
2. Setup [S3](https://aws.amazon.com/s3/) and [Transcribe](https://aws.amazon.com/transcribe/) on your AWS account
3. Install [http-server](https://www.npmjs.com/package/http-server)* or use another server

Note: http-server requires [node](https://nodejs.org/en/). The recommended way to install node is via the [node version manager](https://github.com/nvm-sh/nvm) (nvm):

1. install nvm

`curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.34.0/install.sh | bash`

2. use nvm to install node

`nvm install node`

### Transcribing with AWS

#### Cleaning audio
See bottom of this page for steps to take to clean your audio.

#### Uploading audio to S3
1. Create a bucket for your audio in S3, using the default settings
2. Upload your audio file to the bucket, using the default settings
4. Right click the file in S3 and select 'Copy Path'

#### Using Amazon Transcribe
*note you may have to set your region to US East (Ohio)) for this stage to work*
1. Navigate to the 'Transcription jobs' page
2. Create new job
3. Choose the language and dialect used by most of the speakers
4. Paste the path location of the audio (should look something like this )
5. On the next page, enable audio identification and set the number of speakers.
6. (Optional) add a custom vocabulary or filtering lists (or use mine for non-verbals)
7. Once the job is finished download the transcription (which shold be json file)

#### Installing the app
1. Clone the repository:
```
git clone https://github.com/samFredLumley/transcription-buddy
cd transcription-buddy
```
2. In the "json" folder copy the downloaded json file (suggested name "transcript.json")
3. Add your audio file to the "audio" folder
3. Launch the app
```
http-server
```
You should now be able to access the app from your browser via the url: [http://localhost:8080/](http://localhost:8080/)

#### Using the app
* Enter filenames for your audio json files and click "load audio" and "load transcript"
* Click "hyperaudio" to link the transcript to the audio playback
* You can control the audio while writing using keyboard shortcuts:

| Task        | Shortcut           |
| ------------- |:-------------:|
| go back 5s      | ctrl + , |
| skip 5s     | ctrl + .      |
| slow down | ctrl + shift + ,      |
| speed up | ctrl + shift + .      |

## Extras

### Audio recording

To work well, automated transcription services need clear audio. For recording interviews, it can help for each participant to have a microphone (e.g. the one included on [Apple headphones](https://apple.stackexchange.com/questions/248404/where-is-the-mic-located-in-apple-earphones)).

### Audio preprocessing

Two steps you can take to clean your audio after recording are noise removal (taking out constant background noise) and normalisation (raising the volume of the audio). Both can be done easily using the open source software [Audacity](https://www.audacityteam.org/).

Here's a [guide](https://opensource.com/life/14/10/how-clean-digital-recordings-using-audacity).

## Future

*  Make it not ugly
*  Streamline workflow
*  Move to something more open like Mozilla's [DeepSpeech](https://github.com/mozilla/DeepSpeech)


