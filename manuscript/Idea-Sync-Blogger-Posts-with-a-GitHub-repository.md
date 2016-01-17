## Idea: Sync Blogger Posts with a GitHub repository

From the end of the [So if my blog account is compromised can I sue Google?](http://diniscruz.blogspot.co.uk/2012/10/so-if-my-blog-account-is-compromised.html) post comes an interesting WebService idea:

**Sync Blogger posts with a GitHub repository**

The idea is to backup the contents of a blogger account into a Git repository hosted by GitHub, which would give it version control and reusability.

In practice this shouldn't be that hard:

  * Subscribe to RSS feed (starting with the big XML export that Blogger already provides)
  * Create Git repository locally with ability to:

    * Push to GitHub
    * Download 
    * Pull directly

  * There needs to be some thinking on the best way to organize the files on the git repository
  * It would be really cool if the files could be stored in a way that they could be consumed by other tools (like TeamMentor or [http://jekyllrb.com/](http://jekyllrb.com/) )
