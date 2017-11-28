---
title: "Zrozumienie udostępnionego adresów IP w usłudze Azure DevTest Labs | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak Azure DevTest Labs używana udostępnionego adresów IP, aby zminimalizować publiczne adresy IP wymagane do uzyskania dostępu laboratorium maszyn wirtualnych."
services: devtest-lab
documentationcenter: na
author: camsoper
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: casoper
ms.openlocfilehash: 9f6e1980bf5ea5b41da98a135d89f1c5159921a7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="understand-shared-ip-addresses-in-azure-devtest-labs"></a><span data-ttu-id="51737-103">Zrozumienie udostępnionego adresów IP w usłudze Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="51737-103">Understand shared IP addresses in Azure DevTest Labs</span></span>

<span data-ttu-id="51737-104">Azure DevTest Labs umożliwia maszyn wirtualnych laboratorium udostępnianie tego samego publiczny adres IP, aby zminimalizować liczbę publicznych adresów IP wymagane do uzyskania dostępu laboratorium poszczególnych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="51737-104">Azure DevTest Labs lets lab VMs share the same public IP address to minimize the number of public IP addresses required to access your individual lab VMs.</span></span>  <span data-ttu-id="51737-105">W tym artykule opisano, jak udostępnione pracy adresów IP oraz ich powiązane opcje konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="51737-105">This article describes how shared IPs work and their related configuration options.</span></span>

## <a name="shared-ip-setting"></a><span data-ttu-id="51737-106">Udostępnione ustawienie adresu IP</span><span class="sxs-lookup"><span data-stu-id="51737-106">Shared IP setting</span></span>

