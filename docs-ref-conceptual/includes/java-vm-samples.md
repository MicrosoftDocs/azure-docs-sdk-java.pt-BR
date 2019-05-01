---
ms.openlocfilehash: ab31ee32ea940db2d7bcfa2fe36475d8a648bfc9
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61592602"
---
| <span data-ttu-id="9b8e6-101">**Criar máquinas virtuais**</span><span class="sxs-lookup"><span data-stu-id="9b8e6-101">**Create virtual machines**</span></span> || 
|---|---|
| <span data-ttu-id="9b8e6-102">[Gerenciar redes virtuais][1]</span><span class="sxs-lookup"><span data-stu-id="9b8e6-102">[Manage virtual machines][1]</span></span> | <span data-ttu-id="9b8e6-103">Criar, modificar, iniciar, parar e excluir máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="9b8e6-103">Create, modify, start, stop, and delete virtual machines.</span></span> |
| <span data-ttu-id="9b8e6-104">[Criar uma máquina virtual a partir de uma imagem personalizada][2]</span><span class="sxs-lookup"><span data-stu-id="9b8e6-104">[Create a virtual machine from a custom image][2]</span></span> | <span data-ttu-id="9b8e6-105">Criar uma imagem da máquina virtual e usá-la para criar novas máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="9b8e6-105">Create a custom virtual machine image and use it to create new virtual machines.</span></span> | 
| <span data-ttu-id="9b8e6-106">[Criar uma máquina virtual usando a VHD específica a partir de um instantâneo][3]</span><span class="sxs-lookup"><span data-stu-id="9b8e6-106">[Create a virtual machine using specialized VHD from a snapshot][3]</span></span> | <span data-ttu-id="9b8e6-107">Crie um instantâneo a partir dos discos de dados e do sistema operacional da máquina virtual, crie discos gerenciados a partir de instantâneos e, em seguida, crie uma máquina virtual anexando os discos gerenciados.</span><span class="sxs-lookup"><span data-stu-id="9b8e6-107">Create snapshot from the virtual machine's OS and data disks, create managed disks from the snapshots, and then create a virtual machine by attaching the managed disks.</span></span> |  
| <span data-ttu-id="9b8e6-108">[Criar máquinas virtuais em paralelo na mesma rede][4]</span><span class="sxs-lookup"><span data-stu-id="9b8e6-108">[Create virtual machines in parallel in the same network][4]</span></span> | <span data-ttu-id="9b8e6-109">Crie máquinas virtuais na mesma região e na mesma rede virtual com duas sub-redes em paralelo.</span><span class="sxs-lookup"><span data-stu-id="9b8e6-109">Create virtual machines in the same region on the same virtual network with two subnets in parallel.</span></span> |
| <span data-ttu-id="9b8e6-110">[Criar máquinas virtuais entre regiões em paralelo][5]</span><span class="sxs-lookup"><span data-stu-id="9b8e6-110">[Create virtual machines across regions in parallel][5]</span></span> | <span data-ttu-id="9b8e6-111">Crie e faça o balanceamento de carga de um conjunto de máquinas virtuais entre várias regiões do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b8e6-111">Create and load-balance a set of virtual machines across multiple Azure regions.</span></span> |
| <span data-ttu-id="9b8e6-112">**Máquinas virtuais de rede**</span><span class="sxs-lookup"><span data-stu-id="9b8e6-112">**Network virtual machines**</span></span> || 
| <span data-ttu-id="9b8e6-113">[Gerenciar redes virtuais][6]</span><span class="sxs-lookup"><span data-stu-id="9b8e6-113">[Manage virtual networks][6]</span></span> | <span data-ttu-id="9b8e6-114">Configure uma rede virtual com duas sub-redes e restrinja o acesso delas à Internet.</span><span class="sxs-lookup"><span data-stu-id="9b8e6-114">Set up a virtual network with two subnets and restrict Internet access to them.</span></span> |
| <span data-ttu-id="9b8e6-115">**Criar conjuntos de dimensionamento**</span><span class="sxs-lookup"><span data-stu-id="9b8e6-115">**Create scale sets**</span></span> ||
| <span data-ttu-id="9b8e6-116">[Criar um conjunto de dimensionamento de máquinas virtuais com um balanceador de carga][7]</span><span class="sxs-lookup"><span data-stu-id="9b8e6-116">[Create a virtual machine scale set with a load balancer][7]</span></span> | <span data-ttu-id="9b8e6-117">Crie um conjunto de dimensionamento da VM, configure um balanceador de carga e obtenha cadeias de conexão SSH para as VMs do conjunto de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="9b8e6-117">Create a VM scale set, set up a load balancer, and get SSH connection strings to the scale set VMs.</span></span> |

[1]: ../java-sdk-manage-virtual-machines.md
[2]: https://azure.microsoft.com/resources/samples/managed-disk-java-create-virtual-machine-using-custom-image/
[3]: https://azure.microsoft.com/resources/samples/managed-disk-java-create-virtual-machine-using-specialized-disk-from-vhd/
[4]: https://azure.microsoft.com/resources/samples/compute-java-manage-virtual-machines-in-parallel/
[5]: ../java-sdk-virtual-machines-in-parallel.md
[6]: ../java-sdk-manage-virtual-networks.md
[7]: ../java-sdk-manage-vm-scalesets.md