---
title: 'How To Create An Audio/Video Recording App With React Native: An In-Depth Tutorial'
slug: audio-video-recording-react-native-expo
author: oleh-mryhlod
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/099c0951-0860-4dfb-ab88-34d866c54f54/video-recording-ui-800w.png
date: 2018-04-19T12:15:26+02:00
summary: >-
  Not all developers are aware of how useful React Native actually is. Here are some tips on how to create an audio and video recording app by using Expo development tools.
description: >-
  Not all developers are aware of how useful React Native actually is. Here are some tips on how to create an audio and video recording app by using Expo development tools.
categories:
  - Performance
  - React
  - Native
  - JavaScript
  - Apps
---
<p>React Native is a young technology, already gaining popularity among developers. It is a great option for smooth, fast, and efficient mobile app development. High-performance rates for mobile environments, code reuse, and a strong community: These are just some of the benefits React Native provides.</p>

<p>In this guide, I will share some insights about the high-level capabilities of React Native and the products you can develop with it in a short period of time.</p>

<p>We will delve into the step-by-step process of creating a video/audio recording app with React Native and <a href="https://expo.io/">Expo</a>.  Expo is an open-source toolchain built around React Native for developing iOS and Android projects with React and JavaScript. It provides a bunch of native APIs maintained by native developers and the open-source community.</p>

<p>After reading this article, you should have all the necessary knowledge to create video/audio recording functionality with React Native.</p>

<p>Let's get right to it.</p>

## Brief Description Of The Application

<p>The application you will learn to develop is called a multimedia notebook. I have implemented part of this functionality in an online job board application for the film industry. The main goal of this mobile app is to connect people who work in the film industry with employers. They can create a profile, add a video or audio introduction, and apply for jobs.</p>

<p>The application consists of three main screens that you can switch between with the help of a tab navigator:</p>

<ul>
<li>the audio recording screen,</li>
<li>the video recording screen,</li>
<li>a screen with a list of all recorded media and functionality to play back or delete them.</li>
</ul>

<p><em>Check out how this app works by <a href="https://expo.io/@apiko_dev/multimedia-notes">opening this link with Expo</a>, but please note that opening the app on iOS with the latest expo version (SDK 26) can't be performed (falling back to Apple's guidelines).
The iOS client will no longer be able to open projects published by other Expo users. You will only be able to open projects published by the same account that’s signed into the Expo client.
The Android client will continue with the same functionality as always.</em></p>

{{% feature-panel %}}

<p>First, download Expo to your mobile phone. There are two options to open the project :</p>

<ol>
<li>Open the link in the browser, scan the QR code with your mobile phone, and wait for the project to load.</li>
<li>Open the link with your mobile phone and click on “Open project using Expo”.</li>
</ol>

<p>You can also open the app in the browser. Click on “Open project in the browser”. If you have a paid account on <a href="https://appetize.io/">Appetize.io</a>, visit it and enter the code in the field to open the project. If you don’t have an account, click on “Open project” and wait in an account-level queue to open the project.</p>

<p>However, I recommend that you download the Expo app and open this project on your mobile phone to check out all of the features of the video and audio recording app.</p>

<p><em>You can find the full code for the media recording app in the <a href="https://github.com/apiko-dev/Multimedia-Notes">repository</a> on GitHub.</em></p>

### Dependencies Used For App Development

<p>As mentioned, the media recording app is developed with React Native and Expo.</p>

<p>You can see the full list of dependencies in the repository’s <code>package.json</code> file.</p>

<p>These are the main libraries used:</p>

<ul>
<li>React-navigation, for navigating the application,</li>
<li>Redux, for saving the application’s state,</li>
<li>React-redux, which are React bindings for Redux,</li>
<li>Recompose, for writing the components’ logic,</li>
<li>Reselect, for extracting the state fragments from Redux.</li>
</ul>

<p>Let's look at the project's structure:</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8d47762c-3e33-4bdf-a2c2-d0c4d66ff6f6/project-s-structure.png" sizes="70vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8d47762c-3e33-4bdf-a2c2-d0c4d66ff6f6/project-s-structure.png'>Large preview</a>" alt="" >}}

