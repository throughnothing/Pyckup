#Pyckup
Pyckup is a wrapper around duplicity (http://duplicity.nongnu.org/duplicity.1.html) that allows you to setup multiple targets and sources, use public/private key encryption, and backup the same source to multiple locations easily, and with a single config

##Config
Here is a sample config for pyckup (sample\_pyckuprc in the repo).

    [TARGETS]
      [[amazon_photos]]
      path = s3://my_s3_bucket/duplicity-photos/
      encrypt = 2D9E0CB3

      [[amazon_dot_files]]
      path = s3://my_s3_bucket/duplicity-dot-files/
      encrypt = 2D9E0CB3

      [[local_photos]]
      path = file:///home/throughnothing/backups/photos/
      encrypt = none

      [[local_dot_files]]
      path = file:///home/throughnothing/backups/dot_files/
      encrypt = none


    [SOURCES]
      [[photos]]
      path = /home/throughnothing/Pictures/
      exclude = **
      include = *.jpg,*.JPG,*.jpeg,*.JPEG

      [[dot_files]]
      path = /home/throughnothing/
      exclude = **
      include = .vim,.vimrc,.irss,.ssh,.gnupg,.bashrc,.alias


##Usage
Pyckup is pretty simple to use.  Once you have your config set up, you can run it like so:

    pyckup -s photos -t amazon_photos

This will back up your photos source to your amazon\_photos target.  You can also backup to multiple targets by using:

    pyckup -s photos -t amazon_photos,local_photos

This way you can have a local copy for quick restores, as well as a backup in s3 for disaster recovery when your local backup dies.

The --help option should explain everything else you can do with pyckup.

#TODO

Only local files are currently working.  Amazon s3, CloudFiles, and scp support should be coming soon.

Support:
    --full-if-older-than
    --dry-run
    --file-to-restore
    --asynchronous-upload (experimental in duplicity)
    --time
    --restore-time
    --volsize


#Disclaimer
This software comes with no guarantees and very well may destroy your backups and burn your external hard drives.  Use at your own risk.

#License
This software is uncopyrighted.  Do whatever you like with it, recognition is appreciated.
