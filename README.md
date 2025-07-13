Here’s a `README.md` in Markdown format, written in code block syntax, that mirrors the style of your Brainfuck interpreter README — but for your ultra-lightweight Java web server project:

````markdown
# Ultra-Lightweight Java WebServer

This repository contains an extremely lightweight Java HTTPS web server built with minimal dependencies. It is designed to serve static files, handle basic API endpoints, and parse JSON requests.

## Features

- Native HTTPS support using `.p12` certificates.
- Static file hosting with custom routing.
- Lightweight JSON parsing using `Gson`.
- POST/GET routing with simple lambda mappings.
- Minimal dependencies for fast startup and low resource usage.
- No frameworks like Spring — just plain Java and a few utility classes.

## How it Works

The server initializes on port `443` using an HTTPS certificate, and supports the following routes:

### Static File Hosting

```java
webServer.prepareStaticFiles("/", "/home/page/");
````

This serves static files (like `index.html`, CSS, JS) from the `/home/page/` directory.

### GET Mapping Example

```java
webServer.getMapping("/", (request, response) -> {
    response.writeFile("/home/page/index.html");
});
```

### POST API Endpoints

* `/results`: Returns previously cached results by key.
* `/submit`: Accepts a base64 image and returns a unique key for results.
* `/captcha`: Verifies a Turnstile CAPTCHA and caches valid tokens.

## Dependencies

Only the following are used:

* [`Gson`](https://github.com/google/gson): For parsing JSON.
* [`Apache Commons Lang`](https://commons.apache.org/proper/commons-lang/): For generating secure random strings.

No heavyweight web libraries are included.

## Compilation

Use `javac` to compile:

```bash
javac -cp ".:gson-2.10.1.jar:commons-lang3-3.12.0.jar" -d out src/**/*.java
```

Ensure you replace the version numbers with the ones you use, and the paths accordingly.

## Running

Use the compiled output with the classpath and your certificate:

```bash
java -cp ".:out:gson-2.10.1.jar:commons-lang3-3.12.0.jar" me.meiallu.sayori.Main
```

## Example HTTPS Certificate

Use a `.p12` certificate, and pass it to the server like:

```java
new WebServer(443, "/home/certificate.p12", "your_password");
```

## File Upload + Processing

The `/submit` route allows uploading an image as a base64 string, saves it to disk, and processes it with a `ResultList`.

```json
{
  "image": "data:image/png;base64,...",
  "token": "captcha-token"
}
```

A unique result key is returned and used later via `/results`.

## Limitations

* No concurrent request handling — keep usage light.
* No session management or auth system.
* Must manage `.p12` certificates manually.

## Why?

This server was built for environments where minimalism, speed, and control matter more than scalability or full-stack features.

## License

MIT — do whatever you want with it.

```

Let me know if you'd like the README to include API response examples, certificate generation steps, or Docker support.
```
