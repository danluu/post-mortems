A List of Post-mortems!
===

<br/><br/>

##Table of Contents

**[Config Errors](#config-errors)**

**[Hardware/Power Failures](#hardwarepower-failures)**

**[Conflicts](#conflicts)**

**[Time](#time)**

**[Uncategorized](#uncategorized)**

**[Other lists of postmortems](#other-lists-of-postmortems)**

**[Analysis](#analysis)**

**[Contributors](#contributors)**
<br/><br/>

## Config Errors

[Cloudflare](https://blog.cloudflare.com/todays-outage-post-mortem-82515/). A bad config (router rule) caused all of their edge routers to crash, taking down all of Cloudflare.

[Etsy](https://codeascraft.com/2012/01/23/solr-bittorrent-index-replication/). Sending multicast traffic without properly configuring switches caused an Etsy global outage.

[Facebook](https://blog.thousandeyes.com/facebook-outage-deep-dive/). A bad config took down both Facebook and Instagram.

[Google Cloud](https://status.cloud.google.com/incident/compute/16007). A bad config (autogenerated) removed all Google Compute Engine IP blocks from BGP announcements.

[Google](http://googleblog.blogspot.com/2014/01/todays-outage-for-several-google.html). A bad config (autogenerated) took down most Google services.

[Google](https://code.google.com/p/chromium/issues/detail?id=165171#c27). A bad config caused a quota service to fail, which caused multiple services to fail (including gmail).

[Google](https://googleblog.blogspot.com/2009/01/this-site-may-harm-your-computer-on.html). `/` was checked into the URL blacklist, causing every URL to show a warning.

[Microsoft](http://azure.microsoft.com/blog/2014/11/19/update-on-azure-storage-service-interruption/). A bad config took down Azure storage.

[Stack Overflow](http://stackstatus.net/post/96025967369/outage-post-mortem-august-25th-2014). A bad firewall config blocked stackexchange/stackoverflow.

[Sentry](http://blog.getsentry.com/2016/06/14/security-incident-june-12-2016.html). Wrong Amazon S3 settings on backups lead to data leak.

[TravisCI](https://www.traviscistatus.com/incidents/khzk8bg4p9sy). A configuration issue (incomplete password rotation) led to "leaking" VMs, leading to elevated build queue times.

[TravisCI](https://blog.travis-ci.com/2016-09-30-the-day-we-deleted-our-vm-images/). A configuration issue (automated age-based Google Compute Engine VM image cleanup job) caused stable base VM images to be deleted.

[Valve](https://blog.thousandeyes.com/steam-outage-monitor-data-center-connectivity/). Although there's no official postmortem, it looks like a bad BGP config severed Valve's connection to Level 3, Telia, and Abovenet/Zayo, which resulted in a global Steam outage.


## Hardware/Power Failures

[Amazon](http://aws.amazon.com/message/2329B7/). An unknown event caused a transformer to fail. One of the PLCs that checks that generator power is in phase failed for an unknown reason, which prevented a set of backup generators from coming online. This affected EC2, EBS, and RDS in EU West.

[Amazon](https://aws.amazon.com/message/67457/). Bad weather caused power failures throughout AWS US East. A single backup generator failed to deliver stable power when power switched over to backup and the generator was loaded. This is despite having passed a load tests two months earlier, and passing weekly power-on tests.

[Amazon](http://aws.amazon.com/message/4372T8/). At 10:25pm PDT on June 4, loss of power at an AWS Sydney facility resulting from severe weather in that area lead to disruption to a significant number of instances in an Availability Zone. Due to the signature of the power loss, power  isolation breakers did not engage, resulting in backup energy reserves draining into the degraded power grid.

[ARPANET](http://www.faqs.org/rfcs/rfc789.html). A malfunctioning IMP (<a href="https://en.wikipedia.org/wiki/Interface_Message_Processor">Interface Message Processor</a>) corrupted routing data, software recomputed checksums propagating bad data with good checksums, incorrect sequence numbers caused buffers to fill, full buffers caused loss of keepalive packets and nodes took themselves off the network. From 1980.

[FirstEnergy / General Electric](https://en.wikipedia.org/wiki/Northeast_blackout_of_2003). FirstEnergy had a local failure when some transmission lines hit untrimmed foliage. The normal process is to have an alarm go off, which causes human operators to re-distribute power. But the GE system that was monitoring this had a bug which prevented the alarm from getting triggered, which eventually caused a cascading failure that eventually affected 55 million people.

[GitHub](https://github.com/blog/2106-january-28th-incident-report). On January 28th, 2016 GitHub experienced a disruption in the power at their primary datacenter.

[Google](https://status.cloud.google.com/incident/compute/15056#5719570367119360). Successive lightning strikes on their European datacenter (europe-west1-b) caused loss of power to Google Compute Engine storage systems within that region. I/O errors were observed on a subset of Standard Persistent Disks (HDDs) and permanent data loss was observed on a small fraction of those.

Sun/Oracle. Sun famously didn't include ECC in a couple generations of server parts. This resulted in data corruption and crashing. Following Sun's typical MO, they made customers that reported a bug sign an NDA before explaining the issue.

## Conflicts

[CCP Games](http://community.eveonline.com/news/dev-blogs/about-the-boot.ini-issue/) A typo and a name conflict caused the installer to sometimes delete the *boot.ini* file on installation of an expansion for *EVE Online* - with [consequences.](https://www.youtube.com/watch?v=msXRFJ2ar_E)

[GoCardless](https://gocardless.com/blog/zero-downtime-postgres-migrations-the-hard-parts/). All queries on a critical PostgreSQL table were blocked by the combination of an extremely fast database migration and a long-running read query, causing 15 seconds of downtime.

[Knight Capital](http://pythonsweetness.tumblr.com/post/64740079543/how-to-lose-172222-a-second-for-45-minutes). A combination of conflicting deployed versions and re-using a previously used bit caused a $460M loss.

[Webkit code repository](http://blogs.collab.net/subversion/subversion-sha1-collision-problem-statement-prevention-remediation-options). The Webit repository, a Subversion repository configured to use deduplication, became unavailable after two files with the same SHA-1 hash were checked in as test data, with the intention of implementing a safety check for collisions. The two files had different md5 sums and so a checkout would fail a consistency check. For context, the first public SHA-1 hash collision had very recently been announced, with an example of two colliding files.

## Time

[Azure](https://azure.microsoft.com/en-us/blog/summary-of-windows-azure-service-disruption-on-feb-29th-2012/) Certificates that were valid for one year were created. Instead of using an appropriate library, someone wrote code that computed one year to be the current date plus one year. On Februrary 29th 2012, this resulted in the creation of certificates with an expiration date of February 29th 2013, which were rejected because of the invalid date. This caused an Azure global outage that lasted for most of a day.

[Cloudflare](https://blog.cloudflare.com/how-and-why-the-leap-second-affected-cloudflare-dns/) Backwards time flow from tracking [the 27th leap second on 2016-12-31T23:59:60Z](https://hpiers.obspm.fr/iers/bul/bulc/bulletinc.52) caused the weighted round-robin selection of DNS resolvers (RRDNS) to panic and fail on some CNAME lookups.  Go's `time.Now()` was incorrectly assumed to be monotonic; this injected negative values into calls to `rand.Int63n()`, which panics in that case.

[Linux](https://lkml.org/lkml/2009/1/2/373) Leap second code was called from the timer interrupt handler, which held `xtime_lock`. That code did a `printk` to log the leap second. `printk` wakes up `klogd`, which can sometimes try to get the time, which waits on `xtime_lock`, causing a deadlock.

[Linux](https://lkml.org/lkml/2012/7/1/203) When a leap second occured, CLOCK_REALTIME was rewound by one second. This was not done via a mechanism that would update hrtimer base.offset (clock_was_set). This meant that when a timer interrupt happened, TIMER_ABSTIME CLOCK_REALTIME timers got expired one second early, including timers set for less than one second. This caused applications that used sleep for less than one second in a loop to spinwait without sleeping, causing high load on many systems. This caused a large number of web services to go down in 2012.

## Uncategorized

[Allegro](http://allegro.tech/allegro-cast-post-mortem.html). The [Allegro](http://allegro.pl) platform suffered a failure of a subsystem responsible for asynchronous distributed task processing. The problem affected many areas, e.g. features such as purchasing numerous offers via cart and bulk offer editing (including price list editing) did not work at all. Moreover, it partially failed to send daily newsletter with new offers. Also some parts of internal administration panel were affected.

[Amazon](http://status.aws.amazon.com/s3-20080720.html). Message corruption caused the distributed server state function to overwhelm resources on the S3 request processing fleet.

[Amazon](https://aws.amazon.com/message/65648/). Human error during a routine networking upgrade led to a resource crunch, exacerbated by software bugs, that ultimately resulted in an outage across all US East Availability Zones as well as a loss of 0.07% of volumes.

[Amazon](http://aws.amazon.com/message/680587/). Elastic Load Balancer ran into problems when "a maintenance process that was inadvertently run against the production ELB state data".

[Amazon](https://aws.amazon.com/message/5467D2/). A "network disruption" caused metadata services to experience load that caused resposne times to exceed timeout values, causing storage nodes to take themselves down. Nodes that took themselves down continued to retry, ensuring that load on metadata services couldn't decrease.

[AppNexus](http://techblog.appnexus.com/2013/2013-09-17-outage-postmortem/). A double free revealed by a database update caused all "impression bus" servers to crash simultaneously. This wasn't caught in staging and made it into production because a time delay is required to trigger the bug, and the staging period didn't have a built-in delay.

[AT&T](http://users.csc.calpoly.edu/~jdalbey/SWE/Papers/att_collapse.html). A bad line of C code introduced a race hazard which in due course collapsed the phone network. After a planned outage, the quickfire resumption messages triggered the race,  causing more reboots which retriggered the problem. "The problem repeated iteratively throughout the 114 switches in the network, blocking over 50 million calls in the nine hours it took to stabilize the system." From 1990.

[Bitly](http://blog.bitly.com/post/85260908544/more-detail). Hosted source code repo contained credentials granting access to bitly backups, including hashed passwords.

[BrowserStack](https://www.browserstack.com/attack-and-downtime-on-9-November). An old prototype machine with the [Shellshock](https://en.wikipedia.org/wiki/Shellshock_(software_bug)) vulnerability still active had secret keys on it which ultimately led to a security breach of the Production system.

[Buildkite](https://building.buildkite.com/outage-post-mortem-for-august-23rd-82b619a3679b). Database capacity downgrade in an attempt to minimise AWS spend resulted in lack of capacity to support Buildkite customers at peak, leading to cascading collapse of dependent servers.

[CCP Games](http://community.eveonline.com/news/dev-blogs/behind-the-scenes-of-a-long-eve-online-downtime/). A problematic logging channel caused cluster nodes dying off during the cluster start sequence after rolling out a new game patch.

[CircleCI](https://circleci.statuspage.io/incidents/hr0mm9xmm3x6). A GitHub outage and recovery caused an unexpectedly large incoming load. For reasons that aren't specified, a large load causes CircleCI's queue system to slow down, in this case to handling one transaction per minute.

[Dropbox](https://blogs.dropbox.com/tech/2014/01/outage-post-mortem/). This postmortem is pretty thin and I'm not sure what happened. It sounds like, maybe, a scheduled OS upgrade somehow caused some machines to get wiped out, which took out some databases.

[European Space Agency](https://en.wikipedia.org/wiki/Cluster_%28spacecraft%29?oldid=217305667). An overflow occured when converting a 16-bit number to a 64-bit numer in the Ariane 5 intertial guidance system, causing the rocket to crash. The actual overflow occured in code that wasn't necessary for operation but was running anyway. According to [one account](http://www.around.com/ariane.html), this caused a diagnostic error message to get printed out, and the diagnostic error message was somehow interpreted as actual valid data. According to [another account](https://en.wikipedia.org/wiki/Cluster_%28spacecraft%29?oldid=217305667), no trap handler was installed for the overflow.

[Etsy](https://blog.etsy.com/news/2012/demystifying-site-outages/). First, a deploy that was supposed to be a small bugfix deploy also caused live databases to get upgraded on running production machines. To make sure that this didn't cause any corruption, Etsy stopped serving traffic to run integrity checks. Second, an overflow in ids (signed 32-bit ints) caused some database operations to fail. Etsy didn't trust that this wouldn't result in data corruption and took down the site while the upgrade got pushed.

[Foursquare](https://news.ycombinator.com/item?id=1769761). MongoDB fell over under load when it ran out of memory. The failure was catastrophic and not graceful due to a a query pattern that involved a read-load with low levels of locality (each user check-in caused a read of all check-ins for the user's history, and records were 300 bytes with no spatial locality, meaning that most of the data pulled in from each page was unecessary). A lack of monitoring on the MongoDB instances caused the high load to go undetected until the load became catastrophic, causing 17 hours of downtime spanning two incidents in two days.

[Gitlab 2014](https://docs.google.com/document/d/1ScqXAdb6BjhsDzCo3qdPYbt1uULzgZqPO8zHeHHarS0/preview?sle=true&hl=en&forcehl=1#heading=h.dfbilqgnc5sf). After the primary locked up and was restarted, it was brought back up with the wrong filesystem, causing a global outage. See also [HN discussion](https://news.ycombinator.com/item?id=8003601).

[Gitlab 2017](https://about.gitlab.com/2017/02/10/postmortem-of-database-outage-of-january-31/). Influx of requests overloaded the database, caused replication to lag, tired admin deleted the wrong directory, six hours of data lost. See also [earlier report](https://about.gitlab.com/2017/02/01/gitlab-dot-com-database-incident) and [HN discussion](https://news.ycombinator.com/item?id=13537052).

[Gliffy](http://support.gliffy.com/entries/98911057--Gliffy-Online-System-Outage). While attempting to resolve an issue with a backup system the production database was accidentally deleted causing a system outage.

[Google](https://code.google.com/p/nativeclient/issues/detail?id=2508). Checking the vendor string instead of feature flags renders NaCl unusable on otherwise compatible non-mainstream hardware platforms.

[Google](https://gist.github.com/jomo/2bae3821acb433d0446d). A mail system emailed people more than 20 times. This happened because mail was sent with a batch cron job that sent mail to everyone who was marked as waiting for mail. This was a non-atomic operation and the batch job didn't mark people as not waiting until all messages were sent.

[GPS/GLONASS](http://www.gps.gov/governance/advisory/meetings/2014-06/beutler1.pdf). A bad update that caused incorrect orbital mechanics calculations caused GPS satellites that use GLONASS to broadcast incorrect positions for 10 hours. The bug was noticed and rolled back almost immediately due to (?) this didn't fix the issue.

[Healthcare.gov](https://plus.google.com/+AndreasSchou/posts/FhWtABz7ew9).

[Heroku](https://status.heroku.com/incidents/642?postmortem). Having a system that requires scheduled manual updates resulted in an error which caused US customers to be unable to scale, stop or restart dynos, or route HTTP traffic, and also prevented all customers from being able to deploy.

[Intel](http://42gems.com/blog/?p=735). A scripting bug caused the generation of the divider logic in the Pentium to very occasionally produce incorrect results. The bug wasn't caught in testing because of an incorrect assumption in a proof of correctness.

[Joyent](https://www.joyent.com/blog/manta-postmortem-7-27-2015). Operations on Manta were blocked because a lock couldn't be obtained on their PostgreSQL metadata servers. This was due to a combination of PostgreSQL's transaction wraparound maintence taking a lock on something, and a Joyent query that unecessarily tried to take a global lock.

[Kickstarter](https://www.kickstarter.com/backing-and-hacking/the-day-the-replication-died). Primary DB became inconsistent with all replicas, which wasn't detected until a query failed. This was caused by a MySQL bug which sometimes caused `order by` to be ignored.

[Mailgun](http://status.mailgun.com/incidents/p9nxxql8g9rh). Secondary MongoDB servers became overloaded and while troubleshooting accidentally pushed a change that sent all secondary traffic to the primary MongoDB server, overloading it as well and exacerbating the problem.

[Medium](https://medium.com/medium-eng/the-curious-case-of-disappearing-polish-s-fa398313d4df). Polish users were unable to use their "Ś" key on Medium.

[NASA](http://www.doneyles.com/LM/Tales.html). A design flaw in the Apollo 11 rendezvous radar produced excess CPU load, causing the spacecraft computer to restart during lunar landing.

[NASA](https://en.wikipedia.org/wiki/Mars_Climate_Orbiter). Use of different units of measurement (metric vs. English) caused Mars Climate Orbiter to fail. This is basically the same issue Sweden ran into in 1628 with its ship.

[NASA](http://research.microsoft.com/en-us/um/people/mbj/Mars_Pathfinder/Authoritative_Account.html). NASA's Mars Pathfilder spacecraft experienced system resets a few days after landing on Mars (1997).  Debugging features were remotely enabled until the cause was found: a [priority inversion](https://en.wikipedia.org/wiki/Priority_inversion) problem in the VxWorks operating system.  The OS software was remotely patched (all the way to Mars) to fix the problem by adding priority inheritance to the task scheduler.

[Netflix](http://techblog.netflix.com/2012/10/post-mortem-of-october-222012-aws.html). An EBS outage in one availability zone was mitigated by migrating to other availability zones.

[Platform.sh](https://medium.com/@florian_7764/technical-post-mortem-of-the-august-incident-82ab4c3d6547). Outage during a scheduled maintenance window because there were too much data for Zookeeper to boot.

[Reddit](https://www.reddit.com/r/announcements/comments/4y0m56/why_reddit_was_down_on_aug_11/)
experienced an outage for 1.5 hours, followed by another 1.5 hours of
degraded performance on Thursday August 11 2016. This was due to an error during
a migration of a critical backend system.

[Salesforce](https://help.salesforce.com/apex/HTViewSolution?urlname=Root-Cause-Message-for-Disruption-of-Service-on-NA14-May-2016&language=en_US) Initial disruption due to power failure in one datacenter led to cascading failures with a database cluster and file discrepancies resulting in cross data center failover issues.

[Sentry](http://blog.getsentry.com/2015/07/23/transaction-id-wraparound-in-postgres.html). Transaction ID Wraparound in Postgres caused Sentry to go down for most of a working day.

[Spotify](https://labs.spotify.com/2013/06/04/incident-management-at-spotify/). Lack of exponential backoff in a microservice caused a cascading failure, leading to notable service degradation.

[Stack Exchange](http://stackstatus.net/post/115305251014/outage-postmortem-march-31-2015). Enabling StackEgg for all users resulted in heavy load on load balancers and consequently, a DDoS.

[Stack Exchange](http://stackstatus.net/post/147710624694/outage-postmortem-july-20-2016). Backtracking implementation in the underlying regex engine turned out to be very expensive for a particular post leading to health-check failures and eventual outage.

[Stack Exchange](http://meta.stackoverflow.com/q/340960/2422776). Porting old Careers 2.0 code to the new Developer Story caused a leak of users' information.

[Stack Exchange](http://stackstatus.net/post/156407746074/outage-postmortem-january-24-2017). The primary SQL-Server triggered a bugcheck on the SQL Server process, causing the Stack Exchange sites to go into read only mode, and eventually a complete outage.

[Strava](http://engineering.strava.com/the-upload-outage-of-july-29-2014/). Hit the signed integer limit on a primary key, causing uploads to fail.

[Stripe](https://support.stripe.com/questions/outage-postmortem-2015-10-08-utc). Manual operations are regularly executed on production databases. A manual operation was done incorrectly (missing dependency), causing the Stripe API to go down for 90 minutes.

[Sweden](http://www.pri.org/stories/2012-02-23/new-clues-emerge-centuries-old-swedish-shipwreck). Use of different rulers by builders caused the _Vasa_ to be more heavily built on its port side and the ship's designer, not having built a ship with two gun decks before, overbuilt the upper decks, leading to a design that was top heavy. Twenty minutes into its maiden voyage in 1628, the ship heeled to port and sank.

[Tarsnap](http://mail.tarsnap.com/tarsnap-announce/msg00035.html). A batch job which scans for unused blocks in Amazon S3 and marks them to be freed encountered a condition where all retries for freeing certain blocks would fail. The batch job logs its actions to local disk and this log grew without bound. When the filesystem filled, this caused other filesystem writes to fail, and the Tarsnap service stopped. Manually removing the log file restored service.

[Therac-25](http://sunnyday.mit.edu/papers/therac.pdf). The Therac-25 was a radiation therapy machine involved in at least six accidents between 1985 and 1987 in which patients were given massive overdoses of radiation. Because of concurrent programming errors, it sometimes gave its patients radiation doses that were thousands of times greater than normal, resulting in death or serious injury.

[Valve](https://github.com/valvesoftware/steam-for-linux/issues/3671). Steam's desktop client deleted all local files and directories. The thing I find most interesting about this is that, after this blew up on social media, there were widespread reports that this was reported to Valve months earlier. But Valve doesn't triage most bugs, resulting in an extremely long time-to-mitigate, despite having multiple bugreports on this issue.

[Yeller](http://yellerapp.com/posts/2014-08-04-postmortem1.html). A network partition in a cluster caused some messages to get delayed, up to 6-7 hours. For reasons that aren't clear, a rolling restart of the cluster healed the partition. There's some suspicious that it was due to cached routes, but there wasn't enough logging information to tell for sure.

*Unfortunately, most of the interesting post-mortems I know about are locked inside confidential pages at Google and Microsoft. Please add more links if you know of any interesting public post mortems!  is a pretty good resource; other links to collections of post mortems are also appreciated.*

## Other lists of postmortems

[Availability Digest website](http://www.availabilitydigest.com/articles.htm).

[Google+ postmortems community](https://plus.google.com/communities/115136140203018391796).

[John Daily's list of postmortems (in json)](https://github.com/macintux/Service-postmortems).

[Jeff Hammerbacher's list of postmortems](http://www.quora.com/Jeff-Hammerbacher/Post-mortems).

[NASA lessons learned database](http://llis.nasa.gov/).

[Tim Freeman's list of postmortems](https://pinboard.in/u:peakscale/t:postmortem/)

[Wikimedia's postmortems](https://wikitech.wikimedia.org/wiki/Incident_documentation).

[Autopsy.io's list of Startup failures](http://autopsy.io/).

## Analysis

[How Complex Systems Fail](http://web.mit.edu/2.75/resources/random/How%20Complex%20Systems%20Fail.pdf)

[John Allspaw on Resilience Engineering](http://www.kitchensoap.com/2011/04/07/resilience-engineering-part-i/)

## Contributors

* Aaron Wigley
* Ahmet Alp Balkan
* Allon Murienik
* Amber Yust
* Anthony Elizondo
* Anuj Pahuja
* Benjamin Gilbert
* Brian Scanlan
* Brock Boland
* Chris Higgs
* Connor Shea
* Dan Luu
* Dan Nguyen
* David Pate
* Dov Murik
* Ed Spittles
* Florent Genette
* Franck Arnulfo
* gnomon
* Grey Baker
* Jacob Kaplan-Moss
* James Graham
* Jason Dusek
* John Daily
* jomo
* Julia Hansbrough
* Julian Szulc
* Justin Montgomery
* KS Chan
* Kunal Mehta
* Luan Cestari
* Mark Dennehy
* Massimiliano Arione
* Matt Day
* Michael Robinson
* Mike Doherty
* Mohit Agarwal
* Nat Welch
* Nate Parsons
* Nick Sweeting
* Raul Ochoa
* Samuel Hunter
* Sean Escriva
* Siddharth Kannan
* Tim Freeman
* Tom Crayford
* Vaibhav Bhembre
* Vincent Ambo
