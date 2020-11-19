# Geometry Utils Polyfill

TODO

But basically it will polyfill Geometry Utils defined here:
https://drafts.csswg.org/cssom-view/#the-geometryutils-interface

Geometry Utils is useful if you want to get coordinate from one Element to another.
It will respect all the positioning including the css transform.

Because it's not well defined in the specification, I will refer the implementation in Firefox Browser (because it's the only one that has already implemented getBoxQuads()).

Below is the copy-pasted from the specification

```
enum CSSBoxType { "margin", "border", "padding", "content" };
dictionary BoxQuadOptions {
  CSSBoxType box = "border";
  GeometryNode relativeTo; // XXX default document (i.e. viewport)
};

dictionary ConvertCoordinateOptions {
  CSSBoxType fromBox = "border";
  CSSBoxType toBox = "border";
};

interface mixin GeometryUtils {
  sequence<DOMQuad> getBoxQuads(optional BoxQuadOptions options = {});
  DOMQuad convertQuadFromNode(DOMQuadInit quad, GeometryNode from, optional ConvertCoordinateOptions options = {});
  DOMQuad convertRectFromNode(DOMRectReadOnly rect, GeometryNode from, optional ConvertCoordinateOptions options = {});
  DOMPoint convertPointFromNode(DOMPointInit point, GeometryNode from, optional ConvertCoordinateOptions options = {}); // XXX z,w turns into 0
};

Text includes GeometryUtils; // like Range
Element includes GeometryUtils;
CSSPseudoElement includes GeometryUtils;
Document includes GeometryUtils;

typedef (Text or Element or CSSPseudoElement or Document) GeometryNode;
```

More information about this:
https://hacks.mozilla.org/2014/03/introducing-the-getboxquads-api/
https://hacks.mozilla.org/2014/04/coordinate-conversion-made-easy/

Some stackoverflow regarding this:
https://stackoverflow.com/questions/6773481/how-to-get-the-mouseevent-coordinates-for-an-element-that-has-css3-transform/64909356#64909356
