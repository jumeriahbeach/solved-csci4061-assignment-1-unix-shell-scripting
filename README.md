Download Link: https://assignmentchef.com/product/solved-csci4061-assignment-1-unix-shell-scripting
<br>
The purpose of this assignment is to learn shell scripting with different commands, control constructs, conditional expressions and environment variables.

Scenario

After the winter holidays, you may have taken a lot of nice pictures. And you may want to show them on your personal web page (an html file). However, these pictures are of various format and resolution (e.g., some are from your smart phone and some are from your camera). Changing the format and resolution one by one is a laborious work. Fortunately, your knowledge of shell scripts saves you from the laborious work, helping you change the resolution and format of pictures automatically and merge them into an html file in a nice way.

Assignment <sub> </sub>

Your job is to write a shell script that searches through a directory tree looking for images of a specified type (<strong>gif</strong>, <strong>png</strong>, <strong>tiff</strong>, etc), convert all the images into <strong>JPEG</strong> format in a specified output directory, and create a web page called <strong>pic_name_xx.html</strong> that contains links to the converted images in the form of small “thumbnail” images. In other words, the website would basically be a presentation of all the thumbnail images of the images processed. The usage message [1] for your script will be:

<strong>Usage</strong>: create_images input_dir output_dir pattern_1 [pattern_2] … [pattern_n] where 
<strong>create_images</strong>

The name of your script.

<strong> </strong>input_dir

This is the TOP/ROOT of a directory tree in which images are to be found. Images may occur in this directory, or in any subdirectory. There may also be other, non-image files in this directory. Any directory or file that is not readable, i.e., permission not allowed, should be skipped, after putting out an error message to standard output.

Attention:

<ol>

 <li>Input directory may or may not exist.</li>

 <li>Input directory may or may not have multiple subdirectories.</li>

 <li>Input directory/subdirectories may or may not be readable.</li>

 <li>Input file names in the input_dir will NOT have spaces. 
Input file names will have only ONE period (.) in the filename, e.g., hello.png</li>

</ol>

<strong> </strong>output_dir

Each image that satisfies the pattern requirement is to be converted to JPEG format (see the ImageMagick manual page) and stored in this directory. Thumbnail images must also be generated from each image. These must be stored in a subdirectory of output_dir called “<strong>thumbs</strong>“. The output directory may or may not already exist, and may or may not be empty initially.

Attention:

<ol>

 <li>Output directory may or may not exist – create it if it does not exist</li>

 <li>Output directory may or may not have multiple subdirectories (including the ‘thumbs’ subdirectory) – create thumbs if it does not exist.</li>

 <li>Do not touch any files already present in the output directory or any of the subdirectories.</li>

</ol>

pattern

You will be given at least one pattern (the “[]” around the other patterns means they are optional). You need to finish 3 tasks as follows

<ol>

 <li>Search the directory and subdirectory, find all the images satisfying the pattern(s).</li>

 <li>Convert required images to *.JPG and according thumbnail images with specified resolution.</li>

 <li>Merge the converted images into an html file.</li>

</ol>

<h2>Task 1 Find all files satisfying the patterns</h2>

One or more pattern arguments may be present. Each one is a search pattern (usable with find), that will identify image files to be converted. For example, the pattern *.png would identify images in the portable network graphics format. For this assignment, you need to handle conversion of ONLY <strong>PNG</strong>, <strong>GIF</strong> and <strong>TIFF</strong> images. Appropriate error messages must be written to standard output in case invalid patterns are used (e.g. *.pgn, *.tif) (Hint: Use regular expressions [2] to identify valid patterns)




Attention:

<ol>

 <li>Valid regex patterns should be usable with the ‘find’ or ‘grep’ command, such as “*.png”, “he*.gif”.</li>

 <li>If there are multiple patterns, deal with them one by one. For example, if you see both pattern “*.png” and “he*.gif”, you first convert all images satisfying pattern “*.png”, then deal with pattern “he*.gif”. When you are converting images, follow the instructions below.</li>

</ol>




<h2> Task 2 Convert images to *.JPG format</h2>

The dimensions of the converted images should be the same dimensions as the original (in other words, do not scale the original images), and the thumbnail images must all be 200 pixels in the largest dimension (either width or height).

Converted images must be named as <strong>&lt;name-sans-ext-in-uppercase&gt;.jpg</strong>, and thumbnail images must be named as <strong>&lt;name-sans-ext-in-uppercase&gt;_thumb.jpg</strong>, where <strong>&lt;name-sans- ext-in-uppercase&gt;</strong> is the name of the original file without its original suffix in uppercase letters.  In other words, if you convert an image called “<strong>xyzzy.tiff</strong>”, the image must be named “<strong>XYZZY.jpg</strong>” and the thumbnail image must be named “<strong>XYZZY_thumb.jpg</strong>”.

Each thumbnail image <strong>you converted</strong> should be embedded into the web page. At the same time, each of the thumbnail image should link to the original size version of the image.




Attention:

<ol>

 <li>You must convert ONLY PNG, GIF &amp; TIFF files; you must not attempt to convert any</li>

</ol>

other files.

