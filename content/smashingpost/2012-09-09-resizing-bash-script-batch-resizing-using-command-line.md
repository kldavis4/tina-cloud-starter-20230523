---
title: Batch Resizing Using Command Line and ImageMagick
slug: resizing-bash-script-batch-resizing-using-command-line
image: null
date: 2012-09-09T14:17:46.000Z
author: vlad-gerasimov
description: >-
  If you deal with images, sooner or later you will want to **automate the
  repeating process of saving different sizes** from one source image.
categories:
  - Coding
  - Freebies
  - Techniques
---
If you own Adobe Photoshop and do not save too many output sizes, Photoshop actions are probably quite enough for your needs. However, keeping a Photoshop action up-to-date is quite painful — change a source folder, and you're screwed.

As you probably noticed in Smashing Magazine's <a href="https://www.smashingmagazine.com/2012/08/31/free-desktop-wallpaper-calendar-september-2012/">monthly desktop wallpaper series</a>, especially if you work on wallpapers, preparing them for a plethora of desktop resolutions is quite a task. On my own wallpapers website (<a href="https://www.vladstudio.com">Vladstudio</a>), I generate more than 300 JPEG files for each wallpaper! I want my art to reach as many devices as possible, which means I need to publish my wallpapers in as many sizes as I can support. On the other hand, I do not want to spend the rest of my life resizing my artworks — I'd rather draw new ones!

## <span class="rh">Further Reading</span> on SmashingMag:

