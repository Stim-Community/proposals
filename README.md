# How to put in a Proposal

**1. Useful console commands**

*getgovernanceinfo* - This shows when the next superblock will be produced.

*gobject list* - This shows the proposals currently available for voting.

*gobject vote-many HASH funding yes* (or no).

**2. How it works**

This is a very complicated process and at a future date we will have a proposal website where most of this will be done for you.

To put in a proposal it costs 5 STM so before you put in the proposal you will want to make sure that you have a general idea if the proposal will pass or not.

**3. Tools needed**

You will need a Ascii Text to Hexadecimal converter that can remove "padding" I recommend this one: http://www.binaryhexconverter.com/ascii-text-to-hex-converter

Uncheck the padding option

You will also need to convert current and future times into a Epoch Unix Time Stamp.  Here is the site I recommend: https://www.unixtimestamp.com/

**4. Prepare**

Now is when it gets complicated.

Each proposal needs this info:

[["proposal",{"end_epoch":"1531159200","name":"Stim Test","payment_address":"SQQCDEYSRS5av49bYHkH8p6jWL7CBfyhwU","payment_amount":"0","start_epoch":"1531072800","type":1,"url":"https://github.com/Stim-Community/proposals/issues/1"}]]

So the syntax here is this:

"proposal" just means that you are putting in a proposal so that always needs to be there.

"end_epoch" is the approximate time when the proposal ends.  So if you want the proposal to last a year you will need to use the Unix Time Stamp page to figure that out.  For a normal proposal you want the put this as about a week after the superblock.

"name" a name for the proposal

"payment_address" this is your STM address where you will receive payment

“payment_amount” is the amount you will get paid per 30 day period (At this time this should always be "0")

“start_epoch” is the Unix Time Stamp of when you want the proposal to start.  Depending how far into the proposal month you are you might want it to start the next month.

“type” should always be 1.

“url” This is the url of your proposal.  It can be any website, but it is recommended that people use the issues tab here on Github.

Once you have filled out all of those areas your proposal should look like this:

[["proposal",{"end_epoch":"1531159200","name":"Stim Test","payment_address":"SQQCDEYSRS5av49bYHkH8p6jWL7CBfyhwU","payment_amount":"0","start_epoch":"1531072800","type":1,"url":"https://github.com/Stim-Community/proposals/issues/1"}]]

Now you need to “prepare” the proposal.

First open up the Ascii to hex converter: http://www.binaryhexconverter.com/ascii-text-to-hex-converter

Paste that whole thing into it, uncheck padding and convert to Hexadecimal.  It will return something like this:

5b5b2270726f706f73616c222c7b22656e645f65706f6368223a2231353331313539323030222c226e616d65223a225374696d2054657374222c227061796d656e745f61646472657373223a225351514344455953525335617634396259486b483870366a574c3743426679687755222c227061796d656e745f616d6f756e74223a2230222c2273746172745f65706f6368223a2231353331303732383030222c2274797065223a312c2275726c223a2268747470733a2f2f6769746875622e636f6d2f5374696d2d436f6d6d756e6974792f70726f706f73616c732f6973737565732f31227d5d5d
In front of that line of hex put in gobject prepare 0 1 and the current time in Unix Time.  So it should look like this:

gobject prepare 0 1 1531059486 5b5b2270726f706f73616c222c7b22656e645f65706f6368223a2231353331313539323030222c226e616d65223a225374696d2054657374222c227061796d656e745f61646472657373223a225351514344455953525335617634396259486b483870366a574c3743426679687755222c227061796d656e745f616d6f756e74223a2230222c2273746172745f65706f6368223a2231353331303732383030222c2274797065223a312c2275726c223a2268747470733a2f2f6769746875622e636f6d2f5374696d2d436f6d6d756e6974792f70726f706f73616c732f6973737565732f31227d5d5d
The 0 after the prepare is always a 0 if it is the first version of the proposal.  The 1 is a one if it is the first version.

Unlock your wallet, and now you are going to copy and paste that into the debug console, but remember once you hit enter your  5 STM is gone and the proposal is “prepared.”

It will output a transaction hash which needs to be saved for the next step. It should look something like this:
413b794b339b33866821d38e842d503009111faf7c8c1f34810f82686d27500f

Lock your wallet.

**Step 6. Submit**

Wait for your proposal payment to get 6 confirmations.  Once that is done you are going to take your last command and change two things.  Change “prepare” to “submit” and put the transaction hash at the end.  It should look like this:

gobject submit 0 1 1531059486 5b5b2270726f706f73616c222c7b22656e645f65706f6368223a2231353331313539323030222c226e616d65223a225374696d2054657374222c227061796d656e745f61646472657373223a225351514344455953525335617634396259486b483870366a574c3743426679687755222c227061796d656e745f616d6f756e74223a2230222c2273746172745f65706f6368223a2231353331303732383030222c2274797065223a312c2275726c223a2268747470733a2f2f6769746875622e636f6d2f5374696d2d436f6d6d756e6974792f70726f706f73616c732f6973737565732f31227d5d5d
413b794b339b33866821d38e842d503009111faf7c8c1f34810f82686d27500f

Once you hit enter it will return the proposal hash.  This is very important because this is how you get people to vote on your proposal.

**Step 7. Vote**

To vote you will need that hash that was just generated and the vote command.


gobject vote-many 8c826b2b42bc770f6ee64e5f96f613248e52063ecd53a1c839d2ed2ace48160e funding yes

Take that line and post it as a comment on your issue and also post it all over so people can vote on your proposal.

The "vote-many" command is used to vote on all masternodes contained in masternode.conf.  To vote no the command would be:


gobject vote-many 8c826b2b42bc770f6ee64e5f96f613248e52063ecd53a1c839d2ed2ace48160e funding no


That is it!  You are done!

#For more information on syntax and other commands refer to the debug console type <code>"help"</code>.
