# Scripts

> Repository for various scripts

## Install

```
git clone <repository> ~/bin
```

## Usage

### borg

`borg` is a script to make a fully deduplicated and secured backup.  
[BorgBackup] is used to make a local backup on another device (USB disk or ssh) then [Rclone] is used to sync this backup to a cloud provider (currently [Hubic]).

Before running the script you need to create a [BorgBackup] repository :
```
borg init --encryption=repokey /path/to/repo
```

Then you need to create a file `borg.conf` with the repository key passphrase (**do not commit or share this file ever !**) :
```
BORG_REPOKEY_PASSPHRASE="your passphrase"
```

You can also create a file `borg.exclude` to exclude paths from backup.

For [Rclone] you need to create one or two new remotes :

  - one sftp remote for your local backup (source)
  - one cloud remote for the cloud backup (destination)

#### Checking a backup

Regularly backing up your data is only half the job, you also need to regularly check that these backups are useable !  

For local backups you can run these commands :
```
borg check <repository or archive>
borg extract --dry-run <archive>
```

For cloud backups you need first to retrieve the data using [Rclone] :
```
rclone copy <remote>:<path> <local path>
```

Then you can use the previous [BorgBackup] commands to check and verify the integrity of the data.

### shrinkpdk

`shrinkpdf` is a script to optimize the size of a PDF file.  

```
./shrinkpdf <mypdf.pdf>
```

You might change the quality setting directly in the script :

  - `screen` for smaller size and quality
  - `ebook` for medium size
  - `prepress` or printer for best quality

## License

MIT © Benoît Giraudou

[BorgBackup]: https://borgbackup.readthedocs.io
[Rclone]: https://rclone.org/
[Hubic]: https://hubic.com
