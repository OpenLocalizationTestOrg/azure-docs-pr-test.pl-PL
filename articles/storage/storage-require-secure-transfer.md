---
title: "Wymaga zapewnienia bezpiecznego transferu w usłudze Azure Storage | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat funkcji \"Wymaga zapewnienia bezpiecznego transferu\" dla usługi Azure Storage i jak je włączyć."
services: storage
documentationcenter: na
author: fhryo-msft
manager: Jason.Hogg
editor: fhryo-msft
ms.assetid: 
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 06/20/2017
ms.author: fryu
ms.openlocfilehash: bc5b7fc79869c632db96958f17aaf953a5fd3b19
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="require-secure-transfer"></a><span data-ttu-id="5ba98-103">Wymaganie bezpiecznego transferu</span><span class="sxs-lookup"><span data-stu-id="5ba98-103">Require secure transfer</span></span>

<span data-ttu-id="5ba98-104">Opcja "Bezpieczny transfer wymagane" podnosi poziom bezpieczeństwa konta magazynu, zezwalając tylko żądania do konta magazynu z bezpiecznych połączeń.</span><span class="sxs-lookup"><span data-stu-id="5ba98-104">The "Secure transfer required" option enhances the security of your storage account by only allowing requests to the storage account from secure connections.</span></span> <span data-ttu-id="5ba98-105">Na przykład podczas wywoływania interfejsów API REST, aby uzyskać dostęp do konta magazynu, należy połączyć przy użyciu protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="5ba98-105">For example, when calling REST APIs to access your storage account, you must connect using HTTPS.</span></span> <span data-ttu-id="5ba98-106">Wszystkie żądania przy użyciu protokołu HTTP są odrzucane po włączeniu "Bezpieczny transfer wymagane".</span><span class="sxs-lookup"><span data-stu-id="5ba98-106">Any requests using HTTP are rejected when "Secure transfer required" is enabled.</span></span>

<span data-ttu-id="5ba98-107">Usługa pliki Azure jest używana, każde połączenie bez szyfrowania nie powiedzie się po włączeniu "Bezpieczny transfer wymagane".</span><span class="sxs-lookup"><span data-stu-id="5ba98-107">When you are using the Azure Files service, any connection without encryption fails when "Secure transfer required" is enabled.</span></span> <span data-ttu-id="5ba98-108">W tym scenariuszy przy użyciu protokołu SMB 2.1, SMB 3.0 bez szyfrowania i niektórych odmian klient protokołu SMB w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="5ba98-108">This includes scenarios using SMB 2.1, SMB 3.0 without encryption, and some flavors of the Linux SMB client.</span></span> 

<span data-ttu-id="5ba98-109">Domyślnie opcja "Bezpieczny transfer wymagane" jest wyłączona.</span><span class="sxs-lookup"><span data-stu-id="5ba98-109">By default, the "Secure transfer required" option is disabled.</span></span>

> [!NOTE]
> <span data-ttu-id="5ba98-110">Ponieważ Magazyn Azure nie obsługuje protokołu HTTPS dla niestandardowych nazw domen, ta opcja nie została zastosowana podczas korzystania z niestandardowej nazwy domeny.</span><span class="sxs-lookup"><span data-stu-id="5ba98-110">Because Azure Storage doesn't support HTTPS for custom domain names, this option is not applied when using a custom domain name.</span></span>

## <a name="enable-secure-transfer-required-in-the-azure-portal"></a><span data-ttu-id="5ba98-111">Włącz "Bezpieczny transfer wymagane" w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="5ba98-111">Enable "Secure transfer required" in the Azure portal</span></span>

