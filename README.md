#libwebvtt
The library for interpreting and authoring conformant WebVTT content
WebVTT is a caption and subtitle format designed for use with HTML5
audio and video elements.

See: [W3C WebVTT Draft](http://dev.w3.org/html5/webvtt/)

##Build Instructions:

In Unix-like environments, we use autotools:

```
./bootstrap.sh && ./configure && make
```

On Windows, we use a Visual Studio Project, see files in build/msvc2010

##Routines available to application:
### Parser object routines
	webvtt_status webvtt_create_parser( webvtt_cue_fn_ptr, webvtt_error_fn_ptr,
		void *, webvtt_parser * );
	void webvtt_delete_parser( webvtt_parser );
	webvtt_status webvtt_parse_chunk( webvtt_parser, const void *, webvtt_uint );

### String object routines
	webvtt_status webvtt_string_new( webvtt_uint32, webvtt_string * );
	void webvtt_string_delete( webvtt_string );
	webvtt_status webvtt_string_append_utf8( webvtt_string *, const webvtt_byte *,
		webvtt_uint *, webvtt_uint, webvtt_utf8_reader );

### Memory allocation routines
	void *webvtt_alloc( webvtt_uint );
	void *webvtt_alloc0( webvtt_uint );
	void webvtt_free( void * );
	void webvtt_set_allocator( webvtt_alloc_fn_ptr, webvtt_free_fn_ptr, void * );

### Error handling
	const char *webvtt_strerror( webvtt_error );

##TODO:
- *** IMPORTANT *** Implement routine to validate cue-text and produce a tree of nodes
- Normalize routine names ( webvtt_create_XXX, webvtt_delete_XXX, rather than webvtt_XXX_new, webvtt_XXX_delete)
- node-ffi bindings for libwebvtt structures and public API, to assist with unit testing
- New unit tests, and convert some existing conformance tests to unit tests
- Integration with TravisCI
- Bug fixes
- Thread-safety where needed (Lock before setting global function pointers)
- Reference counting objects (may be a hassle, but would help to prevent leaking
  dropped cue objects)
- Improvements to lexer/parser state machines, in terms of speed and conformance
- Default error handlers when not provided by user
- Internationalized error messages
- Shared-library compilation
- Routines for generating conformant WebVTT text
- Language bindings (Rust, C++, D, etc)
- GNU Autotools build system to enhance portability (With MPL2'd M4 from Mozilla-Central to support Windows environments)