<ol start="2">

 <li>The converted JPG image must be placed in the output directory.</li>

 <li>All thumbnail images must be placed in the thumbs subdirectory.</li>

 <li>Do not scale the images while converting (Maintain the same dimensions). Thumbnails should be generated and EITHER the width OR the height needs to be 200px.</li>

 <li>Convert the images if and only if the output directory contains neither the original image nor the thumbnail image: If EITHER HELLO.jpg OR HELLO_thumb.jpg already exists in the output directory, you need to SKIP conversion of HELLO.png.</li>

 <li>If multiple input files have the same <strong>basename</strong> (i.e., name without directory path, such as hello.png, hello.gif), since both will be converted to the same filename (HELLO.jpg &amp; HELLO_thumb.jpg), only the file which matches the first pattern passed to the script must be converted.</li>

</ol>




<h2> Task 3 Merge the converted images into an html file</h2>

The HTML file is a presentation of the images you have converted. You should include ONLY those images which YOUR SCRIPT has converted. The HTML file contains links to the converted images in the form of small “thumbnail” images.

In addition, the HTML webpage should also display 1) the resolution (e.g., 200 x 300) of THUMBNAIL image, 2) the last MODIFY date of the image (hint, parse the “stat” command), 3) a user input theme message of the webpage (i.e., the script should prompt for user input, and use the input as the THEME), and 4) today’s date and day (hint, parse the “date” command).

For the format of the HTML file, see the example <strong>“mypic.html</strong>”. Generate your <strong>pic_name_xx.html</strong> similar to the example.




Attention:

<ol>

 <li>The name of the HTML page: “pic_name_xx.html”. You are allowed to overwrite the HTML file if present.</li>

 <li>Date &amp; day (no time) should be displayed only ONCE below the thumbnail images.</li>

 <li>If the output directory previously contained images before your script was run, do not add those images to the HTML file.</li>

 <li>Your script need to ask user to input the theme of the web page.</li>

</ol>




<h1>Error Handling <sub> </sub></h1>

While the script runs, it must write to its standard output some messages that describe what it is doing. Lines should be printed at least when the script starts, when a file is converted, when a thumbnail image is created, and when the script finishes.

Errors must be handled gracefully, with informative error messages on standard output. Refer to all the “Attention” mentioned before and the grading part.




<h1>Platform <sub> </sub></h1>

You may work on the platform of your choice: Linux, Solaris, MacOSX or Windows (using Cygwin). However, you need to ensure that your script works correctly on one of the CSELabs UNIX machines, wherewe will grade your assignments. All commands required in this project have already been tested on CSELabs UNIX (e.g., KH4240)

Your CSELabs UNIX account uses bash as its default shell. However, since the objective of

this assignment is to learn shell scripting (not to build a webpage or learn python or perl), this assignment must be done with the C shell [3] meaning the first line of your script should be #!/bin/csh

Another way to go into c shell environment is to directly type “csh” in the command line.




<h1>Test Data <sub> </sub></h1>

The compressed tar file provided along with this assignment handout contains a directory tree containing a few images, as well as a sample web page with thumbnails and converted images so you can see what the output should look like. (Note that the sample web page does not include all the images in the sample directory.)

You can extract a compressed tar file with the command  tar xzf tarfile

Error handling: 25 pts (5 pt each)

<ol>

 <li>Usage message from wrong #args</li>

 <li>Non-existent input directory</li>

 <li>Unreadable input directory</li>

 <li>Unreadable input files</li>

 <li>Existence of output directory
 
</li>

</ol>

<ol>

 <li>Create output directory and a subdirectory for thumbnail images</li>

 <li>No image files match the pattern</li>

 <li>A single image file matches the pattern</li>

 <li>Multiple image files match the pattern</li>

 <li>Script is able to convert all files within a multi-level directory tree</li>

 <li>Uppercase letters for converted image filenames.</li>

</ol>




<h2>Correct handling of multiple patterns: 15 pts (5 pt each)</h2>

<ol>

 <li>Multiple patterns given, all patterns match</li>

 <li>Multiple patterns given, some match</li>

 <li>Multiple files with same base name, different type (e.g., sunset.gif and sunset.png)</li>

</ol>

<strong> </strong>

<h2>Correctly build the HTML page as specified: 25 pts (5 pt each)</h2>

<ol>

 <li>Show thumbnail images (200 pixels in the largest dimension) on the web page</li>

 <li>Show the full sized image whenever a thumbnail image is clicked.</li>

 <li>Display the resolution and the last modified date of the images</li>

 <li>Display the day and date correctly on the webpage.</li>

 <li>Display user input theme message</li>

</ol>




#!/bin/csh

# CSci4061 Spring 2017 Assignment 1

# Name: &lt;Full name1&gt;, &lt;Full name2&gt;

# Student ID: &lt;ID1&gt;, &lt;ID2&gt;

# CSELabs machine: &lt;machine&gt;

# Additional comments




In the README, you should explain, briefly, what your script does, how it works, how you use it, and how to interpret its output.

<h1>Resources &amp; Hints</h1>

<ol>

 <li>The format of usage message: https://en.wikipedia.org/wiki/Usage_message</li>

 <li>A tutorial of regex patterns can be found in http://ryanstutorials.net/regular-expressionstutorial/</li>

 <li>In case c shell is not installed, in Linux, you can install csh by: sudo apt-get install csh</li>

 <li>The class moodle page contains links to several shell-related documents.</li>

 <li>You can parse the output of the ‘date’ command to obtain today’s date and day.</li>

 <li>You can parse the ‘stat’ of an image to find its modified date.</li>

 <li>You might want to use following commands (not limited to) in your script. Refer to the man pages of these commands for more details.</li>

</ol>

echo set convert find shift mkdir chmod rm basename identify stat


