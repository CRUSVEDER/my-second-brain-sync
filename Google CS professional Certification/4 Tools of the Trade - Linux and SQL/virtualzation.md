# Virtualization technology

You've explored a lot about operating systems. One more aspect to consider is that operating systems can run on virtual machines. In this reading, you’ll learn about virtual machines and the general concept of virtualization. You’ll explore how virtual machines work and the benefits of using them.

## What is a virtual machine?

A **virtual machine (VM)** is a virtual version of a physical computer. Virtual machines are one example of virtualization. Virtualization is the process of using software to create virtual representations of various physical machines. The term “virtual” refers to machines that don’t exist physically, but operate like they do because their software simulates physical hardware. Virtual systems don’t use dedicated physical hardware. Instead, they use software-defined versions of the physical hardware. This means that a single virtual machine has a virtual CPU, virtual storage, and other virtual hardware. Virtual systems are just code.

![A dark gray computer with arrows to light gray computers that have “VM” on the screen and are surrounded by dotted lines.](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/C0Cpca6gRquuxTow47dD1A_2a73d66bee5c40b78984e532c09994f1_82635VQFzN8LaD6GAv3bNTQs6oACAmxKjdlZebYCGsO10hvIVpxBElK4gbJ-KJvmRBsxvQd3XHXUfUtgWzNhR4Va6ODC5D42owmm2vyiluDeV86UAaL9d-pyaxXnjzgHARaWckVzCqj12dnrOq1Ca4o?expiry=1740960000000&hmac=VCZT6cy0oQ8v9EtOqvFI7Ns3jojEfyoUKRloB1-qIyI)

You can run multiple virtual machines using the physical hardware of a single computer. This involves dividing the resources of the host computer to be shared across all physical and virtual components. For example, **Random Access Memory (RAM)** is a hardware component used for short-term memory. If a computer has 16GB of RAM, it can host three virtual machines so that the physical computer and virtual machines each have 4GB of RAM. Also, each of these virtual machines would have their own operating system and function similarly to a typical computer.

## Benefits of virtual machines

Security professionals commonly use virtualization and virtual machines. Virtualization can increase security for many tasks and can also increase efficiency.

### **Security**

One benefit is that virtualization can provide an isolated environment, or a sandbox, on the physical host machine. When a computer has multiple virtual machines, these virtual machines are “guests” of the computer. Specifically, they are isolated from the host computer and other guest virtual machines. This provides a layer of security, because virtual machines can be kept separate from the other systems. For example, if an individual virtual machine becomes infected with malware, it can be dealt with more securely because it’s isolated from the other machines. A security professional could also intentionally place malware on a virtual machine to examine it in a more secure environment.

**Note:** Although using virtual machines is useful when investigating potentially infected machines or running malware in a constrained environment, there are still some risks. For example, a malicious program can escape virtualization and access the host machine. This is why you should never completely trust virtualized systems.

### **Efficiency**

Using virtual machines can also be an efficient and convenient way to perform security tasks. You can open multiple virtual machines at once and switch easily between them. This allows you to streamline security tasks, such as testing and exploring various applications.

You can compare the efficiency of a virtual machine to a city bus. A single city bus has a lot of room and is an efficient way to transport many people simultaneously. If city buses didn’t exist, then everyone on the bus would have to drive their own cars. This uses more gas, cars, and other resources than riding the city bus. 

Similar to how many people can ride one bus, many virtual machines can be hosted on the same physical machine. That way, separate physical machines aren't needed to perform certain tasks.

## Managing virtual machines

Virtual machines can be managed with a software called a hypervisor. Hypervisors help users manage multiple virtual machines and connect the virtual and physical hardware. Hypervisors also help with allocating the shared resources of the physical host machine to one or more virtual machines.

One hypervisor that is useful for you to be familiar with is the Kernel-based Virtual Machine (KVM). KVM is an open-source hypervisor that is supported by most major Linux distributions. It is built into the Linux kernel, which means it can be used to create virtual machines on any machine running a Linux operating system without the need for additional software.

## Other forms of virtualization

In addition to virtual machines, there are other forms of virtualization. Some of these virtualization technologies do not use operating systems. For example, multiple virtual servers can be created from a single physical server. Virtual networks can also be created to more efficiently use the hardware of a physical network. 

## Key takeaways

Virtual machines are virtual versions of physical computers and are one example of virtualization. Virtualization is a key technology in the security industry, and it’s important for security analysts to understand the basics. There are many benefits to using virtual machines, such as isolation of malware and other security risks. However, it’s important to remember there’s still a risk of malicious software escaping their virtualized environments.