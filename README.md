# find-and-replace
 Regex-based find and replace tool for editing subreddit wiki pages.
 
Python 3; requires the praw module ("pip install praw").

## Usage:

The program is text-based, and hopefully pretty straightforward, but this guide is in case it isn't. 

You'll first be directed to authorize the app to read and edit wiki pages on your behalf, which will open a browser window. This is so the edits that you make with the program will actually be made by your account. 

For the word or phrase to search, you can enter some literal string, in plain english, or you can enter a regular expression. (Be warned, valid regex syntax will be interpreted as such; backslashes, for example, must be escaped.)

To do more advanced replacements, where the replacement string depends on what exactly the found string is, you should be familiar with the Python re module. The replacement can be a function, which will take each match as an input, and return the replacement string. For an example, see the section below.

For each match, the program will allow you to decide whether or not to make the replacement. You can, however, allow the program to make changes without confirmations.

Finally, there is an adjustable "view margin". This is the number of characters to show you for each match, on either side of the match itself (to help you judge if each instance should be replaced or not). The larger this is, the clearer it is for you, but too large of a margin, and matches might overlap, in which case you would need to run the program again to replace all of them. It's set at a default of six characters on each side.

The replacements you make are applied to reddit once you finish each page (not after each individual edit).


## Example Execution
This example showcases the regex and advanced replacement functionality. This converts links of the form "/r/SpaceX/\<id\>/" to "/r/SpaceX/comments/\<id\>/"). Case is ignored, to match both "/r/SpaceX" and "/r/spacex".

	-=-=-=-=-=-=-=-=-=-=-
	  find-and-replace
	   /u/thatnerdguy1
	-=-=-=-=-=-=-=-=-=-=-
	
	Complete the authorization that opened in your browser.
	Authorization successful.
	(you can close the browser tab that opened)
	
	Enter the name of the subreddit: SpaceX
	Enter the pages to be edited, separated by spaces.
	To list all pages, enter "pages".
	To edit all pages, enter "all".
	all
	Enter the string to search (regex syntax is valid!): (r\/spacex\/)([a-zA-Z0-9]{6}[\/)])
	Ignore case? ("y"/"n"): y
	Enter the string to replace each instance with. For advanced functionality, enter "!ADV!": !ADV!
	Complete the lambda function, which takes a single match object as input, and outputs the replacement string: (or, enter "X" to return to the simple functionality)
	lambda match: match.group(1) + "comments/" + match.group(2)
	The current view margin is 6. Do you want to adjust it? ("y"/"n"): n
	Would you like to skip confirmation of each replacement? This is risky. ("y"/"n"): n
	
	Each match will be shown. Enter "y" to replace, or anything else to skip replacement.
