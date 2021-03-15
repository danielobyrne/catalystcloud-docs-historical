##############
Lift and Shift
##############

This method is the simplest to understand, like the title suggests you lift all
of the structure and data from your old VM solution and shift it onto the
Catalyst Cloud. The majority of the time this will be successful as the
infrastructure between the two systems are mostly compatible. However there are
some considerations that you need to make before uprooting everything.

********************************
OS images need to be cloud aware
********************************

By default most images that are used for VMs are not cloud aware. This presents
an issue if you plan to use the images from your previous VMs on the Catalyst
Cloud. In some cases there will be replacement images that are provided under
our image service. These include a large amount of Unix based images such as
Fedora, Ubuntu and Debian. We also carry some Windows images on our cloud, both
Windows server 2012 and 2016 and for licensing purposes we only support these
windows images.

For more information on our image service you can see the
:ref:`image section<images>` of these documents. If you are looking to convert
images that cannot be found on the Catalyst Cloud you can find information on
creating images for the cloud under the
:ref:`converting images <converting-images>` section of the docs.

*****************
OS image versions
*****************

Catalyst Cloud's image service has many different operating system versions
available. However it is important to keep in mind that each version of an
operating system behaves differently and programs that run on one may not be
compatible with others. This is particularly relevant when discussing Windows
images; because the updates that go on between each Windows versions change
on a large scale. In cases like this, you may need to think twice about what to
do with said programs. Can you find a newer version of your programs compatible
with the new OS version? Or can you find a suitable replacement? Has the
program been deprecated between OS versions? etc.
