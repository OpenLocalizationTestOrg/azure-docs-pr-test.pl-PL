---
title: "aaaSet się klucz magazynu dla maszyn wirtualnych systemu Windows w usłudze Azure Resource Manager | Dokumentacja firmy Microsoft"
description: "Jak tooset się Key Vault do użycia z maszyny wirtualnej platformy Azure Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 33a483e2-cfbc-4c62-a588-5d9fd52491e2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.author: kasing
ms.openlocfilehash: 53bbe90708202ecfdcf754822d04bf2469631f08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager"></a><span data-ttu-id="767b7-103">Konfigurowanie magazynu kluczy dla maszyn wirtualnych w usłudze Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="767b7-103">Set up Key Vault for virtual machines in Azure Resource Manager</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="767b7-104">W stosie usługi Azure Resource Manager kluczy tajnych/certyfikaty są modelowane jako zasoby, które są udostępniane przez dostawcę zasobów hello klucza magazynu.</span><span class="sxs-lookup"><span data-stu-id="767b7-104">In Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by hello resource provider of Key Vault.</span></span> <span data-ttu-id="767b7-105">toolearn więcej informacji na temat usługi Key Vault, zobacz [co to jest usługa Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="767b7-105">toolearn more about Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span>

> [!NOTE]
> 1. <span data-ttu-id="767b7-106">Aby używać z maszynami wirtualnymi Azure Resource Manager toobe Key Vault, hello **EnabledForDeployment** tootrue musi być ustawiona właściwość na magazyn kluczy.</span><span class="sxs-lookup"><span data-stu-id="767b7-106">In order for Key Vault toobe used with Azure Resource Manager virtual machines, hello **EnabledForDeployment** property on Key Vault must be set tootrue.</span></span> <span data-ttu-id="767b7-107">Można to zrobić w różnych klientów.</span><span class="sxs-lookup"><span data-stu-id="767b7-107">You can do this in various clients.</span></span>
> 2. <span data-ttu-id="767b7-108">Hello magazynu kluczy musi toobe utworzone w hello tej samej subskrypcji i lokalizacji jako hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="767b7-108">hello Key Vault needs toobe created in hello same subscription and location as hello Virtual Machine.</span></span>
>
>

## <a name="use-powershell-tooset-up-key-vault"></a><span data-ttu-id="767b7-109">Użyj programu PowerShell tooset zapasowej magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="767b7-109">Use PowerShell tooset up Key Vault</span></span>
<span data-ttu-id="767b7-110">toocreate magazynu kluczy przy użyciu programu PowerShell, zobacz [wprowadzenie do usługi Azure Key Vault](../../key-vault/key-vault-get-started.md#vault).</span><span class="sxs-lookup"><span data-stu-id="767b7-110">toocreate a key vault by using PowerShell, see [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md#vault).</span></span>

<span data-ttu-id="767b7-111">Dla nowych magazynów kluczy można użyć tego polecenia cmdlet programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="767b7-111">For new key vaults, you can use this PowerShell cmdlet:</span></span>

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia' -EnabledForDeployment

<span data-ttu-id="767b7-112">Dla istniejących magazynów kluczy można użyć tego polecenia cmdlet programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="767b7-112">For existing key vaults, you can use this PowerShell cmdlet:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

## <a name="us-cli-tooset-up-key-vault"></a><span data-ttu-id="767b7-113">Nam CLI tooset zapasowej magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="767b7-113">Us CLI tooset up Key Vault</span></span>
<span data-ttu-id="767b7-114">toocreate magazynu kluczy przy użyciu hello interfejsu wiersza polecenia (CLI), zobacz [Zarządzanie Key Vault przy użyciu interfejsu wiersza polecenia](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span><span class="sxs-lookup"><span data-stu-id="767b7-114">toocreate a key vault by using hello command-line interface (CLI), see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span></span>

<span data-ttu-id="767b7-115">Dla interfejsu wiersza polecenia masz magazynu kluczy hello toocreate przed przypisaniem hello wdrożenia zasad.</span><span class="sxs-lookup"><span data-stu-id="767b7-115">For CLI, you have toocreate hello key vault before you assign hello deployment policy.</span></span> <span data-ttu-id="767b7-116">Można to zrobić za pomocą hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="767b7-116">You can do this by using hello following command:</span></span>

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-tooset-up-key-vault"></a><span data-ttu-id="767b7-117">Użycie szablonów tooset zapasowej magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="767b7-117">Use templates tooset up Key Vault</span></span>
<span data-ttu-id="767b7-118">Gdy używasz szablonu należy tooset hello `enabledForDeployment` właściwości zbyt`true` dla hello zasobu magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="767b7-118">While you use a template, you need tooset hello `enabledForDeployment` property too`true` for hello Key Vault resource.</span></span>

    {
      "type": "Microsoft.KeyVault/vaults",
      "name": "ContosoKeyVault",
      "apiVersion": "2015-06-01",
      "location": "<location-of-key-vault>",
      "properties": {
        "enabledForDeployment": "true",
        ....
        ....
      }
    }

<span data-ttu-id="767b7-119">Inne opcje, które można skonfigurować podczas tworzenia magazynu kluczy przy użyciu szablonów, zobacz [utworzyć magazyn kluczy](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span><span class="sxs-lookup"><span data-stu-id="767b7-119">For other options that you can configure when you create a key vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>
