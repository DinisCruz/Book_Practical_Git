## The need to create forks/clones for TeamMentor.net website

_(Here is an email I sent earlier today at SI, that covers a number of interesting challenges that we're now having with TeamMentor, and how Git/GitHub can help)_

One of the scenarios/problems that is starting to happen is **_'how to manage the specific requirements for deployed sites like Teammentor.net who need custom changes?'_**  

So here is a description of 'the problem':

a) there is a master version of the code: [https://github.com/TeamMentor/Master](https://github.com/TeamMentor/Master)

b) there is a master version of the content: [https://github.com/TeamMentor/Library_SI](https://github.com/TeamMentor/Library_SI)

c) there is a master version of the code+content (which is a 'virtual copy' of the two above): [https://github.com/TeamMentor/TeamMentor_SI_Library](https://github.com/TeamMentor/TeamMentor_SI_Library) (think of this as a copy of the code and master repositories in a way that keeps the git connections and commit history)

d) there is a website that is based on the code + content version (i.e. [http://teammentor.net](http://teammentor.net/)) , BUT has a number of specific requirements.

* the content should not be publicly available (not TM default), ie require account creation
* specific SI requirements (see this list: [https://github.com/TeamMentor/Master/issues?milestone=3&page=1&state=open](https://github.com/TeamMentor/Master/issues?milestone=3&page=1&state=open))

e) how to deal with changes to [http://teammentor.net](http://teammentor.net/) , that are only relevant to that site (i.e will not be propagated to the main Code+Content repo)

* interestingly in the case of TeamMentor.net site, (at least at the moment), the only changes will be on the Code (where the content is the same as the one in  [https://github.com/TeamMentor/Library_SI](https://github.com/TeamMentor/Library_SI))

* but I can see how as our content generation capabilities improves (and we start to have fresh and 'current/recent-events' articles)  we might want to push those into [teammentor.net](http://teammentor.net/) (since they will be the best advertisement for TM that we could ever get)

f) since [teammentor.net](http://teammentor.net/) is a 'read-only' website, there is also an argument (from a security point of view) that that site should not have the advanced editing capabilities that TeamMentor has (this is also a feature that I can see customers wanting)

**So what is the solution?**

At the moment, the solution that I see is to:

* create a (private) fork of [https://github.com/TeamMentor/TeamMentor_SI_Library](https://github.com/TeamMentor/TeamMentor_SI_Library) (the Code+Content) repository at TMClients organisation (technically it will be a clone not a fork).

* apply the Code changes (specific to SI) in that fork

* use that fork as the source repository of [teammentor.net](http://teammentor.net/)

Any other ideas on how to deal with this?

Note that we have the exact same issue (or a variation of this) on:

* [https://owasp.teammentor.net](https://owasp.teammentor.net/) (which will have for example 'Google analytics' tracking by default and 'SSL only' enabled)
* [https://docs.teammentor.net](https://docs.teammentor.net/) (used to host the tm documentations)
* [https://download.teammentor.net](https://download.teammentor.net/) (tm site soon to be created to host the Marketing pages (for example the current [https://docs.teammentor.net/xml/Eval](https://docs.teammentor.net/xml/Eval) and [https://docs.teammentor.net/xml/Customer](https://docs.teammentor.net/xml/Customer) )
* [https://teammentor.teammentor.net](https://teammentor.teammentor.net/) (also called tm4tm, which is a site that will host all technical and non-tm-user documentation/info about TeamMentor (for example [https://docs.teammentor.net/xsl/Table_of_Contents](https://docs.teammentor.net/xsl/Table_of_Contents) will move to this tm4tm site )
* a client that wants to make code changes (for example on TM GUI), most likely another security company (a Partner) or a security department inside a bigger company
