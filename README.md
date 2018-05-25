# IST-Week-8-IP-Assignment

Time spent: [UPDATE WHEN DONE] hours spent in total

> Objective: Identify vulnerabilities in three different versions of the Globitek website: blue, green, and red.

The six possible exploits are:
* Username Enumeration
* Insecure Direct Object Reference (IDOR)
* SQL Injection (SQLi)
* Cross-Site Scripting (XSS)
* Crost-Site Request Forgery (CSRF)
* Session Hijacking/Fixation

Each version of the site has been given two of the six vulnerabilities. (In other words, all six of the exploits should be assignable to one of the sites.)

## BLUE
Vulnerability #1: Session Hijacking

Vulnerability #2: SQL Injection

## GREEN
Vulnerability #1:XSS

Vulnerability #2: User Enumeration

## RED
Vulnerabiltiy #1: IDOR

Vulnerability #2: N/A

## NOTES - (Describe any challenges encountered while doing the work)
* Session Hijacking: https://i.imgur.com/mkd0Ucx.gif
 
To complete this task, I remembered some techniques used on CTF's week 4 flags. If an attacker can obtain the session ID of a victim, then, the attacker could "hijack" the session and act as a privileged user. This was tested with the tool that changes the session IDs, given to us during the week 4 CTF, and performed just like one of those CTF challenges. I used two different browsers, the one with the session ID changer tool is on Firefox, while the the browser that will be doing the "hijacking" is on Chrome. On Firefox, the session ID was changed with that of a logged on user and then copied over into Chrome, replacing the cookie value with the new ID of a logged in user. In Chrome, once the session ID is chanegd witht the new ID, selecting "Log In" would automatically resume the logged in session.
 
* SQL Injection: https://i.imgur.com/bDJ3bSF.gif

To complete this task, I began to insert the code that was provided to us, via codepath, into sections where values could be placed in. I inserted it within the "Contact" tab, which did not work, then inserted it in the log in fields, thinking that it would be similar to one of the CTF/Security Shepherd challenges but that did not give me results. After doing some research about where else SQL Injections could be placed in, an example showed that the URL could be used as well. At first, I began to randomly insert it at the end of the URL of each page, hoping that I would get lucky. I began to think that there must be another way, which is when I noticed the values at the end of the URL's when clicking on the different salesmen. I noticed that these values could be manipulated, so I removed the numerical value at the end of the URL and inserted the SQL code, which then triggered database error on the Blue server. I did not think that this was the answer until I repeated it on a different server (green). With the green server, unlike the blue one, I was pushed back into the "Find a Salesperson" page, meaning that the injection failed.
 
* XSS: https://i.imgur.com/wu8LSbI.gif

To complete this task, I struggled a bit with figuring it out. I attempted to manipulated the HTML code in hopes that something would trigger. I did not have any luck with this method, so I went back to code path website to re-read the XSS portion. Upon closer inspection, I noticed that it mentioned both stored and reflected XSS attacks. I began to question the difference between a stored and a reflected XSS attack, so I went back to the previous weeks to re-read some old material on XSS attacks. I found that reflected XSS attacks, which is what I was doing earlier, would give instant results since it is a client-side based attack. However, the tasks emphasized stored XSS. Stored XSS is when malicious script is stored within the server and triggered when it is accessed. I figured that I must use the script given to me via codepath and submit that into the server. I figured that the logical way to do that is to submitted the script through the "Contact" tab as feedback. So I attempted this by submitting this script as a feedback, logged into the website, and clicked on the "Feedback" tab, which triggered the XSS attack.

* User Enumeration: https://i.imgur.com/xtur2he.gif

To complete this task, I was not sure what I was looking for at first. I went to the previous weeks to re-read on User Enumeration as well as googling what User Enumeration was. User Enumeration is the process of figuring out the right combination of a user's credential by using their username and some passwords to see what results are given. The User Enumeration section on code path mentions that the user "jmonroe99" could be probed to see if we can retrieve some hint about the existence of that user within the sites database. within the Red server, I began to insert random characters within the log in fields, which returned an error message in bold; the same thing happened when I used the "jmonroe99" username along with random characters within the password field. This was not the case within the Green server. Entering random characters in the log in field within the Green server, returned a non-bold error message. However, when "jmonroe99" is entered, an error message is returned in bold, meaning that this user does exist.
 
* IDOR: https://i.imgur.com/mRyAzGJ.gif

To complete this task, it was fairly simple. I remembered what IDOR is: being able accesse data by manipulating a parameter. I remebered that during week 1, we manipulated numerical parameters, which resulted in data being revealed. After clicking around the site, within the Red server, I entered the "Find a Salesperson" tab. Clicking on each of those Salesmen would display a URL with a numerical value at the end which referred to the Salesperson ID value. I began to change the value from 1 to 9, which displayed regular people until I changed the values to 10 and 11. Doing this, allowed me to see information that i should not be able to see. I tested this with the Blue server. I changed the ID values within the URL from 1 to 9, which displayed the same regular people as the Red server. However, when I changed the ID values to 10, i was sent back to the main "Find a Salesperson" page.

> I was not able to find the last remaining vulnerability. I have attempted to probe for Cross-Site Request Forgery, however, I had no luck with achieving results. 
