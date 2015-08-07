A list of post mortems!

[Knight Capital](http://pythonsweetness.tumblr.com/post/64740079543/how-to-lose-172222-a-second-for-45-minutes). A combination of conflicting deployed versions and re-using a previously used bit caused a $460M loss.

[Etsy](https://codeascraft.com/2012/01/23/solr-bittorrent-index-replication/). Sending multicast traffic without properly configuring switches caused an Etsy global outage.

[Healthcare.gov](https://plus.google.com/+AndreasSchou/posts/FhWtABz7ew9).

[Sweden](http://www.pri.org/stories/2012-02-23/new-clues-emerge-centuries-old-swedish-shipwreck). Use of different rulers by builders causes lopsided ship, which sank in 1628.

[NASA](https://en.wikipedia.org/wiki/Mars_Climate_Orbiter). Use of different units of measurement (metric vs. English) caused Mars Climate Orbiter to fail. This is basically the same issue Sweden ran into in 1628 with its ship.

[Stack Overflow](http://stackstatus.net/post/96025967369/outage-post-mortem-august-25th-2014). A bad firewall config blocked stackexchange/stackoverflow.

[Microsoft](http://azure.microsoft.com/blog/2014/11/19/update-on-azure-storage-service-interruption/). A bad config took down Azure storage.

[Gitlab](https://docs.google.com/document/d/1ScqXAdb6BjhsDzCo3qdPYbt1uULzgZqPO8zHeHHarS0/preview?sle=true&hl=en&forcehl=1#heading=h.dfbilqgnc5sf). After the primary locked up and was restarted, it was brought back up with the wrong filesystem, causing a global outage.

[Heroku](https://status.heroku.com/incidents/642?postmortem). Having a system that requires scheduled downtime with manual updates inevitably resulted in an error which caused US customers to be unable to scale, stop or restart dynos, or route HTTP traffic.

[Bitly](http://blog.bitly.com/post/85260908544/more-detail). Hosted source code repo contained credentials granting access to bitly backups, including hashed passwords.

Sun/Oracle. Sun famously didn't include ECC in a couple generations of server parts. This resulted in data corruption and crashing. Following Sun's typical MO, they made customers that reported a bug sign an NDA before explaining the issue.

[Kickstarter](https://www.kickstarter.com/backing-and-hacking/the-day-the-replication-died). Primary DB became inconsistent with all replicas, which wasn't detected until a query failed. This was caused by a MySQL bug which sometimes caused `order by` to be ignored.

Unfortunately, most of the interesting post-mortems I know about are locked inside confidential pages at Google and Microsoft. Please add more links if you know of any interesting public post mortems! [This](https://plus.google.com/communities/115136140203018391796) is a pretty good resource; other links to collections of post mortems are also appreciated.

## Contributors

* Dan Luu
* Julia Hansbrough
* Nat Welch

