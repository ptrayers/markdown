# Publish SA Config Settings
 * Pull SA config XML files from *Internal Engineering* Repo 
   * http://stash.fms.allfinanz.com/projects/BRIG/repos/brighthouse/browse
   * link top left provides URL to clone i.e
     * http://stash.fms.allfinanz.com/scm/brig/brighthouse.git

 * Update local properties settings external to SA config 
   * Set support.skip.db=true in allfinanz.properties

 * Wipe the database;
   * Copy the configure/publish JAR file locally from
     * \\\\abate\data\Releases\Internal Releases\IS Product Suite 4.19
     * file: URE-4.19.1.31-distribution.zip
   * Run configure to wipe all data
     * configure -a https://<domain:port>/allfinanz/publish <user> <password>

 * Publish the SA config files
   * configure -p https://<domain:port>/allfinanz/publish admin abc123 C:/<local_folder>/brighthouse/DEV/bhf-users.xml
   * configure -p https://<domain:port>/allfinanz/publish admin abc123 C:/<local_folder>/brighthouse/DEV/ais-profiles.xml
   * configure -p https://<domain:port>/allfinanz/publish admin abc123 C:/<local_folder>/brighthouse/DEV/allfinanz.xml

