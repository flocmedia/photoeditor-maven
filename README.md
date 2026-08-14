# photoeditor-maven

Built releases of [flocmedia/PhotoEditor](https://github.com/flocmedia/PhotoEditor)'s
`photoeditor` library (`com.flocmedia:photoeditor`), published as a static Maven repository.

**No source code lives here.** This repo exists solely so the built `.aar`/`.pom`/sources
`.jar` can be consumed publicly and anonymously, while the source repo stays private.
Artifacts are published automatically by CI on every push to `flocmedia/PhotoEditor`'s
`production` branch — nothing here is hand-edited.

## Usage

```gradle
repositories {
    maven { url = uri("https://raw.githubusercontent.com/flocmedia/photoeditor-maven/main/") }
}

dependencies {
    implementation 'com.flocmedia:photoeditor:<version>'
}
```

No credentials needed -- `raw.githubusercontent.com` serves these files as plain static
content, so this resolves anonymously.

Browse available versions under `com/flocmedia/photoeditor/`.

## License

MIT, same as the source library -- see [LICENSE](LICENSE).
