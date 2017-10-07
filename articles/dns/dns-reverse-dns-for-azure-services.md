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
# <a name="configure-reverse-dns-for-services-hosted-in-azure"></a>Skonfiguruj wstecznego DNS dla usługi hostowanej na platformie Azure

W tym artykule opisano, jak tooconfigure wstecznego wyszukiwania DNS dla usługi hostowanej na platformie Azure.

Usługi w usłudze Azure używać adresów IP przypisany przez usługę Azure i należących do firmy Microsoft. Te rekordy DNS odwrotnej (rekordów PTR) należy utworzyć w hello odpowiedniego należące do firmy Microsoft stref wyszukiwania wstecznego DNS wyszukiwania. W tym artykule opisano sposób toodo to.

W tym scenariuszu nie należy mylić z możliwością hello zbyt[hostowanie strefy hello do wyszukiwania wstecznego DNS dla przypisane zakresy IP w usłudze Azure DNS](dns-reverse-dns-hosting.md). W takim przypadku zakresów adresów IP hello reprezentowany przez strefy wyszukiwania wstecznego hello musi być przypisany organizacji tooyour zwykle przez Usługodawcę internetowego.

Przed przeczytaniem tego artykułu, należy się zapoznać z tym [omówienie wstecznego DNS i pomocy technicznej na platformie Azure](dns-reverse-dns-overview.md).

Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../azure-resource-manager/resource-manager-deployment-model.md).
* W modelu wdrażania usługi Resource Manager hello zasobów obliczeniowych (np. maszyny wirtualne, zestawy skalowania maszyny wirtualnej lub klastrów sieci szkieletowej usług) są udostępniane za pośrednictwem publicznego adresu IP zasobu. Wyszukiwania wstecznego DNS są skonfigurowane przy użyciu właściwości "ReverseFqdn" hello hello publicznego adresu IP.
* W hello klasycznego modelu wdrożenia zasoby obliczeniowe są widoczne, przy użyciu usługi w chmurze. Wyszukiwania wstecznego DNS są skonfigurowane przy użyciu właściwości "ReverseDnsFqdn" hello hello usługi w chmurze.

Wstecznego DNS nie jest obecnie obsługiwany dla hello Azure App Service.

## <a name="validation-of-reverse-dns-records"></a>Sprawdzanie poprawności odwrotnej rekordów DNS

Innej firmy nie może być możliwe toocreate odwrotnej rekordy DNS dla domeny DNS tooyour mapowanie usługi Azure. tooprevent, Azure umożliwia tylko tworzenie hello wstecznego rekord DNS, gdzie nazwa domeny określona w odwrotnej rekord DNS hello jest identyczny hello, lub jest rozpoznawana jako hello nazwę DNS lub adres IP publicznego adresu IP lub w chmurze usługi w hello sam subskrypcji platformy Azure.

To tylko weryfikacji hello wstecznego rekord DNS jest ustawiona lub modyfikacji. Okresowe ponowne sprawdzanie poprawności nie jest wykonywane.

Na przykład: Załóżmy, że hello publicznego adresu IP zasobu ma contosoapp1.northus.cloudapp.azure.com nazwy DNS hello i adres IP 23.96.52.53. Witaj ReverseFqdn dla powitalne publicznego adresu IP może być określona jako:
* Nazwa DNS Hello hello publicznego adresu IP, contosoapp1.northus.cloudapp.azure.com
* Hello nazwy DNS dla publicznego adresu IP innego w hello sam subskrypcję, taką jak contosoapp2.westus.cloudapp.azure.com
* Niestandardowych nazw DNS, takich jak app1.contoso.com, tak długo, jak ta nazwa jest *pierwszy* skonfigurowany jako CNAME toocontosoapp1.northus.cloudapp.azure.com lub tooa różnych publicznego adresu IP w hello tej samej subskrypcji.
* Niestandardowych nazw DNS, takich jak app1.contoso.com, tak długo, jak ta nazwa jest *pierwszy* skonfigurowany jako adres IP toohello rekordów A 23.96.52.53 lub adres IP toohello różnych publicznego adresu IP w hello tej samej subskrypcji.

Witaj takich samych ograniczeń zastosować tooreverse DNS dla usługi w chmurze.


## <a name="reverse-dns-for-publicipaddress-resources"></a>Reverse DNS dla zasobów publicznego adresu IP

Ta sekcja zawiera szczegółowe instrukcje dotyczące sposobu tooconfigure reverse DNS dla publicznego adresu IP zasobów w modelu wdrażania usługi Resource Manager hello przy użyciu programu Azure PowerShell, interfejsu wiersza polecenia platformy Azure w wersji 1.0 lub 2.0 interfejsu wiersza polecenia platformy Azure. Konfigurowanie wstecznego DNS dla zasobów publicznego adresu IP nie jest obecnie obsługiwane za pośrednictwem hello portalu Azure.

