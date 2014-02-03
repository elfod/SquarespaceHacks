#Gallery Title Injection

This was developed for the [Bedford template](https://bedford-demo.squarespace.com), specifically for use in gallery collections/pages - a gallery viewed on it's own as a page as opposed to embedded in a page.

##The problem
The Bedford template displays a nice banner on each page, with text overlaid from the page settings Description field. All content collections (pages) except the gallery page, display a banner based on the page thumbnail - I'm told by support this was an intentional choice in the design, because the banner overwhelmed the gallery.

That's a fair point and on reflection I agree, but what about the page title text?

#A Solution
This hack allows you to inject a page title above the gallery images. See fig1 example picture accompanying this document.

The process for installation is as follows:

1. add the "Footer Code" to the Site Settings / Code Injection /Footer
2. on each gallery
	1. add the "Header Flag" to the gallery settings Advanced page in the Header field
	2. add the "Description Content" to the gallery settings Basic page in the Description field

The content added to the Description field need to be modified to suit your gallery page. In the code below this is the "London Street". If you want to add an additional line of text before the gallery instructions add the new text between paragraph tags as follows:

	<p>this is your new shiny text that's full of awesome</p>

##How this works
1. the page loads with the "Header Flag" called injectMe
2. the page renders and the footer code executes
	1. does the page have the meta tag injectMe?
	2. if yes, get the page description from the header (Squarespace does this by default, even if the page doesn't use it)
	3. grab the page content
	4. join the page description with the page content and insert into the page

All pages will have the footer code inserted, but unless the page header contains the injectMe header tag it won't execute, which means you can selectively choose which galleries to add this to instead of all of them.

Wait! Couldn't you have just put this in the header and no need the injectMe header thing? No, the page will run the code before the body is rendered so will grab no content.

#Code to Insert Mentioned Above

###Description Content
	<div class="desc-wrapper"><p>
	<strong class="data-shrink-ready" data-shrink-original-spacing="4" data-shrink-original-size="68" style="letter-spacing: 4px; color: rgb(0, 0, 0);">
	London Street
	</strong></p></div>
	<p><i>
	click an image to launch a lightbox with more detail for each picture
	</i><p> 

###Header Flag
	<meta itemprop="injectMe" content="yes"/>

###Footer Code
	<script>
		var metas = document.getElementsByTagName('meta');
		var bodyGrab = "";
		var result = "";
		var ml = metas.length;
	
	
		for (x=0; x<ml; x++) {
			if (metas[x].getAttribute("itemprop") == "injectMe") {
				for (y=0; y<ml; y++) {
					if (metas[y].getAttribute("itemprop") == "description") {
						result = metas[y].getAttribute("content");
						bodyGrab = document.getElementById("content").innerHTML;
						document.getElementById("content").innerHTML = result + bodyGrab;
						break;
					}
				}
				break;
			}
		}
	</script>
