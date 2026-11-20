# ClipParse Android SDK

The official ClipParse SDK for Android — extract structured recipes (ingredients, steps, timings) from TikTok and Instagram post links. Distributed as an Android library (AAR) on Maven Central.

## Requirements

- Android 6.0 (API level 23) or later
- Kotlin 2.0 or later

## Installation

Maven Central is already listed in the `repositories` block of most Android projects. Add the dependency to your app module's `build.gradle.kts`:

```kotlin
dependencies {
    implementation("com.clipparse:clipparse-android-sdk:1.1.0")
}
```

The SDK uses one permission, `INTERNET`, which it declares in its own manifest.

## Usage

Create a client with your API key, then extract a recipe from a TikTok or Instagram link. `extract` is a suspending function: call it from a coroutine. It is safe to call from the main thread.

```kotlin
import com.clipparse.sdk.ClipParseClient
import com.clipparse.sdk.model.ExtractionResult

val client = ClipParseClient(context, apiKey = "<your API key>")

val url = "https://www.tiktok.com/@somecreator/video/1234567890"
when (val result = client.extract(url)) {
    is ExtractionResult.Success -> {
        val recipe = result.recipe
        println(recipe.title)
        println("${recipe.servings} servings, ${recipe.prepTimeMinutes} min prep, ${recipe.cookTimeMinutes} min cook")
        for (ingredient in recipe.ingredients) {
            println("${ingredient.name} ${ingredient.quantity ?: ""} ${ingredient.unit?.raw ?: ""}")
        }
        for (step in recipe.steps) {
            println(step.text)
        }
    }
    is ExtractionResult.NoRecipe -> println("No recipe found: ${result.reason}")
}
```

The client reads your app's package name from the `Context` and does not keep a reference to it, so any context works.

### Error handling

Failures throw a `ClipParseException`. Its `code` says what went wrong, so you can give users specific feedback:

```kotlin
import com.clipparse.sdk.ClipParseErrorCode
import com.clipparse.sdk.ClipParseException

try {
    val result = client.extract(url)
} catch (e: ClipParseException) {
    when (e.code) {
        ClipParseErrorCode.PlatformUnsupported -> {
            // Only TikTok and Instagram links are supported
        }
        ClipParseErrorCode.PostUnavailable -> {
            // The post was deleted, is private, or doesn't exist
        }
        ClipParseErrorCode.InvalidApiKey -> {
            // Check the API key configured for this client
        }
        ClipParseErrorCode.RateLimited, ClipParseErrorCode.QuotaExceeded -> {
            // Wait for e.retryAfter before trying again
        }
        else -> if (e.isRetryable) {
            // Transient failure (e.g. network) — safe to retry
        }
    }
}
```

Always keep the `else` branch: new error codes can be added over time, and the SDK passes on a code it doesn't know yet as is.
## Privacy

[DATA_SAFETY.md](DATA_SAFETY.md) lists what the SDK sends and to whom, to help you fill in Google Play's Data safety form.

## License

This SDK is distributed under the ClipParse SDK License. See [LICENSE](LICENSE) for details.
