# fuel-comfy 
[![Kotlin](https://img.shields.io/badge/Kotlin-1.3.21-blue.svg)](https://kotlinlang.org)
[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2Falexxxdev%2Ffuel-comfy.svg?type=shield)](https://app.fossa.io/projects/git%2Bgithub.com%2Falexxxdev%2Ffuel-comfy?ref=badge_shield)
[![](https://jitpack.io/v/alexxxdev/fuel-comfy.svg)](https://jitpack.io/#alexxxdev/fuel-comfy)
![](https://img.shields.io/github/license/alexxxdev/fuel-comfy.svg?style=flat)

More comfortable use of [Fuel](https://github.com/kittinunf/fuel) as in [Retrofit](https://square.github.io/retrofit/) or [Feign](https://github.com/OpenFeign/feign) for Kotlin/Android

## Basics

Usage typically looks like this

```kotlin
@FuelInterface
interface GitHubService {

    @Get("repos/{owner}/{repo}/contributors")
    fun contributors(@Param("owner") owner: String, @Param("repo") repo: String): Result<Contributor, Exception>
}

FuelManager.instance.basePath = "https://api.github.com/"

val service = FuelManager.instance.setInterface(GitHubService::class)
val contributors = service.contributors("alexxxdev", "fuel-comfy")
contributors.fold({ list ->
            // TODO
        }, { exception ->
            // TODO
        })

```

## Features
- [x] HTTP GET/POST/PUT/DELETE/HEAD/PATCH requests
- [x] Serialization/Deserialization using [fuel-kotlinx-serialization](https://github.com/kittinunf/fuel/tree/master/fuel-kotlinx-serialization)
- [x] Support `suspend` function
- [ ] Serialization/Deserialization using [Gson](https://github.com/google/gson)
- [ ] Maybe something else ...
<br><br>

### Interface Annotations

#### @FuelInterface

Defines the interface for fuel-comfy

#### @Get

Defines the GET HttpMethod and UriTemplate for request. Expressions, values wrapped in curly-braces {expression} are resolved using their corresponding @Param annotated parameters.

#### @Post

Defines the POST HttpMethod and UriTemplate for request. Expressions, values wrapped in curly-braces {expression} are resolved using their corresponding @Param annotated parameters.

#### @Param

Defines a template variable, whose value will be used to resolve the corresponding template Expression, by name.

#### @Header

When used on a Interface, will be applied to every request. When used on a Method, will apply only to the annotated method.

```kotlin
@FuelInterface
@Headers("Accept: application/json")
interface GitHubService {

  @Headers("Content-Type: application/json")
  @POST("...")
  fun post()
}
```

#### @QueryMap

Defines a Map of name-value pairs, to expand into a query string.

```kotlin
@FuelInterface
interface GitHubService {

  @GET("...")
  fun get(@QueryMap params: Map<String, Any>)
}
```

#### @Query

Defines name-value pair, to expand into a query string.

```kotlin
@FuelInterface
interface GitHubService {

  @GET("...")
  fun get(@Query("id") id: Int)
}
```

####  @Body	

Defines a request body

```kotlin
@FuelInterface
interface GitHubService {

  @GET("...")
  fun get(@Body contributor: Contributor)
}
```

<br><br><br>
## Installation
Add it in your root build.gradle at the end of repositories:
```groovy
allprojects {
    repositories {
        ...
        maven { url 'https://jitpack.io' }
    }
}
```
Add the dependency
```groovy
dependencies {
    implementation 'com.github.alexxxdev.fuel-comfy:api:-SNAPSHOT'
    kapt 'com.github.alexxxdev.fuel-comfy:processor:-SNAPSHOT'
}
```


## License
[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2Falexxxdev%2Ffuel-comfy.svg?type=large)](https://app.fossa.io/projects/git%2Bgithub.com%2Falexxxdev%2Ffuel-comfy?ref=badge_large)