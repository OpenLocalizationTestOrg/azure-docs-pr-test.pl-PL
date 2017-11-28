---
title: "aaaAzure zarządzanych aplikacji VirtualNetworkCombo elementu interfejsu użytkownika | Dokumentacja firmy Microsoft"
description: "Opisuje hello elementu Microsoft.Network.VirtualNetworkCombo interfejsu użytkownika dla aplikacji Azure"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/12/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: 1b0fa5360d93306f7a814723f77e42540bdaaa9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftnetworkvirtualnetworkcombo-ui-element"></a><span data-ttu-id="ba13b-103">Element Microsoft.Network.VirtualNetworkCombo interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="ba13b-103">Microsoft.Network.VirtualNetworkCombo UI element</span></span>
<span data-ttu-id="ba13b-104">Grupa służy do wybierania nowej lub istniejącej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ba13b-104">A group of controls for selecting a new or existing virtual network.</span></span> <span data-ttu-id="ba13b-105">Użyj tego elementu po [tworzenie aplikacji zarządzanych Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="ba13b-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="ba13b-106">Przykład interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="ba13b-106">UI sample</span></span>
![Microsoft.Network.VirtualNetworkCombo](./media/managed-application-elements/microsoft.network.virtualnetworkcombo.png)

- <span data-ttu-id="ba13b-108">W górnym szkielet hello hello użytkownika pobrał nowej sieci wirtualnej, więc hello użytkownik może dostosować prefiks nazwy i adresu każdej podsieci.</span><span class="sxs-lookup"><span data-stu-id="ba13b-108">In hello top wireframe, hello user has picked a new virtual network, so hello user can customize each subnet's name and address prefix.</span></span> <span data-ttu-id="ba13b-109">W takim przypadku Konfigurowanie podsieci jest opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="ba13b-109">Configuring subnets in this case is optional.</span></span>
- <span data-ttu-id="ba13b-110">W szkielet dolnej hello hello użytkownik pobrał istniejącej sieci wirtualnej, więc hello użytkownika musi być zamapowany każdego szablonu wdrożenia hello podsieci wymaga tooan istniejącą podsieć.</span><span class="sxs-lookup"><span data-stu-id="ba13b-110">In hello bottom wireframe, hello user has picked an existing virtual network, so hello user must map each subnet hello deployment template requires tooan existing subnet.</span></span> <span data-ttu-id="ba13b-111">W takim przypadku Konfigurowanie podsieci jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="ba13b-111">Configuring subnets in this case is required.</span></span>

