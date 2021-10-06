# SDP Jetpack Compose

Kotlin Extension function to use [sdp](https://github.com/intuit/sdp) in Jetpack Compose.

## Installation
add [sdp](https://github.com/intuit/sdp) to your project (Using Android Studio and Gradle):
```
  dependencies {
    implementation 'com.intuit.sdp:sdp-android:1.0.6'
  }
  ```

## Usage

```kotlin
@Composable
private fun Int.sdpGet(): Dp {

    val id = when (this) {
        in 1..600 -> "_${this}sdp"
        in (-60..-1) -> "_minus${this}sdp"
        else -> return this.dp
    }

    val resourceField = getFieldId(id)
    return if (resourceField != 0) dimensionResource(resourceField) else this.dp

}

@Composable
private fun getFieldId(id: String): Int {
    val context = LocalContext.current
    return context.resources.getIdentifier(id, "dimen", context.packageName)

}

val Int.sdp: Dp
    @Composable
    get() = this.sdpGet()

@Composable
private fun Int.textSdp(density: Density): TextUnit = with(density) {
    this@textSdp.sdp.toSp()
}

val Int.textSdp: TextUnit
    @Composable get() = this.textSdp(density = LocalDensity.current)

```

## Contributing
Pull requests are welcome.
