#How to add random quotes to Squarespace

#Why?

Quotes are fun, random quotes more so.

#Features

1. Inserts a random quote into a quote block page, when a quote block is configured for random insert.
2. Other quote blocks not configured for randomness will be untouched.

#Installation guide

1. add a quote block on any page using quote text "Etaoin" with attribution "Shrdlu"*
2. get list of quotes together and replace the list at the top of the footer code (below)
3. add the footer code to the site wide footer in Code Injection section of Settings

* *the key phrases can be changed to anything you choose such as "eat me" and "drink me" for instance*

#How This Works

1. the page loads displaying the quote block with quote text "Etaoin" with attribution "Shrdlu"
2. the footer loads and executes the code
	1. all the quote blocks are grabbed into a list
	2. list is processed:
		1. a random quote is chosen from an embedded list
		2. each quote block gets replaced with a different random quote
		3. the updated code block is inserted into the page, replacing the original
3. the random quote is now visible

#Known Issues

1. Sometime if the page loads slowly due to poor connection or any number of issues the reader may briefly see quote text "Etaoin Shrdlu" before it's replaced. Perhaps you could look at this as an opportunity to add some mystery to your pages...
3. The design assumes certain page structures are in place and leverages those to make it work. If they're not present because the template is something new or it's your own custom design, it may not work.

#Alternate Implementations

1. You could load the quotes from an external file, hosted say in dropbox or any CDN based storage, however a secondary call, parsing then processing will result in a delay in replacing the quote.

#Footer Code

	<script>
	
		var myQs = new Array();
		myQs[0] = "quote 1~unknown";
		myQs[1] = "quote 2~unknown";
		myQs[2] = "quote 3~unknown";
		myQs[3] = "quote 4~unknown";
	    myQs[4] = "quote 5~unknown";
	    myQs[5] = "quote 6~unknown";
	    myQs[6] = "quote 7~unknown";
	    myQs[7] = "quote 8~unknown";
	    myQs[8] = "quote 9~unknown";
	    myQs[9] = "quote 10~unknown";
	    myQs[10] = "quote 11~unknown";
	
		var range = myQs.length;
	  	var index;
	  	var quote;
	  	var res;
	  	var attribution;
	  	var bodyGrab;
	  
		function getQuote()
		{
			index = Math.floor(Math.random()*range);
			quote = myQs[index];
			res = quote.split("~");
			quote = res[0];
			attribution = res[1];
		}
	  	
		var blocks = document.getElementsByTagName("blockquote");
		var captions = document.getElementsByTagName("figcaption");
		for (var i=0;i<blocks.length;i++)
		{
			getQuote();
			bodyGrab = blocks[i].innerHTML;
			bodyGrab = bodyGrab.replace("Etaoin", quote);
			blocks[i].innerHTML = bodyGrab;
			bodyGrab = captions[i].innerHTML;
			bodyGrab = bodyGrab.replace("Shrdlu", attribution);
			captions[i].innerHTML = bodyGrab;
		}
	
	</script>

#Updates

* Added 4th known issue regarding template/page structures
* Changed Footer code from using content block to page block and is works with more squarespace templates. If you know what this means you fix this issue yourself if you into it :)
* Code reengineered to be more robust across the variety of squarespace template structures

