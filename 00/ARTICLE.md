# Creating our first Ionic camera app

Ionic is development framework for hybrid mobile apps originally developed in [Angular](https://angular.io/) but it also has implementations for React and Vue. Hybrid applications are a sort of websites which looks like native applications and have access to the native platform layer through wrappers like Capacitor or Cordova. Hybrid mobile apps have the advantages of being very fast to develop and easier to maintain since the code can be shared between the Web, iOS and Android.

<img width="450" src="https://github.com/celerik/celerik-articles/blob/main/00/pictures/react.png?raw=true">

## The Ionic's Role

Ionic is itself provides a wide range of front-end UI components, animations and events that gives a very close look and feel to what we would have if we were using native code. Ionic by itself is not able to access the hardward's functionalities

<img width=400 src='https://images.prismic.io/ionicframeworkcom/ffa25bb6-a032-44e4-b2f6-b83c5a73226f_capacitor-homepage-top-0%402x.png?auto=compress,format&rect=0,0,1089,1220&w=1089&h=1220&q=65'>
## Prerequisites

Beforestarting our first ionic app we need to make sure that Node.js is installed into our environment, then we'll need to install a bunch of dependencies

### Node.js

In order to install Node.js it's preferred to use the binaries available in the [official site](https://nodejs.org/es/).

Once node has been installed into our environment we can check it's availability by running the command

```
$ node -v
v14.16.1 # This version might differ
```
### Ionic and Capacitor

```
$ npm i -g @ionic/cli @capacitor/cli
```

### Angular, React or Vue

you will notice that there is no specific cli to work with react so instancing a react project won't need a command line tool

```
$ npm i -g @angular/cli
$ npm i -g @vue/cli

```

## Creating a new project

there are two principal ways of creating a new ionic project, using the [web interface](https://ionicframework.com/start#basics) which can directly intialice a project on github, gitlab or bitbucket and the second way which is using the the command line to init a new project following the steps

```
$ ionic start
...
? Framework: (Use arrow keys)
❯ Angular | https://angular.io
  React   | https://reactjs.org
  Vue     | https://vuejs.org

  Framework: Angular
...

? Project name: camera-example
...

? Starter template:
  blank        | A blank starter project
  list         | A starting project with a list
❯ my-first-app | An example application that builds a camera with gallery
  conference   | A kitchen-sink application that shows off all Ionic has to offer
  
  Your Ionic app is ready! Follow these next steps:
```

Once this finishes initializing our new project it's necessary to add the native platforms:

```
$ cd camera-example
$ npx cap add ios         #if we are on Mac OS
$ npx cap add android
```

to run our app on the browser we'll only need to run the next command

```
$ ionic serve
```
<img width=680 src='https://raw.githubusercontent.com/celerik/celerik-articles/main/00/pictures/app-terminal-running.png'>

## What makes camera work
```
import { Plugins} from '@capacitor/core';
const { Camera } = Plugins;
```
By just calling this imports we are able to access the hardware, plugins is a set of wrapper which connect the JavaScript layer with native functions, you can learn more about [here](https://capacitorjs.com/docs/apis).

once the plugins we are going to use has been imported, we can directly use them as if they were pure JavaScript/TypeScript Functions

```
const capturedPhoto = await Camera.getPhoto(
{
  resultType: CameraResultType.Uri,
  source: CameraSource.Camera, 
  quality: 100
});
```


<div>
<img width=200 src='https://raw.githubusercontent.com/celerik/celerik-articles/main/00/pictures/app-running.png'>
<img width=200 src='https://raw.githubusercontent.com/celerik/celerik-articles/main/00/pictures/pre-camera.png'>
<img width=200 src='https://raw.githubusercontent.com/celerik/celerik-articles/main/00/pictures/camera-working.png'>
</div>
## Saving our picture into the device
we can directly save the taken picture into our device or access the device LocalStorage in order to have the pictures in our device in-app storage.

```
const readFile = await Filesystem.readFile({
          path: photo.filepath,
          directory: FilesystemDirectory.Data
 });
```
## Compiling our app into our device

it's necessary to have xcode (ios) or android studio if we want to run our application directly on our device, to open the project for our device run npx cap {{platform}} but first it's necessary to build our web project


```
$ ionic build
$ npx cap sync android    #To synchroze the built project and plugins
$ npx cap open android    #To open android studio
```

<img with=850 src='https://raw.githubusercontent.com/celerik/celerik-articles/main/00/pictures/android-studio.png'>


