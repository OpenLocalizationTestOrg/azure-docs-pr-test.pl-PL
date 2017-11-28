---
title: "aaaReverse DNS dla usługi Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure wstecznego wyszukiwania DNS dla usługi hostowanej na platformie Azure"
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/29/2017
ms.author: jonatul
ms.openlocfilehash: c6fe1d80232f124be86dd7fc57abc20699be7eba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-reverse-dns-for-services-hosted-in-azure"></a><span data-ttu-id="5be92-103">Skonfiguruj wstecznego DNS dla usługi hostowanej na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="5be92-103">Configure reverse DNS for services hosted in Azure</span></span>

<span data-ttu-id="5be92-104">W tym artykule opisano, jak tooconfigure wstecznego wyszukiwania DNS dla usługi hostowanej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="5be92-104">This article explains how tooconfigure reverse DNS lookups for services hosted in Azure.</span></span>

<span data-ttu-id="5be92-105">Usługi w usłudze Azure używać adresów IP przypisany przez usługę Azure i należących do firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="5be92-105">Services in Azure use IP addresses assigned by Azure and owned by Microsoft.</span></span> <span data-ttu-id="5be92-106">Te rekordy DNS odwrotnej (rekordów PTR) należy utworzyć w hello odpowiedniego należące do firmy Microsoft stref wyszukiwania wstecznego DNS wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="5be92-106">These reverse DNS records (PTR records) must be created in hello corresponding Microsoft-owned reverse DNS lookup zones.</span></span> <span data-ttu-id="5be92-107">W tym artykule opisano sposób toodo to.</span><span class="sxs-lookup"><span data-stu-id="5be92-107">This article explains how toodo this.</span></span>

<span data-ttu-id="5be92-108">W tym scenariuszu nie należy mylić z możliwością hello zbyt[hostowanie strefy hello do wyszukiwania wstecznego DNS dla przypisane zakresy IP w usłudze Azure DNS](dns-reverse-dns-hosting.md).</span><span class="sxs-lookup"><span data-stu-id="5be92-108">This scenario should not be confused with hello ability too[host hello reverse DNS lookup zones for your assigned IP ranges in Azure DNS](dns-reverse-dns-hosting.md).</span></span> <span data-ttu-id="5be92-109">W takim przypadku zakresów adresów IP hello reprezentowany przez strefy wyszukiwania wstecznego hello musi być przypisany organizacji tooyour zwykle przez Usługodawcę internetowego.</span><span class="sxs-lookup"><span data-stu-id="5be92-109">In this case, hello IP ranges represented by hello reverse lookup zone must be assigned tooyour organization, typically by your ISP.</span></span>

