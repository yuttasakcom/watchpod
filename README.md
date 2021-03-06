<div align="center">
  <a href="https://github.com/MinikubeAddon/watchpod">
    <img height="250" width="250" src="https://github.com/MinikubeAddon/watchpod/blob/master/watchpodLogo.png">
  </a>

  ## Watchpod                                                                                                        
  **Single instance K8s cluster tool that detects local file changes and automates the build and deployment of pods**

![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)
</div>

[Minikube]: https://github.com/kubernetes/minikube
[Minikube clone]: https://github.com/MinikubeAddon/minikube
[build guide]: https://github.com/kubernetes/minikube/blob/master/docs/contributors/build_guide.md
[Codesmith]: https://www.codesmith.io/

## Quick Overview
```bash
minikube start 
minikube mount /{file directory to watch}:/mount-9p# (run this in new terminal tab. Keep open)  
 - # add watchpod.json to root of the directory that will be mounted (look at demo folder for example)
kubectl apply -f https://raw.githubusercontent.com/MinikubeAddon/watchpod/master/watchpod.yaml
 - # wait ~60 seconds for watchpod to build
minikube service watchpod
```

This is all that is needed to run Watchpod. 
Please see the demo folder for instructions if running Docker with Mac.
<br>   

## Demo
![Alt Text](https://github.com/MinikubeAddon/watchpod/blob/master/watchpod-final.gif)  
<br>   

## Applying Manifest Directly
Watchpod can be used on Minikube or Docker for Windows/Mac. Please see the demo folder for specifics.   
`kubectl apply -f https://raw.githubusercontent.com/MinikubeAddon/watchpod/master/watchpod.yaml`  
<br>   

## Stepwise Guide
1. Run `minikube start` in a terminal tab
2. Open a seperate terminal window. Mount working directory where files are to be watched by running:  
`minikube mount /"path to files":/mount-9p`  
   * Example: `minikube mount /Users/Github/frasaja/watchme:/mount-9p`  
   * Leave the tab used to mount open. Move back to the tab where minikube is running  
   * Add watchpod.json to root of the directory that will be mounted (look at demo folder for example)
3. Run `kubectl apply -f https://raw.githubusercontent.com/MinikubeAddon/watchpod/master/watchpod.yaml`
4. In same non-mount terminal tab, run `minikube service watchpod`
   * Initial build here takes ~60 seconds. See "Terminal Output" tab to track progress
5. The addon will now rebuild your application(s) in the "Service View" tab when a file in the mounted directory is changed  
<br>   

## watchpod.json
Watchpod requires a `watchpod.json` file in the root of the directory that is being mounted (watched). `watchpod.json` indicates the commands that need to be run in order to build docker images and kubernetes objects.
```
{
  "docker": ["docker build -t my-image:v1 ."],
  "kubernetes": ["kubectl create -f ./my-deployment.yaml"]
}
```

## Use Directly As Minikube Addon
Watchpod is currently not available on [Minikube]. We are in the process of submitting the code for adoption.
You can fork our [Minikube clone] with the Watchpod addon included, then follow the instructions on [build guide] to run Watchpod locally.  

Run the two commands below with Minikube running to enable Watchpod as a Minikube addon:

```bash
  minikube mount /{file directory to watch}:/mount-9p  # (run this in new terminal tab. Keep open)
 ./out/minikube addons enable watchpod
```  
<br>   

<h2>Core Team</h2>
 <table>
  <tbody>
   <tr>
    <td align="center" valign="top">
     <img width="150" height="150" src="https://github.com/ASimpleHuman.png?s=150">
     <br>
     <a href="https://github.com/ASimpleHuman"> Frank Hu </a>
     <br>
     <!-- <a href="https://www.linkedin.com/in/frankjunhu/"> LinkedIn </a> -->
    </td>
    <td align="center" valign="top">
     <img width="150" height="150" src="https://github.com/sarahheacock.png?s=150">
     <br>
     <a href="https://github.com/sarahheacock"> Sarah Heacock </a>
     <br>
     <!-- <a href="https://www.linkedin.com/in/sarah-heacock-ab8677126"/> LinkedIn </a> -->  
    </td>
    <td align="center" valign="top">
     <img width="150" height="150" src="https://github.com/jmw1493.png?s=150">
     <br>
     <a href="https://github.com/jmw1493"> Jared Weiss </a>
     <br>
     <!-- <a href="https://www.linkedin.com/in/jaredmweiss/"> LinkedIn </a> -->
    </td>
   </tr>
  </tbody>
 </table>  
 <br>   

## Contributing
We'd love to have your helping hand on Watchpod! Please reach out if interested in contributing  
<br>   

## Thanks to
* The [Minikube] team for building an amazing tool    
* [Codesmith] for the encouragement and fostering a great environment   
* Everyone that provided feedback in the development of Watchpod    