<span data-ttu-id="51737-107">Po utworzeniu laboratorium znajduje się w podsieci sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="51737-107">When you create a lab, it resides in a subnet of a virtual network.</span></span>  <span data-ttu-id="51737-108">Domyślnie ta podsieć jest tworzony z **Włącz udostępnione publicznego adresu IP** ustawioną *tak*.</span><span class="sxs-lookup"><span data-stu-id="51737-108">By default, this subnet is created with **Enable shared public IP** set to *Yes*.</span></span>  <span data-ttu-id="51737-109">Ta konfiguracja tworzy jeden publiczny adres IP w całej podsieci.</span><span class="sxs-lookup"><span data-stu-id="51737-109">This configuration creates one public IP address for the entire subnet.</span></span>  <span data-ttu-id="51737-110">Aby uzyskać więcej informacji na temat konfigurowania sieci wirtualnych i podsieci, zobacz [Konfigurowanie sieci wirtualnej w usłudze Azure DevTest Labs](devtest-lab-configure-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="51737-110">For more information about configuring virtual networks and subnets, see [Configure a virtual network in Azure DevTest Labs](devtest-lab-configure-vnet.md).</span></span>

![Nowa podsieć laboratorium](media/devtest-lab-shared-ip/lab-subnet.png)

<span data-ttu-id="51737-112">Istniejące labs tę opcję można włączyć, wybierając **konfiguracji i zasadach > sieci wirtualnych**.</span><span class="sxs-lookup"><span data-stu-id="51737-112">For existing labs, you can enable this option by selecting **Configuration and policies > Virtual Networks**.</span></span> <span data-ttu-id="51737-113">Następnie wybierz sieć wirtualną z listy i wybierz **Włącz UDOSTĘPNIONE publicznego adresu IP** dla wybranej podsieci.</span><span class="sxs-lookup"><span data-stu-id="51737-113">Then, select a virtual network from the list and choose **ENABLE SHARED PUBLIC IP** for a selected subnet.</span></span> <span data-ttu-id="51737-114">Można również wyłączyć tę opcję w dowolnym laboratorium, jeśli nie chcesz udostępniać publicznego adresu IP w laboratorium maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="51737-114">You can also disable this option in any lab if you don't want to share a public IP address across lab VMs.</span></span>

<span data-ttu-id="51737-115">Wszystkie maszyny wirtualne utworzone z tego laboratorium domyślną przy użyciu udostępnionych protokołu IP.</span><span class="sxs-lookup"><span data-stu-id="51737-115">Any VMs created in this lab default to using a shared IP.</span></span>  <span data-ttu-id="51737-116">Podczas tworzenia maszyny Wirtualnej, to ustawienie można zaobserwować w **Zaawansowane ustawienia** bloku w obszarze **konfiguracji adresu IP**.</span><span class="sxs-lookup"><span data-stu-id="51737-116">When creating the VM, this setting can be observed in the **Advanced settings** blade under **IP address configuration**.</span></span>

![Nowej maszyny Wirtualnej](media/devtest-lab-shared-ip/new-vm.png)

- <span data-ttu-id="51737-118">**Shared:** wszystkie maszyny wirtualne utworzone jako **Shared** są umieszczane w jednej grupy zasobów (zarządcy zasobów).</span><span class="sxs-lookup"><span data-stu-id="51737-118">**Shared:** All VMs created as **Shared** are placed into one resource group (RG).</span></span> <span data-ttu-id="51737-119">Pojedynczy adres IP jest przypisany do tego zarządcy zasobów i wszystkich maszyn wirtualnych w grupie replikacji użyje tego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="51737-119">A single IP address is assigned for that RG and all VMs in the RG will use that IP address.</span></span>
- <span data-ttu-id="51737-120">**Publicznego:** każdej maszyny Wirtualnej tworzonej ma swój adres IP i jest tworzona w jego własnej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="51737-120">**Public:** Every VM you create has its own IP address and is created in its own resource group.</span></span>
- <span data-ttu-id="51737-121">**Prywatne:** każdej maszyny Wirtualnej tworzonej używa prywatnego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="51737-121">**Private:** Every VM you create uses a private IP address.</span></span> <span data-ttu-id="51737-122">Nie można nawiązać połączenia z tej maszyny Wirtualnej bezpośrednio z Internetu przy użyciu pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="51737-122">You will not be able to connect to this VM directly from the internet with Remote Desktop.</span></span>

<span data-ttu-id="51737-123">Zawsze, gdy maszyny Wirtualnej z udostępnionego IP włączony jest dodawany do podsieci, DevTest Labs automatycznie dodaje maszynę Wirtualną z modułem równoważenia obciążenia i przypisuje numer portu TCP na publiczny adres IP, przesyłania dalej z portem RDP na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="51737-123">Whenever a VM with shared IP enabled is added to the subnet, DevTest Labs automatically adds the VM to a load balancer and assigns a TCP port number on the public IP address, forwarding to the RDP port on the VM.</span></span>  

## <a name="using-the-shared-ip"></a><span data-ttu-id="51737-124">Za pomocą udostępnionego IP</span><span class="sxs-lookup"><span data-stu-id="51737-124">Using the shared IP</span></span>

- <span data-ttu-id="51737-125">**Użytkownicy systemu Linux:** SSH z maszyną Wirtualną przy użyciu adresu IP lub nazwy FQDN, wprowadź dwukropek, a następnie port.</span><span class="sxs-lookup"><span data-stu-id="51737-125">**Linux users:** SSH to the VM by using the IP address or fully qualified domain name, followed by a colon, followed by the port.</span></span> <span data-ttu-id="51737-126">Na przykład na poniższej ilustracji, adres protokołu RDP do nawiązania połączenia z maszyną Wirtualną jest `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.</span><span class="sxs-lookup"><span data-stu-id="51737-126">For example, in the image below, the RDP address to connect to the VM is `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.</span></span>

  ![Przykład maszyny Wirtualnej](media/devtest-lab-shared-ip/vm-info.png)

- <span data-ttu-id="51737-128">**Użytkownicy systemu Windows:** wybierz **Connect** przycisk w portalu Azure, aby pobrać plik RDP wstępnie skonfigurowane i dostęp do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="51737-128">**Windows users:** Select the **Connect** button on the Azure portal to download a pre-configured RDP file and access the VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="51737-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="51737-129">Next steps</span></span>

* [<span data-ttu-id="51737-130">Definiowanie zasad laboratorium w usłudze Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="51737-130">Define lab policies in Azure DevTest Labs</span></span>](devtest-lab-set-lab-policy.md)
* [<span data-ttu-id="51737-131">Konfigurowanie sieci wirtualnej w usłudze Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="51737-131">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md)