Azure obecnie obsługuje reverse DNS tylko dla zasobów IPv4 publicznego adresu IP. Nie jest obsługiwana w przypadku protokołu IPv6.

### <a name="add-reverse-dns-tooan-existing-publicipaddresses"></a>Dodaj odwrotnej tooan DNS istniejących elementów Publicipaddress

#### <a name="powershell"></a>PowerShell

tooadd reverse DNS tooan istniejącego publicznego adresu IP:

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

tooadd odwrotnej tooan DNS istniejącego publicznego adresu IP, który nie ma nazwy DNS, należy również określić nazwę DNS:

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings = New-Object -TypeName "Microsoft.Azure.Commands.Network.Models.PSPublicIpAddressDnsSettings"
$pip.DnsSettings.DomainNameLabel = "contosoapp1"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a>Interfejs wiersza polecenia platformy Azure CLI w wersji 1.0

tooadd reverse DNS tooan istniejącego publicznego adresu IP:

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -f contosoapp1.westus.cloudapp.azure.com.
```

tooadd odwrotnej tooan DNS istniejącego publicznego adresu IP, który nie ma nazwy DNS, należy również określić nazwę DNS:

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -d contosoapp1 -f contosoapp1.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a>Interfejs wiersza polecenia platformy Azure 2.0

tooadd reverse DNS tooan istniejącego publicznego adresu IP:

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com.
```

tooadd odwrotnej tooan DNS istniejącego publicznego adresu IP, który nie ma nazwy DNS, należy również określić nazwę DNS:

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com --dns-name contosoapp1
```

### <a name="create-a-public-ip-address-with-reverse-dns"></a>Utwórz publiczny adres IP z wstecznego DNS

toocreate nowego publicznego adresu IP z hello wstecznego DNS we właściwości już określony:

#### <a name="powershell"></a>PowerShell

```powershell
New-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup" -Location "WestUS" -AllocationMethod Dynamic -DomainNameLabel "contosoapp2" -ReverseFqdn "contosoapp2.westus.cloudapp.azure.com."
```

#### <a name="azure-cli-10"></a>Interfejs wiersza polecenia platformy Azure CLI w wersji 1.0

```azurecli
azure network public-ip create -n PublicIp -g MyResourceGroup -l westus -d contosoapp3 -f contosoapp3.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a>Interfejs wiersza polecenia platformy Azure 2.0

```azurecli
az network public-ip create --name PublicIp --resource-group MyResourceGroup --location westcentralus --dns-name contosoapp1 --reverse-fqdn contosoapp1.westcentralus.cloudapp.azure.com
```

### <a name="view-reverse-dns-for-an-existing-publicipaddress"></a>Widok wstecznego DNS dla istniejącego publicznego adresu IP

Witaj tooview wartość skonfigurowana dla istniejącego publicznego adresu IP:

#### <a name="powershell"></a>PowerShell

```powershell
Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
```

#### <a name="azure-cli-10"></a>Interfejs wiersza polecenia platformy Azure CLI w wersji 1.0

```azurecli
azure network public-ip show -n PublicIp -g MyResourceGroup
```

#### <a name="azure-cli-20"></a>Interfejs wiersza polecenia platformy Azure 2.0

```azurecli
az network public-ip show --name PublicIp --resource-group MyResourceGroup
```

### <a name="remove-reverse-dns-from-existing-public-ip-addresses"></a>Usuń wstecznego DNS z istniejących publicznych adresów IP

tooremove odwrotnej właściwości DNS z istniejącego publicznego adresu IP:

#### <a name="powershell"></a>PowerShell

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = ""
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a>Interfejs wiersza polecenia platformy Azure CLI w wersji 1.0

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup –f ""
```

#### <a name="azure-cli-20"></a>Interfejs wiersza polecenia platformy Azure 2.0

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn ""
```


## <a name="configure-reverse-dns-for-cloud-services"></a>Konfigurowanie wstecznego DNS dla usługi w chmurze

Ta sekcja zawiera szczegółowe instrukcje dotyczące sposobu tooconfigure reverse DNS dla usługi w chmurze w klasycznym modelu wdrażania hello, przy użyciu programu Azure PowerShell. Nie jest obsługiwane Konfigurowanie wstecznego DNS dla usługi w chmurze za pośrednictwem hello portalu Azure, Azure CLI w wersji 1.0 lub 2.0 interfejsu wiersza polecenia platformy Azure.

