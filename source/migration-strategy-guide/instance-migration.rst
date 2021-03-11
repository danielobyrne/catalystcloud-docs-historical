#############################################
Moving resources to the Catalyst Cloud
#############################################


********************************
Migrating ec2 instance from AWS
********************************
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
