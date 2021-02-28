#####################
Cloud native redesign
#####################

.. _cloud-native-design:

This is the most difficult method of migration as it entails restructuring your
entire system. A fully Cloud Native system should have each process or
application containerised so that it's resources are securely isolated from
every other process on your system. It should also be dynamically orchestrated
and managed and it should be microservice-oriented. This is the end goal of
what a cloud platform should be, however this is not to say that every
application should be run in a cloud native way. You will find that some
programs run more effectively in a traditional manner or cannot be run
natively. Although, for the majority of programs that can be run natively, it
is the optimal way to run them.

*****************************
Containers and microservicing
*****************************

Containers unlike traditional VM's use operating system level virtualization,
meaning a single OS instance can be dynamically divided between isolated
containers. Combining these containers with microservices builds a network that
is more secure, more fault tolerant, and is adaptable to the needs of consumers.
Microservicing is the the act of taking monolithic applications that do
many things, and breaking them down into several small apps that do one thing
each. The purpose of joining microservicing with containers is so that you are
able to identify problems with specific services on an isolated level. This
means that instead of having to repair one large application with thousands of
lines of code when something goes wrong, you can instead spin up a new
container with the old microservice and delete the malfunctioning one. Coupled
with a service like Kubernetes, containers and microservicing allow you to
provide extremely robust cloud native services.

Docker_ is the current industry standard for container implementation and is
compatible with the orchestration system Kubernetes which is discussed below.

.. _Docker: https://www.docker.com/

**********
Kubernetes
**********

Kubernetes is an open-source container orchestration engine (COE) for
automating deployment, scaling, and management of containerised applications. A
large portion of the hassle that comes with building a microservicing system
and running a cloud native platform can be handled by kubernetes.

Kubernetes works by creating clusters. These clusters consist of a number of
master nodes and worker nodes. The master nodes manage the scheduling,
auto-scaling, auto-healing, load balancing and all other aspects of the
cluster. The worker nodes simply run the workloads that are given to them by
the master nodes. Each node is run in a container and is monitored by the
master nodes, should an error occur on a worker node the master will spin up a
new worker to complete the task and kill the old node instead of trying to fix
the issue. This is because each worker node is replaceable, the workload itself
is what is important.

More information on Kubernetes on the Catalyst Cloud can be found
:ref:`here<kubernetes-landing>`
