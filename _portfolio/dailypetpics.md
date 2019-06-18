---
layout: post
title: Daily Pet Pics
thumbnail-path: "img/DailyPetPics.png"
short-description: Daily Pet Pics is an imgur type site that allows users to create an account and post pictures of their pets.
---

{:.center}
![]({{ site.baseurl }}/img/DailyPetPics.png)

## Explanation

As part of the Bloc curriculum I was tasked with creating a "capstone" project. An unguided project which would allow me to test my skills as a developer and utilize the skills I've learned in HTML, CSS, JavaScript, jQuery, Ruby, Ruby on Rails, or any other language or framework of my choosing.

For my project, I chose to create an imgur type site that would allow people to create a username and then post images of their pets. They would have the ability to tag these posts as is commonplace on most social media sites these days. They would also have the ability to like, favorite, comment, and reply on posts. The project reinforced some concepts I'd implemented on other projects during the curriculum and also introduced some new ones.

This project was the first truly freeform project during the curriculum where no real guidance was given. All of the features and implementation of those features were dictated only by my design.

## Execution

During the course of developing the app, I ran into some new concepts and, therefore, new issues. One of the new concepts I implemented was a polymorphic relationship. This was utilized such that, rather than having a model for Posts, Comments, and Replies, I only created models for Posts and Comments and allowed a Comment to belong to either a Post OR a Comment object through polymorphic relations.

Setting up the relations wasn't too difficult. It only required adding an additional column of 'commentable_id' rather than simply relying on a 'post_id' or 'comment_id' to relate a reply to a commentable object. The difficulty came when trying to implement a form partial that would allow use for both Posts and Comments to keep the code DRY.

I set up my form easily enough using a tutorial that had helped me set up the initial relationship and altered to fit my needs:

{% highlight erb %}
  <%= form_for [commentable, Comment.new] do |f| %>
    <div class="form-group">
      <% if commentable.class == Post %>
        <%= f.text_field :body, class: 'form-control', placeholder: "Enter a new comment (or paste the reaction gif image url from gif search)" %>
      <% else %>
        <%= f.text_field :body, class: 'form-control', placeholder: "Enter a new reply (or paste the reaction gif image url from gif search)" %>
      <% end %>
    </div>
    <%= f.submit "Submit Comment", class: 'btn-small pull-right light-blue lighten-2', style: 'margin-bottom: 5px;', :data => { disable_with: false } %>
    <%= f.button "Search gif reactions", class: 'btn-small light-blue lighten-2', id: "comment_#{commentable.id}_link_to_gif_reactions", style: 'margin-bottom: 5px;'%>

    <div class="row">
      <%= content_tag :div, class: "col s12 m8", id: "commentable_#{commentable.id}_giphy", style: 'display: none; margin-bottom: 20px;' do %>
        <%= text_field_tag "gif_search_text_#{commentable.id}", nil,  placeholder: "search gifs", type: "search" %>
        <div class='row'>
          <%= f.button "search", class: 'btn-small light-blue lighten-2', id: "comment__#{commentable.id}_search_gif_submit", type: "submit" %>
        </div>
      <% end %>
    </div>
  <% end %>
{% endhighlight %}

However, when I started formatting my views with materialize-css and adding JavaScript and jQuery functionality to my app, I had an issue. I was using jQuery to unhide/hide the comment reply form on a Post view page. The form worked fine before I formatted the HTML to have a ```style="hidden: true;"``` to begin with, however, when I started using jQuery to manipulate the page, the form stopped posting. It wasn't even showing a POST action in the Rails server.

I checked the form, I checked my jQuery, I logged every variable I could to the console and couldn't figure it out. I sought help from 3 different sources over the next week and none of them could figure it out either. We tried explicitly defining the controller and actions for the form, logging when controller functions were called, logging JavaScript events and nothing seemed to make sense. No matter what we changed, the submit button on the form didn't commit the comment to the database.

Finally, I noticed one of the new logs I added to my JavaScript showing an event in the console when I clicked the text field in the form. I looked at my jQuery event again and realized my issue.

The problem was the way in which I was originally selecting the `<div>` id in the jQuery. The id on the `<div>` originally followed the form: `comment_reply_link_5`. As such, my jQuery selector was matching based only on the beginning of the id text:

```
$(document).ready(function(){
  $("[id^='comment_reply_link_']").on('click', function(event) {
    ...
```
{: .language-javascript}

However, this meant that the click event was firing on the form's text field as well which had a `<div>` id that followed the form: `comment_reply_link_5_partial`. Once I realized this, I altered the form of both id's to follow the format: `comment_5_reply_link*`. With this change, I could update my jQuery click event to match the beginning and end of the id and allow the comment_id to update dynamically without having adverse effects on the jQuery.

The final jQuery event:

```
  $(document).ready(function(){
    $("[id^='comment_'][id$='reply_link']").on('click', function(event) {
      event.preventDefault();
      var replyLinkId = event.currentTarget.id;
      var partialId = replyLinkId + "_partial";
      $('#' + partialId).toggle();
      $('#post_comment_partial').toggle();
    });
  });
```
{: .language-javascript}


## Conclusion

Being assigned the task of creating an app from scratch with no real guidelines to follow was an eye-opening experience. During my curriculum with Bloc, I've been so busy trying to keep on pace with the program that I haven't taken the time to experiment with my own ideas. This project gave me that opportunity and as a result, I had some of my most significant growth as a developer. My debugging skills have improved markedly and I feel that I have a greater understanding of how the pieces of an app fit together to function properly. Overall, I feel more confident in my own skills though I know I still have a lot to learn.  