*   [<span class="headline">Automatically Art-Directed Responsive Images? Here You Go.</span>](https://www.smashingmagazine.com/2016/02/automatically-art-directed-responsive-images-go/)
*   [Leaner Responsive Images With Client Hints](https://www.smashingmagazine.com/2016/01/leaner-responsive-images-client-hints/)
*   [Choosing A Responsive Image Solution](https://www.smashingmagazine.com/2013/07/choosing-a-responsive-image-solution/)
*   [Responsive Image Container: A Way Forward For Responsive Images?](https://www.smashingmagazine.com/2013/09/responsive-image-container/)

Long ago, I used Photoshop actions to save multiple sizes from a source file, but it quickly became a nightmare to maintain. Photoshop provides a more powerful tool — <strong>scripting language</strong> (it's not the same as “actions”, though the concept is similar). When writing a script, you use a programming language to tell Photoshop what to do (compared to actions, where Photoshop records what you do with mouse and keyboard). However, it's not easy to learn at all, and I also wanted to completely remove Photoshop from process.

{{% feature-panel %}}

The solution I found is <a href="https://www.imagemagick.org/">ImageMagick</a> — a command-line image manipulation program, available for <a href="https://www.imagemagick.org/script/binary-releases.php">Windows, Mac and Linux</a>. Unless you are a server administrator, you probably never thought of resizing images using command line. However, after switching to command line, I never looked back at Photoshop for batch resizing.

Using command line is:

*   Easy to expand — adding new sizes takes only one line of code.
*   Easy to maintain — changing folders is as easy as changing one variable.
*   Portable — I can save images on my server as well as my main computer.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4b38e8d-1741-419a-ab69-d8c02ce14e39/terminal.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4b38e8d-1741-419a-ab69-d8c02ce14e39/terminal.png" alt="Terminal in Python" /></a><br>
<em>The bash script in use in Terminal. <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4b38e8d-1741-419a-ab69-d8c02ce14e39/terminal.png">Large view</a>.</em>

If you have never worked with command line before, it all might look scary at first. However, with a bit of patience, you will find that it's actually a very powerful tool.

Below is the bash script I wrote, simplified for more universal usage. It takes the following parameters (from either you or from default values):

*   Set of output sizes.
*   Source file.
*   Destination path (path must include the `%` symbol, which will be replaced by output size, i.e. “800x600”).
*   Optional signature image.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9686730-6688-4d42-990f-135bcc5a43bf/finder.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e7a04028-99be-4caf-8db0-a2bb27a4f50a/finder1.png" alt="Batch Resize Script" width="500" height="328" /></a><br>
<em>The result after the script was applied. <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9686730-6688-4d42-990f-135bcc5a43bf/finder.png">Large view</a>.</em>

Then it resizes source image into every output size, applying a signature. For a better understanding, please look through the comments in source code.

The script requires:

*   [imagemagick](https://www.imagemagick.org/script/binary-releases.php) — to install. Follow instructions for your OS.
*   python — I'm sure your PC already has it installed!

Tested in Ubuntu and Mac OS X. How to use:

*   Save **resize.sh** to any folder on your computer.
*   Edit the file and set default values for variables (optional).
*   Open Terminal, navigate to this folder, and execute the following command: `bash resize.sh`.
*   Follow instructions, sit back and enjoy!

## The Bash Script

Here is the full bash script. Of course, you can also <a href="https://github.com/vladstudio/smashing-resizer">download it from GitHub</a>.

<pre><code class="language-markup tmp-python">#!/bin/bash

# Edit the settings below:

# Output sizes - 
# Please note the format: each size is wrapped with quotes, width and height are separated with space.
output=("800 600" "1024 768" "1152 864" "1280 960" "1280 1024" "1400 1050" "1440 960" "1600 1200" "1920 1440" "1024 600" "1366 768" "1440 900" "1600 900" "1680 1050" "1280 800" "1920 1080" "1920 1200" "2560 1440" "2560 1600" "2880 1800")

# If you frequently use the same source file (e.g. "~/Desktop/src.jpg"), 
# set it in "default_src"
default_src="src.jpg";

# If you frequently use the same destination
# (e.g. "~/Desktop/Some_folder/%.jpg"), set it in "default_dst"
# Destination must include "%", it will be replaced by output size, e.g. "800x600"
default_dst="%.jpg";

# Add signature? 
default_sign='y'

# If you frequently use the same signature file (e.g. "~/Desktop/sig.png"), 
# set it in "default_sig"
default_sig="sig.png";

# Gravity is for cropping left/right edges for different proportions (center, east, west)
default_gravity="center"

# Output JPG quality: maximum is 100 (recommended)
quality=100

# ======
# Do not edit below.
# ======
# Welcome to Smashing resizer!
# Written by Vlad Gerasimov from https://www.vladstudio.com
# 
# This script takes one "source" image and saves it in different sizes.
# 
# Requires:
# * imagemagick - https://www.imagemagick.org/
# * python - I'm sure your PC already has it!

# Unfortunately, bash is awful at math operations.
# We'll create a simple function that handles math for us.
# Example: $(math 2 * 2)

function math(){
  echo $(python -c "from __future__ import division; print $@")
}

# To make our script short and nice, here is the "save()" function.
# We'll use it to save each size.

function save(){

  # read target width and height from function parameters
  local dst_w=${1}
  local dst_h=${2}

  # calculate ratio 
  local ratio=$(math $dst_w/$dst_h);

  # calculate "intermediate" width and height
  local inter_w=$(math "int(round($src_h*$ratio))")
  local inter_h=${src_h}

  # calculate best sharpness
  local sharp=$(math "round((1/$ratio)/4, 2)")

  # which size we're saving now
  local size="${dst_w}x${dst_h}"
  echo "Saving ${size}..."

  #crop intermediate image (with target ratio)
  convert ${src} -gravity ${gravity} -crop ${inter_w}x${inter_h}+0+0 +repage temp.psd

  # apply signature
  if [ "${sign}" == "y" ]; then
  convert temp.psd ${sig} -gravity southeast -geometry ${sig_w}x${sig_h}+24+48 -composite temp.psd
  fi

  # final convert! resize, sharpen, save
  convert temp.psd -interpolate bicubic -filter Lagrange -resize ${dst_w}x${dst_h} -unsharp 0x${sharp} +repage -density 72x72 +repage -quality ${quality} ${dst/%/${size}}

}

# Ask for source image, or use default value
echo "Enter path to source image, or hit Enter to keep default value (${default_src}): "
read src
src=${src:-${default_src}}

# ask for destination path, or use default value
echo "Enter destination path, or hit Enter to keep default value (${default_dst})."
echo "must include % symbol, it will be replaced by output size, e.g. '800x600'"
read dst
dst=${dst:-${default_dst}}

# Ask for signature image, or use default value
echo "Apply signature? (hit Enter for 'yes' or type 'n' for 'no') "
read sign
sign=${sign:-${default_sign}}

# Ask for signature image, or use default value
echo "Enter path to signature image, or hit Enter to keep default value (${default_sig}): "
read sig
sig=${sig:-${default_sig}}

# ask for gravity, or use default value
echo "Enter gravity for cropping left/right edges (center, east, west), or hit Enter to keep default value (${default_gravity}): "
read gravity
gravity=${gravity:-${default_gravity}}

# detect source image width and height
src_w=$(identify -format "%w" "${src}")
src_h=$(identify -format "%h" "${src}")

# detect signature width and height
sig_w=$(identify -format "%w" "${sig}")
sig_h=$(identify -format "%h" "${sig}")

# loop throught output sizes and save each size
for i in "${output[@]}"
do
  save ${i}
done

# Delete temporary file
rm temp.psd

# Done!
echo "Done!"</code></pre>

Please let me know if you have any suggestions for improvements. Or perhaps you use a different technique to batch resize your images? Please share your thoughts, opinions and ideas in the comments section below!

<em>(jvb) (vf)</em>