<ul>
<li><code>src/index.js</code>: root app component imported in the <code>app.js</code> file;</li>
<li><code>src/components</code>: reusable components;</li>
<li><code>src/constants</code>: global constants;</li>
<li><code>src/styles</code>: global styles, colors, fonts sizes and dimensions.</li>
<li><code>src/utils</code>: useful utilities and recompose enhancers;</li>
<li><code>src/screens</code>: screens components;</li>
<li><code>src/store</code>: Redux store;</li>
<li><code>src/navigation</code>: application’s navigator;</li>
<li><code>src/modules</code>: Redux modules divided by entities as modules/audio, modules/video, modules/navigation.</li>
</ul>

<p>Let’s proceed to the practical part.</p>

## Create Audio Recording Functionality With React Native

<p>First, it's important to сheck the <a href="https://docs.expo.io/versions/latest/sdk/audio.html">documentation for the Expo Audio API</a>, related to audio recording and playback. You can see all of the code in the <a href="https://github.com/apiko-dev/Multimedia-Notes">repository</a>. I recommend opening the code as you read this article to better understand the process.</p>

<p>When launching the application for the first time, you’ll need the user's permission for audio recording, which entails access to the microphone. Let's use <code>Expo.AppLoading</code> and ask permission for recording by using <code>Expo.Permissions</code> (see the <code>src/index.js</code>) during <code>startAsync</code>.</p>

<p><strong>Await</strong> <code>Permissions.askAsync(Permissions.AUDIO_RECORDING);</code></p>

<p>Audio recordings are displayed on a seperate screen whose UI changes depending on the state.</p>

<p>First, you can see the button “Start recording”. After it is clicked, the audio recording begins, and you will find the current audio duration on the screen. After stopping the recording, you will have to type the recording’s name and save the audio to the <strong>Redux store</strong>.</p>

<p>My audio recording UI looks like this:</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d729edd-0fd1-40f5-bc89-3613b916eac1/audio-recording-ui.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d729edd-0fd1-40f5-bc89-3613b916eac1/audio-recording-ui.png'>Large preview</a>" alt="" >}}

<p>I can save the audio in the <strong>Redux store</strong> in the following format:</p>

<pre><code class="language-javascript">audioItemsIds: [‘id1’, ‘id2’],
audioItems: {
 ‘id1’: {
    id: string,
    title: string,
    recordDate: date string,
    duration: number,
    audioUrl: string,
 }
},</code></pre>

<p>Let’s write the audio logic by using Recompose in the screen’s container <code>src/screens/RecordAudioScreenContainer</code>.</p>

<p>Before you start recording, customize the audio mode with the help of <code>Expo.Audio.set.AudioModeAsync</code> (mode), where mode is the dictionary with the following <strong>key-value pairs</strong>:</p>

<ul>
<li><code>playsInSilentModeIOS</code>: A boolean selecting whether your experience’s audio should play in silent mode on iOS. This value defaults to false.</li>
<li><code>allowsRecordingIOS</code>: A boolean selecting whether recording is enabled on iOS. This value defaults to false. Note: When this flag is set to true, playback may be routed to the phone receiver, instead of to the speaker.</li>
<li><code>interruptionModeIOS</code>: An enum selecting how your experience’s audio should interact with the audio from other apps on iOS.</li>
<li><code>shouldDuckAndroid</code>: A boolean selecting whether your experience’s audio should automatically be lowered in volume (“duck”) if audio from another app interrupts your experience. This value defaults to true. If false, audio from other apps will pause your audio.</li>
<li><code>interruptionModeAndroid</code>: An enum selecting how your experience’s audio should interact with the audio from other apps on Android.</li>
</ul>

<p><strong>Note</strong>: <em>You can learn more about the customization of <strong>AudioMode</strong> in <a href="https://docs.expo.io/versions/latest/sdk/audio.html#expoaudiosetaudiomodeasyncmode">the documentation</a>.</em></p>

<p>I have used the following values in this app:</p>

<p><code>interruptionModeIOS: Audio.INTERRUPTION_MODE_IOS_DO_NOT_MIX</code>, &mdash; Our record interrupts audio from other apps on IOS.</p>

