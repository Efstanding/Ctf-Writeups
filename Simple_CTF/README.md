### Question 1 : How many services are running under port 1000?

*I'm not gonna lie, at first i thought this means 'how many services are on the port '1000'*
And because i'm beginner and don't know much about ports, I thought many services can run 
under one specific port, so i searched everything and googled for how to do this, with no result.

**Realization** : this means ports : 1-1000 not on '1000'. So i know nmap generally provides information on open ports on a remote IP (I learned this the hard way, trying to use netstat which is for local machines) and i used
```nmap -sC -sV [target_ip]``` which was fruitful

results gave 3 different open ports with 3 different services : 
1. port 21 -> tcp
2. port 80 -> http
3. port 2222 -> ssh
so obviously <1000 = 2 ports only. 

### Question 2 : what's running on the higher port ? 
from previous scan : on port 2222 runs ssh. 

### question 3 : what's the CVE you're using against the application ? 

This was sooo difficult. I didn't know what i was doing at first, I was googling everything. 
I tried googling CVEs against the apache ubuntu version of port 80, but every CVE was producing errors. So i realized **it's not that easy** 
I then saw that http port is open, so there has to be some type of site. 
I  searched the ```target_ip``` on the url. And it produced a page about ubuntu apache 2.
*hmmm* nothing really of value. I then searched for a lot of time endlessly. 
And came accross a tool called gobuster.

## what is gobuster and why it's useful

I saw that gobuster does 2 things : 
1. searches using wordlists (lists of common words) for hidden directory paths
2. searches using wordlists for certain subdomains
and that gobuster is used a lot of ctfs, mostly using 1.
So basically, 1. produces a type of url that you can also find yourself, if I DO ``` CD /path/x/ ``` 100000 times or something but with urls. it works with status error codes.

You know status error codes : 404 not found, 200 = okay, 403 is protected, there's a whole list somewhere for every category 100-200, 200-300 etc. 
So if it finds a url that responds with something good, it returns it.
And that's how it returned 4-5 queries.

One of them had the word 'simple' in it. ouuuuu probably its this.
And boom.
