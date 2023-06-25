# BurpSuite Glossary

**Author:** David Boyd<br>
**Date:** 2023-06-24

## Sections Overview

**Proxy:** What allows us to funnel traffic through Burp Suite for further
analysis.

**Target:** How we set the scope of our project. We can also use this to
effectively create a site map of the application we are testing.

**Intruder:** Incredibly powerful tool for everything from field fuzzing to
credential stuffing and more.

**Repeater:** Allows us to 'repeat' requests that have previously been made
with or without modification. Often used in a precursor step to fuzzing with
the aforementioned **Intruder**.

**Sequencer:** Analyzes the 'randomness' present in parts of the web app
which are intended to be unpredictable. This is commonly used for testing
session cookies.

**Decoder:** As the name suggests, Decoder is a tool that allows us to
perform various transforms on pieces of data. These transforms vary from
decoding/encoding to various bases or URL encoding.

**Comparer:** Comparer as you might have guessed is a tool we can use to
compare different responses or other pieces of data such as site maps or proxy
histories (awesome for access control issue testing). This is very similar to
the Linux tool diff.

**Extender:** Similar to adding mods to a game like Minecraft, Extender allows
us to add components such as tool integrations, additional scan definitions,
and more!

**Scanner:** Automated web vulnerability scanner that can highlight areas of
the application for further manual investigation or possible exploitation with
another section of Burp. This feature, while not in the community edition of
Burp Suite, is still a key facet of performing a web application test.

## Repeater

**Purpose:** Meant for repeat testing once a proof of concept has been established.

**Uses:** Automation, fuzzing, brute-forcing, handles experimentation or
one-off testing.

### Common Uses

- *Enumerating* **identifiers:**
  - usernames, cycling through predictable session/password recovery tokens,
    attempting simple password guessing.
- *Harvesting* useful **data** from:
  - user profiles, pages of interest *(via grepping our responses)*.
- *Fuzzing* for **vulnerabilities:**
  - SQL injection, cross-site scripting (XSS), and file path traversal.

## Attack Types

### Sniper

Sniper is the most popular attack type.

Sniper cycles through our selected positions, by putting the next available
payload (item from our wordlist) in each position in turn.

:warning: This uses only *one set* of payloads (one wordlist).

:bulb: Think of one shot per target. Hence the name, *Sniper*.

### Battering Ram

Battering Ram puts every payload into every selected position *(unlike
Sniper)*.

:warning: Uses only *one set* of payloads *(similar to Sniper)*.

:bulb: Think about how a battering ram makes contact across a large surface
area with a single object. Hence the name, *Battering Ram*.

### Pitchfork

Pitchfork allows us to use *multiple payload sets*, where one set is positioned
on a target paramter, then iterates through both payload sets simultaneously
*(in parallel)*.

:gun::gun: Think of a dual pistol wielding badass but with forks
:fork_and_knife:

#### Example

**Setup**

| Position (@Param) | Payload Set       |
|-------------------|-------------------|
| `username`        | username_wordlist |
| `password`        | password_wordlist |

**Result**

| Request | Value                                                            |
|---------|------------------------------------------------------------------|
| 1       | `username`=username_wordlist[0], `password`=password_wordlist[0] |
| 2       | `username`=username_wordlist[1], `password`=password_wordlist[1] |
| 3       | `username`=username_wordlist[2], `password`=password_wordlist[2] |
| 4       | `username`=username_wordlist[3], `password`=password_wordlist[3] |

:bulb: Resulting total number of combinations will equal the smallest payload
set provided.

### Cluster Bomb

Cluster Bomb allows us to use multiple payload sets *(one per position
selected)* and iterate through ***all combinations*** of the payload lists
provided.

:boom: Think of how a grenade propels shrapnel in every which directional
combination possible :boom:

#### Example

**Setup**

| Position (@Param) | Payload Set |
|-------------------|-------------|
| `username`        | a_wordlist  |
| `password`        | a_wordlist  |

**Result**

| Request | Value                                              |
|---------|----------------------------------------------------|
| 1       | `username`=a_wordlist[0], `password`=a_wordlist[0] |
| 2       | `username`=a_wordlist[0], `password`=a_wordlist[1] |
| 3       | `username`=a_wordlist[0], `password`=a_wordlist[2] |
| 4       | `username`=a_wordlist[0], `password`=a_wordlist[3] |

:bulb: Resulting total number of combinations will equal the `n(positions) *
len(wordlist)`

## Other Terms

**Payload:** an item *(or word)* from our wordlist.

**Set of payloads:** a wordlist.

## Sequencer

:pencil: `Set-Cookie` **response** needs to be `MIME type`: `JSON` (HTTP
history col)

Sequencer is a tool that analyzes the **quality of randomness** in an
application's **sessions tokens** and similar data that is otherwise expected
to be unpredictable.

### Common Uses

- Sessions tokens
- Anti-CSRF tokens
- Password reset tokens
  - **Password reset tokens:** are tokens that are sent w/ password resets 
    that, in theory, uniquely tie users with their password reset requests.

### Decoder && Comparer