<p><code>playsInSilentModeIOS</code>: <strong>true</strong>,</p>

<p><code>shouldDuckAndroid</code>: <strong>true</strong>,</p>

<p><code>interruptionModeAndroid: Audio.INTERRUPTION_MODE_ANDROID_DO_NOT_MIX</code> &mdash; Our record interrupts audio from other apps on Android.</p>

<p><code>allowsRecordingIOS</code> Will change to true before the audio recording and to false after its completion.</p>

<p>To implement this, let's write the handler <code>setAudioMode</code> with <strong>Recompose</strong>.</p>

<div class="break-out">

<pre><code class="language-javascript">withHandlers({
 setAudioMode: () => async ({ allowsRecordingIOS }) => {
   try {
     await Audio.setAudioModeAsync({
       allowsRecordingIOS,
       interruptionModeIOS: Audio.INTERRUPTION_MODE_IOS_DO_NOT_MIX,
       playsInSilentModeIOS: true,
       shouldDuckAndroid: true,
       interruptionModeAndroid: Audio.INTERRUPTION_MODE_ANDROID_DO_NOT_MIX,
     });
   } catch (error) {
     console.log(error) // eslint-disable-line
   }
 },
}),</code></pre></div>

<p>To record the audio, you’ll need to create an instance of the <code>Expo.Audio.Recording class</code>.</p>

<pre><code class="language-javascript">const recording = new Audio.Recording();</code></pre>

<p>After creating the recording instance, you will be able to receive the <strong>status of the Recording</strong> with the help of <code>recordingInstance.getStatusAsync()</code>.</p>

<p>The status of the recording is a dictionary with the following key-value pairs:</p>

<ul>
<li><code>canRecord:</code> a boolean.</li>
<li><code>isRecording:</code> a boolean describing whether the recording is currently recording.</li>
<li><code>isDoneRecording:</code> a boolean.</li>
<li><code>durationMillis:</code> current duration of the recorded audio.</li>
</ul>

<p>You can also set a function to be called at regular intervals with <code>recordingInstance.setOnRecordingStatusUpdate(onRecordingStatusUpdate).</code></p>

<p>To update the UI, you will need to call <code>setOnRecordingStatusUpdate</code> and set your own callback.</p>

<p>Let’s add some props and a recording callback to the container.</p>

<div class="break-out">

<pre><code class="language-javascript">withStateHandlers({
    recording: null,
    isRecording: false,
    durationMillis: 0,
    isDoneRecording: false,
    fileUrl: null,
    audioName: '',
  }, {
    setState: () => obj => obj,
    setAudioName: () => audioName => ({ audioName }),
   recordingCallback: () => ({ durationMillis, isRecording, isDoneRecording }) =>
      ({ durationMillis, isRecording, isDoneRecording }),
  }),</code></pre></div>

<p>The callback setting for <code>setOnRecordingStatusUpdate</code> is:</p>

<p><code>recording.setOnRecordingStatusUpdate(props.recordingCallback);</code></p>

<p><code>onRecordingStatusUpdate</code> is called every 500 milliseconds by default. To make the UI update valid, set the 200 milliseconds interval with the help of <code>setProgressUpdateInterval</code>:</p>

<p><code>recording.setProgressUpdateInterval(200);</code></p>

<p>After creating an instance of this class, call <code>prepareToRecordAsync</code> to record the audio.</p>

<p><code>recordingInstance.prepareToRecordAsync(options)</code> loads the recorder into memory and prepares it for recording. It must be called before calling <code>startAsync()</code>. This method can be used if the <strong>recording instance</strong> has never been prepared.</p>

<p>The parameters of this method include such options for the recording as sample rate, bitrate, channels, format, encoder and extension. You can find a list of all recording options in this <a href="https://docs.expo.io/versions/latest/sdk/audio.html#recordingoptions">document</a>.</p>

<p>In this case, let’s use <code>Audio.RECORDING_OPTIONS_PRESET_HIGH_QUALITY</code>.</p>

<p>After the recording has been prepared, you can start recording by calling the method <code>recordingInstance.startAsync()</code>.</p>

<p>Before creating a new <strong>recording instance</strong>, check whether it has been created before. <strong>The handler</strong> for beginning the recording looks like this:</p>

