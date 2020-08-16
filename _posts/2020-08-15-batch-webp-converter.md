---
published: true
---
# Batch image conversion to webp

Converting images to various formats and sizes for the web is a modern necessity. Some services automate image conversion or delivery but sometimes manual processing makes the most sense. 

One of the common image formats on the web is webp from Google. ImageMagick, which is a brilliant and highly capable tool, can convert to and from webp pretty handily but often all I want is to generate a set of webp versions from a folder of images. Google has released their [conversion tools][1] for webp (which ImageMagick uses too) and I decided to create a fish function so with a simple command I can batch convert all images in the current folder.

## An aside about fish
I like fish as it just works (for me), I don't have to set up an rc file so I can get command history (*cough* zsh *cough*) and I don't need to find and install a plethora of plugins for sensible features such as syntax highlighting or history-based autocomplete. If you don't use fish then the scripts shown won't work, you are welcome to make a version for your preferred shell.

## The function

Since cwebp converts one file at a time, each file needs to be fed into the tool separately. It is really easy to set up a simple batch convert for a set of images of one file type like this:

```
for file in *.jpg
	cwebp -o (basename $file .jpg).webp $file
end
```

To make my script more thorough I made it check all jpg, jpeg and png file endings by default. The function can take options, which are implemented using argparse—which is similar to setopts. To check all images the function uses a list of file type endings `{jpg,jpeg,png}` and checks for all matches ending in `.$format`. To later use the list of matching files I create a sort of dictionary using a list of strings of the root name and the extension separated by `:_+_:` like this `my_image:_+_:.jpg`. When encoding each string can be separated into a two-element list where the root can have .webp appended and the full name can be recombined from these pieces.

The supported arguments are for help, decode and a subset of options like resize, I could add other options if I wanted to use them. Since I typically resize to fit a specific width and cwebp can automatically set the other dimension based on the aspect ratio, the function only takes one value for width. An editor or ImageMagick would be better for cropping or other adjustments, although cwebp does offer a cropping option.

The function will also decode webp to png, tiff or bmp; as supported by cwebp. Not only can I batch convert images in my folder but I can choose which file types to encode from, what size output and the conversion method easily. Here is the difference when converting a set of images to webp at 500px with my script vs cwebp directly. 

```
# with my script
wpc -r 500

# manually with cwebp
cwebp -o output_file_1.webp -quiet -mt -resize 500 0 input_file.png
cwebp -o output_file_2.webp -quiet -mt -resize 500 0 input_file.jpg
.
.
.
```

Not only is it far faster to only type one command for a batch rather than each image, but the actual command is also far shorter. This is because the name is chosen to be the same as the root name of the original file and the options that I pretty much always use are turned on already. Resizing requires only `-r` instead of `-resize` and takes just one argument rather than needing two.

You can see my full script as a gist below

<script src="https://gist.github.com/FraserEmbrey/7ab665cf4fc0268ea3f51dbdaccaf42d.js"></script>

[1]: https://developers.google.com/speed/webp/download
