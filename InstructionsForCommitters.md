# How to commit code changes #

  * commit all source files that have changed or that have been added or deleted.
  * after the above step completes successfully, update your local svn (this updates the local revision number to the latest in the repository)
  * run "ant jar" to update the jars with the latest revision number (file svn.version)
  * commit the new jar files and svn.version file.