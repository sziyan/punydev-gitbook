# Using ios shortcuts to publish github

_Disclaimer: Although workable, this method requires some setting up of files in iCloud Drive before hand, as well as a paid app for it to work_

## Table of Contents

* Requirements
* Preparation 
* Shortcut explaination

### Requirements

* GitHub account with GitHub pages repo created and setup.
* Jekyll installed on GitHub pages \(optional, but require some work on editing the shortcut\)
* iOS device with Shortcuts installed
* iCloud Drive or Dropbox enabled on iOS device
* [‎Bear Notes](https://apps.apple.com/us/app/bear/id1016366447) \(Pro optional if posts are created on iOS device only\)
* Pro version unlocked for [‎Working Copy](https://apps.apple.com/us/app/working-copy/id896694807?ign-mpt=uo%3D6)
* [‎Esse](https://apps.apple.com/us/app/esse/id1438921989)

### Preparation

~**Cloud Storage**~

With the requirements out of the way, let’s start with preparation work.

In order for the shortcut to work with assets such as images, a storage location is required. iCloud Drive and Dropbox works best as the built in file picker only has these 2 options available. In my shortcut, iCloud Drive is used but can be easily switch to Dropbox.

Create a folder in your storage of choice to house your assets.

> **Optional**: Create subfolders for each post for an easier time organising your assets. Folders and assets can be removed once post is published.  
>   
> It is also a good practice to move your assets into the folder **BEFORE** importing into Bear Notes so that both the file name in markdown and iCloud Drive will be identical.

![](https://i.imgur.com/W3pP7Uh.jpg)

Once your folder is created in your cloud storage of choice, it is time for configuration of Working Copy to sync our GitHub repo.

~**Working Copy**~

Working Copy is a full fledged git client for our iOS devices. The killer feature is the ability to integrate it with our shortcuts. However, in order for Working Copy to push to our GitHub repo, pro version unlock is required.

> **Tips:** If you’re currently a student, you might consider applying for [GitHub Student Developer Pack](https://education.github.com/pack). Simply register with your school email. Once approved, you will be entitled to pro unlock of Working Copy for as long as you’re a student.

Logging in to Working Copy is pretty straight forward. Tap on + button, select “Clone Repository”, sign in to your GitHub account and voila! Select your GitHub Pages repo to add it to your device.

### Shortcut explanation

I will not be going through each and every step of what my shortcut does. It will be too long for this post. Instead, I will explain the brief idea during the creation of shortcut. The way I create my shortcut might not be the best, but I find that it fits quite well into my workflow.

* Posts are first created in  [‎Bear Notes](https://apps.apple.com/us/app/bear/id1016366447), exported as Markdown and shared into shortcuts.
* Shortcuts take shortcut input and split text by new lines.
* Convert to rich text to remove  “\#\#” from title and set it as _title_ variable.
* Transform _title_ variable to lowercase and apply Kebab case transformation with [‎Esse](https://apps.apple.com/us/app/esse/id1438921989) due to Jekyll criteria.
* Replace first line of text from shortcut input with a blank space to essentially remove title from markdown so it will not be rendered twice in resulting blog post.
* Using regex, catch all lines with assets markdown tags.
* For each matched lines: 
  * show the whole line of markdown tags
  * prompt to select a file from cloud storage.
  * quick preview to confirm file selected is correct
  * perform image convert function from shortcuts to strip away all metadata
  * upload to imgur and return with direct url
  * replace whole line of markdown tags with direct link to imgur. \(Reason I choose to upload to imgur instead of local GitHub folder is due to GitHub Pages [limitations](https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages#usage-limits) of 1GB per GitHub Pages repo.\)
* Prompt for category and tags
* Create metadata due to Jekyll posts frontend criteria
* Combine metadata and shortcut input contents to form a blog post.
* Pull, commit and push to repo with [‎Working Copy](https://apps.apple.com/us/app/working-copy/id896694807?ign-mpt=uo%3D6) 

## Signing off

Although the shortcut created might not be optimised for speed, it fulfils my current workflow. Publishing of post and uploading to imgur takes no more than 1 minute. I might post the shortcut itself once I ironed some of the possible bugs as well as clean it up for general usage.