<span data-ttu-id="5ba98-112">Można włączyć "bezpieczny transfer wymagane" ustawienie zarówno podczas tworzenia konta magazynu w [portalu Azure](https://portal.azure.com), a w przypadku istniejących kont magazynu.</span><span class="sxs-lookup"><span data-stu-id="5ba98-112">You can enable the "Secure transfer required" setting both when you create a storage account in the [Azure portal](https://portal.azure.com), and for existing storage accounts.</span></span>

### <a name="require-secure-transfer-when-you-create-a-storage-account"></a><span data-ttu-id="5ba98-113">Wymaga zapewnienia bezpiecznego transferu podczas tworzenia konta magazynu</span><span class="sxs-lookup"><span data-stu-id="5ba98-113">Require secure transfer when you create a storage account</span></span>

1. <span data-ttu-id="5ba98-114">Otwórz **utworzyć konto magazynu** bloku w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="5ba98-114">Open the **Create storage account** blade in the Azure portal.</span></span>
1. <span data-ttu-id="5ba98-115">W obszarze **bezpieczny transfer wymagane**, wybierz pozycję **włączone**.</span><span class="sxs-lookup"><span data-stu-id="5ba98-115">Under **Secure transfer required**, select **Enabled**.</span></span>

  ![Zrzut ekranu](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_1.png)

### <a name="require-secure-transfer-for-an-existing-storage-account"></a><span data-ttu-id="5ba98-117">Wymaga zapewnienia bezpiecznego transferu do istniejącego konta magazynu</span><span class="sxs-lookup"><span data-stu-id="5ba98-117">Require secure transfer for an existing storage account</span></span>

1. <span data-ttu-id="5ba98-118">Wybierz istniejące konto magazynu w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="5ba98-118">Select an existing storage account in the Azure portal.</span></span>
1. <span data-ttu-id="5ba98-119">Wybierz **konfiguracji** w obszarze **ustawienia** w bloku menu konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="5ba98-119">Select **Configuration** under **SETTINGS** in the storage account menu blade.</span></span>
1. <span data-ttu-id="5ba98-120">W obszarze **bezpieczny transfer wymagane**, wybierz pozycję **włączone**.</span><span class="sxs-lookup"><span data-stu-id="5ba98-120">Under **Secure transfer required**, select **Enabled**.</span></span>

  ![Zrzut ekranu](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_2.png)

## <a name="enable-secure-transfer-required-programmatically"></a><span data-ttu-id="5ba98-122">Włącz "Bezpieczny transfer wymagane" programowo</span><span class="sxs-lookup"><span data-stu-id="5ba98-122">Enable "Secure transfer required" programmatically</span></span>

<span data-ttu-id="5ba98-123">Nazwa ustawienia to _supportsHttpsTrafficOnly_ we właściwościach konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="5ba98-123">The setting name is _supportsHttpsTrafficOnly_ in storage account properties.</span></span> <span data-ttu-id="5ba98-124">Można włączyć "Zapewnienia bezpiecznego transferu wymagane" Ustawianie za pomocą interfejsu API REST, narzędzi lub biblioteki:</span><span class="sxs-lookup"><span data-stu-id="5ba98-124">You can enable "Secure transfer required" setting with REST API, tools or libraries:</span></span>

* <span data-ttu-id="5ba98-125">**Interfejs API REST** (wersja: 2016-12-01): [wersji pakietu](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)</span><span class="sxs-lookup"><span data-stu-id="5ba98-125">**REST API** (Version: 2016-12-01): [release package](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)</span></span>
* <span data-ttu-id="5ba98-126">**PowerShell** (wersja: 4.1.0): [wersji pakietu](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)</span><span class="sxs-lookup"><span data-stu-id="5ba98-126">**PowerShell** (Version: 4.1.0): [release package](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)</span></span>
* <span data-ttu-id="5ba98-127">**Interfejs wiersza polecenia** (wersja: 2.0.11): [wersji pakietu](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)</span><span class="sxs-lookup"><span data-stu-id="5ba98-127">**CLI** (Version: 2.0.11): [release package](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)</span></span>
* <span data-ttu-id="5ba98-128">**NodeJS** (wersja: 1.1.0): [wersji pakietu](https://www.npmjs.com/package/azure-arm-storage/)</span><span class="sxs-lookup"><span data-stu-id="5ba98-128">**NodeJS** (Version: 1.1.0): [release package](https://www.npmjs.com/package/azure-arm-storage/)</span></span>
* <span data-ttu-id="5ba98-129">**Zestaw .NET SDK** (wersja: 6.3.0): [wersji pakietu](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)</span><span class="sxs-lookup"><span data-stu-id="5ba98-129">**.NET SDK** (Version: 6.3.0): [release package](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)</span></span>
* <span data-ttu-id="5ba98-130">**Zestaw SDK Python** (wersja: 1.1.0): [wersji pakietu](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)</span><span class="sxs-lookup"><span data-stu-id="5ba98-130">**Python SDK** (Version: 1.1.0): [release package](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)</span></span>
* <span data-ttu-id="5ba98-131">**Zestaw SDK dopisków fonetycznych** (wersja: 0.11.0): [wersji pakietu](https://rubygems.org/gems/azure_mgmt_storage)</span><span class="sxs-lookup"><span data-stu-id="5ba98-131">**Ruby SDK** (Version: 0.11.0): [release package](https://rubygems.org/gems/azure_mgmt_storage)</span></span>

### <a name="enable-secure-transfer-required-setting-with-rest-api"></a><span data-ttu-id="5ba98-132">Włącz "Zapewnienia bezpiecznego transferu wymagane" Ustawianie za pomocą interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="5ba98-132">Enable "Secure transfer required" setting with REST API</span></span>

<span data-ttu-id="5ba98-133">Aby ułatwić testowanie za pomocą interfejsu API REST, można użyć [ArmClient](https://github.com/projectkudu/ARMClient) wywoływanie z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="5ba98-133">To simplify testing with REST API, you can use [ArmClient](https://github.com/projectkudu/ARMClient) to call from command line.</span></span>

 <span data-ttu-id="5ba98-134">Aby sprawdzić ustawienie przy użyciu interfejsu API REST służy poniżej wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="5ba98-134">You can use below command line to check the setting with the REST API:</span></span>

```
# Login Azure and proceed with your credentials
> armclient login

> armclient GET  /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01
```

<span data-ttu-id="5ba98-135">W odpowiedzi, można znaleźć _supportsHttpsTrafficOnly_ ustawienie.</span><span class="sxs-lookup"><span data-stu-id="5ba98-135">In the response, you can find _supportsHttpsTrafficOnly_ setting.</span></span> <span data-ttu-id="5ba98-136">Przykład:</span><span class="sxs-lookup"><span data-stu-id="5ba98-136">Sample:</span></span>

```Json
{
  "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}",
  "kind": "Storage",
  ...
  "properties": {
    ...
    "supportsHttpsTrafficOnly": false
  },
  "type": "Microsoft.Storage/storageAccounts"
}
```

<span data-ttu-id="5ba98-137">Aby włączyć ustawienie przy użyciu interfejsu API REST służy poniżej wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="5ba98-137">You can use below command line to enable the setting with the REST API:</span></span>

```
# Login Azure and proceed with your credentials
> armclient login

> armclient PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01 < Input.json
```
<span data-ttu-id="5ba98-138">Przykład Input.json:</span><span class="sxs-lookup"><span data-stu-id="5ba98-138">Sample of Input.json:</span></span>
```Json
{
  "location": "westus",
  "properties": {
    "supportsHttpsTrafficOnly": true
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="5ba98-139">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5ba98-139">Next steps</span></span>
<span data-ttu-id="5ba98-140">Magazyn Azure oferuje rozbudowany zestaw funkcji zabezpieczeń, które razem umożliwiają deweloperom tworzenie bezpiecznych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5ba98-140">Azure Storage provides a comprehensive set of security capabilities, which together enable developers to build secure applications.</span></span> <span data-ttu-id="5ba98-141">Aby uzyskać więcej informacji, odwiedź stronę [przewodnik zabezpieczeń magazynu](storage-security-guide.md).</span><span class="sxs-lookup"><span data-stu-id="5ba98-141">For more details, visit the [Storage Security Guide](storage-security-guide.md).</span></span>
