# Releasing

From a direct clone (rather than a fork), as the release process will push the new tags and update the version to the 
next -SNAPSHOT as well. You will need permission in sonatype to push to akka repositories.

* sbt -Dpublish.maven.central=true
  * release skip-tests
* check out the new tag and perform a release for other scala versions (`++2.12...` then `publishSigned`)
* close the staging repo in sonatype (https://oss.sonatype.org/#welcome)
* verify the contents of the staging
* release the staging repo in sonatype
* push to origin including tags
* SCP docs to gustav (the akka docs server)
  - `VERSION=....`
  - `scp -r docs/target/paradox/site/main/* akkarepo@gustav.akka.io:www/docs/akka-stream-kafka/$VERSION/`
  - `scp -r core/target/api/* akkarepo@gustav.akka.io:www/api/akka-stream-kafka/$VERSION/`
* Update the current links on gustav
  - `ssh akkarepo@gustav.akka.io`
  - `cd www/docs/akka-stream-kafka/; ln -snf VERSION current`
  - `cd`
  - `cd www/api/akka-stream-kafka/; ln -snf VERSION current`

If you don't have access to gustav ask someone from the core Akka team to do it or give you access.
