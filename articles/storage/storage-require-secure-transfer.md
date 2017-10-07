---
title: "zapewnienia bezpiecznego transferu aaaRequire w usłudze Azure Storage | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o funkcji \"Wymaga zapewnienia bezpiecznego transferu\" hello usługi Azure Storage i jak tooenable go."
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
ms.openlocfilehash: 27f745c5e771b50213c1dbb39dee081947be1f39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="require-secure-transfer"></a><span data-ttu-id="d7c91-103">Wymaganie bezpiecznego transferu</span><span class="sxs-lookup"><span data-stu-id="d7c91-103">Require secure transfer</span></span>

<span data-ttu-id="d7c91-104">Opcja Hello "zapewnienia bezpiecznego transferu wymagane" zwiększa bezpieczeństwo hello konta magazynu, zezwalając tylko żądania toohello konta magazynu z bezpiecznych połączeń.</span><span class="sxs-lookup"><span data-stu-id="d7c91-104">hello "Secure transfer required" option enhances hello security of your storage account by only allowing requests toohello storage account from secure connections.</span></span> <span data-ttu-id="d7c91-105">Na przykład podczas wywoływania interfejsów API REST tooaccess Twojego konta magazynu, należy połączyć przy użyciu protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d7c91-105">For example, when calling REST APIs tooaccess your storage account, you must connect using HTTPS.</span></span> <span data-ttu-id="d7c91-106">Wszystkie żądania przy użyciu protokołu HTTP są odrzucane po włączeniu "Bezpieczny transfer wymagane".</span><span class="sxs-lookup"><span data-stu-id="d7c91-106">Any requests using HTTP are rejected when "Secure transfer required" is enabled.</span></span>

<span data-ttu-id="d7c91-107">Korzystając z usługi pliki Azure hello, każde połączenie bez szyfrowania nie powiedzie się, gdy "Bezpieczny transfer wymagane" jest włączona.</span><span class="sxs-lookup"><span data-stu-id="d7c91-107">When you are using hello Azure Files service, any connection without encryption fails when "Secure transfer required" is enabled.</span></span> <span data-ttu-id="d7c91-108">W tym scenariuszy przy użyciu protokołu SMB 2.1, SMB 3.0 bez szyfrowania i niektórych odmian powitania klienta SMB w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="d7c91-108">This includes scenarios using SMB 2.1, SMB 3.0 without encryption, and some flavors of hello Linux SMB client.</span></span> 

<span data-ttu-id="d7c91-109">Domyślnie opcja hello "zapewnienia bezpiecznego transferu wymagane" jest wyłączona.</span><span class="sxs-lookup"><span data-stu-id="d7c91-109">By default, hello "Secure transfer required" option is disabled.</span></span>

> [!NOTE]
> <span data-ttu-id="d7c91-110">Ponieważ Magazyn Azure nie obsługuje protokołu HTTPS dla niestandardowych nazw domen, ta opcja nie została zastosowana podczas korzystania z niestandardowej nazwy domeny.</span><span class="sxs-lookup"><span data-stu-id="d7c91-110">Because Azure Storage doesn't support HTTPS for custom domain names, this option is not applied when using a custom domain name.</span></span>

## <a name="enable-secure-transfer-required-in-hello-azure-portal"></a><span data-ttu-id="d7c91-111">Włącz "Zapewnienia bezpiecznego transferu wymagane" w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="d7c91-111">Enable "Secure transfer required" in hello Azure portal</span></span>

