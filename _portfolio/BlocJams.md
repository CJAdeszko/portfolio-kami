---
layout: post
title: BlocJams
thumbnail-path: "img/BlocJams.png"
short-description: BlocJams is a Spotify replica for streaming music on desktop and mobile devices.
---

{:.center}
![]({{ site.baseurl }}/img/BlocJams.png)

## Explanation

The purpose of BlocJams was to learn the basic concepts of HTML, CSS, JavaScript, and jQuery through an interactive set of checkpoints and assignments. These checkpoints and assignments rely on a combination of reading, watching videos, copying code, and trial and error to create a replica of a streaming music service such as Spotify.

## Problem

During the course of the module, I was faced with the challenge of utilizing a basic knowledge of HTML, CSS, JavaScript, and jQuery to accomplish various tasks such as updating the layout of the page to match a specified design or to write a function that accomplishes a given task within the framework of the project.

## Solution

Through a combination of reading, watching videos, endless Google searches, and the guidance of a mentor, I was able to complete the task of creating a replica music streaming service while being introduced to the basics of frontend design and programming. This required maintaining a delicate balance between struggling through the curriculum to the point of wanting to throw an expensive computer at the wall in frustration, and seeking help and guidance when a breakthrough could not be reached on my own.

## Results

The results of the sometimes [seemingly] endless frustration is a responsive app design for desktop and mobile use that introduced me to the basic elements of HTML, CSS, JavaScript, and jQuery. I learned new ways, such as the use of pseudocode lines within my JavaScript, to make learning and writing code more manageable when the task at hand seems impossible.

{% highlight javascript %}
    var togglePlayFromPlayerBar = function(){
      var currentlyPlayingCell = getSongNumberCell(currentlyPlayingSongNumber);

    //Conditional statement to check if song is paused and the play button is clicked in the player bar
    if (currentSoundFile.isPaused() && $playBarSelector.data("clicked", true)){

      //Change the song number cell from a play button to a pause button
      currentlyPlayingCell.html(pauseButtonTemplate);

      //Change the HTML of the player bar's play button to a pause button
      $('.main-controls .play-pause').html(playerBarPauseButton);

      //PLay the song
      currentSoundFile.play();
    }else{

      //Change the song number cell from a pause button to a play button
      currentlyPlayingCell.html(playButtonTemplate);

      //Change the HTML of the player bar's pause button to a play button
      $('.main-controls .play-pause').html(playerBarPlayButton);

      //pause the song
      currentSoundFile.pause();
    }

    };
{% endhighlight %}


## Conclusion

With this foundational knowledge, I now have the ability to move forward in the curriculum and reinforce my understanding of the concepts while furthering my skill set within the respective languages. By building a foundation in the concepts of HTML, CSS, JavaScript, and jQuery, I can begin to gain a deeper understanding of how the different elements work together to form the framework for frontend web development.
