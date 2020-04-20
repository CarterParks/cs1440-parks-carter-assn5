# 1. Requirements

* Your program will accept one or two command line arguments:
    0.  The starting URL specified as an absolute URL (see below for an explanation of what an absolute URL is)
        *   Print an error message when this argument is not given
        *   Print an error message when the user-specified URL is not absolute
    1.  *[Optional]* the maximum distance in number of links from the starting website to navigate.  When this parameter is not supplied or is not a positive integer your program will default to `3` links.
*   Update the function `crawl()` to take the following parameters:
    *   `url`: an absolute URL
    *   `depth`: the current depth of recursion
    *   `maxdepth`: the maximum depth of recursion
    *   `visited`: a `set` of URLs which have already been visited
*   The return value of `crawl()` does not matter and may be ignored
*   Supply a starting distance of `0` the first time `crawl()` is called in
    your program.  In other words, the initial URL supplied from the command
    line is considered to be depth **0**.
*   You may supply an empty set as the initial value of `visited`.  If there
    are some URLs which cause your program to behave poorly, you can add them
    to `visited` to avoid them later.
*   Each time `crawl()` is called
    *   If the current value of `depth` exceeds `maxdepth`, immediately return from `crawl()`
    *   Otherwise, fetch the webpage indicated by `url`
        *   Report any exceptions that are raised and proceed to the next URL.
            Your program *must not crash* when an unreachable resource is
            encountered.
    *   Scan the resulting HTML for anchor tags `<a>`.  If the anchor tag has an `href` attribute:
        *   Discard the URL indicated by the `href` attribute if it does
            not specify a resource reachable by either the HTTP or HTTPS
            protocols.  The **Requests** library only understands these two
            protocols.
        *   Determine whether the `href` attribute refers to an absolute
            URL.  If not, make it into an absolute URL by using the
            `urljoin()` function.
        *   Discard the *fragment* portion of the URL, if present.
    *   Check whether the newly-formed absolute URL has been visited before
        *   If it has, loop to the next anchor tag found in the document
        *   Otherwise, record this URL into `visited` and proceed
            *   Print out the URL, using indentation to indicate the current
                depth of recursion.  Output four spaces  for each level of
                recursion (see the sample output below)
            *   Repeat the entire process by recursively calling `crawl()` upon
                this URL

# 2. Design

The starter code will remain the same, except for the following changes:
* Print this URL with indentation indicating the depth of recursion
* crawl() must be able to keep track of the max depth: no globals allowed!
* Don't just print URLs found in this document, visit them!
* Trim fragments ('#' to the end) from URLs
* Use a data structure to track whether you've already visited a URL
* Call crawl() on unvisited newly formed URLs
* Don't visit a URL if you've reached the max depth of recursion

## Input
The program will take an absolute URL and an optional number of levels to follow links.

## Processing
The processing will be handled by the starter code, and will consist of traversing a webpage for links that will then be followed and traversed, recursively.

## Output
The visited URLs will be printed to the screen.

# 3. Implementation
* The program is contained in the file `src/crawler.py`.
* The user is prompted for information on the console with Python's built-in `input()` function.
* The user's input URL is searched for link, will follow those links if the maximum depth has not been reached, and will print the URL of the page to the terminal.

# 4. Verification

## Test Case 1
The command 
```bash
python src/crawler.py http://unnovative.net/level0.html 30
```
will be run to verify that the program does not infinitely loop.
## Test Case 2
The command 
```bash
python src/crawler.py http://cs.usu.edu
```
will be run to verify that the program runs as expected.