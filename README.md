JH Labs Java Image Filters
==========================

Project originally available from: http://www.jhlabs.com/ip/filters/  
Original project author: Jerry Huxtable

Beyond the 'building' section, the text below is the description as found on Jerry
Huxtable's website.

## Building

You'll need both a Java JDK and [Apache Ant](https://ant.apache.org/) installed. 

Then to build, simply run `ant` in the current folder. The resultant
jar file will be in the `dist` folder.

## Java Image Filters

I have a large number of Java Image filters which are freely available for download
from this site.  The filters are all standard Java BufferedImageOps and can be
plugged directly into existing programs. All the filters are available in the Java
Image Editor and most have dialogs to allow you to play with their settings. If you
want to try out any of these filters, I recommend downloading the editor and using
the dialogs, which is generally much easier than writing code to try them.

Many of these filters are useful in applications such as games where images need to
be generated on the fly, or where it's quicker to generate them rather than
downloading them. For instance, it's quicker to download one image and rotate it
several times than to download several separate images.

Another use for the filters is in animation. For example animating the Water Ripple
filter can produce a nice rippling effect. Some of the filters have a time
parameter for this purpose.

## Philosophy and General Points

None of these filters are finely-tuned for speed, or even coarsely-tuned. Think of
them as sample code for writing your own filters. I've preferred floating-point
math over integer or fixed-point pretty well everywhere. By making the appropriate
changes you'll probably be able to get these to go quite a bit faster.

All of the filters are designed to work with TYPE_INT_ARGB images. Some may work
with other image types, but I make no guarantees.

All the filters are Java beans in the sense that they have default constructors and
a set of properties. None of them have BeanInfo classes. This is for three reasons:
firstly, the original versions predate the introduction of JavaBeans, and secondly,
a BeanInfo class doesn't provide enough information to do a good UI for the
properties, and thirdly, writing BeanInfo classes is really boring.

For the UI, we need all sorts of extra information that a BeanInfo doesn't provide:
permitted ranges for values, usage (is this float a distance or an angle? what are
its units?), grouping of properties and so on. Some of this could be overcome by
providing more classes, e.g. having an Angle class, but this would just complicate
usage and not provide any obvious benefit beyond a sort of warm object-oriented
glow. To do this, I've provided an XML file with each filter which specifies the UI.
The format of this file will probably change as the Image Editor UI evolves. The
filters don't support serialization. XMLEncoder does a much better job of handling
this and I encourage you to use that instead.

Some of the filters have position parameters, e.g. for specifying the centre of the
effect. These are generally expressed as a proportion of the width or height of the
image in the range 0 to 1 rather than being measured in pixels. This allows the same
filter settings to be applied to different size images.

Some filters, such as the transitions, take more than one source image. Where this
happens, there are often two ways to call the filter. The first way is to call
setXXX() methods on the filter for the extra images and then call the normal
filter() method. The second way is to call a new filter() method which takes an
array of images as its first parameter. The reasoning behind this is to allow the
use of the filters anywhere a BufferedImageOp is allowed, but also to make it more
convenient to use filters which require more than one source image.