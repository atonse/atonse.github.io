---
author: Ashish
comments: true
date: 2009-01-11 21:08:43+00:00
layout: post
slug: using-the-quickbooks-api-for-time-tracking
title: '"Using" the Quickbooks API for Time Tracking'
wordpress_id: 68
---

As an IT consultant who subcontracts from various companies, I enter my hours in at least 3 different systems on any given day.



	
  1. My own company's system hosted on Freshbooks - This is the master copy since my invoicing is driven by it

	
  2. Quickbooks, two of my clients use it and require me to enter hours in there for accurate billing

	
  3. GHG's Timesheet software - err... this abomination of an app barely functions, forget asking for an API


I want to be able to record hours on all 3 systems in one click or even from my iPhone.

<!-- more -->


### Freshbooks


Freshbooks' API is very clean and they have an iPhone app, so this is the least of my worries.

Request:

`<request method="time_entry.create">
<time_entry>
<project_id>1</project_id>        # Associated project_id (Required)
<task_id>1</task_id>              # Associated task_id    (Required)
<hours>4.5</hours>                # (Optional)
<notes>Freshbooks Test</notes> # (Optional)
<date>2007-01-01</date>           # (Optional)
</time_entry>
</request>`

Response:

`<response status="ok">
<time_entry_id>211</time_entry_id>
</response>`

Almost too easy. :) Thank you Freshbooks.


### Quickbooks (the Big Kahuna)


Quickbooks doesn't have an API, but have exposed API-like functionality to their Outlook plugin and Vista Gadget. Since Vista Gadgets (and Apple Dashboard Widgets as well) are just html/javascript, some simple hacking revealed exactly what I needed.

"Extracting" the Quickbooks Time Tracker Vista Gadget's protocol

I first downloaded the .gadget file from Quickbooks' site after logging in. Since this is a CAB (Cabinet) file, you can open it natively within Windows or use File Juicer on the Mac. The CAB file reveals a directory structure with tons of images, html files, and javascript files. From here, it's relatively easy to find the right files you need.

Of particular interest are:

`js/loginAndSynch.js
js/persistentSettings.js`

After about half an hour of hacking at the javascript code and many invalid cURL requests to the QB server, this is essentially the protocol I was able to get working:

"GetLists" - Obtains the list of customers and service jobs from the Quickbooks server

Endpoint: https://timetracking.quickbooks.com/j/tts/widget

POST Body:

`cmd=getLists&version=1.0v&login=%7B%22companyid%22%3A%22your_company_id%22%2C%22username%22%3A%22your_username_value%22%2C%22password%22%3A%22your_password_value%22%7D`

cURL command for debugging: `curl -v -d @post.data -X POST https://timetracking.quickbooks.com/j/tts/widget`

Make sure you put the POST body above in a file named "post.data" in the same directory where you run cURL. It'll use the contents of the file as the POST body.

And you will receive all the Customer Names and Service Items in JSON (fake company names/IDs for confidentiality):

`{"CustomerJobs":[{"Name":"Food Network","ID":"999999"},{"Name":"Food Network:Rachael Ray","ID":"7777777"},{"Name":"Cartoon Network","ID":"25252525"},{"Name":"Cartoon Network:Family Guy","ID":"2343333"},{"Name":"Vacation","ID":"888888"}],"ServiceItems":[{"Name":"Contractor-Admin work","ID":"111111"},{"Name":"Contractor-Support Work","ID":"222222"},{"Name":"Contractor-Support Work:Training","ID":"33333"},{"Name":"Support Work","ID":"444444"},{"Name":"Support Work:Maintenance Work","ID":"5555555"}]}`

The easiest way for me to quickly inspect a JSON struct is to fire up the Ruby interactive console (irb) and do the following:

`>> require 'rubygems'
=> false
>> require 'json'  # 'sudo gem install json' if you don't have the json gem
=> true
>> a = JSON.parse(File.read('customers.json'))`

... 'a' now has the json struct

From here, I can iterate through the hash and inspect its keys and data:

`>> a.keys
=> ["ServiceItems", "CustomerJobs"]
>> a['CustomerJobs'].each do |job| puts job['Name'] end`

... prints out all the customer job names

Voila! We have the first half (and arguably the easier half) of this Quickbooks API project.

In the next part, I will outline how I did the second half, the actual Time Entry piece. (After I figure it out)
