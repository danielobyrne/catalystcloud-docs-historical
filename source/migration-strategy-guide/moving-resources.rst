###################################################
Migrating existing resources to the Catalyst Cloud
###################################################

The following section contains information that is useful for users who are
familiar with how a cloud platform functions and are wanting to migrate
resources from an existing cloud solution over to the Catalyst Cloud. It should
be noted that not all resources that you want to bring over to the cloud will
be immediately compatible with our cloud infrastructure. You may need to change
some of your resources before uploading them to the Catalyst Cloud, in order for
them to function correctly. The most common example of this would be that you
have to make sure that any images that you are uploading are able to interact
with the cloud.

We talk more in each section about the specific considerations that you need to
think of before moving resources across, but it is something to be mindful of
while you progress through this section.

.. Note::

  The following list of examples is still being expanded and we are working on
  adding more tutorials as the need arises.


*******************************
Compute instances
*******************************

Migrating an ec2 instance from AWS
==================================

There are two methods for migrating an instance away from AWS, these depend on
whether or not you originally imported your instance into AWS in the first place
or whether you built your compute instances from scratch on the AWS cloud.

Before we get into this however, you need to check that you have the following
prerequisites ready:

- Install the :ref:`openstackCLI<installing_cli_os>` and other dependencies
- Source an :ref:`openRC file <configuring-the-cli>`
- Have the `AWS CLI`_ installed
- Have an Amazon S3 bucket ready to store some data.

.. _AWS CLI: https://docs.aws.amazon.com/cli/latest/userguide/welcome-versions.html

Once you have all of these things ready, you can proceed with whichever strategy
below is relevant to you.

Migrating resources that were imported to AWS
---------------------------------------------

.. Note::

  There are some additional restrictions for exporting an instance in this way,
  the full list of which can be found on the `Amazon VM Import-Export`_
  documentation.

If when creating your resources on your AWS project you imported some resources
from a previous solution, you will have the ability to export those same
resources using the AWS CLI. The following command will create an export task
which will export your instance image to an s3 bucket of your choice:

.. _Amazon VM Import-Export: https://docs.aws.amazon.com/vm-import/latest/userguide/vmexport.html#vmexport-limits

.. code-block:: bash

  $ aws ec2 create-instance-export-task --instance-id <INSERT INSTANCE ID> \
  --target-environment vmware --export-to-s3-task DiskImageFormat=RAW, ContainerFormat=ova, S3Bucket=<INSERT BUCKET NAME>

  # The DiskImageFormat for this command must use RAW as it is the image type that is compatible with the cloud infrastructure.

Once we have our instance image uploaded to our S3 bucket, our next step is to
transfer the image over to the Catalyst Cloud. Depending on the size of your
image, you can can either download the image directly to your machine and upload
it to the cloud via the command line. Or you can use the dashboard to upload
your image straight to the catalyst Cloud from the s3 bucket. Examples for both
of these methods can be found in the :ref:`Uploading images <uploading-images>`
section of the docs.

After your image is uploaded to the cloud, you just need to create a new
instance using your image. Instructions for creating an instance can be found
under the :ref:`Compute<quickstart_for_compute>` section of the documentation.

Migrating resources created using an AMI
-----------------------------------------------

If you did not import your instances then you have to take the long road:

- create a volume:

.. code-block::

  $ aws ec2 create-volume --size 16 --region us-west-1 --availability-zone us-west-1b --volume-type gp2

- attach the volume to your instance:

.. code-block::

  $ aws ec2 attach-volume --volume-id vol-0c6df10a4d2d2a408 --instance-id i-09ec9d3f6f91eead5 --device /dev/sdf

- create a file system on your volume:

.. code-block::

  $ mkfs.ext4 /dev/xvdf1

- create a temp directory and mount the disk:

.. code-block::

  $ mkdir /tmp/disk mount /dev/xvdf1 /tmp/disk

- copy the information on your current hard drive to an image file:

.. code-block::

  $ dd if=/dev/xvda of=/tmp/disk/disk.img

- export the disk file to S3:

.. code-block::

  $ aws s3 cp /tmp/disk/disk.img s3://my-b1-bucket/ upload: ../tmp/disk/disk.img to s3://my-b1-bucket/disk.img

- download the image from s3

.. code-block::

  $ aws s3 cp s3://my-b1-bucket/disk.img /tmp/ami/ download: s3://my-b1-bucket/disk.img to ../tmp/ami/disk.img

- convert the image to RAW and re-upload to the cloud:
    - <link to documentation>


*******************************
Volumes
*******************************

- convert to image
- download to local
- upload to openstack project
- convert to volume

*******************************
Networks
*******************************

- Recreate your network on the catalyst cloud. No way to port things over.

*******************************
Object storage
*******************************

- s3 compatible and you can just upload straight to it.

*******************************
Kubernetes clusters
*******************************

- Not entirely sure... If you have a template then you can just use that to
  recreate your cluster?

*******************************
Database
*******************************

- Should be able to download the instructions to create your database and just
  recompute them on your new one?