<span data-ttu-id="5be92-110">Przed przeczytaniem tego artykułu, należy się zapoznać z tym [omówienie wstecznego DNS i pomocy technicznej na platformie Azure](dns-reverse-dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5be92-110">Before reading this article, you should be familiar with this [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>

<span data-ttu-id="5be92-111">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="5be92-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>
* <span data-ttu-id="5be92-112">W modelu wdrażania usługi Resource Manager hello zasobów obliczeniowych (np. maszyny wirtualne, zestawy skalowania maszyny wirtualnej lub klastrów sieci szkieletowej usług) są udostępniane za pośrednictwem publicznego adresu IP zasobu.</span><span class="sxs-lookup"><span data-stu-id="5be92-112">In hello Resource Manager deployment model, compute resources (such as virtual machines, virtual machine scale sets, or Service Fabric clusters) are exposed via a PublicIpAddress resource.</span></span> <span data-ttu-id="5be92-113">Wyszukiwania wstecznego DNS są skonfigurowane przy użyciu właściwości "ReverseFqdn" hello hello publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="5be92-113">Reverse DNS lookups are configured using hello 'ReverseFqdn' property of hello PublicIpAddress.</span></span>
* <span data-ttu-id="5be92-114">W hello klasycznego modelu wdrożenia zasoby obliczeniowe są widoczne, przy użyciu usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="5be92-114">In hello Classic deployment model, compute resources are exposed using Cloud Services.</span></span> <span data-ttu-id="5be92-115">Wyszukiwania wstecznego DNS są skonfigurowane przy użyciu właściwości "ReverseDnsFqdn" hello hello usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="5be92-115">Reverse DNS lookups are configured using hello 'ReverseDnsFqdn' property of hello Cloud Service.</span></span>

<span data-ttu-id="5be92-116">Wstecznego DNS nie jest obecnie obsługiwany dla hello Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="5be92-116">Reverse DNS is not currently supported for hello Azure App Service.</span></span>

## <a name="validation-of-reverse-dns-records"></a><span data-ttu-id="5be92-117">Sprawdzanie poprawności odwrotnej rekordów DNS</span><span class="sxs-lookup"><span data-stu-id="5be92-117">Validation of reverse DNS records</span></span>

<span data-ttu-id="5be92-118">Innej firmy nie może być możliwe toocreate odwrotnej rekordy DNS dla domeny DNS tooyour mapowanie usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="5be92-118">A third party should not be able toocreate reverse DNS records for their Azure service mapping tooyour DNS domains.</span></span> <span data-ttu-id="5be92-119">tooprevent, Azure umożliwia tylko tworzenie hello wstecznego rekord DNS, gdzie nazwa domeny określona w odwrotnej rekord DNS hello jest identyczny hello, lub jest rozpoznawana jako hello nazwę DNS lub adres IP publicznego adresu IP lub w chmurze usługi w hello sam subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5be92-119">tooprevent this, Azure only allows hello creation of a reverse DNS record where domain name specified in hello reverse DNS record is hello same as, or resolves to, hello DNS name or IP address of a PublicIpAddress or Cloud Service in hello same Azure subscription.</span></span>

<span data-ttu-id="5be92-120">To tylko weryfikacji hello wstecznego rekord DNS jest ustawiona lub modyfikacji.</span><span class="sxs-lookup"><span data-stu-id="5be92-120">This validation is only performed when hello reverse DNS record is set or modified.</span></span> <span data-ttu-id="5be92-121">Okresowe ponowne sprawdzanie poprawności nie jest wykonywane.</span><span class="sxs-lookup"><span data-stu-id="5be92-121">Periodic re-validation is not performed.</span></span>

<span data-ttu-id="5be92-122">Na przykład: Załóżmy, że hello publicznego adresu IP zasobu ma contosoapp1.northus.cloudapp.azure.com nazwy DNS hello i adres IP 23.96.52.53.</span><span class="sxs-lookup"><span data-stu-id="5be92-122">For example: suppose hello PublicIpAddress resource has hello DNS name contosoapp1.northus.cloudapp.azure.com and IP address 23.96.52.53.</span></span> <span data-ttu-id="5be92-123">Witaj ReverseFqdn dla powitalne publicznego adresu IP może być określona jako:</span><span class="sxs-lookup"><span data-stu-id="5be92-123">hello ReverseFqdn for hello PublicIpAddress can be specified as:</span></span>
* <span data-ttu-id="5be92-124">Nazwa DNS Hello hello publicznego adresu IP, contosoapp1.northus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="5be92-124">hello DNS name for hello PublicIpAddress, contosoapp1.northus.cloudapp.azure.com</span></span>
* <span data-ttu-id="5be92-125">Hello nazwy DNS dla publicznego adresu IP innego w hello sam subskrypcję, taką jak contosoapp2.westus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="5be92-125">hello DNS name for a different PublicIpAddress in hello same subscription, such as contosoapp2.westus.cloudapp.azure.com</span></span>
* <span data-ttu-id="5be92-126">Niestandardowych nazw DNS, takich jak app1.contoso.com, tak długo, jak ta nazwa jest *pierwszy* skonfigurowany jako CNAME toocontosoapp1.northus.cloudapp.azure.com lub tooa różnych publicznego adresu IP w hello tej samej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="5be92-126">A vanity DNS name, such as app1.contoso.com, so long as this name is *first* configured as a CNAME toocontosoapp1.northus.cloudapp.azure.com, or tooa different PublicIpAddress in hello same subscription.</span></span>
* <span data-ttu-id="5be92-127">Niestandardowych nazw DNS, takich jak app1.contoso.com, tak długo, jak ta nazwa jest *pierwszy* skonfigurowany jako adres IP toohello rekordów A 23.96.52.53 lub adres IP toohello różnych publicznego adresu IP w hello tej samej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="5be92-127">A vanity DNS name, such as app1.contoso.com, so long as this name is *first* configured as an A record toohello IP address 23.96.52.53, or toohello IP address of a different PublicIpAddress in hello same subscription.</span></span>

<span data-ttu-id="5be92-128">Witaj takich samych ograniczeń zastosować tooreverse DNS dla usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="5be92-128">hello same constraints apply tooreverse DNS for Cloud Services.</span></span>


## <a name="reverse-dns-for-publicipaddress-resources"></a><span data-ttu-id="5be92-129">Reverse DNS dla zasobów publicznego adresu IP</span><span class="sxs-lookup"><span data-stu-id="5be92-129">Reverse DNS for PublicIpAddress resources</span></span>

<span data-ttu-id="5be92-130">Ta sekcja zawiera szczegółowe instrukcje dotyczące sposobu tooconfigure reverse DNS dla publicznego adresu IP zasobów w modelu wdrażania usługi Resource Manager hello przy użyciu programu Azure PowerShell, interfejsu wiersza polecenia platformy Azure w wersji 1.0 lub 2.0 interfejsu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5be92-130">This section provides detailed instructions for how tooconfigure reverse DNS for PublicIpAddress resources in hello Resource Manager deployment model, using either Azure PowerShell, Azure CLI 1.0, or Azure CLI 2.0.</span></span> <span data-ttu-id="5be92-131">Konfigurowanie wstecznego DNS dla zasobów publicznego adresu IP nie jest obecnie obsługiwane za pośrednictwem hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="5be92-131">Configuring reverse DNS for PublicIpAddress resources is not currently supported via hello Azure portal.</span></span>

<span data-ttu-id="5be92-132">Azure obecnie obsługuje reverse DNS tylko dla zasobów IPv4 publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="5be92-132">Azure currently supports reverse DNS only for IPv4 PublicIpAddress resources.</span></span> <span data-ttu-id="5be92-133">Nie jest obsługiwana w przypadku protokołu IPv6.</span><span class="sxs-lookup"><span data-stu-id="5be92-133">It is not supported for IPv6.</span></span>

### <a name="add-reverse-dns-tooan-existing-publicipaddresses"></a><span data-ttu-id="5be92-134">Dodaj odwrotnej tooan DNS istniejących elementów Publicipaddress</span><span class="sxs-lookup"><span data-stu-id="5be92-134">Add reverse DNS tooan existing PublicIpAddresses</span></span>

#### <a name="powershell"></a><span data-ttu-id="5be92-135">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5be92-135">PowerShell</span></span>

<span data-ttu-id="5be92-136">tooadd reverse DNS tooan istniejącego publicznego adresu IP:</span><span class="sxs-lookup"><span data-stu-id="5be92-136">tooadd reverse DNS tooan existing PublicIpAddress:</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

<span data-ttu-id="5be92-137">tooadd odwrotnej tooan DNS istniejącego publicznego adresu IP, który nie ma nazwy DNS, należy również określić nazwę DNS:</span><span class="sxs-lookup"><span data-stu-id="5be92-137">tooadd reverse DNS tooan existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings = New-Object -TypeName "Microsoft.Azure.Commands.Network.Models.PSPublicIpAddressDnsSettings"
$pip.DnsSettings.DomainNameLabel = "contosoapp1"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a><span data-ttu-id="5be92-138">Interfejs wiersza polecenia platformy Azure CLI w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="5be92-138">Azure CLI 1.0</span></span>

<span data-ttu-id="5be92-139">tooadd reverse DNS tooan istniejącego publicznego adresu IP:</span><span class="sxs-lookup"><span data-stu-id="5be92-139">tooadd reverse DNS tooan existing PublicIpAddress:</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -f contosoapp1.westus.cloudapp.azure.com.
```

<span data-ttu-id="5be92-140">tooadd odwrotnej tooan DNS istniejącego publicznego adresu IP, który nie ma nazwy DNS, należy również określić nazwę DNS:</span><span class="sxs-lookup"><span data-stu-id="5be92-140">tooadd reverse DNS tooan existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -d contosoapp1 -f contosoapp1.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a><span data-ttu-id="5be92-141">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="5be92-141">Azure CLI 2.0</span></span>

<span data-ttu-id="5be92-142">tooadd reverse DNS tooan istniejącego publicznego adresu IP:</span><span class="sxs-lookup"><span data-stu-id="5be92-142">tooadd reverse DNS tooan existing PublicIpAddress:</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com.
```

<span data-ttu-id="5be92-143">tooadd odwrotnej tooan DNS istniejącego publicznego adresu IP, który nie ma nazwy DNS, należy również określić nazwę DNS:</span><span class="sxs-lookup"><span data-stu-id="5be92-143">tooadd reverse DNS tooan existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com --dns-name contosoapp1
```

### <a name="create-a-public-ip-address-with-reverse-dns"></a><span data-ttu-id="5be92-144">Utwórz publiczny adres IP z wstecznego DNS</span><span class="sxs-lookup"><span data-stu-id="5be92-144">Create a Public IP Address with reverse DNS</span></span>

<span data-ttu-id="5be92-145">toocreate nowego publicznego adresu IP z hello wstecznego DNS we właściwości już określony:</span><span class="sxs-lookup"><span data-stu-id="5be92-145">toocreate a new PublicIpAddress with hello reverse DNS property already specified:</span></span>

#### <a name="powershell"></a><span data-ttu-id="5be92-146">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5be92-146">PowerShell</span></span>

```powershell
New-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup" -Location "WestUS" -AllocationMethod Dynamic -DomainNameLabel "contosoapp2" -ReverseFqdn "contosoapp2.westus.cloudapp.azure.com."
```

#### <a name="azure-cli-10"></a><span data-ttu-id="5be92-147">Interfejs wiersza polecenia platformy Azure CLI w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="5be92-147">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip create -n PublicIp -g MyResourceGroup -l westus -d contosoapp3 -f contosoapp3.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a><span data-ttu-id="5be92-148">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="5be92-148">Azure CLI 2.0</span></span>

```azurecli
az network public-ip create --name PublicIp --resource-group MyResourceGroup --location westcentralus --dns-name contosoapp1 --reverse-fqdn contosoapp1.westcentralus.cloudapp.azure.com
```

### <a name="view-reverse-dns-for-an-existing-publicipaddress"></a><span data-ttu-id="5be92-149">Widok wstecznego DNS dla istniejącego publicznego adresu IP</span><span class="sxs-lookup"><span data-stu-id="5be92-149">View reverse DNS for an existing PublicIpAddress</span></span>

<span data-ttu-id="5be92-150">Witaj tooview wartość skonfigurowana dla istniejącego publicznego adresu IP:</span><span class="sxs-lookup"><span data-stu-id="5be92-150">tooview hello configured value for an existing PublicIpAddress:</span></span>

#### <a name="powershell"></a><span data-ttu-id="5be92-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5be92-151">PowerShell</span></span>

```powershell
Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
```

#### <a name="azure-cli-10"></a><span data-ttu-id="5be92-152">Interfejs wiersza polecenia platformy Azure CLI w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="5be92-152">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip show -n PublicIp -g MyResourceGroup
```

#### <a name="azure-cli-20"></a><span data-ttu-id="5be92-153">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="5be92-153">Azure CLI 2.0</span></span>

```azurecli
az network public-ip show --name PublicIp --resource-group MyResourceGroup
```

### <a name="remove-reverse-dns-from-existing-public-ip-addresses"></a><span data-ttu-id="5be92-154">Usuń wstecznego DNS z istniejących publicznych adresów IP</span><span class="sxs-lookup"><span data-stu-id="5be92-154">Remove reverse DNS from existing Public IP Addresses</span></span>

<span data-ttu-id="5be92-155">tooremove odwrotnej właściwości DNS z istniejącego publicznego adresu IP:</span><span class="sxs-lookup"><span data-stu-id="5be92-155">tooremove a reverse DNS property from an existing PublicIpAddress:</span></span>

#### <a name="powershell"></a><span data-ttu-id="5be92-156">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5be92-156">PowerShell</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = ""
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a><span data-ttu-id="5be92-157">Interfejs wiersza polecenia platformy Azure CLI w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="5be92-157">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup –f ""
```

#### <a name="azure-cli-20"></a><span data-ttu-id="5be92-158">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="5be92-158">Azure CLI 2.0</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn ""
```


## <a name="configure-reverse-dns-for-cloud-services"></a><span data-ttu-id="5be92-159">Konfigurowanie wstecznego DNS dla usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="5be92-159">Configure reverse DNS for Cloud Services</span></span>

<span data-ttu-id="5be92-160">Ta sekcja zawiera szczegółowe instrukcje dotyczące sposobu tooconfigure reverse DNS dla usługi w chmurze w klasycznym modelu wdrażania hello, przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5be92-160">This section provides detailed instructions for how tooconfigure reverse DNS for Cloud Services in hello Classic deployment model, using Azure PowerShell.</span></span> <span data-ttu-id="5be92-161">Nie jest obsługiwane Konfigurowanie wstecznego DNS dla usługi w chmurze za pośrednictwem hello portalu Azure, Azure CLI w wersji 1.0 lub 2.0 interfejsu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5be92-161">Configuring reverse DNS for Cloud Services is not supported via hello Azure portal, Azure CLI 1.0, or Azure CLI 2.0.</span></span>

### <a name="add-reverse-dns-tooexisting-cloud-services"></a><span data-ttu-id="5be92-162">Dodawanie usługi w chmurze tooexisting wstecznego DNS</span><span class="sxs-lookup"><span data-stu-id="5be92-162">Add reverse DNS tooexisting Cloud Services</span></span>

<span data-ttu-id="5be92-163">tooadd tooan odwrotnej rekordów DNS, istniejące usługi w chmurze:</span><span class="sxs-lookup"><span data-stu-id="5be92-163">tooadd a reverse DNS record tooan existing Cloud Service:</span></span>

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="create-a-cloud-service-with-reverse-dns"></a><span data-ttu-id="5be92-164">Tworzenie usługi w chmurze z wstecznego DNS</span><span class="sxs-lookup"><span data-stu-id="5be92-164">Create a Cloud Service with reverse DNS</span></span>

<span data-ttu-id="5be92-165">toocreate nową usługę w chmurze z hello wstecznego DNS we właściwości już określony:</span><span class="sxs-lookup"><span data-stu-id="5be92-165">toocreate a new Cloud Service with hello reverse DNS property already specified:</span></span>

```powershell
New-AzureService –ServiceName "contosoapp1" –Location "West US" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="view-reverse-dns-for-existing-cloud-services"></a><span data-ttu-id="5be92-166">Widok wstecznego DNS dla istniejącej usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="5be92-166">View reverse DNS for existing Cloud Services</span></span>

<span data-ttu-id="5be92-167">Witaj tooview reverse DNS we właściwości dla istniejącej usługi w chmurze:</span><span class="sxs-lookup"><span data-stu-id="5be92-167">tooview hello reverse DNS property for an existing Cloud Service:</span></span>

```powershell
Get-AzureService "contosoapp1"
```

### <a name="remove-reverse-dns-from-existing-cloud-services"></a><span data-ttu-id="5be92-168">Usuń wstecznego DNS z istniejącej usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="5be92-168">Remove reverse DNS from existing Cloud Services</span></span>

<span data-ttu-id="5be92-169">tooremove wstecznego DNS właściwości z istniejącej usługi w chmurze:</span><span class="sxs-lookup"><span data-stu-id="5be92-169">tooremove a reverse DNS property from an existing Cloud Service:</span></span>

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn ""
```

## <a name="faq"></a><span data-ttu-id="5be92-170">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="5be92-170">FAQ</span></span>

### <a name="how-much-do-reverse-dns-records-cost"></a><span data-ttu-id="5be92-171">Ile wstecznego koszt rekordy DNS?</span><span class="sxs-lookup"><span data-stu-id="5be92-171">How much do reverse DNS records cost?</span></span>

<span data-ttu-id="5be92-172">Są one wolnego!</span><span class="sxs-lookup"><span data-stu-id="5be92-172">They're free!</span></span>  <span data-ttu-id="5be92-173">Nie ma żadnych dodatkowych kosztów odwrotnej rekordów DNS lub zapytania.</span><span class="sxs-lookup"><span data-stu-id="5be92-173">There is no additional cost for reverse DNS records or queries.</span></span>

### <a name="will-my-reverse-dns-records-resolve-from-hello-internet"></a><span data-ttu-id="5be92-174">Moje odwrotnej rozpoznania rekordów DNS z będzie hello internet?</span><span class="sxs-lookup"><span data-stu-id="5be92-174">Will my reverse DNS records resolve from hello internet?</span></span>

<span data-ttu-id="5be92-175">Tak.</span><span class="sxs-lookup"><span data-stu-id="5be92-175">Yes.</span></span> <span data-ttu-id="5be92-176">Po ustawieniu hello odwrotnej właściwości DNS dla usługi Azure, Azure zarządza wszystkie delegowania DNS hello i wymagane stref DNS rozpoznaje tooensure, który wstecznego rekordu DNS dla wszystkich użytkowników Internetu.</span><span class="sxs-lookup"><span data-stu-id="5be92-176">Once you set hello reverse DNS property for your Azure service, Azure manages all hello DNS delegations and DNS zones required tooensure that reverse DNS record resolves for all Internet users.</span></span>

### <a name="are-default-reverse-dns-records-created-for-my-azure-services"></a><span data-ttu-id="5be92-177">Domyślne odwrotnej rekordy DNS są tworzone dla moich usług platformy Azure?</span><span class="sxs-lookup"><span data-stu-id="5be92-177">Are default reverse DNS records created for my Azure services?</span></span>

<span data-ttu-id="5be92-178">Nie.</span><span class="sxs-lookup"><span data-stu-id="5be92-178">No.</span></span> <span data-ttu-id="5be92-179">Wstecznego DNS jest funkcji opcjonalnych.</span><span class="sxs-lookup"><span data-stu-id="5be92-179">Reverse DNS is an opt-in feature.</span></span> <span data-ttu-id="5be92-180">Brak wartości domyślnej odwrotnej rekordy DNS są tworzone, jeśli wybierzesz nie tooconfigure je.</span><span class="sxs-lookup"><span data-stu-id="5be92-180">No default reverse DNS records are created if you choose not tooconfigure them.</span></span>

### <a name="what-is-hello-format-for-hello-fully-qualified-domain-name-fqdn"></a><span data-ttu-id="5be92-181">Co to jest format hello hello pełni kwalifikowaną nazwą domeny (FQDN)?</span><span class="sxs-lookup"><span data-stu-id="5be92-181">What is hello format for hello fully-qualified domain name (FQDN)?</span></span>

<span data-ttu-id="5be92-182">Nazwy FQDN są określone w kolejności do przodu, a musi być zakończona kropką (na przykład "app1.contoso.com.").</span><span class="sxs-lookup"><span data-stu-id="5be92-182">FQDNs are specified in forward order, and must be terminated by a dot (for example, "app1.contoso.com.").</span></span>

### <a name="what-happens-if-hello-validation-check-for-hello-reverse-dns-ive-specified-fails"></a><span data-ttu-id="5be92-183">Co się stanie, jeśli hello weryfikację hello wstecznego DNS I wybranymi zakończy się niepowodzeniem?</span><span class="sxs-lookup"><span data-stu-id="5be92-183">What happens if hello validation check for hello reverse DNS I've specified fails?</span></span>

<span data-ttu-id="5be92-184">W przypadku, gdy hello wstecznego DNS weryfikacji sprawdzenie nie powiedzie się, hello operacji tooconfigure hello wstecznego rekord DNS nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="5be92-184">Where hello reverse DNS validation check fails, hello operation tooconfigure hello reverse DNS record fails.</span></span> <span data-ttu-id="5be92-185">Popraw wartość wstecznego DNS hello zgodnie z wymaganiami i spróbuj ponownie.</span><span class="sxs-lookup"><span data-stu-id="5be92-185">Correct hello reverse DNS value as required, and retry.</span></span>

### <a name="can-i-configure-reverse-dns-for-azure-app-service"></a><span data-ttu-id="5be92-186">Można skonfigurować wstecznego DNS dla usługi Azure App Service?</span><span class="sxs-lookup"><span data-stu-id="5be92-186">Can I configure reverse DNS for Azure App Service?</span></span>

<span data-ttu-id="5be92-187">Nie.</span><span class="sxs-lookup"><span data-stu-id="5be92-187">No.</span></span> <span data-ttu-id="5be92-188">Wstecznego DNS nie jest obsługiwana dla hello Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="5be92-188">Reverse DNS is not supported for hello Azure App Service.</span></span>

### <a name="can-i-configure-multiple-reverse-dns-records-for-my-azure-service"></a><span data-ttu-id="5be92-189">Moje usługi Azure można skonfigurować wiele rekordów DNS odwrotnej?</span><span class="sxs-lookup"><span data-stu-id="5be92-189">Can I configure multiple reverse DNS records for my Azure service?</span></span>

<span data-ttu-id="5be92-190">Nie.</span><span class="sxs-lookup"><span data-stu-id="5be92-190">No.</span></span> <span data-ttu-id="5be92-191">Azure obsługuje odwrotnej pojedynczego rekordu DNS dla każdej usługi w chmurze Azure lub publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="5be92-191">Azure supports a single reverse DNS record for each Azure Cloud Service or PublicIpAddress.</span></span>

### <a name="can-i-configure-reverse-dns-for-ipv6-publicipaddress-resources"></a><span data-ttu-id="5be92-192">Można skonfigurować wstecznego DNS dla zasobów publicznego adresu IP protokołu IPv6?</span><span class="sxs-lookup"><span data-stu-id="5be92-192">Can I configure reverse DNS for IPv6 PublicIpAddress resources?</span></span>

<span data-ttu-id="5be92-193">Nie.</span><span class="sxs-lookup"><span data-stu-id="5be92-193">No.</span></span> <span data-ttu-id="5be92-194">Azure obecnie obsługuje reverse DNS tylko dla zasobów IPv4 publicznego adresu IP i usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="5be92-194">Azure currently supports reverse DNS only for IPv4 PublicIpAddress resources and Cloud Services.</span></span>

### <a name="can-i-send-emails-tooexternal-domains-from-my-azure-compute-services"></a><span data-ttu-id="5be92-195">Można wysyłać wiadomości e-mail tooexternal domen z mojej usług rozwiązań usługi obliczenia Azure?</span><span class="sxs-lookup"><span data-stu-id="5be92-195">Can I send emails tooexternal domains from my Azure Compute services?</span></span>

<span data-ttu-id="5be92-196">Nie.</span><span class="sxs-lookup"><span data-stu-id="5be92-196">No.</span></span> [<span data-ttu-id="5be92-197">Usługi obliczeniowe systemu Azure nie obsługują wysyłania wiadomości e-mail tooexternal domen</span><span class="sxs-lookup"><span data-stu-id="5be92-197">Azure Compute services do not support sending emails tooexternal domains</span></span>](https://blogs.msdn.microsoft.com/mast/2016/04/04/sending-e-mail-from-azure-compute-resource-to-external-domains/)

## <a name="next-steps"></a><span data-ttu-id="5be92-198">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5be92-198">Next steps</span></span>

<span data-ttu-id="5be92-199">Aby uzyskać więcej informacji dotyczących wstecznego DNS, zobacz [istnienia wstecznego wyszukiwania DNS dla Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span><span class="sxs-lookup"><span data-stu-id="5be92-199">For more information on reverse DNS, see [reverse DNS lookup on Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span></span>
<br>
<span data-ttu-id="5be92-200">Dowiedz się, jak za[strefy wyszukiwania wstecznego hello hosta zakres IP przypisany usługodawcy internetowego w usłudze Azure DNS](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="5be92-200">Learn how too[host hello reverse lookup zone for your ISP-assigned IP range in Azure DNS](dns-reverse-dns-for-azure-services.md).</span></span>