### <a name="add-reverse-dns-tooexisting-cloud-services"></a>Dodawanie usługi w chmurze tooexisting wstecznego DNS

tooadd tooan odwrotnej rekordów DNS, istniejące usługi w chmurze:

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="create-a-cloud-service-with-reverse-dns"></a>Tworzenie usługi w chmurze z wstecznego DNS

toocreate nową usługę w chmurze z hello wstecznego DNS we właściwości już określony:

```powershell
New-AzureService –ServiceName "contosoapp1" –Location "West US" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="view-reverse-dns-for-existing-cloud-services"></a>Widok wstecznego DNS dla istniejącej usługi w chmurze

Witaj tooview reverse DNS we właściwości dla istniejącej usługi w chmurze:

```powershell
Get-AzureService "contosoapp1"
```

### <a name="remove-reverse-dns-from-existing-cloud-services"></a>Usuń wstecznego DNS z istniejącej usługi w chmurze

tooremove wstecznego DNS właściwości z istniejącej usługi w chmurze:

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn ""
```

## <a name="faq"></a>Często zadawane pytania

### <a name="how-much-do-reverse-dns-records-cost"></a>Ile wstecznego koszt rekordy DNS?

Są one wolnego!  Nie ma żadnych dodatkowych kosztów odwrotnej rekordów DNS lub zapytania.

### <a name="will-my-reverse-dns-records-resolve-from-hello-internet"></a>Moje odwrotnej rozpoznania rekordów DNS z będzie hello internet?

Tak. Po ustawieniu hello odwrotnej właściwości DNS dla usługi Azure, Azure zarządza wszystkie delegowania DNS hello i wymagane stref DNS rozpoznaje tooensure, który wstecznego rekordu DNS dla wszystkich użytkowników Internetu.

### <a name="are-default-reverse-dns-records-created-for-my-azure-services"></a>Domyślne odwrotnej rekordy DNS są tworzone dla moich usług platformy Azure?

Nie. Wstecznego DNS jest funkcji opcjonalnych. Brak wartości domyślnej odwrotnej rekordy DNS są tworzone, jeśli wybierzesz nie tooconfigure je.

### <a name="what-is-hello-format-for-hello-fully-qualified-domain-name-fqdn"></a>Co to jest format hello hello pełni kwalifikowaną nazwą domeny (FQDN)?

Nazwy FQDN są określone w kolejności do przodu, a musi być zakończona kropką (na przykład "app1.contoso.com.").

### <a name="what-happens-if-hello-validation-check-for-hello-reverse-dns-ive-specified-fails"></a>Co się stanie, jeśli hello weryfikację hello wstecznego DNS I wybranymi zakończy się niepowodzeniem?

W przypadku, gdy hello wstecznego DNS weryfikacji sprawdzenie nie powiedzie się, hello operacji tooconfigure hello wstecznego rekord DNS nie powiedzie się. Popraw wartość wstecznego DNS hello zgodnie z wymaganiami i spróbuj ponownie.

### <a name="can-i-configure-reverse-dns-for-azure-app-service"></a>Można skonfigurować wstecznego DNS dla usługi Azure App Service?

Nie. Wstecznego DNS nie jest obsługiwana dla hello Azure App Service.

### <a name="can-i-configure-multiple-reverse-dns-records-for-my-azure-service"></a>Moje usługi Azure można skonfigurować wiele rekordów DNS odwrotnej?

Nie. Azure obsługuje odwrotnej pojedynczego rekordu DNS dla każdej usługi w chmurze Azure lub publicznego adresu IP.

### <a name="can-i-configure-reverse-dns-for-ipv6-publicipaddress-resources"></a>Można skonfigurować wstecznego DNS dla zasobów publicznego adresu IP protokołu IPv6?

Nie. Azure obecnie obsługuje reverse DNS tylko dla zasobów IPv4 publicznego adresu IP i usługi w chmurze.

### <a name="can-i-send-emails-tooexternal-domains-from-my-azure-compute-services"></a>Można wysyłać wiadomości e-mail tooexternal domen z mojej usług rozwiązań usługi obliczenia Azure?

Nie. [Usługi obliczeniowe systemu Azure nie obsługują wysyłania wiadomości e-mail tooexternal domen](https://blogs.msdn.microsoft.com/mast/2016/04/04/sending-e-mail-from-azure-compute-resource-to-external-domains/)

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji dotyczących wstecznego DNS, zobacz [istnienia wstecznego wyszukiwania DNS dla Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).
<br>
Dowiedz się, jak za[strefy wyszukiwania wstecznego hello hosta zakres IP przypisany usługodawcy internetowego w usłudze Azure DNS](dns-reverse-dns-for-azure-services.md).

