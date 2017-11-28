---
title: "aaaSet się toocreate PowerShell maszyny Wirtualnej dla hello Marketplace | Dokumentacja firmy Microsoft"
description: "Instrukcje dotyczące konfigurowania programu Azure PowerShell i używać go jako opcjonalny procesu przepływu toodeploy obrazów maszyny Wirtualnej toocreate i sprzedawać w, hello Azure Marketplace"
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e19d6cda-76df-4e42-be84-c9fe47a636db
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/04/2016
ms.author: hascipio
ms.openlocfilehash: cd2ebad7472248b8f921706e1a8c82d41f33b9cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-azure-powershell-toocreate-an-offer-for-hello-azure-marketplace"></a><span data-ttu-id="a0d3b-103">Konfigurowanie programu Azure PowerShell toocreate ofertę hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="a0d3b-103">Set up Azure PowerShell toocreate an offer for hello Azure Marketplace</span></span>
<span data-ttu-id="a0d3b-104">Aby uzyskać szczegółowe informacje na temat tooset się programu PowerShell w programie Azure, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a0d3b-104">For detailed information on how tooset up PowerShell in Azure, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="a0d3b-105">Proste podejście jest toouse hello certyfikatu metodę, która pobiera i importuje certyfikatu wymagane do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="a0d3b-105">A simple approach is toouse hello certificate method, which downloads and imports a certificate needed for authentication.</span></span> <span data-ttu-id="a0d3b-106">Witaj tooobtain potrzebne certyfikatów, należy użyć hello **Get-AzurePublishSettingsFile** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a0d3b-106">tooobtain hello needed certificate, use hello **Get-AzurePublishSettingsFile** cmdlet.</span></span> <span data-ttu-id="a0d3b-107">Zapisz plik hello, po wyświetleniu monitu.</span><span class="sxs-lookup"><span data-stu-id="a0d3b-107">Save hello file when you're prompted.</span></span> <span data-ttu-id="a0d3b-108">certyfikat hello tooimport w sesji programu PowerShell, użyj hello **AzurePublishSettingsFile importu** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a0d3b-108">tooimport hello certificate into a PowerShell session, use hello **Import-AzurePublishSettingsFile** cmdlet.</span></span>

<span data-ttu-id="a0d3b-109">tooconfigure i zapisać hello wspólnej Microsoft Azure subskrypcji ustawienia hello sesji programu PowerShell, użyj hello **AzureSubscription zestaw** i **AzureSubscription wybierz** poleceń cmdlet:</span><span class="sxs-lookup"><span data-stu-id="a0d3b-109">tooconfigure and store hello common Microsoft Azure subscription settings for hello PowerShell session, use hello **Set-AzureSubscription** and **Select-AzureSubscription** cmdlets:</span></span>

        Set-AzureSubscription -SubscriptionName “mySubName” -CurrentStorageAccountName “mystorageaccount”
        Select-AzureSubscription -SubscriptionName "mySubName" –Current

<span data-ttu-id="a0d3b-110">pierwsze polecenie Hello kojarzy domyślne konto magazynu z subskrypcji hello (wymagane dla niektórych operacji inicjowania obsługi administracyjnej maszyn wirtualnych).</span><span class="sxs-lookup"><span data-stu-id="a0d3b-110">hello first command associates a default storage account with hello subscription (needed for some VM provisioning operations).</span></span>  <span data-ttu-id="a0d3b-111">Witaj drugi sprawia, że subskrypcja hello hello obecną (rozpoznawane przez inne polecenia cmdlet).</span><span class="sxs-lookup"><span data-stu-id="a0d3b-111">hello second makes hello subscription hello current one (recognized by other cmdlets).</span></span>

## <a name="see-also"></a><span data-ttu-id="a0d3b-112">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="a0d3b-112">See also</span></span>
* [<span data-ttu-id="a0d3b-113">Wprowadzenie: jak toopublish toohello oferta portalu Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="a0d3b-113">Getting started: How toopublish an offer toohello Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)
* [<span data-ttu-id="a0d3b-114">Tworzenie obrazu maszyny wirtualnej dla hello Marketplace</span><span class="sxs-lookup"><span data-stu-id="a0d3b-114">Creating a virtual machine image for hello Marketplace</span></span>](marketplace-publishing-vm-image-creation.md)

