## Back up your data

IBM Cloudant creates three copies of each document
and stores it on three different servers in a cluster to ensure high availability.
This practice is the default for all Cloudant users.
Even when your data is replicated in triplicate,
it is still  important to back it up.

You can lose access to your data in more than one way.
For example,
if a hurricane destroys your data center and all three nodes are in that location,
you lose your data.
You can prevent the loss of your data in a disaster by replicating your data to a
cluster (dedicated or multi-tenant) in a different geographic location.
However,
if a faulty application deletes or overwrites the data in your database,
duplicate data is not helpful.

With Cloudant,
you can have incremental backups that update daily.
These daily updates or 'deltas' enable document comparison,
and easier single document restoration.
At regular intervals,
which can be configured,
the smaller daily deltas are rolled up into weekly deltas.
Similarly,
weekly deltas are rolled up into monthly deltas,
and monthly deltas into yearly ones.
This process of rolling up deltas is a pragmatic compromise between
being able to restore exactly the right version of a document,
and requiring a lot of storage space.

Should you wish to restore some documents,
for example as part of a disaster recovery scenario,
you can contact the support team and have your data restored to a specific day,
week,
month or year,
subject to the deltas you have available.

More information about how Cloudant backs up data is provided in the rest of this topic.
For further assistance,
or to request that data backup is enabled,
contact the Cloudant support team:
[support@cloudant.com](mailto:support@cloudant.com).

### Incremental backups

The first step in enabling incremental backups is to take a full backup of your entire database.
This provides a 'baseline' for the subsequent incremental backups.

Every day,
after the first 'baseline' backup,
a daily,
incremental backup is taken.
This daily incremental backup contains only the data that has changed in the database since the last backup. The daily backup is the 'daily delta'.

As part of the request to enable data backups,
you can specific a time of day for the backup to run.
The daily delta is created each day,
at the time you specified.

<aside class="warning">The interval between backups must be 24 hours or more.
In other words,
you can run daily backups but not hourly backups.</aside>

### Roll ups

A roll up combines daily backups into weekly,
rolled up databases.
These roll up databases combine the daily deltas into a coarser time slice.
Weekly databases roll up into monthly databases,
and monthly databases roll up into yearly databases.
When requesting that backups are enabled,
you decide a specific number of days to wait between each of these roll up activities.

Once the delta databases have been rolled up,
they are removed to free up storage space.

### Restores

When you have backups for a database,
you can view individual documents within that database,
and also see changes made to that document.
You can also restore the document to the version that was current on a particular date,
if it is available within the deltas.

For more complex restores,
such as a full database restore,
request assistance from Cloudant support.

### Using the Dashboard

You can review the status and history of backups using the Cloudant Dashboard.

Tasks you can perform include:

-	View the status of the last backup, including its date and time.
-	View the history of all backup replications that have run for a specific backup operation.
-	View a list of backup document versions by date and time.
-	View a current document and the difference between it and any backed up version.
-	Restore a document from a backed up version.