## <a name="schema"></a><span data-ttu-id="ba13b-112">Schemat</span><span class="sxs-lookup"><span data-stu-id="ba13b-112">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Network.VirtualNetworkCombo",
  "label": {
    "virtualNetwork": "Virtual network",
    "subnets": "Subnets"
  },
  "toolTip": {
    "virtualNetwork": "",
    "subnets": ""
  },
  "defaultValue": {
    "name": "vnet01",
    "addressPrefixSize": "/16"
  },
  "constraints": {
    "minAddressPrefixSize": "/16"
  },
  "options": {
    "hideExisting": false
  },
  "subnets": {
    "subnet1": {
      "label": "First subnet",
      "defaultValue": {
        "name": "subnet-1",
        "addressPrefixSize": "/24"
      },
      "constraints": {
        "minAddressPrefixSize": "/24",
        "minAddressCount": 12,
        "requireContiguousAddresses": true
      }
    },
    "subnet2": {
      "label": "Second subnet",
      "defaultValue": {
        "name": "subnet-2",
        "addressPrefixSize": "/26"
      },
      "constraints": {
        "minAddressPrefixSize": "/26",
        "minAddressCount": 8,
        "requireContiguousAddresses": true
      }
    }
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="ba13b-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="ba13b-113">Remarks</span></span>
- <span data-ttu-id="ba13b-114">Jeśli zostanie określona, hello pierwszy nienakładający prefiksu adresu rozmiar `defaultValue.addressPrefixSize` jest określane automatycznie w oparciu o istniejących sieci wirtualnych w subskrypcji hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ba13b-114">If specified, hello first non-overlapping address prefix of size `defaultValue.addressPrefixSize` is determined automatically based on the existing virtual networks in hello user's subscription.</span></span>
- <span data-ttu-id="ba13b-115">Witaj wartości domyślnej dla `defaultValue.name` i `defaultValue.addressPrefixSize` jest **null**.</span><span class="sxs-lookup"><span data-stu-id="ba13b-115">hello default value for `defaultValue.name` and `defaultValue.addressPrefixSize` is **null**.</span></span>
- <span data-ttu-id="ba13b-116">`constraints.minAddressPrefixSize`musi być określona.</span><span class="sxs-lookup"><span data-stu-id="ba13b-116">`constraints.minAddressPrefixSize` must be specified.</span></span> <span data-ttu-id="ba13b-117">Wszystkie istniejące sieci wirtualne się na przestrzeń adresową mniejsze niż hello określona wartość jest niedostępna w przypadku zaznaczenia.</span><span class="sxs-lookup"><span data-stu-id="ba13b-117">Any existing virtual networks with an address space smaller than hello specified value are unavailable for selection.</span></span>
- <span data-ttu-id="ba13b-118">`subnets`musi być określona, i `constraints.minAddressPrefixSize` musi być określona dla każdej podsieci.</span><span class="sxs-lookup"><span data-stu-id="ba13b-118">`subnets` must be specified, and `constraints.minAddressPrefixSize` must be specified for each subnet.</span></span>
- <span data-ttu-id="ba13b-119">Podczas tworzenia nowej sieci wirtualnej, prefiks adresu w każdej podsieci jest obliczana automatycznie na podstawie prefiksów adresów sieci wirtualnej hello i odpowiednio `addressPrefixSize`.</span><span class="sxs-lookup"><span data-stu-id="ba13b-119">When creating a new virtual network, each subnet's address prefix is calculated automatically based on hello virtual network's address prefix and the respective `addressPrefixSize`.</span></span>
- <span data-ttu-id="ba13b-120">Podczas korzystania z istniejącej wirtualnych sieci, żadnych podsieci mniejsze niż odpowiednie `constraints.minAddressPrefixSize` nie są dostępne do wyboru.</span><span class="sxs-lookup"><span data-stu-id="ba13b-120">When using an existing virtual network, any subnets smaller than the respective `constraints.minAddressPrefixSize` are unavailable for selection.</span></span> <span data-ttu-id="ba13b-121">Ponadto jeśli jest określony, podsieci, które nie zawierają co najmniej `minAddressCount` dostępne adresy są niedostępne do wybrania.</span><span class="sxs-lookup"><span data-stu-id="ba13b-121">Additionally, if specified, subnets that do not contain at least `minAddressCount` available addresses are unavailable for selection.</span></span>
<span data-ttu-id="ba13b-122">Witaj, wartość domyślna to **0**.</span><span class="sxs-lookup"><span data-stu-id="ba13b-122">hello default value is **0**.</span></span> <span data-ttu-id="ba13b-123">tooensure, który hello dostępnych adresów są ciągłe, określ **true** dla `requireContiguousAddresses`.</span><span class="sxs-lookup"><span data-stu-id="ba13b-123">tooensure that hello available addresses are contiguous, specify **true** for `requireContiguousAddresses`.</span></span> <span data-ttu-id="ba13b-124">Witaj, wartość domyślna to **true**.</span><span class="sxs-lookup"><span data-stu-id="ba13b-124">hello default value is **true**.</span></span>
- <span data-ttu-id="ba13b-125">Tworzenie podsieci w istniejącej sieci wirtualnej nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="ba13b-125">Creating subnets in an existing virtual network is not supported.</span></span>
- <span data-ttu-id="ba13b-126">Jeśli `options.hideExisting` jest **true**, hello użytkownika nie można wybrać istniejącą sieć wirtualną.</span><span class="sxs-lookup"><span data-stu-id="ba13b-126">If `options.hideExisting` is **true**, hello user can't choose an existing virtual network.</span></span> <span data-ttu-id="ba13b-127">Witaj, wartość domyślna to **false**.</span><span class="sxs-lookup"><span data-stu-id="ba13b-127">hello default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="ba13b-128">Przykładowe dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="ba13b-128">Sample output</span></span>
```json
{
  "name": "vnet01",
  "resourceGroup": "rg01",
  "addressPrefixes": ["10.0.0.0/16"],
  "newOrExisting": "new",
  "subnets": {
    "subnet1": {
      "name": "subnet-1",
      "addressPrefix": "10.0.0.0/24",
      "startAddress": "10.0.0.1"
    },
    "subnet2": {
      "name": "subnet-2",
      "addressPrefix": "10.0.1.0/26",
      "startAddress": "10.0.1.1"
    }
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="ba13b-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ba13b-129">Next steps</span></span>
* <span data-ttu-id="ba13b-130">Wprowadzenie toomanaged aplikacji, zobacz [zarządzanej aplikacji Azure — omówienie](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ba13b-130">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="ba13b-131">Definicje interfejsu użytkownika toocreating wprowadzenie, zobacz [wprowadzenie CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ba13b-131">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="ba13b-132">Opis właściwości wspólnych elementów interfejsu użytkownika, zobacz [elementy CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="ba13b-132">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
