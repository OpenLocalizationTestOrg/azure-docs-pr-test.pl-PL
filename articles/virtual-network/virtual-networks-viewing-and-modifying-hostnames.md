---
title: "Wyświetlanie i modyfikowanie nazwy hostów | Dokumentacja firmy Microsoft"
description: "Jak przeglądać i zmieniać nazwy hostów maszyn wirtualnych platformy Azure, sieci web i proces roboczy do rozpoznawania nazw"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: c668cd8e-4e43-4d05-acc3-db64fa78d828
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2016
ms.author: jdial
ms.openlocfilehash: 9a3a1e1b58dcb828e2d2d09c18f1aab6d46051aa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="viewing-and-modifying-hostnames"></a><span data-ttu-id="cd951-103">Wyświetlanie i modyfikowanie nazwy hostów</span><span class="sxs-lookup"><span data-stu-id="cd951-103">Viewing and modifying hostnames</span></span>
<span data-ttu-id="cd951-104">Aby zezwolić wystąpienia roli przywoływanie według nazwy hosta, należy ustawić wartość nazwy hosta w pliku konfiguracji usługi dla każdej roli.</span><span class="sxs-lookup"><span data-stu-id="cd951-104">To allow your role instances to be referenced by host name, you must set the value for the host name in the service configuration file for each role.</span></span> <span data-ttu-id="cd951-105">Można to zrobić przez dodanie nazwy wybranego hosta, aby **vmName** atrybutu **roli** elementu.</span><span class="sxs-lookup"><span data-stu-id="cd951-105">You do that by adding the desired host name to the **vmName** attribute of the **Role** element.</span></span> <span data-ttu-id="cd951-106">Wartość **vmName** atrybutu jest używana jako podstawa dla każdego wystąpienia roli nazwy hosta.</span><span class="sxs-lookup"><span data-stu-id="cd951-106">The value of the **vmName** attribute is used as a base for the host name of each role instance.</span></span> <span data-ttu-id="cd951-107">Na przykład jeśli **vmName** jest *sieć Web* istnieją trzy wystąpień tej roli, nazwy hosta wystąpień będą *webrole0*, *webrole1*, i *webrole2*.</span><span class="sxs-lookup"><span data-stu-id="cd951-107">For example, if **vmName** is *webrole* and there are three instances of that role, the host names of the instances will be *webrole0*, *webrole1*, and *webrole2*.</span></span> <span data-ttu-id="cd951-108">Nie trzeba określić nazwę hosta dla maszyn wirtualnych w pliku konfiguracji, ponieważ nazwa hosta dla maszyny wirtualnej jest wypełniana na podstawie nazwy maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="cd951-108">You do not need to specify a host name for virtual machines in the configuration file, because the host name for a virtual machine is populated based on the virtual machine name.</span></span> <span data-ttu-id="cd951-109">Aby uzyskać więcej informacji o konfigurowaniu usługi Microsoft Azure, zobacz [schemat konfiguracji usługi Azure (cscfg plików)](https://msdn.microsoft.com/library/azure/ee758710.aspx)</span><span class="sxs-lookup"><span data-stu-id="cd951-109">For more information about configuring a Microsoft Azure service, see [Azure Service Configuration Schema (.cscfg File)](https://msdn.microsoft.com/library/azure/ee758710.aspx)</span></span>

## <a name="viewing-hostnames"></a><span data-ttu-id="cd951-110">Wyświetlanie nazwy hostów</span><span class="sxs-lookup"><span data-stu-id="cd951-110">Viewing hostnames</span></span>
<span data-ttu-id="cd951-111">Można wyświetlić nazwy hostów maszyn wirtualnych i wystąpień roli w usłudze w chmurze przy użyciu dowolnej z poniższych narzędzi.</span><span class="sxs-lookup"><span data-stu-id="cd951-111">You can view the host names of virtual machines and role instances in a cloud service by using any of the tools below.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="cd951-112">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="cd951-112">Azure Portal</span></span>
<span data-ttu-id="cd951-113">Można użyć [portalu Azure](http://portal.azure.com) Aby wyświetlić nazwy hostów dla maszyn wirtualnych w bloku omówienie maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="cd951-113">You can use the [Azure portal](http://portal.azure.com) to view the host names for virtual machines on the overview blade for a virtual machine.</span></span> <span data-ttu-id="cd951-114">Należy pamiętać, że blok zawiera wartość dla **nazwa** i **nazwy hosta**.</span><span class="sxs-lookup"><span data-stu-id="cd951-114">Keep in mind that the blade shows a value for **Name** and **Host Name**.</span></span> <span data-ttu-id="cd951-115">Chociaż początkowo są takie same, zmiana nazwy hosta nie zmieni nazwę maszyny wirtualnej lub wystąpienia roli.</span><span class="sxs-lookup"><span data-stu-id="cd951-115">Although they are initially the same, changing the host name will not change the name of the virtual machine or role instance.</span></span>

<span data-ttu-id="cd951-116">Można również wyświetlać wystąpień roli w portalu Azure, ale jeśli lista wystąpień w usłudze w chmurze, nazwy hosta nie jest wyświetlana.</span><span class="sxs-lookup"><span data-stu-id="cd951-116">Role instances can also be viewed in the Azure portal, but when you list the instances in a cloud service, the host name is not displayed.</span></span> <span data-ttu-id="cd951-117">Zobaczysz nazwy dla każdego wystąpienia, ale ta nazwa reprezentuje nazwę hosta.</span><span class="sxs-lookup"><span data-stu-id="cd951-117">You will see a name for each instance, but that name does not represent the host name.</span></span>

### <a name="service-configuration-file"></a><span data-ttu-id="cd951-118">Plik konfiguracji usługi</span><span class="sxs-lookup"><span data-stu-id="cd951-118">Service configuration file</span></span>
<span data-ttu-id="cd951-119">Możesz pobrać plik konfiguracji usługi dla wdrożonej usługi z **Konfiguruj** bloku usługi w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="cd951-119">You can download the service configuration file for a deployed service from the **Configure** blade of the service in the Azure portal.</span></span> <span data-ttu-id="cd951-120">Następnie można wyszukać **vmName** atrybutu dla **nazwy roli** element, aby zobaczyć nazwę hosta.</span><span class="sxs-lookup"><span data-stu-id="cd951-120">You can then look for the **vmName** attribute for the **Role name** element to see the host name.</span></span> <span data-ttu-id="cd951-121">Należy pamiętać, że ta nazwa hosta jest używana jako podstawa dla każdego wystąpienia roli nazwy hosta.</span><span class="sxs-lookup"><span data-stu-id="cd951-121">Keep in mind that this host name is used as a base for the host name of each role instance.</span></span> <span data-ttu-id="cd951-122">Na przykład jeśli **vmName** jest *sieć Web* istnieją trzy wystąpień tej roli, nazwy hosta wystąpień będą *webrole0*, *webrole1*, i *webrole2*.</span><span class="sxs-lookup"><span data-stu-id="cd951-122">For example, if **vmName** is *webrole* and there are three instances of that role, the host names of the instances will be *webrole0*, *webrole1*, and *webrole2*.</span></span>

### <a name="remote-desktop"></a><span data-ttu-id="cd951-123">Pulpit zdalny</span><span class="sxs-lookup"><span data-stu-id="cd951-123">Remote Desktop</span></span>
<span data-ttu-id="cd951-124">Po włączeniu pulpitu zdalnego (system Windows), komunikacji zdalnej programu Windows PowerShell (Windows) lub połączeń SSH (Linux i Windows) do maszyny wirtualnej lub wystąpień roli można wyświetlić nazwy hosta z aktywnego połączenia pulpitu zdalnego na różne sposoby:</span><span class="sxs-lookup"><span data-stu-id="cd951-124">After you enable Remote Desktop (Windows), Windows PowerShell remoting (Windows), or SSH (Linux and Windows) connections to your virtual machines or role instances, you can view the host name from an active Remote Desktop connection in various ways:</span></span>

* <span data-ttu-id="cd951-125">W wierszu polecenia lub SSH terminal, wpisz nazwę hosta.</span><span class="sxs-lookup"><span data-stu-id="cd951-125">Type hostname at the command prompt or SSH terminal.</span></span>
* <span data-ttu-id="cd951-126">Wpisz polecenie ipconfig/wszystkich w wierszu polecenia monit (tylko system Windows).</span><span class="sxs-lookup"><span data-stu-id="cd951-126">Type ipconfig /all at the command prompt (Windows only).</span></span>
* <span data-ttu-id="cd951-127">Wyświetl nazwę komputera w ustawieniach systemu (tylko system Windows).</span><span class="sxs-lookup"><span data-stu-id="cd951-127">View the computer name in the system settings (Windows only).</span></span>

### <a name="azure-service-management-rest-api"></a><span data-ttu-id="cd951-128">Usługa Azure Service Management REST API</span><span class="sxs-lookup"><span data-stu-id="cd951-128">Azure Service Management REST API</span></span>
<span data-ttu-id="cd951-129">W kliencie REST wykonaj następujące instrukcje:</span><span class="sxs-lookup"><span data-stu-id="cd951-129">From a REST client, follow these instructions:</span></span>

1. <span data-ttu-id="cd951-130">Upewnij się, że certyfikat klienta do nawiązania połączenia z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="cd951-130">Ensure that you have a client certificate to connect to the Azure portal.</span></span> <span data-ttu-id="cd951-131">Aby uzyskać certyfikat klienta, wykonaj kroki przedstawione w [porady: pobieranie i importowanie ustawień publikowania i informacji o subskrypcji](https://msdn.microsoft.com/library/dn385850.aspx).</span><span class="sxs-lookup"><span data-stu-id="cd951-131">To obtain a client certificate, follow the steps presented in [How to: Download and Import Publish Settings and Subscription Information](https://msdn.microsoft.com/library/dn385850.aspx).</span></span> 
2. <span data-ttu-id="cd951-132">Ustaw wpis nagłówka o nazwie x-ms-version o wartości 2013-11-01.</span><span class="sxs-lookup"><span data-stu-id="cd951-132">Set a header entry named x-ms-version with a value of 2013-11-01.</span></span>
3. <span data-ttu-id="cd951-133">Wyślij żądanie w następującym formacie: https://management.core.windows.net/\<identyfikator subscrition\>/services/hostedservices/\<nazwa usługi\>? osadzić szczegółów = true</span><span class="sxs-lookup"><span data-stu-id="cd951-133">Send a request in the following format: https://management.core.windows.net/\<subscrition-id\>/services/hostedservices/\<service-name\>?embed-detail=true</span></span>
4. <span data-ttu-id="cd951-134">Wyszukaj **HostName** elementu dla każdego **RoleInstance** elementu.</span><span class="sxs-lookup"><span data-stu-id="cd951-134">Look for the **HostName** element for each **RoleInstance** element.</span></span>

> [!WARNING]
> <span data-ttu-id="cd951-135">Możesz również wyświetlić sufiks domeny wewnętrznej dla usługi w chmurze z odpowiedzi wywołań REST, sprawdzając **InternalDnsSuffix** elementu, lub przez uruchomienie polecenia ipconfig/z wiersza polecenia w sesji pulpitu zdalnego (Windows) lub przez polecenia cat /etc/resolv.conf SSH terminali (Linux).</span><span class="sxs-lookup"><span data-stu-id="cd951-135">You can also view the internal domain suffix for your cloud service from the REST call response by checking the **InternalDnsSuffix** element, or by running ipconfig /all from a command prompt in a Remote Desktop session (Windows), or by running cat /etc/resolv.conf from an SSH terminal (Linux).</span></span>
> 
> 

## <a name="modifying-a-hostname"></a><span data-ttu-id="cd951-136">Modyfikowanie nazwy hosta</span><span class="sxs-lookup"><span data-stu-id="cd951-136">Modifying a hostname</span></span>
<span data-ttu-id="cd951-137">Można zmodyfikować nazwę hosta dla maszyny wirtualnej lub wystąpienia roli, przekazując plik konfiguracji usługi zmodyfikowanych lub zmiana nazwy komputera z sesji pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="cd951-137">You can modify the host name for any virtual machine or role instance by uploading a modified service configuration file, or by renaming the computer from a Remote Desktop session.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cd951-138">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cd951-138">Next steps</span></span>
[<span data-ttu-id="cd951-139">Rozpoznawanie nazw (domen DNS)</span><span class="sxs-lookup"><span data-stu-id="cd951-139">Name Resolution (DNS)</span></span>](virtual-networks-name-resolution-for-vms-and-role-instances.md)

[<span data-ttu-id="cd951-140">Schemat konfiguracji usługi Azure (cscfg)</span><span class="sxs-lookup"><span data-stu-id="cd951-140">Azure Service Configuration Schema (.cscfg)</span></span>](https://msdn.microsoft.com/library/windowsazure/ee758710.aspx)

[<span data-ttu-id="cd951-141">Schemat konfiguracji sieci wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="cd951-141">Azure Virtual Network Configuration Schema</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

[<span data-ttu-id="cd951-142">Określ ustawienia DNS za pomocą plików konfiguracji sieci</span><span class="sxs-lookup"><span data-stu-id="cd951-142">Specify DNS settings using network configuration files</span></span>](virtual-networks-specifying-a-dns-settings-in-a-virtual-network-configuration-file.md)