Decoder
	- is a tool
	  that allows us to perform various *transforms*
	  on pieces of data.
	[+] These transforms vary
		from decoding/encoding to
		various bases
		or URL encoding.
	[+] We chain these transforms together
		and Decoder will automatically spawn
		an additional tier
		each time we select a decoder, encoder, or hash.
	[+] This tool ultimately functions very similarly to CyberChef,
		albeit slightly less powerful.

Comparer
	- is a tool
	  to compare different responses or
	  other pieces of data
		- such as:
			- **site maps**
			- proxy histories (awesome for access control issue testing)
	[+] This is very similar to the Linux tool diff.

-----------
common uses
-----------

Comparer

	- When looking for username enumeration conditions,
		- compare responses to
			- failed logins using valid and invalid usernames,
				looking for subtle differences in responses.
		[+] Useful for enumerating password recovery forms
			or another similar recovery/account access mechanism.

	- When an Intruder attack has resulted in some
	  very large responses
	  with different lengths than the base response,
		- you can compare these
		  to quickly see where the differences lie.

	- When comparing the
		site maps or Proxy history entries
		generated by different types of users,
			- you can compare pairs of
				similar requests
				to see where the differences lie
				that give rise to different application behavior.
		[+] This may reveal possible access control issues
		    in the application
			wherein lower privileged users can access pages
			they really shouldn't be able to.

	- When testing for blind SQL injection bugs
	  using Boolean condition injection
	  and other similar tests,
		- you can compare two responses
		  to see whether injecting different conditions
		  has resulted in a relevant difference
		  in responses.

Supplemental Information
========================

URI Generic Syntax (Uniform Resouce Identifier)
-----------------------------------------------
:URL: https://tools.ietf.org/html/rfc3986

Uniform Resource Identifier (URI)
	is a compact sequence of characters
	that identifies an abstract or physical resource.

URI Generic Syntax (RFC 3986)
	resolves URI references that might be in relative form,
	along with guidelines and security considerations for the use of URIs
	on the Internet.
	[+] URI syntax defines a grammar that is a **superset of all valid URIs**,
	    allowing an implementation to parse the common components of a URI
		reference without knowing the scheme-spcefic requirements of every
		possible identifier.

Percent-Encoding
	is used to represent a **data octet** in a component when that octet's
	corresponding character is outside the allowed set or is being used as a
	delimeter of, or within, the component.
	[+] SYNTAX: char triplet consisting of '%' and two HEX chars.
	pct-encoded = "%" HEXDIG HEXDIG
	:%20: Space char


###############
Extender [Mods]
###############
:Extender/Mods: Similar to adding mods to games, like Minecraft, lol

Extender
	allows us to add components
	such as:
		- tool integrations
		- additional scan definitions
		- etc

Popular Extensions
------------------
:Prerequisite: Jython, the Java implementation of Python
:YouTube: `RequestSmuggle: <https://www.youtube.com/watch?v=_A04msdplXs/>`

+-----------+-----------------------------------------------------------------+
| Extension | Description                                                     |
+===========+=================================================================+
| Logger++  | Adds enhanced logging to all requests and responses from all    |
|           | Burp Suite tools, enable this one before you need it!           |
+-----------+-----------------------------------------------------------------+
| Request   | A relatively new extension, this allows you to attempt to       |
| Smuggle   | smuggle requets to backend servers.                             |
+-----------+-----------------------------------------------------------------+
| Autorize  | Useful for authentication testing in web app tests. These       |
|           | tests typically revolve around navigating to restricted pages   |
|           | or issuing restricted GET requests with the session cookies of  |
|           | low-privileged users.                                           |
+-----------+-----------------------------------------------------------------+
| Burp Team | Allows for collaboration on a Burp project amongst team         |
| Server    | members.  Project details are shared in a chatroom-like format. |
+-----------+-----------------------------------------------------------------+
| Retire.js | Adds scanner checks for outdated JavaScript libraries that      |
|           | contain vulnerabilities, this is a **premium extension**.       |
+-----------+-----------------------------------------------------------------+
| J2EEScan  | Adds a scanner test coverage for J2EE (Java platform for web    |
|           | development) applications, this is a **premium extension**.     |
+-----------+-----------------------------------------------------------------+
| Request   | Captures response times for requests made by all Burp tools,    |
| Timer     | usefule for discovering *timing attack vectors*.                |
+-----------+-----------------------------------------------------------------+

Jython Installation
-------------------
:URL: https://www.jython.org/download.html
:Download: Jython Standalone
:Filetype: jython-2.7.2.jar
:Summary: A Java implementation of Python
:Purpose: Set up Burp for installing extensions.

Burp > Extender > Options > Python Environment
> Location of Jython standalone JAR lone JAR file:

Installing Extensions
---------------------

1.	`Jython Installation`_
2.	Burp > Extender > BApp Store

##################
Scanner and Spider
##################
:NOTE: Run this before testing the web application.

Scanner
	allows us to
		*passively & actively*
		**scan     & spider**
		the website to test for vulnerabilities.

Usage
-----
:Method1: Dashboard > (+)New live task
:Method2: Rt-click > Scan