<div class="break-out">

<pre><code class="language-javascript">onStartRecording: props => async () => {
      try {
        if (props.recording) {
          props.recording.setOnRecordingStatusUpdate(null);
          props.setState({ recording: null });
        }

        await props.setAudioMode({ allowsRecordingIOS: true });

        const recording = new Audio.Recording();
        recording.setOnRecordingStatusUpdate(props.recordingCallback);
        recording.setProgressUpdateInterval(200);

        props.setState({ fileUrl: null });

await recording.prepareToRecordAsync(Audio.RECORDING_OPTIONS_PRESET_HIGH_QUALITY);
        await recording.startAsync();

        props.setState({ recording });
      } catch (error) {
        console.log(error) // eslint-disable-line
      }
    },</code></pre></div>

<p>Now you need to write a <strong>handler</strong> for the audio recording completion. After clicking the stop button, you have to stop the recording, disable it on iOS, receive and save the local URL of the recording, and set <code>OnRecordingStatusUpdate</code> and the <strong>recording instance to null</strong>:</p>

<div class="break-out">

<pre><code class="language-javascript">onEndRecording: props => async () => {
      try {
        await props.recording.stopAndUnloadAsync();
        await props.setAudioMode({ allowsRecordingIOS: false });
      } catch (error) {
        console.log(error); // eslint-disable-line
      }

      if (props.recording) {
        const fileUrl = props.recording.getURI();
        props.recording.setOnRecordingStatusUpdate(null);
        props.setState({ recording: null, fileUrl });
      }
    },</code></pre></div>

<p>After this, type the audio name, click the <strong>“continue”</strong> button, and the audio note will be saved in the <strong>Redux store</strong>.</p>

<pre><code class="language-javascript">onSubmit: props => () => {
      if (props.audioName && props.fileUrl) {
        const audioItem = {
          id: uuid(),
          recordDate: moment().format(),
          title: props.audioName,
          audioUrl: props.fileUrl,
          duration: props.durationMillis,
        };

        props.addAudio(audioItem);
        props.setState({
          audioName: '',
          isDoneRecording: false,
        });

        props.navigation.navigate(screens.LibraryTab);
      }
    },</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1be2e40f-3e37-48f0-9047-5fe0483f5c6e/recordaudio.gif"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1be2e40f-3e37-48f0-9047-5fe0483f5c6e/recordaudio.gif" width="384" height="680" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1be2e40f-3e37-48f0-9047-5fe0483f5c6e/recordaudio.gif">Large preview</a>)</figcaption></figure>

## Audio Playback With React Native

<p>You can play the audio on the screen with the saved audio notes. To start the audio playback, click one of the items on the list. Below, you can see the audio player that allows you to track the current position of playback, to set the playback starting point and to toggle the playing audio.</p>

<p>Here’s what my audio playback UI looks like:</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5dbf7c5-3b4b-463e-8bc5-37f842df6534/audio-playback-ui.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5dbf7c5-3b4b-463e-8bc5-37f842df6534/audio-playback-ui.png'>Large preview</a>" alt="" >}}

<p><a href="https://docs.expo.io/versions/latest/sdk/av.html">The Expo.Audio.Sound objects and Expo.Video components</a> share a unified imperative API for media playback.</p>

<p>Let's write the logic of the audio playback by using Recompose in the screen container <code>src/screens/LibraryScreen/LibraryScreenContainer</code>, as the audio player is available only on this screen.</p>

<p>If you want to display the player at any point of the application, I recommend writing the logic of the player and audio playback in <strong>Redux operations</strong> using <strong>redux-thunk</strong>.</p>

<p>Let's customize the audio mode in the same way we did for the audio recording. First, set <code>allowsRecordingIOS</code> to <strong>false</strong>.</p>

<div class="break-out">

<pre><code class="language-javascript">lifecycle({
    async componentDidMount() {
      await Audio.setAudioModeAsync({
        allowsRecordingIOS: false,
        interruptionModeIOS: Audio.INTERRUPTION_MODE_IOS_DO_NOT_MIX,
        playsInSilentModeIOS: true,
        shouldDuckAndroid: true,
        interruptionModeAndroid: Audio.INTERRUPTION_MODE_ANDROID_DO_NOT_MIX,
      });
    },
  }),</code></pre></div>

