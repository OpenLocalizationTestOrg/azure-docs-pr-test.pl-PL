---
title: "aaaUnderstand udostępnionych adresów IP w usłudze Azure DevTest Labs | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak Azure DevTest Labs używa udostępnionego IP adresów toominimize hello publicznego adresu IP adresy wymagane tooaccess laboratorium maszyn wirtualnych."
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
ms.openlocfilehash: 8756410117a9d550d567d372174bf1ea96703c74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-shared-ip-addresses-in-azure-devtest-labs"></a><span data-ttu-id="05f67-103">Zrozumienie udostępnionego adresów IP w usłudze Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="05f67-103">Understand shared IP addresses in Azure DevTest Labs</span></span>

<span data-ttu-id="05f67-104">Azure DevTest Labs umożliwia laboratorium udziału maszyn wirtualnych hello publicznego adresu IP adres toominimize hello tyle publicznego tooaccess wymaganych adresów IP laboratorium poszczególnych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="05f67-104">Azure DevTest Labs lets lab VMs share hello same public IP address toominimize hello number of public IP addresses required tooaccess your individual lab VMs.</span></span>  <span data-ttu-id="05f67-105">W tym artykule opisano, jak udostępnione pracy adresów IP oraz ich powiązane opcje konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="05f67-105">This article describes how shared IPs work and their related configuration options.</span></span>

## <a name="shared-ip-setting"></a><span data-ttu-id="05f67-106">Udostępnione ustawienie adresu IP</span><span class="sxs-lookup"><span data-stu-id="05f67-106">Shared IP setting</span></span>

