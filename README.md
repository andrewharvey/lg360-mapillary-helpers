# LG360 Mapillary Helpers

Scripts to help process images from the LG360 CAM for Mapillary.

Debian prerequisites (to run bash, find, gimp, parallel, convert, gmic, exiftool utilities):

    sudo apt-get install bash findutils gimp parallel graphicsmagick-imagemagick-compat gmic libimage-exiftool-perl

## lg360_maskhelp

Helps you create a mask for inpainting the region under the camera.

    ./lg360_maskhelp /path/to/images

Will take a sample of images (by default one in every 250 combine them into a single image and open in GIMP. Then in GIMP you can create a black/white mask (white areas to be inpainted) and save it as `mask.png`.


## lg360_inpaint

Inpaints your 360 images using a mask.

    ./lg360_inpaint /path/to/images /path/to/images/mask.png

This will create a new output directory `/path/to/images_inpaint`

Unfortunately the inpainting algorithm is not projection aware, a workaround when only inpainting the "south pole" could be to reproject the image to another projection focusing on the "south pole", do the inpainting, then reproject back. This hasn't been implemented yet.


## lg360_syncRemote

If you have a slow uplink, this script will compress your JPEGs using lepton and rsync them to a remote host. If your connection is interrupted rsync can easily be re-run without re-uploading or data loss.

## lg360_syncRemoteComplete
Once you have rsynced to your remote host, this script will decompress the lep files and upload to Mapillary.
