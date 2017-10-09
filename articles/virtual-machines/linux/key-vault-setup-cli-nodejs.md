---
title: aaaSet zapasowej Key Vault dla maszyn wirtualnych systemu Linux z hello Azure CLI 1.0 | Dokumentacja firmy Microsoft
description: "Jak tooset się Key Vault do użycia z maszyny wirtualnej platformy Azure Resource Manager z hello Azure CLI w wersji 1.0."
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: bccdd5ab-5ccf-4760-9039-92c6eafb15bd
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/24/2017
ms.author: singhkay
ms.openlocfilehash: 275022e4e7e26d7363784c289dd7512047c07bad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager-with-hello-azure-cli-10"></a><span data-ttu-id="e529d-103">Konfigurowanie magazynu kluczy dla maszyn wirtualnych w usłudze Azure Resource Manager z hello Azure CLI w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="e529d-103">Set up Key Vault for virtual machines in Azure Resource Manager with hello Azure CLI 1.0</span></span>
<span data-ttu-id="e529d-104">W stosie usługi Azure Resource Manager hello kluczy tajnych/certyfikaty są modelowane jako zasoby, które są udostępniane przez dostawcę zasobów hello klucza magazynu.</span><span class="sxs-lookup"><span data-stu-id="e529d-104">In hello Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by hello resource provider of Key Vault.</span></span> <span data-ttu-id="e529d-105">toolearn więcej informacji na temat usługi Azure Key Vault, zobacz [co to jest usługa Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="e529d-105">toolearn more about Azure Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span> <span data-ttu-id="e529d-106">Aby używać z maszynami wirtualnymi Azure Resource Manager toobe Key Vault, hello *EnabledForDeployment* tootrue musi być ustawiona właściwość na magazyn kluczy.</span><span class="sxs-lookup"><span data-stu-id="e529d-106">In order for Key Vault toobe used with Azure Resource Manager virtual machines, hello *EnabledForDeployment* property on Key Vault must be set tootrue.</span></span> <span data-ttu-id="e529d-107">Można to zrobić w różnych klientów.</span><span class="sxs-lookup"><span data-stu-id="e529d-107">You can do this in various clients.</span></span> <span data-ttu-id="e529d-108">W tym artykule opisano sposób tooset zapasowej Key Vault do użytku z maszyn wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e529d-108">This article shows you how tooset up Key Vault for use with Azure Virtual Machines.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="e529d-109">Zadanie hello toocomplete wersje interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="e529d-109">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="e529d-110">Można wykonać zadania hello przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="e529d-110">You can complete hello task using one of hello following CLI versions</span></span>

- <span data-ttu-id="e529d-111">[Azure CLI 1.0](#quick-commands) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania wdrażania modeli (w tym artykule)</span><span class="sxs-lookup"><span data-stu-id="e529d-111">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="e529d-112">[Azure CLI 2.0](../windows/key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello</span><span class="sxs-lookup"><span data-stu-id="e529d-112">[Azure CLI 2.0](../windows/key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="use-cli-10-tooset-up-key-vault"></a><span data-ttu-id="e529d-113">Użyj tooset 1.0 interfejsu wiersza polecenia w górę magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="e529d-113">Use CLI 1.0 tooset up Key Vault</span></span>
<span data-ttu-id="e529d-114">toocreate magazynu kluczy przy użyciu hello interfejsu wiersza polecenia (CLI), zobacz [Zarządzanie Key Vault przy użyciu interfejsu wiersza polecenia](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span><span class="sxs-lookup"><span data-stu-id="e529d-114">toocreate a key vault by using hello command-line interface (CLI), see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span></span>

<span data-ttu-id="e529d-115">1.0 interfejsu wiersza polecenia masz magazynu kluczy hello toocreate przed przypisaniem hello wdrożenia zasad.</span><span class="sxs-lookup"><span data-stu-id="e529d-115">For CLI 1.0, you have toocreate hello key vault before you assign hello deployment policy.</span></span> <span data-ttu-id="e529d-116">Następnie można przypisać zasady hello przy użyciu hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="e529d-116">You can then assign hello policy by using hello following command:</span></span>

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-tooset-up-key-vault"></a><span data-ttu-id="e529d-117">Użycie szablonów tooset zapasowej magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="e529d-117">Use templates tooset up Key Vault</span></span>
<span data-ttu-id="e529d-118">W przypadku użycia szablonu należy tooset hello `enabledForDeployment` właściwości zbyt`true` dla hello zasobu magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="e529d-118">When you use a template, you need tooset hello `enabledForDeployment` property too`true` for hello Key Vault resource.</span></span>

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

<span data-ttu-id="e529d-119">Inne opcje, które można skonfigurować podczas tworzenia magazynu kluczy przy użyciu szablonów, zobacz [utworzyć magazyn kluczy](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span><span class="sxs-lookup"><span data-stu-id="e529d-119">For other options that you can configure when you create a key vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>
