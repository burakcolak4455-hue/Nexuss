name: Build
on: [push, workflow_dispatch]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: unzip -q nexus-client-1.21.1.zip -d proj
      - uses: actions/setup-java@v4
        with:
          distribution: temurin
          java-version: 21
      - uses: gradle/actions/setup-gradle@v4
        with:
          gradle-version: "8.8"
      - run: gradle build
        working-directory: proj
      - uses: actions/upload-artifact@v4
        with:
          name: nexus-jar
          path: proj/build/libs/*.jar