<p>We have created the <strong>recording instance</strong> for audio recording. As for audio playback, we need to create the <strong>sound instance</strong>. We can do it in two different ways:</p>

<ol>
<li><code>const playbackObject = new Expo.Audio.Sound();</code></li>
<li><code>Expo.Audio.Sound.create(source, initialStatus = {}, onPlaybackStatusUpdate = null, downloadFirst = true)</code></li>
</ol>

<p>If you use the first method, you will need to call <code>playbackObject.loadAsync()</code>, which loads the media from source into memory and prepares it for playing, after creation of the instance.</p>

<p>The second method is a static convenience method to construct and load a sound. It сreates and loads a sound from source with the optional <code>initialStatus</code>, <code>onPlaybackStatusUpdate</code> and <code>downloadFirst</code> parameters.</p>

<p>The source parameter is the source of the sound. It supports the following forms:</p>

<ul>
<li>a dictionary of the form <code>{ uri: 'https://path/to/file' }</code> with a network URL pointing to an audio file on the web;</li>
<li><code>require('path/to/file')</code> for an audio file asset in the source code directory;</li>
<li>an <a href="https://docs.expo.io/versions/latest/sdk/asset.html">Expo.Asset</a> object for an audio file asset.</li>
</ul>

<p><code>The initialStatus</code> parameter is the initial playback status. <code>PlaybackStatus</code> is the structure returned from all playback API calls describing the state of the <code>playbackObject</code> at that point of time. It is a dictionary with the key-value pairs. You can check all of the keys of the <code>PlaybackStatus</code> in the <a href="https://docs.expo.io/versions/latest/sdk/av.html#playback-status">documentation</a>.</p>

<p><code>onPlaybackStatusUpdate</code> is a function taking a single parameter, <code>PlaybackStatus</code>. It is called at regular intervals while the media is in the loaded state. The interval is 500 milliseconds by default. In my application, I set it to 50 milliseconds interval for a proper UI update.</p>

<p>Before creating the sound instance, you will need to implement the <code>onPlaybackStatusUpdate callback</code>. First, add some props to the screen container:</p>

<pre><code class="language-javascript">withClassVariableHandlers({
    playbackInstance: null,
    isSeeking: false,
    shouldPlayAtEndOfSeek: false,
    playingAudio: null,
  }, 'setClassVariable'),
  withStateHandlers({
    position: null,
    duration: null,
    shouldPlay: false,
    isLoading: true,
    isPlaying: false,
    isBuffering: false,
    showPlayer: false,
  }, {
    setState: () => obj => obj,
  }),</code></pre>

<p>Now, implement <code>onPlaybackStatusUpdate</code>. You will need to make several validations based on <code>PlaybackStatus</code> for a proper UI display:</p>

<div class="break-out">

<pre><code class="language-javascript">withHandlers({
    soundCallback: props => (status) => {
      if (status.didJustFinish) {
        props.playbackInstance().stopAsync();
      } else if (status.isLoaded) {
        const position = props.isSeeking()
          ? props.position
          : status.positionMillis;
        const isPlaying = (props.isSeeking() || status.isBuffering)
          ? props.isPlaying
          : status.isPlaying;
        props.setState({
          position,
          duration: status.durationMillis,
          shouldPlay: status.shouldPlay,
          isPlaying,
          isBuffering: status.isBuffering,
        });
      }
    },
  }),</code></pre></div>

<p>After this, you have to implement a handler for the audio playback. If a sound instance is already created, you need to unload the media from memory by calling <code>playbackInstance.unloadAsync()</code> and clear <code>OnPlaybackStatusUpdate</code>:</p>

<div class="break-out">

<pre><code class="language-javascript">loadPlaybackInstance: props => async (shouldPlay) => {
      props.setState({ isLoading: true });

      if (props.playbackInstance() !== null) {
        await props.playbackInstance().unloadAsync();
        props.playbackInstance().setOnPlaybackStatusUpdate(null);
        props.setClassVariable({ playbackInstance: null });
      }
      const { sound } = await Audio.Sound.create(
        { uri: props.playingAudio().audioUrl },
        { shouldPlay, position: 0, duration: 1, progressUpdateIntervalMillis: 50 },
        props.soundCallback,
      );

      props.setClassVariable({ playbackInstance: sound });

      props.setState({ isLoading: false });
    },</code></pre></div>