<span data-ttu-id="05f67-107">Po utworzeniu laboratorium znajduje się w podsieci sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="05f67-107">When you create a lab, it resides in a subnet of a virtual network.</span></span>  <span data-ttu-id="05f67-108">Domyślnie ta podsieć jest tworzony z **Włącz udostępnione publicznego adresu IP** ustawić także*tak*.</span><span class="sxs-lookup"><span data-stu-id="05f67-108">By default, this subnet is created with **Enable shared public IP** set too*Yes*.</span></span>  <span data-ttu-id="05f67-109">Ta konfiguracja tworzy jeden publiczny adres IP hello całej podsieci.</span><span class="sxs-lookup"><span data-stu-id="05f67-109">This configuration creates one public IP address for hello entire subnet.</span></span>  <span data-ttu-id="05f67-110">Aby uzyskać więcej informacji na temat konfigurowania sieci wirtualnych i podsieci, zobacz [Konfigurowanie sieci wirtualnej w usłudze Azure DevTest Labs](devtest-lab-configure-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="05f67-110">For more information about configuring virtual networks and subnets, see [Configure a virtual network in Azure DevTest Labs](devtest-lab-configure-vnet.md).</span></span>

![Nowa podsieć laboratorium](media/devtest-lab-shared-ip/lab-subnet.png)

<span data-ttu-id="05f67-112">Istniejące labs tę opcję można włączyć, wybierając **konfiguracji i zasadach > sieci wirtualnych**.</span><span class="sxs-lookup"><span data-stu-id="05f67-112">For existing labs, you can enable this option by selecting **Configuration and policies > Virtual Networks**.</span></span> <span data-ttu-id="05f67-113">Następnie wybierz sieć wirtualną z listy hello i wybierz **Włącz UDOSTĘPNIONE publicznego adresu IP** dla wybranej podsieci.</span><span class="sxs-lookup"><span data-stu-id="05f67-113">Then, select a virtual network from hello list and choose **ENABLE SHARED PUBLIC IP** for a selected subnet.</span></span> <span data-ttu-id="05f67-114">Można również wyłączyć tę opcję w dowolnym laboratorium, jeśli nie chcesz tooshare publicznego adresu IP w laboratorium maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="05f67-114">You can also disable this option in any lab if you don't want tooshare a public IP address across lab VMs.</span></span>

<span data-ttu-id="05f67-115">Wszystkie maszyny wirtualne utworzone w toousing domyślne tego laboratorium udostępnionego IP.</span><span class="sxs-lookup"><span data-stu-id="05f67-115">Any VMs created in this lab default toousing a shared IP.</span></span>  <span data-ttu-id="05f67-116">Podczas tworzenia hello maszyny Wirtualnej, to ustawienie można zaobserwować w hello **Zaawansowane ustawienia** bloku w obszarze **konfiguracji adresu IP**.</span><span class="sxs-lookup"><span data-stu-id="05f67-116">When creating hello VM, this setting can be observed in hello **Advanced settings** blade under **IP address configuration**.</span></span>

![Nowej maszyny Wirtualnej](media/devtest-lab-shared-ip/new-vm.png)

- <span data-ttu-id="05f67-118">**Shared:** wszystkie maszyny wirtualne utworzone jako **Shared** są umieszczane w jednej grupy zasobów (zarządcy zasobów).</span><span class="sxs-lookup"><span data-stu-id="05f67-118">**Shared:** All VMs created as **Shared** are placed into one resource group (RG).</span></span> <span data-ttu-id="05f67-119">Pojedynczy adres IP jest przypisany do tego zarządcy zasobów i wszystkich maszyn wirtualnych w hello zarządcy zasobów będzie używać tego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="05f67-119">A single IP address is assigned for that RG and all VMs in hello RG will use that IP address.</span></span>
- <span data-ttu-id="05f67-120">**Publicznego:** każdej maszyny Wirtualnej tworzonej ma swój adres IP i jest tworzona w jego własnej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="05f67-120">**Public:** Every VM you create has its own IP address and is created in its own resource group.</span></span>
- <span data-ttu-id="05f67-121">**Prywatne:** każdej maszyny Wirtualnej tworzonej używa prywatnego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="05f67-121">**Private:** Every VM you create uses a private IP address.</span></span> <span data-ttu-id="05f67-122">Nie będą mogli tooconnect toothis maszyny Wirtualnej bezpośrednio z hello internet przy użyciu pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="05f67-122">You will not be able tooconnect toothis VM directly from hello internet with Remote Desktop.</span></span>

<span data-ttu-id="05f67-123">Przy każdym dodaniu toohello podsieci maszyny Wirtualnej z udostępnionego IP włączone DevTest Labs automatycznie dodaje hello modułu równoważenia obciążenia tooa dla maszyny Wirtualnej i przypisuje numer portu TCP na powitania publicznego adresu IP, przekazywania toohello portem RDP na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="05f67-123">Whenever a VM with shared IP enabled is added toohello subnet, DevTest Labs automatically adds hello VM tooa load balancer and assigns a TCP port number on hello public IP address, forwarding toohello RDP port on hello VM.</span></span>  

## <a name="using-hello-shared-ip"></a><span data-ttu-id="05f67-124">Używanie hello udostępnionego IP</span><span class="sxs-lookup"><span data-stu-id="05f67-124">Using hello shared IP</span></span>

- <span data-ttu-id="05f67-125">**Użytkownicy systemu Linux:** toohello SSH maszyny Wirtualnej za pomocą adresu IP hello lub pełną nazwę domeny, wprowadź dwukropek, a następnie hello portu.</span><span class="sxs-lookup"><span data-stu-id="05f67-125">**Linux users:** SSH toohello VM by using hello IP address or fully qualified domain name, followed by a colon, followed by hello port.</span></span> <span data-ttu-id="05f67-126">Na przykład w poniższym obrazie hello, hello RDP adresów toohello tooconnect maszyna wirtualna jest `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.</span><span class="sxs-lookup"><span data-stu-id="05f67-126">For example, in hello image below, hello RDP address tooconnect toohello VM is `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.</span></span>

  ![Przykład maszyny Wirtualnej](media/devtest-lab-shared-ip/vm-info.png)

- <span data-ttu-id="05f67-128">**Użytkownicy systemu Windows:** wybierz hello **Connect** znajdującego się na powitania toodownload portalu Azure wstępnie skonfigurowany plik RDP i dostępu hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="05f67-128">**Windows users:** Select hello **Connect** button on hello Azure portal toodownload a pre-configured RDP file and access hello VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="05f67-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="05f67-129">Next steps</span></span>

* [<span data-ttu-id="05f67-130">Definiowanie zasad laboratorium w usłudze Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="05f67-130">Define lab policies in Azure DevTest Labs</span></span>](devtest-lab-set-lab-policy.md)
* [<span data-ttu-id="05f67-131">Konfigurowanie sieci wirtualnej w usłudze Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="05f67-131">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md)





