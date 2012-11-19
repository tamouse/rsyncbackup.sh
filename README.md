# Rsync Backup

There has been a long tradition of using rsync as a good backup
solution, especially over a network.

This script owes much to
[others](http://www.sanitarium.net/golug/rsync_backups_2010.html),
having found inspiration along the way to creating this script

## NAME

rsyncbackup

## SYNOPSIS

    rsyncbackup [-d] [-v] [-e <exclude-file> ] [-o <extra-options> ] -s SOURCE -t TARGET

## DESCRIPTION

Create a dated backup of the source in target, utilizing hard links to
keep space usage to a minimum.

## OPTIONS

- -s SOURCE : the source rsync specification

- -t TARGET : the target (local) specification

- -e <exclude-file> : file containing include / exclude directives to
   rsync
   
- -o <extra-options> : a string of extra options to provide the rsync
   command
   
- -d : do a dry run only, nothing is copied

- -v : be verbose

## EXAMPLES

The following will back up a remote wiki using include/exclude info:

    rsyncbackup -s wikiuser@example.com:/var/www/htdocs/wiki/  \
        -t backups/example/wiki -e backups/example/wiki.exclude
	
The following will back up a phone on OS/X:

    rsyncbackup -s /Volumes/MOT -t /Volumes/Archive/DroidBackup

The following will backup a remote server utilizing an rsync daemon
running on the remote server:

    rsyncbackup -s rsync://admin@example.com/system \
        -t backups/example.com/system \
	-e backups/example.com/system.exclude \
	-o '--password-file=backups/example.com/admin.pw'

(backups/example.com/admin.pw contains the log in credentials
established on the rsync daemon side.)

## AUTHOR

Tamara Temple <tamara@tamaratemple.com>

## SEE ALSO

rsync(1),
[Easy Automated Snapshot-Style Backups with Rsync](http://www.mikerubel.org/computers/rsync_snapshots/),
[Backups using rsync](http://www.sanitarium.net/golug/rsync_backups.html)
