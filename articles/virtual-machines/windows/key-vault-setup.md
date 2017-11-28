---
title: "Ustawianie klucza magazynu dla maszyn wirtualnych systemu Windows w usłudze Azure Resource Manager | Dokumentacja firmy Microsoft"
description: "Jak skonfigurować magazyn kluczy do użycia z maszyny wirtualnej platformy Azure Resource Manager."
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
ms.openlocfilehash: a5083a5216efbfd76fd912ec48c2f0ec3b30c4a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager"></a><span data-ttu-id="0def2-103">Konfigurowanie magazynu kluczy dla maszyn wirtualnych w usłudze Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0def2-103">Set up Key Vault for virtual machines in Azure Resource Manager</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="0def2-104">W stosie usługi Azure Resource Manager kluczy tajnych/certyfikaty są modelowane jako zasoby, które są udostępniane przez dostawcę zasobów magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="0def2-104">In Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by the resource provider of Key Vault.</span></span> <span data-ttu-id="0def2-105">Aby dowiedzieć się więcej na temat usługi Key Vault, zobacz [co to jest usługa Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="0def2-105">To learn more about Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span>

> [!NOTE]
> 1. <span data-ttu-id="0def2-106">Aby Key Vault ma być używany z maszyn wirtualnych Menedżera zasobów Azure **EnabledForDeployment** właściwości magazynu kluczy musi ustawić na wartość true.</span><span class="sxs-lookup"><span data-stu-id="0def2-106">In order for Key Vault to be used with Azure Resource Manager virtual machines, the **EnabledForDeployment** property on Key Vault must be set to true.</span></span> <span data-ttu-id="0def2-107">Można to zrobić w różnych klientów.</span><span class="sxs-lookup"><span data-stu-id="0def2-107">You can do this in various clients.</span></span>
> 2. <span data-ttu-id="0def2-108">Magazyn kluczy musi mogą być tworzone w tej samej subskrypcji i lokalizacji co maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0def2-108">The Key Vault needs to be created in the same subscription and location as the Virtual Machine.</span></span>
>
>

## <a name="use-powershell-to-set-up-key-vault"></a><span data-ttu-id="0def2-109">Konfigurowanie usługi Key Vault przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="0def2-109">Use PowerShell to set up Key Vault</span></span>
<span data-ttu-id="0def2-110">Aby utworzyć magazyn kluczy przy użyciu programu PowerShell, zobacz [wprowadzenie do usługi Azure Key Vault](../../key-vault/key-vault-get-started.md#vault).</span><span class="sxs-lookup"><span data-stu-id="0def2-110">To create a key vault by using PowerShell, see [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md#vault).</span></span>

<span data-ttu-id="0def2-111">Dla nowych magazynów kluczy można użyć tego polecenia cmdlet programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="0def2-111">For new key vaults, you can use this PowerShell cmdlet:</span></span>

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia' -EnabledForDeployment

<span data-ttu-id="0def2-112">Dla istniejących magazynów kluczy można użyć tego polecenia cmdlet programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="0def2-112">For existing key vaults, you can use this PowerShell cmdlet:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

## <a name="us-cli-to-set-up-key-vault"></a><span data-ttu-id="0def2-113">Nam interfejsu wiersza polecenia, aby skonfigurować magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="0def2-113">Us CLI to set up Key Vault</span></span>
<span data-ttu-id="0def2-114">Aby utworzyć magazyn kluczy przy użyciu interfejsu wiersza polecenia (CLI), zobacz [Zarządzanie Key Vault przy użyciu interfejsu wiersza polecenia](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span><span class="sxs-lookup"><span data-stu-id="0def2-114">To create a key vault by using the command-line interface (CLI), see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span></span>

<span data-ttu-id="0def2-115">Dla interfejsu wiersza polecenia należy utworzyć magazyn kluczy, przed przypisaniem zasady wdrażania.</span><span class="sxs-lookup"><span data-stu-id="0def2-115">For CLI, you have to create the key vault before you assign the deployment policy.</span></span> <span data-ttu-id="0def2-116">Możesz to zrobić za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="0def2-116">You can do this by using the following command:</span></span>

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-to-set-up-key-vault"></a><span data-ttu-id="0def2-117">Konfigurowanie usługi Key Vault za pomocą szablonów</span><span class="sxs-lookup"><span data-stu-id="0def2-117">Use templates to set up Key Vault</span></span>
<span data-ttu-id="0def2-118">Gdy używasz szablonu, musisz ustawić `enabledForDeployment` właściwości `true` dla zasobu magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="0def2-118">While you use a template, you need to set the `enabledForDeployment` property to `true` for the Key Vault resource.</span></span>

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

<span data-ttu-id="0def2-119">Inne opcje, które można skonfigurować podczas tworzenia magazynu kluczy przy użyciu szablonów, zobacz [utworzyć magazyn kluczy](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span><span class="sxs-lookup"><span data-stu-id="0def2-119">For other options that you can configure when you create a key vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>
