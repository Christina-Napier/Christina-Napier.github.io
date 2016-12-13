---
published: true
title: @HolisticInfoSec Steganography Challenge
layout: post
---
<p>Little Twitter Steg Challenge.</p>

<p>So it was a late winter Monday night,
whilst perusing twitter I seen something that caught my eye.</p>

<p>It was Russ @hollisticinfosec
posting about steganography tools, upon reading down, I seen there was a challenge.
A challenge you say?!</p>

<p><img width=602 height=243 id="Picture 1" src="img/image001.png"></p>

<p>Torn between reading a book to
fall asleep, watching youtube videos or getting back out of bed to get my leet
skillz on, I opted for the latter.</p>

<p>Sat cold and in my Pj�s I was
lead to a page that gave a good basic overview of steganography and the process
in which Russ used the steganography tool.</p>

<p>You can find out for yourself
here: <a href="http://holisticinfosec.blogspot.co.uk/2016/12/toolsmith-gse-edition-image.html">http://holisticinfosec.blogspot.co.uk/2016/12/toolsmith-gse-edition-image.html</a></p>

<p>So upon looking at the challenge there
was a .png we needed to decode. WTF2.png </p>

<p>Once I had downloaded the Steg
tool which can be downloaded here https://imagesteganography.codeplex.com/downloads/get/251046
and the image as per Russ�s blog it was then onto decoding.</p>

<p>Image:</p>

<p><img border=0 width=602 height=268 id="Picture 2" src="img/image002.png"></p>

<p><img width=115 height=157 src="img/image003.jpg" align=left hspace=12></p>

<p>Decoded the image using the
codeplex tool.</p>

<p>Its pretty straight forward, your
enter the path for the file name and choose file or text output, then start.
Bingo you have a file pop out. </p>

<p>The output was a powershell file
called rr.ps1 which had base64 code inside it. </p>

<p>Now at this point, someone with
an up to date and un temperamental vm would have been able to run the
powershell file and presented with the final answer. Which is what I found out
this morning, running it from another machine </p>

<p>I will however explain how I went
about investigating the powershell code last night via my own methods. </p>

<p>I have found this all pretty
interesting. By learning from my errors and debugging, how I can possibly look
further into areas to find out what powershell scripts do. Not taking for
granted whats hidden away encoded.</p>

<p>My starting point:</p>

<p><img border=0 width=601 height=65 id="Picture 6" src="img/image004.jpg"></p>

<p>Ok so I couldn�t run the program, what happens when I try to
debug it. I finally had an output. <img border=0 width=602 height=63 id="Picture 7" src="img/image005.jpg"></p>

<p>Now since I am not a big user of
power shell I originally thought the output below to be in reference to something
along the lines of the powerspoilt / veil framework.</p>

<p>Read up about it here <a
href="http://www.slideshare.net/HaydnJohnson/power-sploit-persistence-walkthrough">http://www.slideshare.net/HaydnJohnson/power-sploit-persistence-walkthrough</a>.
Pretty cool stuff. </p>

<p>I pretty much got the gist of
what was going on, from the looks of things the script was calling another
encoded string and decoding it and possibly carry out some action.</p>

<p>It was coming towards bedtime,
eyes squinting I tried converting the above base64 again and came up with quite
scrambled text. Thought ok perhaps this could be another file, thinking along
the lines of inception here. </p>

<p>So I tried that also in a hex
editor and checked the file sigs just in case. 
<img border=0 width=287 height=136 id="Picture 8" src="img/image006.jpg"></p>

<p>&nbsp;</p>

<p>Let�s just say It wasn�t a hidden
file, some people will be reading thinking why would it be!, just run the
program already LOL! Well my dear sirs, it was 1am a novice at powershell with
a half working windows 7 VM.</p>

<p>I sent what I had collected over
to Russ via email, I had noted that in order for me to get the file running I
would need to change the permissions. Thought ok, get this sent off and have a
go at it in the morning.</p>

<p>I Woke up to a very nice email
from Russ telling me I am nearly there, to adapt the powershell settings and go
from there.</p>

<p>So back onto my VM I adapted the
permissions and ran the file. </p>

<p><img border=0 width=598 height=43 id="Picture 5" src="img/image007.jpg"></p>

<p>Once again I was presented with
some more errors, however these errors helped me identify some of the strings
within the output. I was starting to think this VM really doesn�t like me.
Running the program it just seem to hang and throw error output. </p>

<p><img border=0 width=590 height=111 id="Picture 9" src="img/image008.jpg" alt="https://scontent-lhr3-1.xx.fbcdn.net/v/t31.0-8/15493313_1130018787119338_1364822181189725682_o.jpg?oh=1e1b2a7ebb00d09f0bc6e81347a9cabd&amp;oe=58B8A647"></p>

<p>Reading through I could see now a
different base64 string and also later in the file a bit.ly link</p>

<p><img width=602 height=65 src="img/image009.jpg" align=left hspace=12 alt="https://scontent-lhr3-1.xx.fbcdn.net/v/t31.0-8/15541078_1130018737119343_6405784254145181752_o.jpg?oh=ca25bac0d6a6bf43c04657f125341287&amp;oe=58E76F10"><br
clear=all>
Great I was getting closer to a resolution at this point. �</p>

<p>I wanted to find out what the
apparent base64 code was so I found a little script on Stackoverflow</p>

<p><a
href="http://stackoverflow.com/questions/18726418/decoding-base64-with-powershell">http://stackoverflow.com/questions/18726418/decoding-base64-with-powershell</a></p>

<p>ran the script and came out with
the following:</p>

<p><img border=0 width=574 height=103 id="Picture 11" src="img/image010.jpg"></p>

<p>From this I didn�t get much, I�m
kinda thinking that I�m either doing something wrong here investigating using
this method, or I think I need to learn a little more about how the
encoding/decoding works on the powershell front. </p>

<p>&nbsp;</p>

<p>&nbsp;</p>

<p>And now on to the bit.ly link :</p>

<p><img border=0 width=602 height=111 id="Picture 14" src="img/image011.jpg" alt="https://scontent-lhr3-1.xx.fbcdn.net/v/t31.0-8/15392894_1130018887119328_4485815344930921095_o.jpg?oh=abe66abf5d8d129f3e0ceaf951e24140&amp;oe=58AF787B"></p>

<p>The bit.ly link, http://bit.ly/e0Mw9w I followed the link
and was presented with the following link <a href="http://www.leeholmes.com/projects/ps_html5/Invoke-PSHtml5.ps1">http://www.leeholmes.com/projects/ps_html5/Invoke-PSHtml5.ps1</a>
I could quite clearly see that this was another powershell file.</p>

<p><img border=0 width=601 height=268 id="Picture 12"
src="img/image012.jpg"></p>

<p>I could see from the comments the
following: </p>

<p class=MsoNormal style='margin-bottom:0cm;margin-bottom:.0001pt;line-height:
normal'><span style='font-size:10.0pt;font-family:"Courier New"'>PowerShell +
HTML5 prototype. Needs audio. Run: iex</span></p>

<p>Ahhaaa! This is probably why the
windows 7 VM was giving me issues. As the original script seem to be calling
upon this script in order to run. Once it had hit this end I guess it failed.</p>

<p>So on with the great reveal what
was the final product..</p>

<p>Being Rick Rolled via powershell!<img border=0 width=597 height=188 id="Picture 13"
src="img/image013.jpg"></p>

<p>So now I have a rick rolled
powershell that pops up every time I open it </p>

