Idea
====

A simple job que system that enables repetitive cron job like tasks to happen in the browser persistently as a user browses from page to page on your website. 

Why and when would this be useful? Imagine as the Federated Social Web or Indie Web grows- and some peoples self hosted websites start having subscribers in the 10,000 - 100,000+ range and since messages will need to be federated to different nodes this could become a heavy task, especially also if some syndications never complete (due to load and such).

On my personal node of Social-igniter my messages to Twitter sometimes does not go through and the result message is a failure.

The goal is build a job que so that those messages will get syndicated at a later date when the API is up

Examples
========

Imagine you run a relatively small social network with only 150 different users who publish content, who each post 3 pieces of content a day, totaling 450 total pieces / day.

This small social network also gets a few thousand visitors who make upwards of 50,000 page requests per hour.

Now imagine trying to syndicate that 450 pieces of content from an average shared/grid/cloud hosting platform. Pretty easy job right?

But, remember this is social media and average people have 300 - 600 friends/followers, while bloggers and internet celebrities have considerably more friends/followers

So each piece of content has to be federated to the following Indie Web recipients:

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

Recap
=====

* Syndication of status updates, messages, and content to social networks
* Downloading of content from other nodes
* Email burst limited sending que

Thoughts? 
=========

I am not the JS guru nor a sys admin well versed in scaling apps to the 100,000 user range. I wish I was, but I know many others out there are- maybe something like this already exists, maybe the idea is half baked. 

Please give me feedback, tear me a new one, etc... :)