<span data-ttu-id="d7c91-112">Można włączyć hello "zapewnienia bezpiecznego transferu wymagane" zarówno ustawienie podczas tworzenia konta magazynu w hello [portalu Azure](https://portal.azure.com), a w przypadku istniejących kont magazynu.</span><span class="sxs-lookup"><span data-stu-id="d7c91-112">You can enable hello "Secure transfer required" setting both when you create a storage account in hello [Azure portal](https://portal.azure.com), and for existing storage accounts.</span></span>

### <a name="require-secure-transfer-when-you-create-a-storage-account"></a><span data-ttu-id="d7c91-113">Wymaga zapewnienia bezpiecznego transferu podczas tworzenia konta magazynu</span><span class="sxs-lookup"><span data-stu-id="d7c91-113">Require secure transfer when you create a storage account</span></span>

1. <span data-ttu-id="d7c91-114">Otwórz hello **utworzyć konto magazynu** bloku w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d7c91-114">Open hello **Create storage account** blade in hello Azure portal.</span></span>
1. <span data-ttu-id="d7c91-115">W obszarze **bezpieczny transfer wymagane**, wybierz pozycję **włączone**.</span><span class="sxs-lookup"><span data-stu-id="d7c91-115">Under **Secure transfer required**, select **Enabled**.</span></span>

  ![Zrzut ekranu](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_1.png)

### <a name="require-secure-transfer-for-an-existing-storage-account"></a><span data-ttu-id="d7c91-117">Wymaga zapewnienia bezpiecznego transferu do istniejącego konta magazynu</span><span class="sxs-lookup"><span data-stu-id="d7c91-117">Require secure transfer for an existing storage account</span></span>

1. <span data-ttu-id="d7c91-118">Wybierz istniejące konto magazynu w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d7c91-118">Select an existing storage account in hello Azure portal.</span></span>
1. <span data-ttu-id="d7c91-119">Wybierz **konfiguracji** w obszarze **ustawienia** w bloku menu konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="d7c91-119">Select **Configuration** under **SETTINGS** in hello storage account menu blade.</span></span>
1. <span data-ttu-id="d7c91-120">W obszarze **bezpieczny transfer wymagane**, wybierz pozycję **włączone**.</span><span class="sxs-lookup"><span data-stu-id="d7c91-120">Under **Secure transfer required**, select **Enabled**.</span></span>

  ![Zrzut ekranu](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_2.png)

## <a name="enable-secure-transfer-required-programmatically"></a><span data-ttu-id="d7c91-122">Włącz "Bezpieczny transfer wymagane" programowo</span><span class="sxs-lookup"><span data-stu-id="d7c91-122">Enable "Secure transfer required" programmatically</span></span>

<span data-ttu-id="d7c91-123">Nazwa ustawienia Hello jest _supportsHttpsTrafficOnly_ we właściwościach konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="d7c91-123">hello setting name is _supportsHttpsTrafficOnly_ in storage account properties.</span></span> <span data-ttu-id="d7c91-124">Można włączyć "Zapewnienia bezpiecznego transferu wymagane" Ustawianie za pomocą interfejsu API REST, narzędzi lub biblioteki:</span><span class="sxs-lookup"><span data-stu-id="d7c91-124">You can enable "Secure transfer required" setting with REST API, tools or libraries:</span></span>

* <span data-ttu-id="d7c91-125">**Interfejs API REST** (wersja: 2016-12-01): [wersji pakietu](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)</span><span class="sxs-lookup"><span data-stu-id="d7c91-125">**REST API** (Version: 2016-12-01): [release package](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)</span></span>
* <span data-ttu-id="d7c91-126">**PowerShell** (wersja: 4.1.0): [wersji pakietu](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)</span><span class="sxs-lookup"><span data-stu-id="d7c91-126">**PowerShell** (Version: 4.1.0): [release package](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)</span></span>
* <span data-ttu-id="d7c91-127">**Interfejs wiersza polecenia** (wersja: 2.0.11): [wersji pakietu](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)</span><span class="sxs-lookup"><span data-stu-id="d7c91-127">**CLI** (Version: 2.0.11): [release package](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)</span></span>
* <span data-ttu-id="d7c91-128">**NodeJS** (wersja: 1.1.0): [wersji pakietu](https://www.npmjs.com/package/azure-arm-storage/)</span><span class="sxs-lookup"><span data-stu-id="d7c91-128">**NodeJS** (Version: 1.1.0): [release package](https://www.npmjs.com/package/azure-arm-storage/)</span></span>
* <span data-ttu-id="d7c91-129">**Zestaw .NET SDK** (wersja: 6.3.0): [wersji pakietu](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)</span><span class="sxs-lookup"><span data-stu-id="d7c91-129">**.NET SDK** (Version: 6.3.0): [release package](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)</span></span>
* <span data-ttu-id="d7c91-130">**Zestaw SDK Python** (wersja: 1.1.0): [wersji pakietu](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)</span><span class="sxs-lookup"><span data-stu-id="d7c91-130">**Python SDK** (Version: 1.1.0): [release package](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)</span></span>
* <span data-ttu-id="d7c91-131">**Zestaw SDK dopisków fonetycznych** (wersja: 0.11.0): [wersji pakietu](https://rubygems.org/gems/azure_mgmt_storage)</span><span class="sxs-lookup"><span data-stu-id="d7c91-131">**Ruby SDK** (Version: 0.11.0): [release package](https://rubygems.org/gems/azure_mgmt_storage)</span></span>

### <a name="enable-secure-transfer-required-setting-with-rest-api"></a><span data-ttu-id="d7c91-132">Włącz "Zapewnienia bezpiecznego transferu wymagane" Ustawianie za pomocą interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="d7c91-132">Enable "Secure transfer required" setting with REST API</span></span>

<span data-ttu-id="d7c91-133">toosimplify testowanie za pomocą interfejsu API REST, można użyć [ArmClient](https://github.com/projectkudu/ARMClient) toocall z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="d7c91-133">toosimplify testing with REST API, you can use [ArmClient](https://github.com/projectkudu/ARMClient) toocall from command line.</span></span>

 <span data-ttu-id="d7c91-134">Możesz użyć poniżej ustawienia hello toocheck wiersza polecenia z hello interfejsu API REST:</span><span class="sxs-lookup"><span data-stu-id="d7c91-134">You can use below command line toocheck hello setting with hello REST API:</span></span>

```
# Login Azure and proceed with your credentials
> armclient login

> armclient GET  /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01
```

<span data-ttu-id="d7c91-135">W odpowiedzi hello można znaleźć _supportsHttpsTrafficOnly_ ustawienie.</span><span class="sxs-lookup"><span data-stu-id="d7c91-135">In hello response, you can find _supportsHttpsTrafficOnly_ setting.</span></span> <span data-ttu-id="d7c91-136">Przykład:</span><span class="sxs-lookup"><span data-stu-id="d7c91-136">Sample:</span></span>

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

<span data-ttu-id="d7c91-137">Możesz użyć poniżej ustawienia hello tooenable wiersza polecenia z hello interfejsu API REST:</span><span class="sxs-lookup"><span data-stu-id="d7c91-137">You can use below command line tooenable hello setting with hello REST API:</span></span>

```
# Login Azure and proceed with your credentials
> armclient login

> armclient PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01 < Input.json
```
<span data-ttu-id="d7c91-138">Przykład Input.json:</span><span class="sxs-lookup"><span data-stu-id="d7c91-138">Sample of Input.json:</span></span>
```Json
{
  "location": "westus",
  "properties": {
    "supportsHttpsTrafficOnly": true
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="d7c91-139">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d7c91-139">Next steps</span></span>
<span data-ttu-id="d7c91-140">Usługa Azure Storage zapewnia rozbudowany zestaw funkcji zabezpieczeń, które razem umożliwiają deweloperom toobuild bezpiecznych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d7c91-140">Azure Storage provides a comprehensive set of security capabilities, which together enable developers toobuild secure applications.</span></span> <span data-ttu-id="d7c91-141">Aby uzyskać więcej informacji, odwiedź stronę hello [przewodnik zabezpieczeń magazynu](storage-security-guide.md).</span><span class="sxs-lookup"><span data-stu-id="d7c91-141">For more details, visit hello [Storage Security Guide](storage-security-guide.md).</span></span>
