# java-dropwizard-squeegee

`squeegee` is a simple [Dropwizard-based](http://www.dropwizard.io/) HTTP pony to convert SVG documents in to PNG files using the [Batik](https://xmlgraphics.apache.org/batik) SVG transcoder.

## How to start the squeegee application

1. Run `mvn clean install` to build your application
1. Start application with `java -jar target/squeegee-0.1.jar server config.yml`
1. To check that your application is running enter url `http://localhost:8080`

## Usage

Given a file like [this](examples/circles.svg):

```
<?xml version="1.0"?>
<svg version="1.1" xmlns="http://www.w3.org/2000/svg">
  <circle cx="200" cy="200" r="199" style="fill: red; stroke: blue; stroke-width: 0"/>
  <circle cx="200" cy="200" r="150" style="fill: blue; stroke: green; stroke-width: 5"/>
  <circle cx="200" cy="200" r="50" style="fill: yellow; stroke: orange; stroke-width: 7"/>    
</svg>
```

You would invoke `squeegee` like this:

```
curl -s -v -X POST -F svg=@circles.svg http://localhost:8080
```

Which would produce [this](examples/circles.png):

![circles](examples/circles.png)

## Docker

[Yes](Dockerfile). For example:

```
docker build -t squeegee .
docker run -it -p 6161:8080 squeegee
curl -s -v -X POST -F svg=@circles.svg http://localhost:6161 > circles.png
```

## Caveats

* This does not have a (Dropwizard) health check yet. [It should](https://github.com/whosonfirst/java-dropwizard-squeegee/issues/1).

## Things that `squeegee` can't do yet

* User-defined image dimensions - or more specifically, it doesn't resize images particularly well yet; you can pass a `height` and `width` parameter with your request and see for yourself but you should be aware _this functionality might still be removed_
* User-defined (CSS) stylesheets
* That other thing you're wondering about that I haven't thought of yet

## See also

* https://xmlgraphics.apache.org/batik/using/transcoder.html
* http://www.dropwizard.io/1.0.0/docs/index.html
