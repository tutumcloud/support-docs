# What is Tutum?

Tutum is the Docker Platform for Dev and Ops. A container platform to take full advantage of the amazing technology that are Docker containers. You can build, deploy, and manage your applications across any infrastructure using Tutum.

## What are Containers?

From Docker themselves:

> "The Docker Engine container comprises just the application and its dependencies. It runs as an isolated process in userspace on the host operating system, sharing the kernel with other containers. Thus, it enjoys the resource isolation and allocation benefits of VMs but is much more portable and efficient."

**Translation**: Containers are lightweight, fast, and portable. They are a game-changer. But they are just a building block. To really take advantage of what containers have to offer you need a platform specifically built with containers in mind. Tutum allows you to build, deploy, and manage these containers.

When we first set out to build Tutum, we knew we wanted to steer clear of becoming yet another IaaS (Infrastructure-as-a-Service) or PaaS (Platform-as-a-Service) provider. So what is Tutum?

## Orchestration-as-a-Service

In the IaaS world, there’s already a thriving market of cloud and physical infrastructure providers. As a result of having so many providers, customers have a near limitless choice in price, performance options, and location. However, you don’t have the true freedom cloud promises; how you deploy, manage, and scale your application largely depends on the provider you use.

Tutum decouples the orchestration layer from the underlying infrastructure on which your application runs. Tutum works on top of any infrastructure provider and users can choose the provider that best satisfies their requirements.  Tutum orchestrates the underlying infrastructure and your containerized applications. In this regard, Tutum is OaaS (Orchestration-as-a-Service). But it’s also much more.

## Containers-as-a-Service

IaaS provides users with raw infrastructure on demand. The “basic building block” of IaaS is the virtual machine. With IaaS, users enjoy flexibility and control, but at the expense of simplicity. Simplicity is replaced with the inherently large management overhead that comes with handling raw infrastructure.  Dealing with the management overhead and complexity of IaaS has led to forced compromise in the creation of PaaS.

PaaS gives us a way to abstract infrastructure and make deploying applications easy. The “basic building block” of PaaS is code. PaaS sounds like the solution to IaaS’ problems, but it comes with its own set of pitfalls and constraints. PaaS is very rigid with how you write your code and what services you’re able to use with your application. It is a locked-down experience, that’s optimized to satisfy only very specific use cases. Tutum combines the strengths of IaaS and PaaS, with none of the downside. Tutum’s “basic building block” is the container. In this regard, Tutum can be referred to as Containers-as-a-Service or CaaS. With Tutum and containers, the same application you develop in your laptop can easily be deployed to any cloud, in just a few clicks. Using Tutum means you never have to worry about being locked in to just one infrastructure provider. The power is now truly with the user.

## Container Cloud

A Container Cloud is a cloud service that hosts/runs containers. Since Tutum does not provide any hosting as part of its new service offering, it may not be appropriate to think of Tutum as a Container Cloud. However, with Tutum you have the capability, flexibility and control to build your very own Container Cloud that is tailored to your needs.


## Container Platform

We think of Tutum as a “Container Platform.” Tutum has elements of orchestration, our basic building block is the container, and anyone can use Tutum to build a Container Cloud. But all of those definitions seem to be limiting when we take a look at what we have planned for Tutum: a platform to build, deploy and manage all of your applications across any cloud infrastructure.

Want to learn more about what you can do with a Container Cloud? Head over to our [features section](https://www.tutum.co/features).