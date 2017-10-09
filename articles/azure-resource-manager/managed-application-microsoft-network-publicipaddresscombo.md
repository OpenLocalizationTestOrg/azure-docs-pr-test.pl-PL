---
title: "aaaAzure zarządzanych aplikacji PublicIpAddressCombo elementu interfejsu użytkownika | Dokumentacja firmy Microsoft"
description: "Opisuje hello elementu Microsoft.Network.PublicIpAddressCombo interfejsu użytkownika dla aplikacji Azure"
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
ms.openlocfilehash: 8ba689005c0eccda0a57bf628de4b5197886a950
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftnetworkpublicipaddresscombo-ui-element"></a><span data-ttu-id="6d6c9-103">Element Microsoft.Network.PublicIpAddressCombo interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="6d6c9-103">Microsoft.Network.PublicIpAddressCombo UI element</span></span>
<span data-ttu-id="6d6c9-104">Grupa służy do wybierania nowego lub istniejącego publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="6d6c9-104">A group of controls for selecting a new or existing public IP address.</span></span> <span data-ttu-id="6d6c9-105">Użyj tego elementu po [tworzenie aplikacji zarządzanych Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="6d6c9-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="6d6c9-106">Przykład interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="6d6c9-106">UI sample</span></span>
![Microsoft.Network.PublicIpAddressCombo](./media/managed-application-elements/microsoft.network.publicipaddresscombo.png)

- <span data-ttu-id="6d6c9-108">Jeśli użytkownik hello wybiera 'Brak' publicznego adresu IP, pole tekstowe etykieta nazwy domeny hello jest ukryty.</span><span class="sxs-lookup"><span data-stu-id="6d6c9-108">If hello user selects 'None' for public IP address, hello domain name label text box is hidden.</span></span>
- <span data-ttu-id="6d6c9-109">Jeśli użytkownik hello wybiera istniejącego publicznego adresu IP, pole tekstowe etykieta nazwy domeny hello jest wyłączone.</span><span class="sxs-lookup"><span data-stu-id="6d6c9-109">If hello user selects an existing public IP address, hello domain name label text box is disabled.</span></span> <span data-ttu-id="6d6c9-110">Jego wartość wynosi hello etykieta nazwy domeny adresu IP hello wybrane.</span><span class="sxs-lookup"><span data-stu-id="6d6c9-110">Its value is hello domain name label of hello selected IP address.</span></span>
- <span data-ttu-id="6d6c9-111">Witaj aktualizacje sufiks (na przykład westus.cloudapp.azure.com) nazwa domeny automatycznie na podstawie hello wybrane lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="6d6c9-111">hello domain name suffix (for example, westus.cloudapp.azure.com) updates automatically based on hello selected location.</span></span>

## <a name="schema"></a><span data-ttu-id="6d6c9-112">Schemat</span><span class="sxs-lookup"><span data-stu-id="6d6c9-112">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="6d6c9-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="6d6c9-113">Remarks</span></span>
- <span data-ttu-id="6d6c9-114">Jeśli `constraints.required.domainNameLabel` ustawiono zbyt**true**, hello użytkownik musi podać etykieta nazwy domeny, podczas tworzenia nowego publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="6d6c9-114">If `constraints.required.domainNameLabel` is set too**true**, hello user must provide a domain name label when creating a new public IP address.</span></span> <span data-ttu-id="6d6c9-115">Istniejącego publicznego adresu IP, adresy bez etykiety nie są dostępne do wyboru.</span><span class="sxs-lookup"><span data-stu-id="6d6c9-115">Existing public IP addresses without a label are not available for selection.</span></span>
- <span data-ttu-id="6d6c9-116">Jeśli `options.hideNone` ustawiono zbyt**true**, następnie hello tooselect opcji **Brak** hello publicznego adresu IP adres jest ukryty.</span><span class="sxs-lookup"><span data-stu-id="6d6c9-116">If `options.hideNone` is set too**true**, then hello option tooselect **None** for hello public IP address is hidden.</span></span> <span data-ttu-id="6d6c9-117">Witaj, wartość domyślna to **false**.</span><span class="sxs-lookup"><span data-stu-id="6d6c9-117">hello default value is **false**.</span></span>
- <span data-ttu-id="6d6c9-118">Jeśli `options.hideDomainNameLabel` ustawiono zbyt**true**, a następnie ukryte pole tekstowe hello etykieta nazwy domeny.</span><span class="sxs-lookup"><span data-stu-id="6d6c9-118">If `options.hideDomainNameLabel` is set too**true**, then hello text box for domain name label is hidden.</span></span> <span data-ttu-id="6d6c9-119">Witaj, wartość domyślna to **false**.</span><span class="sxs-lookup"><span data-stu-id="6d6c9-119">hello default value is **false**.</span></span>
- <span data-ttu-id="6d6c9-120">Jeśli `options.hideExisting` ma wartość true, a następnie hello użytkownik nie jest możliwe toochoose istniejącego publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="6d6c9-120">If `options.hideExisting` is true, then hello user is not able toochoose an existing public IP address.</span></span> <span data-ttu-id="6d6c9-121">Witaj, wartość domyślna to **false**.</span><span class="sxs-lookup"><span data-stu-id="6d6c9-121">hello default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="6d6c9-122">Przykładowe dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="6d6c9-122">Sample output</span></span>
<span data-ttu-id="6d6c9-123">Jeśli użytkownik hello wybiera żadnego publicznego adresu IP, hello następujące dane wyjściowe Oczekiwano:</span><span class="sxs-lookup"><span data-stu-id="6d6c9-123">If hello user selects no public IP address, hello following output is expected:</span></span>
```json
{
  "newOrExistingOrNone": "none"
}
```

<span data-ttu-id="6d6c9-124">Jeśli użytkownik hello wybiera nowy lub istniejący adres IP, hello następujące dane wyjściowe Oczekiwano:</span><span class="sxs-lookup"><span data-stu-id="6d6c9-124">If hello user selects a new or existing IP address, hello following output is expected:</span></span>
```json
{
  "name": "ip01",
  "resourceGroup": "rg01",
  "domainNameLabel": "foobar",
  "newOrExistingOrNone": "new"
}
```
- <span data-ttu-id="6d6c9-125">Gdy `options.hideNone` jest określony, `newOrExistingOrNone` zawsze zwraca **Brak**.</span><span class="sxs-lookup"><span data-stu-id="6d6c9-125">When `options.hideNone` is specified, `newOrExistingOrNone` always returns **none**.</span></span>
- <span data-ttu-id="6d6c9-126">Gdy `options.hideDomainNameLabel` jest określony, `domainNameLabel` jest niezadeklarowany.</span><span class="sxs-lookup"><span data-stu-id="6d6c9-126">When `options.hideDomainNameLabel` is specified, `domainNameLabel` is undeclared.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d6c9-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6d6c9-127">Next steps</span></span>
* <span data-ttu-id="6d6c9-128">Wprowadzenie toomanaged aplikacji, zobacz [zarządzanej aplikacji Azure — omówienie](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6d6c9-128">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="6d6c9-129">Definicje interfejsu użytkownika toocreating wprowadzenie, zobacz [wprowadzenie CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6d6c9-129">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="6d6c9-130">Opis właściwości wspólnych elementów interfejsu użytkownika, zobacz [elementy CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="6d6c9-130">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
