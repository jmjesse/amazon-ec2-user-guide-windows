# Windows accelerated computing instances<a name="accelerated-computing-instances"></a>

Accelerated computing instances use hardware accelerators, or co\-processors, to perform some functions, such as floating point number calculations, graphics processing, or data pattern matching, more efficiently than is possible in software running on CPUs\. These instances enable more parallelism for higher throughput on compute\-intensive workloads\.

If you require high processing capability, you'll benefit from using accelerated computing instances, which provide access to hardware\-based compute accelerators such as Graphics Processing Units \(GPUs\)\.

**Topics**
+ [GPU instances](#gpu-instances)
+ [Hardware specifications](#gpu-instance-specifications)
+ [Instance performance](#gpu-instance-performance)
+ [Network performance](#gpu-network-performance)
+ [SSD I/O performance](#accelerated-computing-ssd-perf)
+ [Instance features](#gpu-instances-features)
+ [Release notes](#gpu-instance-release-notes)
+ [Install NVIDIA drivers on Windows instances](install-nvidia-driver.md)
+ [Install AMD drivers on Windows instances](install-amd-driver.md)
+ [Activate NVIDIA GRID Virtual Applications](activate_grid.md)
+ [Optimize GPU settings](optimize_gpu.md)

## GPU instances<a name="gpu-instances"></a>

GPU\-based instances provide access to NVIDIA GPUs with thousands of compute cores\. You can use these instances to accelerate scientific, engineering, and rendering applications by leveraging the CUDA or Open Computing Language \(OpenCL\) parallel computing frameworks\. You can also use them for graphics applications, including game streaming, 3\-D application streaming, and other graphics workloads\.

If your application needs a small amount of additional graphics acceleration, but is better suited for an instance type with different compute, memory, or storage specifications, use an Elastic Graphics accelerator instead\. For more information, see [Amazon Elastic Graphics](elastic-graphics.md)\.

**G5 instances**  
G5 instances use NVIDIA A10G GPUs and provide high performance for graphics\-intensive applications such as remote workstations, video rendering, and cloud gaming, and deep learning models for applications such as natural language processing, computer vision, and recommendation engines\. These instances feature up to 8 NVIDIA A10G GPUs, second generation AMD EPY processors, up to 100 Gbps of network bandwidth, and up to 7\.6 TB of local NVMe SSD storage\.

For more information, see [Amazon EC2 G5 Instances](http://aws.amazon.com/ec2/instance-types/g5/)\.
<a name="g4-instances"></a>
**G4ad and G4dn instances**  
G4ad instances use AMD Radeon Pro V520 GPUs and 2nd generation AMD EPYC processors, and are well\-suited for graphics applications such as remote graphics workstations, game streaming, and rendering that leverage industry\-standard APIs such as OpenGL, DirectX, and Vulkan\. They provide up to 4 AMD Radeon Pro V520 GPUs, 64 vCPUs, 25 Gbps networking, and 2\.4 TB local NVMe\-based SSD storage\.

G4dn instances use NVIDIA Tesla GPUs and provide a cost\-effective, high\-performance platform for general purpose GPU computing using the CUDA or machine learning frameworks along with graphics applications using DirectX or OpenGL\. These instances provide high\- bandwidth networking, powerful half and single\-precision floating\-point capabilities, along with INT8 and INT4 precisions\. Each GPU has 16 GiB of GDDR6 memory, making G4dn instances well\-suited for machine learning inference, video transcoding, and graphics applications like remote graphics workstations and game streaming in the cloud\.

For more information, see [Amazon EC2 G4 Instances](http://aws.amazon.com/ec2/instance-types/g4/)\.

G4dn instances support NVIDIA GRID Virtual Workstation\. For more information, see [NVIDIA Marketplace offerings](http://aws.amazon.com/marketplace/search/results/?page=1&filters=instance_types&instance_types=g4dn.xlarge&searchTerms=NVIDIA%20GRID)\.
<a name="g3-instances"></a>
**G3 instances**  
These instances use NVIDIA Tesla M60 GPUs and provide a cost\-effective, high\-performance platform for graphics applications using DirectX or OpenGL\. G3 instances also provide NVIDIA GRID Virtual Workstation features, such as support for four monitors with resolutions up to 4096x2160, and NVIDIA GRID Virtual Applications\. G3 instances are well\-suited for applications such as 3D visualizations, graphics\-intensive remote workstations, 3D rendering, video encoding, virtual reality, and other server\-side graphics workloads requiring massively parallel processing power\. 

For more information, see [Amazon EC2 G3 Instances](http://aws.amazon.com/ec2/instance-types/g3/)\.

G3 instances support NVIDIA GRID Virtual Workstation and NVIDIA GRID Virtual Applications\. To activate either of these features, see [Activate NVIDIA GRID Virtual Applications](activate_grid.md)\.
<a name="g2-instances"></a>
**G2 instances**  
These instances use NVIDIA GRID K520 GPUs and provide a cost\-effective, high\-performance platform for graphics applications using DirectX or OpenGL\. NVIDIA GRID GPUs also support NVIDIA’s fast capture and encode API operations\. Example applications include video creation services, 3D visualizations, streaming graphics\-intensive applications, and other server\-side graphics workloads\.
<a name="p3-instances"></a>
**P3 instances**  
These instances use NVIDIA Tesla V100 GPUs and are designed for general purpose GPU computing using the CUDA or OpenCL programming models or through a machine learning framework\. P3 instances provide high\-bandwidth networking, powerful half, single, and double\-precision floating\-point capabilities, and up to 32 GiB of memory per GPU, which makes them ideal for deep learning, computational fluid dynamics, computational finance, seismic analysis, molecular modeling, genomics, rendering, and other server\-side GPU compute workloads\. Tesla V100 GPUs do not support graphics mode\.

For more information, see [Amazon EC2 P3 Instances](https://aws.amazon.com/ec2/instance-types/p3)\.

P3 instances support NVIDIA NVLink peer to peer transfers\. For more information, see [NVIDIA NVLink](https://devblogs.nvidia.com/parallelforall/how-nvlink-will-enable-faster-easier-multi-gpu-computing/)\.
<a name="p2-instances"></a>
**P2 instances**  
P2 instances use NVIDIA Tesla K80 GPUs and are designed for general purpose GPU computing using the CUDA or OpenCL programming models\. P2 instances provide high\-bandwidth networking, powerful single and double precision floating\-point capabilities, and 12 GiB of memory per GPU, which makes them ideal for deep learning, graph databases, high\-performance databases, computational fluid dynamics, computational finance, seismic analysis, molecular modeling, genomics, rendering, and other server\-side GPU compute workloads\.

P2 instances support NVIDIA GPUDirect peer to peer transfers\. For more information, see [NVIDIA GPUDirect](https://developer.nvidia.com/gpudirect)\.

## Hardware specifications<a name="gpu-instance-specifications"></a>

The following is a summary of the hardware specifications for accelerated computing instances\. A virtual central processing unit \(vCPU\) represents a portion of the physical CPU assigned to a virtual machine \(VM\)\. For x86 instances, there are two vCPUs per core\. For Graviton instances, there is one vCPU per core\.


| Instance type | Default vCPUs | Memory \(GiB\) | Accelerators | 
| --- | --- | --- | --- | 
| f1\.2xlarge | 8 | 122 | 1 | 
| f1\.4xlarge | 16 | 244 | 2 | 
| f1\.16xlarge | 64 | 976 | 8 | 
| g2\.2xlarge | 8 | 15 | 1 | 
| g2\.8xlarge | 32 | 60 | 4 | 
| g3s\.xlarge | 4 | 30\.5 | 1 | 
| g3\.4xlarge | 16 | 122 | 1 | 
| g3\.8xlarge | 32 | 244 | 2 | 
| g3\.16xlarge | 64 | 488 | 4 | 
| g4ad\.xlarge | 4 | 16 | 1 | 
| g4ad\.2xlarge | 8 | 32 | 1 | 
| g4ad\.4xlarge | 16 | 64 | 1 | 
| g4ad\.8xlarge | 32 | 128 | 2 | 
| g4ad\.16xlarge | 64 | 256 | 4 | 
| g4dn\.xlarge | 4 | 16 | 1 | 
| g4dn\.2xlarge | 8 | 32 | 1 | 
| g4dn\.4xlarge | 16 | 64 | 1 | 
| g4dn\.8xlarge | 32 | 128 | 1 | 
| g4dn\.12xlarge | 48 | 192 | 4 | 
| g4dn\.16xlarge | 64 | 256 | 1 | 
| g4dn\.metal | 96 | 384 | 8 | 
| g5\.xlarge | 4 | 16 | 1 | 
| g5\.2xlarge | 8 | 32 | 1 | 
| g5\.4xlarge | 16 | 64 | 1 | 
| g5\.8xlarge | 32 | 128 | 1 | 
| g5\.12xlarge | 48 | 192 | 4 | 
| g5\.16xlarge | 64 | 256 | 1 | 
| g5\.24xlarge | 96 | 384 | 4 | 
| g5\.48xlarge | 192 | 768 | 8 | 
| p2\.xlarge | 4 | 61 | 1 | 
| p2\.8xlarge | 32 | 488 | 8 | 
| p2\.16xlarge | 64 | 732 | 16 | 
| p3\.2xlarge | 8 | 61 | 1 | 
| p3\.8xlarge | 32 | 244 | 4 | 
| p3\.16xlarge | 64 | 488 | 8 | 
| p3dn\.24xlarge | 96 | 768 | 8 | 

The accelerated computing instances use the following processors\.

**AMD processors**
+ **2nd generation AMD EPYC processors \(AMD EPYC 7R32\)**: G4ad, G5

**Intel processors**
+ **Intel Xeon Scalable processors \(Broadwell E5\-2686 v4\)**: F1, G3, P2, P3
+ **Intel Xeon Scalable processors \(Skylake 8175\)**: P3dn
+ **2nd generation Intel Xeon Scalable processors \(Cascade Lake P\-8259CL\)**: VT1
+ **2nd generation Intel Xeon Scalable processors \(Cascade Lake P\-8259L\)**: G4dn

For more information, see [Amazon EC2 Instance Types](https://aws.amazon.com/ec2/instance-types/)\.

## Instance performance<a name="gpu-instance-performance"></a>

EBS\-optimized instances enable you to get consistently high performance for your EBS volumes by eliminating contention between Amazon EBS I/O and other network traffic from your instance\. Some accelerated computing instances are EBS\-optimized by default at no additional cost\. For more information, see [Amazon EBS–optimized instances](ebs-optimized.md)\.

## Network performance<a name="gpu-network-performance"></a>

You can enable enhanced networking on supported instance types to provide lower latencies, lower network jitter, and higher packet\-per\-second \(PPS\) performance\. Most applications do not consistently need a high level of network performance, but can benefit from access to increased bandwidth when they send or receive data\. For more information, see [Enhanced networking on Windows](enhanced-networking.md)\.

The following is a summary of network performance for accelerated computing instances that support enhanced networking\.


| Instance type | Network performance | Enhanced networking | 
| --- | --- | --- | 
|  f1\.4xlarge and smaller \| g3\.4xlarge \| g3s\.xlarge \| g4ad\.4xlarge and smaller \| g5\.2xlarge and smaller \| p3\.2xlarge  | Up to 10 Gbps † | [ENA](enhanced-networking-ena.md) | 
|  g3\.8xlarge \| p2\.8xlarge \| p3\.8xlarge  | 10 Gbps | [ENA](enhanced-networking-ena.md) | 
| g4ad\.8xlarge | 15 Gbps | [ENA](enhanced-networking-ena.md) | 
|  g4dn\.4xlarge and smaller \| g5\.4xlarge  | Up to 25 Gbps † | [ENA](enhanced-networking-ena.md) | 
|  f1\.16xlarge \| g3\.16xlarge \| g4ad\.16xlarge \| g5\.8xlarge \| g5\.16xlarge \| p2\.16xlarge \| p3\.16xlarge  | 25 Gbps | [ENA](enhanced-networking-ena.md) | 
| g5\.12xlarge | 40 Gbps | [ENA](enhanced-networking-ena.md) | 
|  g4dn\.8xlarge \| g4dn\.12xlarge \| g4dn\.16xlarge \| g5\.24xlarge  | 50 Gbps | [ENA](enhanced-networking-ena.md) | 
|  g4dn\.metal \| g5\.48xlarge \| p3dn\.24xlarge  | 100 Gbps | [ENA](enhanced-networking-ena.md) | 

† These instances have a baseline bandwidth and can use a network I/O credit mechanism to burst beyond their baseline bandwidth on a best effort basis\. For more information, see [instance network bandwidth](ec2-instance-network-bandwidth.md)\.<a name="baseline-bandwidth"></a>


| Instance type | Baseline bandwidth \(Gbps\) | Burst bandwidth \(Gbps\) | 
| --- | --- | --- | 
| f1\.2xlarge | 2\.5 | 10 | 
| f1\.4xlarge | 5 | 10 | 
| g3\.4xlarge | 5 | 10 | 
| g3s\.xlarge | 1\.25 | 10 | 
| g4ad\.xlarge | 2 | 10 | 
| g4ad\.2xlarge | 4\.167 | 10 | 
| g4ad\.4xlarge | 8\.333 | 10 | 
| g4dn\.xlarge | 5 | 25 | 
| g4dn\.2xlarge | 10 | 25 | 
| g4dn\.4xlarge | 20 | 25 | 
| g5\.xlarge | 2\.5 | 10 | 
| g5\.2xlarge | 5 | 10 | 
| g5\.4xlarge | 10 | 25 | 
| p3\.2xlarge | 2\.5 | 10 | 

## SSD I/O performance<a name="accelerated-computing-ssd-perf"></a>

If you use all the SSD\-based instance store volumes available to your instance, you can get up to the IOPS \(4,096 byte block size\) performance listed in the following table \(at queue depth saturation\)\. Otherwise, you get lower IOPS performance\.


| Instance Size | 100% Random Read IOPS | Write IOPS | 
| --- | --- | --- | 
| g4ad\.xlarge | 10,417 | 8,333 | 
| g4ad\.2xlarge | 20,833 | 16,667 | 
| g4ad\.4xlarge | 41,667 | 33,333 | 
| g4ad\.8xlarge | 83,333 | 66,667 | 
| g4ad\.16xlarge | 166,667 | 133,333 | 
| g5\.xlarge | 40,625 | 20,313 | 
| g5\.2xlarge | 40,625 | 20,313 | 
| g5\.4xlarge | 125,000 | 62,500 | 
| g5\.8xlarge | 250,000 | 125,000 | 
| g5\.12xlarge | 312,500 | 156,250 | 
| g5\.16xlarge | 250,000 | 125,000 | 
| g5\.24xlarge | 312,500 | 156,250 | 
| g5\.48xlarge | 625,000 | 312,500 | 

As you fill the SSD\-based instance store volumes for your instance, the number of write IOPS that you can achieve decreases\. This is due to the extra work the SSD controller must do to find available space, rewrite existing data, and erase unused space so that it can be rewritten\. This process of garbage collection results in internal write amplification to the SSD, expressed as the ratio of SSD write operations to user write operations\. This decrease in performance is even larger if the write operations are not in multiples of 4,096 bytes or not aligned to a 4,096\-byte boundary\. If you write a smaller amount of bytes or bytes that are not aligned, the SSD controller must read the surrounding data and store the result in a new location\. This pattern results in significantly increased write amplification, increased latency, and dramatically reduced I/O performance\.

SSD controllers can use several strategies to reduce the impact of write amplification\. One such strategy is to reserve space in the SSD instance storage so that the controller can more efficiently manage the space available for write operations\. This is called *over\-provisioning*\. The SSD\-based instance store volumes provided to an instance don't have any space reserved for over\-provisioning\. To reduce write amplification, we recommend that you leave 10% of the volume unpartitioned so that the SSD controller can use it for over\-provisioning\. This decreases the storage that you can use, but increases performance even if the disk is close to full capacity\.

For instance store volumes that support TRIM, you can use the TRIM command to notify the SSD controller whenever you no longer need data that you've written\. This provides the controller with more free space, which can reduce write amplification and increase performance\. For more information, see [Instance store volume TRIM support](ssd-instance-store.md#InstanceStoreTrimSupport)\.

## Instance features<a name="gpu-instances-features"></a>

The following is a summary of features for accelerated computing instances\.


|  | EBS only | NVMe EBS | Instance store | Placement group | 
| --- | --- | --- | --- | --- | 
| F1 | No | No | NVMe \* | Yes | 
| G2 | No | No | SSD | Yes | 
| G3 | Yes | No | No | Yes | 
| G4ad | No | Yes | NVMe \* | Yes | 
| G4dn | No | Yes | NVMe \* | Yes | 
| G5 | No | Yes | NVMe \* | Yes | 
| P2 | Yes | No | No | Yes | 
| P3 |  24xlarge: No All other sizes: Yes  |  24xlarge: Yes All other sizes: No  | 24xlarge: NVMe \* | Yes | 

**\*** The root device volume must be an Amazon EBS volume\.

For more information, see the following:
+ [Amazon EBS and NVMe on Windows instances](nvme-ebs-volumes.md)
+ [Amazon EC2 instance store](InstanceStorage.md)
+ [Placement groups](placement-groups.md)

## Release notes<a name="gpu-instance-release-notes"></a>
+ You must launch the instance using an HVM AMI\.
+ Instances built on the [Nitro System](instance-types.md#ec2-nitro-instances) have the following requirements:
  + [NVMe drivers](nvme-ebs-volumes.md) must be installed
  + [Elastic Network Adapter \(ENA\) drivers](enhanced-networking-ena.md) must be installed

  The current [AWS Windows AMIs](windows-ami-version-history.md) meet these requirements\.
+ GPU\-based instances can't access the GPU unless the NVIDIA drivers are installed\. For more information, see [Install NVIDIA drivers on Windows instances](install-nvidia-driver.md)\.
+ Launching a bare metal instance boots the underlying server, which includes verifying all hardware and firmware components\. This means that it can take 20 minutes from the time the instance enters the running state until it becomes available over the network\.
+ To attach or detach EBS volumes or secondary network interfaces from a bare metal instance requires PCIe native hotplug support\.
+ Bare metal instances use a PCI\-based serial device rather than an I/O port\-based serial device\. The upstream Linux kernel and the latest Amazon Linux AMIs support this device\. Bare metal instances also provide an ACPI SPCR table to enable the system to automatically use the PCI\-based serial device\. The latest Windows AMIs automatically use the PCI\-based serial device\.
+ There is a limit of 100 AFIs per Region\.
+ There is a limit on the total number of instances that you can launch in a Region, and there are additional limits on some instance types\. For more information, see [How many instances can I run in Amazon EC2?](https://aws.amazon.com/ec2/faqs/#How_many_instances_can_I_run_in_Amazon_EC2) in the Amazon EC2 FAQ\.
+ If you launch a multi\-GPU instance with a Windows AMI that was created on a single\-GPU instance, Windows does not automatically install the NVIDIA driver for all GPUs\. You must authorize the driver installation for the new GPU hardware\. You can correct this manually in the Device Manager by opening the **Other** device category \(the inactive GPUs do not appear under **Display Adapters**\)\. For each inactive GPU, open the context \(right\-click\) menu, choose **Update Driver Software**, and then choose the default **Automatic Update** option\.
+ When using Microsoft Remote Desktop Protocol \(RDP\), GPUs that use the WDDM driver model are replaced with a non\-accelerated Remote Desktop display driver\. We recommend that you use a different remote access tool to access your GPU, such as [Teradici Cloud Access Software](http://www.teradici.com/products/cloud-access/cloud-access-software), [NICE Desktop Cloud Visualization \(DCV\)](https://docs.aws.amazon.com/dcv/latest/userguide/getting-started.html), or VNC\. You can also use one of the GPU AMIs from the AWS Marketplace because they provide remote access tools that support 3D acceleration\.