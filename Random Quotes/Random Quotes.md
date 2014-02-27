#How to add random quotes to Squarespace

#Why?

Quotes are fun, random quotes more so.

#Features

1. Inserts a random quote into a quote block page, when a quote block is configured for random insert.
2. Other quote blocks not configured for randomness will be untouched.

#Installation guide

1. add a quote block on any page using quote text "Etaoin" with attribution "Shrdlu"*
2. get  list of quotes together and replace the list at the top of the footer code (below)
3. add the footer code to the site wide footer

* *the key phrases can be changed to anything you choose such as "eat me" and "drink me" for instance, just remember if the phrase appears in the page outside a quote block it will still get replaced.*

#How This Works

1. the page loads displaying the quote block with quote text "Etaoin" with attribution "Shrdlu"
2. the footer loads and executes the code
	2. a random quote is chosen from an embedded list
	3. the page content is grabbed into a variable
	3. a simple search and replace is performed for the two keywords, placing them with the quote and attribution text
	4. the updated page content is inserted, replacing the original
3. the random quote is now visible

#Known Issues

1. Sometime if the page loads slowly due to poor connection or any number of issues the reader may briefly see quote text "Etaoin Shrdlu" before it's replaced. Perhaps you could look at this as an opportunity to add some mystery to your pages...
2.  If your keywords are added to other content they will get replaced as well, make sure you chose something unusual and be mindful when composing content.
3. If you have more than one block quote configured on a page, they will all be replaced with the same randomly chosen quote. However, why would you have more than 1 random quote block per page?
4. The design assumes certain page structures are in place and leverages those to make it work. If they're not present because the template is something new or it's your own custom design, it may not work.

#Alternate Implementations

1. You could load the quotes from an external file, hosted say in dropbox or any CDN based storage, however a secondary call, parsing then processing will result in a delay in replacing the quote.
2. Instead of doing 2 search and replaces for the quote and attribution on all of the content, we could grab all elements that are quote blocks and cycle through them to avoid potential clashes with other content, however well chosen keywords will obviate this issue if you are mindful of them.

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
		var index = Math.floor(Math.random()*range);
		var quote = myQs[index];
		var res = quote.split("~");
		quote = res[0];
		var attribution = res[1];
		var bodyGrab = document.getElementById("page").innerHTML;
		bodyGrab = bodyGrab.replace("Etaoin", quote);
		bodyGrab = bodyGrab.replace("Shrdlu", attribution);
		document.getElementById("page").innerHTML = bodyGrab;
	</script>

#Updates

* Added 4th known issue regarding template/page structures
* Changed Footer code from using content bloxk to page block and is works with more squarespace templates. If you know what this means you fix this issue yourself if you into it :)

