Idea
====

A simple job que system that enables repetitive cron job like tasks to happen in the browser persistently as a user browses from page to page on your website. 

Why and when would this be useful? Imagine as the Federated Social Web or Indie Web grows- and some peoples self hosted websites start having subscribers in the 10,000 - 100,000+ range and since messages will need to be federated to different nodes this could become a heavy task, especially also if some syndications never complete (due to load and such).

On my personal node of Social-igniter my messages to Twitter sometimes does not go through and the result message is a failure.

The goal is build a job que so that those messages will get syndicated at a later date when the API is up

Examples
========

Imagine you run a relatively small social network with only 150 different users who publish content, who each post 3 pieces of content a day, totaling 450 total pieces / day. This small social network also gets a few thousand visitors who make upwards of 50,000 page requests per hour.

Now imagine trying to syndicate that 450 pieces of content from an average shared/grid/cloud hosting platform. Pretty easy job right? But, remember this is social media and average people have 300 - 600 friends/followers, while bloggers and internet celebrities have considerably more friends/followers

Each piece of content has to be federated to the following Indie Web recipients:

<table>
	<tbody>
		<tr>
			<th>Followers</th>
			<th>Network Type</th>
			<th>Totals</th>
		</tr>
		<tr>
			<td>10,456</td>
			<td>Diaspora nodes</td>
			<td>4,705,200</td>
		</tr>
		<tr>
			<td>3,876</td>
			<td>Social-Igniter nodes</td>
			<td>1,744,200</td>
		</tr>
		<tr>
			<td>6,467</td>
			<td>Status.net nodes</td>
			<td>2,910,150</td>
		</tr>
		<tr>
			<td>150</td>
			<td>Proprietary APIs</td>
			<td>67,500</td>
		</tr>
		<tr>
			<td>13,450</td>
			<td>Email Addresses</td>
			<td>6,052,500</td>
		</tr>
		<tr>
			<td colspan="2" align="right">TOTAL</td>
			<td>15,479,550</td>
		</tr>
	</tbody>
</table>

That is whopping total of 15,479,550 requests that need to be made to syndicate that content throughout the day across the web- all while also serving the web pages of the social network... to me that seems like a lot of work for just an average sized social network.

Solution
========

As a social network website grows the number of requests will rise exponentially and while it may be true if a network is a business venture that it can afford to beef up it's web server to support that load, but if it is just a group of friends, or a large family, or a non profit, those costs do matter.

So why not offset some of that load to each users browser while they are visiting the said site.

Implementation
==============

A relatively small JS file with some basic functions that create jobs, view jobs, and hand jobs off to various application specific callback functions

Later.js could piggy back on top of the project storageLocker by Oscar Godson which does:

*"storageLocker is an easy localStorage wrapper that makes localStorage more robust, chainable, and the way it should have been originally. storageLocker takes in JSON so you can do more complex stores and queries than you normally could with raw localStorage."*

https://github.com/OscarGodson/storageLocker

Once jobs gets added to the Later que they sit in the users localStorage until they are processed, like a sending que stored in a RDBMS

Here is a nifty example of an implementation written by Mr. @OscarGodson

`<script type="text/javascript">
//Var would be set with server side code or something...
var postId = 12;
//Later(name,data,timer,callback)
//@param name is a string that allows to select the cron job
//@param data is an object that allows you to set the _starting_ data
//@param timer is an integer that sets the cron job's interval
//@callback returns the job (a 'Later()' object so you can get the data out...) and do stuff with it

//Example setting a job that looks for new comments, and if so updates the comment count
//in the Later() object and also appends just the new comments to some <div id="post-12">
new Later('updateCommentCount',{ comments:0 },60000,function(job){
  //Save comment count (we set the default in the 2nd param)
  var comments = job.comments;
  //Make the API request
  $.get('/api/comments/'+postId,function(json){
    //If the returned comment count is greater than the cron job's data for comments (job.comments)...
    if(json.comments.length > comments){
      //Update the count of jobs.comments
      comments = json.comments.length;
      //Save only the new comments to a "newComments" var
      var newComments = json.comments.slice(json.comments.length);
      //Finally, loop through all the new comments and append the content to the post-12 div.
      for(x = 0; x < newComments.count; x++){
        $('#post-'+postId).append('<p id="comment-'+newComments[x].id+'">'+newComments[x].content+'</p>');
      }
    }
  });
});

//Example deleting a job...
Later('updateCommentCount').remove();

//Example resetting data (reset the comments to 0)...
Later('updateCommentCount').update({comments:0});

//Example just getting current data.
//This example returns JUST the data for 'comments', but if you wanted to return all
//you could do the 2nd example, or a set of data, the 3nd
Later('updateCommentCount').get('comments');
Later('updateCommentCount').get();
Later('updateCommentCount').get(['comments','lorem','foo']);

//P.S. you could also build Later without the "new Later()" syntax and go more "jQuery" like with:
Later('updateCommentCount',{ comments:0 },60000,function(job){});
</script>`

Recap
=====

* Syndication of status updates, messages, and content to social networks
* Downloading of content from other nodes
* Email burst limited sending que
* Protein Folding, DNA sequencing, etc...

Thoughts? 
=========

I am not the JS guru nor a sys admin well versed in scaling apps to the 100,000 user range. I wish I was, but I know many others out there are- maybe something like this already exists, maybe the idea is half baked. 

Please give me feedback, tear me a new one, etc... :)