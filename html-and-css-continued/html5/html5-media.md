# Lesson: HTML5 Media

## Notes

### Audio Elements in HTML5

- To include audio in a website, use the `<audio>` element. Inside the element, we provide `<source>` elements whose `src` attributes point to a file on the server and whose `type` attributes specify what type of media it is.
  - The `type` name is the "MIME standard" for the filetype. MDN provides a long list of [MIME types](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types/Complete_list_of_MIME_types).
- Files fit into two big buckets: binary and text. Sometimes we need to be more specific within those groups. A MIME type is a way to note _exactly_ what type of file is present and it's more precise than a simple file extension.
  - Examples: `text/html`: a text file that's also HTML, `video/mpeg`: a binary file that's also an MPEG movie
- To pull it all together, the `type` attribute should be set to the "MIME type" for the media pointed to by the `src` attribute for each `<source>` element.
- The `controls` attribute is required to display the audio controls to start and pause playback, adjust the recording's volume, etc. The presence of the `controls` attribute name itself is sufficient, no other properties are needed. There are optional attributes you can provide such as `autoplay` and `loop`. All available audio options can be found [here](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/audio).
- You can provide multiple source files for playback. If the browser does not recognize the first file type, it will ignore it and move on to the next. If neither of the formats are supported, it will instead display any included message. If the browser is able to play one of the source files, it will ignore any other code below until it reaches the closing `</audio>` tag.

### Video Elements in HTML5

- Embedding a video is very similar to embedding audio. This can be done using the `<video>` tag. Inside the video tag are source tags that point to the location of various file formats and specify their MIME types.

## Code Examples

### Audio Element

```html
<audio controls>
  <source src="purrr.mp3" type="audio/mp3">
  <source src="purrr.ogg" type="audio/ogg">
  <p>Sorry your browser doesn't support HTML5 Audio! Please <a href="http://browsehappy.com/?locale=en">upgrade your browser</a>.</p>
</audio>
```