# Basic cURL commands

- `curl`: Runs the program.
- `curl --help`: Lists all the options you can use.

## Basic GET requests
- `curl https://exampleurl.com/posts`: GETs data from `/posts`.
- `curl https://exampleurl.com/posts/4`: GETs data from post `4` of `/posts`.
- `curl -I https://exampleurl.com/posts`: GETs the head data from `/posts`.

### Outputting to a file
- `curl -o output.txt https://exampleurl.com/posts`: Outputs data from `/posts` to a file called `output.txt`.

### Downloading a file
- `curl -O https://exampleurl.com/posts`: Downloads data from `https://exampleurl.com/posts`.

## Basic POST requests
- `curl -d "title=Hello&body=Hello World" https://exampleurl.com/posts/`: POSTs data to `/posts`.

## Basic PUT requests
- `curl -X PUT -d "title=Hello&body=Hello World" https://exampleurl.com/posts/4`: PUTs data to `posts/4`.

## Basic DELETE requests
- `curl -X DELETE https://exampleurl.com/posts/4`: Deletes the data at `https://exampleurl.com/posts/4`.

## Testing
To experiment with any of these commands (without the risk of doing something horrendous) use the endpoints listed on https://jsonplaceholder.typicode.com/
