# Getting started with MegaDetector

## Table of contents

1. [Overview](#overview)<br/>
2. [How people run MegaDetector](#how-people-run-megadetector)<br/>
3. [How people use MegaDetector results](#how-people-use-megadetector-results)<br/>
4. [Questions about specific camera trap use cases](#questions-about-specific-camera-trap-use-cases)<br/>
5. [Learn more](#learn-more)<br/>


## Overview

Conservation biologists invest a huge amount of time reviewing camera trap images, and &ndash; even worse &ndash; a huge fraction of that time is spent reviewing images they aren't interested in.  This primarily includes empty images, but for many projects, images of people and vehicles are also "noise", or at least need to be handled separately from animals.

*Machine learning can accelerate this process, letting biologists spend their time on the images that matter.*

To this end, we've trained an AI model &ndash; called "MegaDetector" &ndash; to detect animals, people, and vehicles in camera trap images.  It does not identify animals, it just finds them.  We've also done a little bit of work on training species classifiers, but 99% of what we do is related to MegaDetector.

This page summarizes what we do with that model to help our collaborators, typically ecologists, more specifically ecologists who are overwhelmed by camera trap images.  This page also includes some questions we ask new collaborators, to help assess whether our tools are useful, and &ndash; if so &ndash; what the right set of tools is for a particular project.

Basically this page is the response we give when someone emails us and says "I have too many camera trap images!  Can you help me?!?!".  If you're an ecologist reading this page, and that sounds familiar, feel free to answer the questions below in an email to <a href="mailto:cameratraps@lila.science">cameratraps@lila.science</a>.

You can see a list of some of the organizations who have used our tools [here](https://github.com/agentmorris/MegaDetector/?tab=readme-ov-file#who-is-using-megadetector).

If you are looking for a more technical description of the MegaDetector model, see the [MegaDetector User Guide](megadetector.md).


## How people run MegaDetector

If you are looking for a convenient, GUI-based tool to run MegaDetector, you don't need anything from this repository: check out [AddaxAI](https://addaxdatascience.com/addaxai/) (formerly EcoAssist).  Other than this section, the information on this page will be the same whether you run MegaDetector with AddaxAI or with our command-line tools.

If you have a more "DIY" use case where AddaxAI doesn't fit, MegaDetector is a publicly-available model, and there are instructions [here](https://github.com/agentmorris/MegaDetector/blob/main/megadetector.md#using-megadetector) for running it using our Python scripts.  You don't need to know anything about Python to follow those instructions.  Most MegaDetector users run it on their own, either on the cloud or on their local computers.

All of that said, it requires significant processing power to run MegaDetector on millions of images.  So many of our users - particularly high-volume users - send us images (anywhere from tens of thousands to millions), which we run through MegaDetector, then we send back a results file.  Often someone could keep up with their image load if they could just get out of their giant backlog of images; those are cases where we can often be helpful by running that big backlog for you.

Whether you're going to run MegaDetector on your own or work with us, often a good first step with a new user is just running our model on a few thousand images and seeing what happens, so if you're interested in trying this on your images, we can work out a way to transfer a set of example images, just email us at <a href="mailto:cameratraps@lila.science">cameratraps@lila.science</a>.  After that, we'll typically send back a page of sample results, like [this one](https://lila.science/public/snapshot_safari_public/snapshot-safari-kar-2022-00-00-v5a.0.0_0.200/), which helps us quickly scan a sample of images to see whether MegaDetector appears to be missing anything.


## How people use MegaDetector results

Of course, running MegaDetector doesn't do anything useful by itself: it just produces a file that tells you which images MegaDetector thinks have animals/people/vehicles in them.  You still need a way to use that file in a real image processing workflow.  We've integrated with a variety of tools that camera trap researchers already use, to make it relatively painless to use our results in the context of a real workflow.  Most MegaDetector users review their images with <a href="http://saul.cpsc.ucalgary.ca/timelapse/">Timelapse</a>, a fantastic open-source tool for reviewing camera trap images (very efficient even if you're not using AI!).  Read more about how to use MegaDetector results with Timelapse in the [Timelapse Image Recognition Guide](https://saul.cpsc.ucalgary.ca/timelapse/uploads/Guides/TimelapseImageRecognitionGuide.pdf).

We also have tools that use MegaDetector results to just separate a folder of images into folders containing images that are probably-empty, probably-animal, etc., preserving the original folder structure within these folders.  Users often use this approach to just get rid of the images that MegaDetector is really sure are empty, then you can go about your workflow exactly as you did before, just with fewer empty images.


## Questions about specific camera trap use cases

These questions help us assess which of our tools (or someone else's tools!) will be most applicable to a particular project, and whether you really want AI in your life at all (we love AI, but sometimes it's not worth the hassle!).

1. Can you provide a short overview of your project?  What ecosystem are you working in, and what are the key species of interest?

2. About how many images do you have waiting for processing right now?

3. About how many images do you expect to process in the next, e.g., 1 year?

4. What tools do you use to process and annotate images?  For example, do you:

  - Move images to folders named by species
  - Keep an Excel spreadsheet open and fill it with filenames and species IDs
  - Use a tool like Timelapse or Reconyx MapView that's specifically for camera traps
  - Use a tool like Adobe Bridge or digiKam that's for general-purpose image management
	
5. About what percentage of your images are empty?

6. About what percentage of your images typically contain vehicles or people?

7. If you are only interested in specific species (i.e., if there are a number of species you consider noise and would prefer not to even review), about what percentage of your images that contain animals contain your target species?

8. Do you have an NVIDIA GPU available (or access to cloud-based NVIDIA GPUs)?  "I don't know what a GPU is" is a perfectly good answer.  If you are running Windows, [here](https://www.windowscentral.com/how-determine-graphics-card-windows-10) is a useful guide to checking your GPU make/model.

9. How did you hear about MegaDetector?

The next few questions aren't directly related to MegaDetector, which does not require connectivity.  But we like to ask because it may impact some of the tools we recommend you use instead of or alongside MegaDetector...

10. At the place where you plan to do most of your work, how is your bandwidth?  If you're able to visit speedtest.net to measure your upload and download speeds, that's helpful. 

11. Do you have any legal or policy constraints that prevent you from using cloud-based tools to manage or review your images?

The remaining questions are only relevant to questions about training a custom model, so if you prefer to focus on off-the-shelf solutions, you can stop here...

12. What is your level of fluency in Python?  

13. About how many images do you have that you've already annotated, from roughly the same environments as the photos you need to process in the future?

14. If you have some images you've already annotated:

  - Did you keep all the empty images, or only the images with animals?
  - Are they from exactly the same camera locations that you need to process in the future (as in, cameras literally bolted in place), or from similar locations?


## Learn more

* Ready to get started with MegaDetector?  Head over to the [MegaDetector User Guide](megadetector.md).
* We maintain a literature survey on "[everything we know about machine learning for camera traps](https://agentmorris.github.io/camera-trap-ml-survey/)".
* We maintain a repository of public, labeled camera trap data to facilitate training new models (the largest such repository that we're aware of) at [lila.science](http://lila.science/datasets).
