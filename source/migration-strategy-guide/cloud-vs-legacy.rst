
########################################
What is different about a Cloud platform
########################################

When comparing the functions and services of a cloud platform with the
traditional method of using virtual machines from a host provider or using High
Performance Compute (HPC), you can see that a cloud solution has many
similarities to these methods. However, when taking a deeper look at the
methods both conceptual and practically, you will find that there are some
clear differences.


In the past you may have purchased a series of virtual machines that already
came in a specific size in terms of RAM and storage space; you would then pay a
predefined amount for these virtual machines on a monthly basis. If you wanted
to increase the size of your storage, RAM or the amount of virtual machines you
were using, you would have to renegotiate the price of your monthly bill.

While you have this ‘subscription’ the virtual machines are yours and you pay
the same price regardless of how much you use them; meaning that if you only use
your instances for a week during the full month or anything less than 24/7 you
are not getting the most out of your monthly bill. On a cloud based system you
only pay for what is used and you can change your resources on the fly. If you
need to horizontally scale an instance you can simply spin up more compute
nodes. If you need to increase the size of your block storage, then you can add
a new volume to your instance. Or you can use our object storage service, which
scales dynamically, as an alternative.

In a cloud environment your instances and other resources are scheduled by the
cloud and you are only billed for the amount of resources you use or for how
long you use them for, whichever makes more sense. For example, we charge per GB
for storage, but we charge in hours for how long you use a compute instance.
This also opens up interesting avenues to save money as you can shelve
instances when they are not in use to save on your monthly bill (as you are only
charged while an instance is active)


After understanding these differences and the benefits that a Cloud platform
can provide your business, the next step is understanding how to migrate to the
Catalyst Cloud.

.. toctree::
   :maxdepth: 1

   lift-and-shift
   partial-restructure-rebuild
   cloud-native-redesign