<p>Call the handler <code>loadPlaybackInstance(true)</code> by clicking the item in the list. It will automatically load and play the audio.</p>

<p>Let's add the pause and play functionality (toggle playing) to the audio player. If audio is already playing, you can pause it with the help of <code>playbackInstance.pauseAsync()</code>.  If audio is paused, you can resume playback from the paused point with the help of the <code>playbackInstance.playAsync()</code> method:</p>

<pre><code class="language-javascript">onTogglePlaying: props => () => {
      if (props.playbackInstance() !== null) {
        if (props.isPlaying) {
          props.playbackInstance().pauseAsync();
        } else {
          props.playbackInstance().playAsync();
        }
      }
    },</code></pre>

<p>When you click on the playing item, it should stop. If you want to stop audio playback and put it into the 0 playing position, you can use the method <code>playbackInstance.stopAsync()</code>:</p>

<pre><code class="language-javascript">onStop: props => () => {
      if (props.playbackInstance() !== null) {
        props.playbackInstance().stopAsync();

        props.setShowPlayer(false);
        props.setClassVariable({ playingAudio: null });
      }
    },</code></pre>

<p>The audio player also allows you to rewind the audio with the help of the slider. When you start sliding, the audio playback should be paused with <code>playbackInstance.pauseAsync()</code>.</p>

<p>After the sliding is complete, you can set the audio playing position with the help of <code>playbackInstance.setPositionAsync(value)</code>, or play back the audio from the set position with <code>playbackInstance.playFromPositionAsync(value)</code>:</p>

<div class="break-out">

<pre><code class="language-javascript">onCompleteSliding: props => async (value) => {
      if (props.playbackInstance() !== null) {
        if (props.shouldPlayAtEndOfSeek) {
          await props.playbackInstance().playFromPositionAsync(value);
        } else {
          await props.playbackInstance().setPositionAsync(value);
        }
        props.setClassVariable({ isSeeking: false });
      }
    },</code></pre></div>

<p>After this, you can pass the props to the components <code>MediaList</code> and <code>AudioPlayer</code> (see the file <code>src/screens/LibraryScreen/LibraryScreenView</code>).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c639efb-c541-4213-bc37-fddfae15d831/playbackaudio.gif"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c639efb-c541-4213-bc37-fddfae15d831/playbackaudio.gif" width="384" height="680" alt="" /></a></figure>

## Video Recording Functionality With React Native

<p>Let's proceed to video recording.</p>

<p>We’ll use <code>Expo.Camera</code> for this purpose. <code>Expo.Camera</code> is a React component that renders a preview of the device’s front or back camera. <code>Expo.Camera</code> can also take photos and record videos that are saved to the app’s cache.</p>

<p>To record video, you need permission for access to the camera and microphone. Let's add the request for camera access as we did with the audio recording (in the file <code>src/index.js</code>):</p>

<pre><code class="language-javascript">await Permissions.askAsync(Permissions.CAMERA);</code></pre>

<p>Video recording is available on the “Video Recording” screen. After switching to this screen, the camera will turn on.</p>

<p>You can change the camera type (front or back) and start video recording. During recording, you can see its general duration and can cancel or stop it. When recording is finished, you will have to type the name of the video, after which it will be saved in the <strong>Redux store</strong>.</p>

<p>Here is what my video recording UI looks like:</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c3bceb69-985d-4765-bf48-e32b347e510e/video-recording-ui.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c3bceb69-985d-4765-bf48-e32b347e510e/video-recording-ui.png'>Large preview</a>" alt="" >}}

<p>Let’s write the video recording logic by using Recompose on the container screen

<code>src/screens/RecordVideoScreen/RecordVideoScreenContainer</code>.</p>

<p>You can see the full list of all props in the <code>Expo.Camera</code> component in <a href="https://docs.expo.io/versions/latest/sdk/camera.html#props">the document</a>.</p>

