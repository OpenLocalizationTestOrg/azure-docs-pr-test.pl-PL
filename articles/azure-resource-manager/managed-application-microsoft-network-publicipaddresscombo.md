---
title: "Azure zarządzanych aplikacji PublicIpAddressCombo elementu interfejsu użytkownika | Dokumentacja firmy Microsoft"
description: "Opis elementu Microsoft.Network.PublicIpAddressCombo interfejsu użytkownika dla aplikacji Azure"
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
ms.openlocfilehash: 2eb773f5f0cf389fc39bc3a0f5fbf9ac726d1949
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftnetworkpublicipaddresscombo-ui-element"></a><span data-ttu-id="8dfaf-103">Element Microsoft.Network.PublicIpAddressCombo interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="8dfaf-103">Microsoft.Network.PublicIpAddressCombo UI element</span></span>
<span data-ttu-id="8dfaf-104">Grupa służy do wybierania nowego lub istniejącego publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="8dfaf-104">A group of controls for selecting a new or existing public IP address.</span></span> <span data-ttu-id="8dfaf-105">Użyj tego elementu po [tworzenie aplikacji zarządzanych Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="8dfaf-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="8dfaf-106">Przykład interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="8dfaf-106">UI sample</span></span>
![Microsoft.Network.PublicIpAddressCombo](./media/managed-application-elements/microsoft.network.publicipaddresscombo.png)

- <span data-ttu-id="8dfaf-108">Jeśli użytkownik wybierze opcję "Brak" publicznego adresu IP, pole tekstowe etykieta nazwy domeny jest ukryty.</span><span class="sxs-lookup"><span data-stu-id="8dfaf-108">If the user selects 'None' for public IP address, the domain name label text box is hidden.</span></span>
- <span data-ttu-id="8dfaf-109">Jeśli użytkownik wybierze istniejącego publicznego adresu IP, pole tekstowe etykieta nazwy domeny jest wyłączone.</span><span class="sxs-lookup"><span data-stu-id="8dfaf-109">If the user selects an existing public IP address, the domain name label text box is disabled.</span></span> <span data-ttu-id="8dfaf-110">Wartość jest etykieta nazwy domeny wybranego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="8dfaf-110">Its value is the domain name label of the selected IP address.</span></span>
- <span data-ttu-id="8dfaf-111">Aktualizacje sufiks (na przykład westus.cloudapp.azure.com) nazwa domeny automatycznie na podstawie wybranej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="8dfaf-111">The domain name suffix (for example, westus.cloudapp.azure.com) updates automatically based on the selected location.</span></span>

## <a name="schema"></a><span data-ttu-id="8dfaf-112">Schemat</span><span class="sxs-lookup"><span data-stu-id="8dfaf-112">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Network.PublicIpAddressCombo",
  "label": {
    "publicIpAddress": "Public IP address",
    "domainNameLabel": "Domain name label"
  },
  "toolTip": {
    "publicIpAddress": "",
    "domainNameLabel": ""
  },
  "defaultValue": {
    "publicIpAddressName": "ip01",
    "domainNameLabel": "foobar"
  },
  "constraints": {
    "required": {
      "domainNameLabel": true
    }
  },
  "options": {
    "hideNone": false,
    "hideDomainNameLabel": false,
    "hideExisting": false
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="8dfaf-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="8dfaf-113">Remarks</span></span>
- <span data-ttu-id="8dfaf-114">Jeśli `constraints.required.domainNameLabel` ustawiono **true**, użytkownik musi podać etykieta nazwy domeny, podczas tworzenia nowego publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="8dfaf-114">If `constraints.required.domainNameLabel` is set to **true**, the user must provide a domain name label when creating a new public IP address.</span></span> <span data-ttu-id="8dfaf-115">Istniejącego publicznego adresu IP, adresy bez etykiety nie są dostępne do wyboru.</span><span class="sxs-lookup"><span data-stu-id="8dfaf-115">Existing public IP addresses without a label are not available for selection.</span></span>
- <span data-ttu-id="8dfaf-116">Jeśli `options.hideNone` ustawiono **true**, następnie wybrać opcję **Brak** publicznego adresu IP adres jest ukryty.</span><span class="sxs-lookup"><span data-stu-id="8dfaf-116">If `options.hideNone` is set to **true**, then the option to select **None** for the public IP address is hidden.</span></span> <span data-ttu-id="8dfaf-117">Wartość domyślna to **false**.</span><span class="sxs-lookup"><span data-stu-id="8dfaf-117">The default value is **false**.</span></span>
- <span data-ttu-id="8dfaf-118">Jeśli `options.hideDomainNameLabel` ustawiono **true**, a następnie w polu tekstowym dla etykiety nazwy domeny jest ukryty.</span><span class="sxs-lookup"><span data-stu-id="8dfaf-118">If `options.hideDomainNameLabel` is set to **true**, then the text box for domain name label is hidden.</span></span> <span data-ttu-id="8dfaf-119">Wartość domyślna to **false**.</span><span class="sxs-lookup"><span data-stu-id="8dfaf-119">The default value is **false**.</span></span>
- <span data-ttu-id="8dfaf-120">Jeśli `options.hideExisting` ma wartość true, a następnie użytkownik nie będzie mógł wybrać istniejącego publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="8dfaf-120">If `options.hideExisting` is true, then the user is not able to choose an existing public IP address.</span></span> <span data-ttu-id="8dfaf-121">Wartość domyślna to **false**.</span><span class="sxs-lookup"><span data-stu-id="8dfaf-121">The default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="8dfaf-122">Przykładowe dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="8dfaf-122">Sample output</span></span>
<span data-ttu-id="8dfaf-123">Jeśli użytkownik wybierze żadnego publicznego adresu IP, oczekiwano następujące dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="8dfaf-123">If the user selects no public IP address, the following output is expected:</span></span>
```json
{
  "newOrExistingOrNone": "none"
}
```

<span data-ttu-id="8dfaf-124">Jeśli użytkownik wybierze nowy lub istniejący adres IP, oczekiwano następujące dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="8dfaf-124">If the user selects a new or existing IP address, the following output is expected:</span></span>
```json
{
  "name": "ip01",
  "resourceGroup": "rg01",
  "domainNameLabel": "foobar",
  "newOrExistingOrNone": "new"
}
```
- <span data-ttu-id="8dfaf-125">Gdy `options.hideNone` jest określony, `newOrExistingOrNone` zawsze zwraca **Brak**.</span><span class="sxs-lookup"><span data-stu-id="8dfaf-125">When `options.hideNone` is specified, `newOrExistingOrNone` always returns **none**.</span></span>
- <span data-ttu-id="8dfaf-126">Gdy `options.hideDomainNameLabel` jest określony, `domainNameLabel` jest niezadeklarowany.</span><span class="sxs-lookup"><span data-stu-id="8dfaf-126">When `options.hideDomainNameLabel` is specified, `domainNameLabel` is undeclared.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8dfaf-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8dfaf-127">Next steps</span></span>
* <span data-ttu-id="8dfaf-128">Aby obejrzeć wprowadzenie do aplikacji zarządzanych, zobacz [zarządzanej aplikacji Azure — omówienie](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8dfaf-128">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="8dfaf-129">Aby obejrzeć wprowadzenie do tworzenia definicji interfejsu użytkownika, zobacz [wprowadzenie CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8dfaf-129">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="8dfaf-130">Opis właściwości wspólnych elementów interfejsu użytkownika, zobacz [elementy CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="8dfaf-130">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
