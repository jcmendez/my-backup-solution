## Summary

This is what I use to backup my Linux laptops.  I think it is a robust backup solution 
that only uses code, leverages S3 and Glacier for storage, with version control for scripts.
It also implements periodic sanity checks and cleanup routines

## Dependencies

* Duplicity for backups
* PGP for encryption.

## Overall structure

### Bucket Creation and Policy Setup Script (Script 1):

* Create an S3 bucket specifically for backups.
* Configure a bucket policy to restrict access.
* Optionally enable versioning for additional protection against accidental deletions.

### Backup Script (Script 2):

* Utilize Duplicity for incremental backups to S3.
* Encrypt backups with PGP using a secure key.
* Schedule the script for periodic execution (e.g., using cron).

### Sanity Check Script (Script 3):

* Attempt to restore a small test file from the backup.
* Verify the integrity of the restored file.
* Schedule the script for periodic execution to ensure backup health.

### Cleanup and Archival Script (Script 4):

* Identify older backups based on retention policies.
* Transition these backups to Glacier for long-term, cost-effective storage.
* Optionally delete very old backups entirely to manage costs.


## Key Considerations

No guarantees provided by using this repo.  If you decide to use it, take into account

* **Security**: Ensure PGP keys are stored securely and never committed to version control


## Guiding principles

As this solution evolved, these are key aspects I took into consideration:
* **Error Handling**: Implement robust error handling in all scripts to gracefully handle potential issues.
* **Testing**: Thoroughly test each script individually and the entire workflow before relying on it for critical backups.
* **Documentation**: Include clear comments and documentation within each script to aid understanding and maintenance.