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

## com/google — ML Kit resilience mirror (GAME-1121)

`com/google/**` is NOT this library's code. It is a static mirror of the ML Kit
segmentation AARs the Thug Life background-removal feature depends on:
`play-services-mlkit-subject-segmentation:16.0.0-beta1` and
`segmentation-selfie:16.0.0-beta6` plus their transitive ML Kit deps. Both are
abandoned Google betas (one release ever / never left beta); a Google-side
removal would otherwise break clean-room builds with no recovery. Insurance,
same pattern as the `com/flocmedia/photoeditor` mirror. Regenerable from
`dl.google.com` / the Gradle cache. The app resolves it through the existing
`raw.githubusercontent.com/flocmedia/photoeditor-maven` repository entry.

`play-services-mlkit-face-detection:17.1.0` was added under GAME-742 (the
face-detection revival spike). It is the only face-detection-specific artifact
that needed mirroring: its ML Kit transitive deps (`common`, `vision-common`,
`vision-interfaces`, `com.google.android.odml:image`) resolve UP to the exact
versions already mirrored for segmentation, and its remaining transitives
(`play-services-base`/`-basement`/`-tasks`, `datatransport`, `firebase-encoders`)
are actively-served Google infra, out of scope for this mirror by the same
boundary as the segmentation entries above. It stays here even if GAME-742's app
change is not merged — 17.1.0 is the newest published face-detection release, so
the insurance is valid regardless.