<p>In this application, we will use the following props for <code>Expo.Camera</code>.</p>

<ul>
<li><code>type</code>: The camera type is set (front or back).</li>
<li><code>onCameraReady</code>: This callback is invoked when the camera preview is set. You won't be able to start recording if the camera is not ready.</li>
<li><code>style</code>: This sets the styles for the camera container. In this case, the size is 4:3.</li>
<li><code>ref</code>: This is used for direct access to the camera component.</li>
</ul>

<p>Let's add the variable for saving the type and handler for its changing.</p>

<pre><code class="language-javascript">cameraType: Camera.Constants.Type.back,
toggleCameraType: state => () => ({
      cameraType: state.cameraType === Camera.Constants.Type.front
        ? Camera.Constants.Type.back
        : Camera.Constants.Type.front,
    }),</code></pre>

<p>Let's add the variable for saving the camera ready state and callback for <code>onCameraReady</code>.</p>

<pre><code class="language-javascript">isCameraReady: false,

setCameraReady: () => () => ({ isCameraReady: true }),</code></pre>

<p>Let's add the variable for saving the camera component reference and setter.</p>

<pre><code class="language-javascript">cameraRef: null,

setCameraRef: () => cameraRef => ({ cameraRef }),</code></pre>

<p>Let's pass these variables and handlers to the camera component.</p>

<pre><code class="language-javascript">&lt;Camera
          type={cameraType}
          onCameraReady={setCameraReady}
          style={s.camera}
          ref={setCameraRef}
        /></code></pre>

<p>Now, when calling <code>toggleCameraType</code> after clicking the button, the camera will switch from the front to the back.</p>

<p>Currently, we have access to the camera component via the reference, and we can start video recording with the help of <code>cameraRef.recordAsync()</code>.</p>

<p>The method <code>recordAsync</code> starts recording a video to be saved to the cache directory.</p>

#### Arguments:

<p>Options (object) &mdash; a map of options:</p>

<ul>
<li><code>quality</code> (VideoQuality): Specify the quality of recorded video. Usage: Camera.Constants.VideoQuality['<value>'], possible values: for 16:9 resolution 2160p, 1080p, 720p, 480p (Android only) and for 4:3 (the size is 640x480). If the chosen quality is not available for the device, choose the highest one.</li>
<li><code>maxDuration</code> (number): Maximum video duration in seconds.</li>
<li><code>maxFileSize</code> (number): Maximum video file size in bytes.</li>
<li><code>mute</code> (boolean): If present, video will be recorded with no sound.</li>
</ul>

<p><code>recordAsync</code> returns a promise that resolves to an object containing the video file’s URI property. You will need to save the file’s URI in order to play back the video hereafter. The promise is returned if <code>stopRecording</code> was invoked, one of <code>maxDuration</code> and <code>maxFileSize</code> is reached or the camera preview is stopped.</p>

<p>Because the ratio set for the camera component sides is 4:3, let's set the same format for the video quality.</p>

<p>Here is what the handler for starting video recording looks like (see the full code of the container in the repository):</p>

<div class="break-out">

<pre><code class="language-javascript">onStartRecording: props => async () => {
      if (props.isCameraReady) {
        props.setState({ isRecording: true, fileUrl: null });
        props.setVideoDuration();
        props.cameraRef.recordAsync({ quality: '4:3' })
          .then((file) => {
            props.setState({ fileUrl: file.uri });
          });
      }
    },</code></pre></div>

<p>During the video recording, we can’t receive the recording status as we have done for audio. That's why I have created a function to set video duration.</p>

<p>To stop the video recording, we have to call the following function:</p>

<pre><code class="language-javascript">stopRecording: props => () => {
      if (props.isRecording) {
        props.cameraRef.stopRecording();
        props.setState({ isRecording: false });
        clearInterval(props.interval);
      }
    },</code></pre>

<p>Check out the entire process of video recording.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/156ff42c-4a55-4510-b02f-e62302e7fb9e/recordvideo.gif"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/156ff42c-4a55-4510-b02f-e62302e7fb9e/recordvideo.gif" width="320" height="584" alt="" /></a></figure>

