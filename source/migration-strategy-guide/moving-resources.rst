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

From aws
- If you previously imported your instances then you can just export them again using:

.. code-block::

  $aws ec2 create-instance-export-task --instance-id i-02651f8e6d0b4378c \
  --target-environment vmware --export-to-s3-task DiskImageFormat=VMDK,ContainerFormat=ova,S3Bucket=my-b1-bucket,S3Prefix=prefix

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

