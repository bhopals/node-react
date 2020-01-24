## Call back hell problem

These are some basic principles that can help us keep the nesting level low and improve the organization of our code in general:

• You must exit as soon as possible. Use return, continue, or break, depending on the context, 
  to immediately exit the current statement instead of writing (and nesting) complete if/else statements. This will help keep our code shallow.

• You need to create named functions for callbacks, keeping them out ofclosures and passing intermediate results as arguments. 
	Naming our functions will also make them look better in stack traces.

• You need to modularize the code. Split the code into smaller, reusable functions whenever it's possible.

EXAMPLE Code - (Problem)

function spider(url, callback) {
var filename = utilities.urlToFilename(url); fs.exists(filename, function(exists) {
//[1]
if(!exists) {
console.log("Downloading " + url); request(url, function(err, response, body) {
    if(err) {
      callback(err);
} else {
mkdirp(path.dirname(filename), function(err) {
if(err) {
  callback(err);
} else {
fs.writeFile(filename, body, function(err) { //[4]
                   if(err) {
                     callback(err);
} else {
callback(null, filename, true);
} });
} });
} });
} else {
callback(null, filename, false);
} });
}


Solution:
function spider(url, callback) {
var filename = utilities.urlToFilename(url); fs.exists(filename, function(exists) {
if(exists) {
return callback(null, filename, false);
}
download(url, filename, function(err) {
         if(err) {
           return callback(err);
}
callback(null, filename, true); })
}); }





## Node Js Stream

Spatial efficiency
Time efficiency
Compasability

Anatomy of streams
Every stream in Node.js is an implementation of one of the four base abstract classes available in the stream core module:
• stream.Readable
• stream.Writable
• stream.Duplex
• stream.Transform