## Video Playback Functionality With React Native

<p>You can play back the video on the “Library” screen. Video notes are located in the “Video” tab.</p>

<p>To start the video playback, click the selected item in the list. Then, switch to the playback screen, where you can watch or delete the video.</p>

<p>The UI for video playback looks like this:</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/52f5acaf-2a76-4cae-bea1-17cb3a3b090a/video-playback-ui.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/52f5acaf-2a76-4cae-bea1-17cb3a3b090a/video-playback-ui.png'>Large preview</a>" alt="" >}}

<p>To play back the video, use <code>Expo.Video</code>, a component that displays a video inline with the other React Native UI elements in your app.</p>

<p>The video will be displayed on the separate screen, PlayVideo.</p>

<p>You can check out all of the <a href="https://docs.expo.io/versions/latest/sdk/video.html#props">props for Expo.Video here</a>.</p>

<p>In our application, the <code>Expo.Video</code> <strong>component</strong> uses native playback controls and looks like this:</p>

<pre><code class="language-javascript">&lt;Video
        source={{ uri: videoUrl }}
        style={s.video}
        shouldPlay={isPlaying}
        resizeMode="contain"
        useNativeControls={isPlaying}
        onLoad={onLoad}
        onError={onError}
      /></code></pre>

<ul>
<li><code>source</code><br />

This is the source of the video data to display. The same forms as for Expo.Audio.Sound are supported.</li>
<li><code>resizeMode</code><br />

This is a string describing how the video should be scaled for display in the component view’s bounds. It can be “stretch”, “contain” or “cover”.</li>
<li><code>shouldPlay</code><br />

This boolean describes whether the media is supposed to play.</li>
<li><code>useNativeControls</code><br />

This boolean, if set to true, displays native playback controls (such as play and pause) within the video component.</li>
<li><code>onLoad</code><br />

This function is called once the video has been loaded.</li>
<li><code>onError</code><br />

This function is called if loading or playback has encountered a fatal error. The function passes a single error message string as a parameter.</li>
</ul>

<p>When the video is uploaded, the play button should be rendered on top of it.</p>

<p>When you click the play button, the video turns on and the native playback controls are displayed.</p>

<p>Let’s write the logic of the video using Recompose in the screen container <code>src/screens/PlayVideoScreen/PlayVideoScreenContainer</code>:</p>

<div class="break-out">

<pre><code class="language-javascript">const defaultState = {
  isError: false,
  isLoading: false,
  isPlaying: false,
};

const enhance = compose(
  paramsToProps('videoUrl'),
  withStateHandlers({
    ...defaultState,
    isLoading: true,
  }, {
    onError: () => () => ({ ...defaultState, isError: true }),
    onLoad: () => () => defaultState,
   onTogglePlaying: ({ isPlaying }) => () => ({ ...defaultState, isPlaying: !isPlaying }),
  }),
);</code></pre></div>

<p>As previously mentioned, the <code>Expo.Audio.Sound</code> objects and <code>Expo.Video</code> components share a unified imperative API for media playback. That's why you can create custom controls and use more advanced functionality with the Playback API.</p>

<p>Check out the video playback process:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d293d27c-b85f-446a-a3da-4bd7d74de879/playbackvideo.gif"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d293d27c-b85f-446a-a3da-4bd7d74de879/playbackvideo.gif" width="320" height="568" alt="" /></a></figure>

<p>See the full code for the application in the <a href="https://github.com/apiko-dev/Multimedia-Notes">repository</a>.</p>

<p>You can also install the app on your phone by using <a href="https://expo.io/@apiko_dev/multimedia-notes">Expo</a> and check out how it works in practice.</p>

## Wrapping Up

<p>I hope you have enjoyed this article and have enriched your knowledge of React Native. You can use this audio and video recording tutorial to create your own custom-designed media player. You can also scale the functionality and add the ability to save media in the phone’s memory or on a server, synchronize media data between different devices, and share media with others.</p>

<p>As you can see, there is a wide scope for imagination. If you have any questions about the process of developing an audio or video recording app with React Native, feel free to drop a comment below.</p>

{{< signature "da, lf, ra, yk, al, il" >}}

