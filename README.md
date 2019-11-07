# Platform Source Map Debugging Guide

The purpose of this project is to demonstrate how our Platform partners can improve debugging capabilities for [manifoldco/ui][ui-project].

## How It Works

Platforms can bundle the UI project and generate source maps that will be available only to UI developers who have access to the files. At a high level, the process would work as follows:

1. Generate source maps as part of the production build.
1. Point the sourceMappingURL pragma to a localhost URL.
1. Upload the source maps to a secure location.
1. Make sure that Manifold developers have access to this location.
1. Manifold developers will run a server at the localhost URL that redirects to the secure location.

The idea for this process came from [a blog post][production-source-maps] which describes it in further detail.

## How This Demo Does It

The project in this repository uses Webpack to bundle the code and generate the source maps, using `localhost:5050` for the sourceMappingURL pragma. It then moves the source maps to another location and runs an HTTP server that will serve the source map files.

### What's Missing From This Demo?

For simplicity, this demo skips the security step. In a real world scenario, the source maps would probably be served by a server that requires an API key or an auth token. The local server that Manifold developers run would have this token, and would send it to the secure server with every request for a source map file. Alternatively, Manifold developers could log into a service that allows them to download the source maps to their local machines.

## To Run This Project

Clone the repository and switch to the project directory. Then,

```
npm install
npm run start-production
```

The application will run on localhost:8080, and you'll be able to debug your code by expanding the `webpack` node in the file tree shown in the "Sources" tab of your devtools.

TODO: add a screenshot

[ui-project]: https://github.com/manifoldco/ui
[production-source-maps]: https://itnext.io/using-sourcemaps-on-production-without-revealing-the-source-code-%EF%B8%8F-d41e78e20c89
