################################
Redesign based on cloud services
################################

This method meets the case for users who want to take advantage of the services
now available to them by their migration to the Catalyst Cloud. For example,
you previously may not have had access to object storage as a service, but now
you want to implement this within your existing system. This requires a partial
redesign of your system, to accommodate the new service.

For the object storage example specifically you can find more information on
the :ref:`object storage section<object-storage>` of the Catalyst Cloud
documentation.

***********
Scalability
***********

There are two types of scaling when it comes to virtualization, horizontal and
vertical. Horizontal scaling can be simplified as adding more machines into
your pool of resources while Vertical scaling means increasing the amount of
CPU/RAM etc that an existing machine is using. There are positives and
negatives to both types of scaling but the important thing to understand in the
context of a cloud based system is that both options are available to you at
any time; you don't have to negotiate with your provider how many VMs (compute
instances) you need or how much RAM you want on an instance, as long as it is
within your :ref:`quota<quota-info>`. One commonly used practice with scaling on a cloud environment is automating your system to horizontally scale with
demand. Using horizontal scaling over vertical ensures that your uptime is not
affected. The process of setting up autoscaling is detailed more in the
:ref:`cloud native<cloud-native-design>` design page.

*****************
High availability
*****************

High availability is a term used to describe systems that use a variety of
different protocols and features to ensure that uptime is kept to the highest
possible degree. The Catalyst Cloud ensures that our system is highly available
by having constant monitoring of our system (24/7) and by having a
geographically diverse cloud with no single point of failure. High availability
also becomes a possibility for your systems when migrating to the Catalyst
Cloud. Depending on the type of system you are planning to run you will either
benefit from the clouds in built high availability or you may have to implement
some protocols yourself, the most common of, having to do with load balancing,
is discussed below.

More specific information on how high availability is implemented across
services on the Catalyst Cloud can be found in the :ref:`best practice
<high-availability>` section of these documents

********************************************
High availability using load balancers
********************************************

This is one of the most common additions people make to their systems when
migrating to a cloud platform. Traditional load balancers take front end
requests to your services and distribute them across a pool of back end servers
for processing based on a set of user defined rules. The Catalyst Cloud load
balancer service takes the complexity of this task and provides a solution that
is multi-tenanted, highly scalable and easy to implement.

This means that you are able to manage the traffic on your instances with more
efficiency and scale horizontally automatically. As for the high availability
of the service itself, each load balancer by default has two loadbalancer
instances clustered using VRRP. This means should one of the loadbalancer
instances experience an error the service will fail-over connections between
the loadbalancers, this process usually takes only five seconds.

More information on the load balancer service can be found in the
:ref:`load balancer section<load-balancer-section>`
