# Travis configuration for publish artifact to GitHub release

Configuration of `.travis.yml` for publish JSupport artifact to GitHub release:

```yml
language: java

jdk:
- oraclejdk8
- openjdk7
- openjdk8

before_deploy:
- mvn help:evaluate -N -Dexpression=project.version|grep -v '\['
- export project_version=$(mvn help:evaluate -N -Dexpression=project.version|grep
  -v '\[')

deploy:
  provider: releases
  api_key:
    secure: KUpD+6aaADsFgShdfJudBvGlxWGhnaOYcP77jTXIrQw1CjX4731RkvNPI96e6Bm+vfkRyNmClySS1jY6wlfF14fMok1q6131IblgUbNzaDTZ1iXUkJocFjpS9xSwehW0+Sft8ECBog1znoC9nPAJpwHybpW7GteQv98XykSmiucBuUB8G4UIzC5f1aEJrUpJ8O1/HYhRIOwA151mcn0+z7+gFAKFs7/oi+SuYrn+bCrxU+DHupS5po9QdoqXvZyq0aKsmp7NhzccYco73HrneE3wK2yCx6jx6jpcv6RAUZwfhlQj3f2gN6pfwc+Z0LtcrdgEaAEOgDhMqToi14PYAsaCB/eIHYJCHJHqvL75z6QTrutVI2JWT7Xymb8JCrJCaNNR+2QQHCdf1hfGOP99G5GkLST76uzA6MNbVY2qMxlIxdDDqbfJDJ3wOLsnvS8wfzhUM4VQ+RvD7+Rv2EMT9boqLbCJefyiNte2ZOvRna9YhKha4+5ZOPVlC3QTo0C1TqnjDL+MCOm9NqorqNr40vfD+jirsYXNxaYo8fKnEHrzoqO7868KSSx/2sa9707pD08OEiJZ34w9uumKYcKXVXEbS8EKBqDhC1f/LXYc7lUTYW1ls06xwmeYRehIdJGJbCuKEkX97CMK0KvmiSbWR7ptQq0oRhudvTSPY3G+uGM=
  file:
    - target/jsupport-$project_version.jar
    - target/jsupport-$project_version-javadoc.jar
    - target/jsupport-$project_version-sources.jar
  skip_cleanup: true
  on:
    repo: mforoni/jsupport
  name: $project_version

notifications:
  on_success: never
  on_failure: always
```