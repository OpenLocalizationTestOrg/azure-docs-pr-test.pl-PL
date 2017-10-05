---
title: Konfigurowanie programu PowerShell do tworzenia maszyn wirtualnych dla witryny Marketplace | Dokumentacja firmy Microsoft
description: "Instrukcje dotyczące konfigurowania programu Azure PowerShell i używać go jako opcjonalny procesu przepływać do tworzenia obrazów maszyn wirtualnych do wdrożenia i sprzedawać w portalu Azure Marketplace"
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
ms.openlocfilehash: bbcce5093d2bbd5326523063db7d0e565fe4de6d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-azure-powershell-to-create-an-offer-for-the-azure-marketplace"></a><span data-ttu-id="806f1-103">Konfigurowanie programu Azure PowerShell, aby utworzyć ofertę do portalu Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="806f1-103">Set up Azure PowerShell to create an offer for the Azure Marketplace</span></span>
<span data-ttu-id="806f1-104">Aby uzyskać szczegółowe informacje na temat sposobu konfigurowania programu PowerShell w programie Azure, zobacz [jak instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="806f1-104">For detailed information on how to set up PowerShell in Azure, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="806f1-105">Proste podejście jest przy użyciu metody certyfikatów, które pobiera i importuje certyfikatu wymagane do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="806f1-105">A simple approach is to use the certificate method, which downloads and imports a certificate needed for authentication.</span></span> <span data-ttu-id="806f1-106">Aby uzyskać potrzebny certyfikat, użyj **Get-AzurePublishSettingsFile** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="806f1-106">To obtain the needed certificate, use the **Get-AzurePublishSettingsFile** cmdlet.</span></span> <span data-ttu-id="806f1-107">Po wyświetleniu monitu, Zapisz plik.</span><span class="sxs-lookup"><span data-stu-id="806f1-107">Save the file when you're prompted.</span></span> <span data-ttu-id="806f1-108">Aby zaimportować certyfikat do sesji programu PowerShell, użyj **AzurePublishSettingsFile importu** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="806f1-108">To import the certificate into a PowerShell session, use the **Import-AzurePublishSettingsFile** cmdlet.</span></span>

<span data-ttu-id="806f1-109">Aby skonfigurować i zapisać typowe ustawienia subskrypcji Microsoft Azure dla sesji programu PowerShell, użyj **AzureSubscription zestaw** i **AzureSubscription wybierz** poleceń cmdlet:</span><span class="sxs-lookup"><span data-stu-id="806f1-109">To configure and store the common Microsoft Azure subscription settings for the PowerShell session, use the **Set-AzureSubscription** and **Select-AzureSubscription** cmdlets:</span></span>

        Set-AzureSubscription -SubscriptionName “mySubName” -CurrentStorageAccountName “mystorageaccount”
        Select-AzureSubscription -SubscriptionName "mySubName" –Current

<span data-ttu-id="806f1-110">Pierwsze polecenie kojarzy domyślne konto magazynu z subskrypcji (wymagane dla niektórych operacji inicjowania obsługi administracyjnej maszyn wirtualnych).</span><span class="sxs-lookup"><span data-stu-id="806f1-110">The first command associates a default storage account with the subscription (needed for some VM provisioning operations).</span></span>  <span data-ttu-id="806f1-111">Drugi sprawia, że subskrypcja obecną (rozpoznawane przez inne polecenia cmdlet).</span><span class="sxs-lookup"><span data-stu-id="806f1-111">The second makes the subscription the current one (recognized by other cmdlets).</span></span>

## <a name="see-also"></a><span data-ttu-id="806f1-112">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="806f1-112">See also</span></span>
* [<span data-ttu-id="806f1-113">Wprowadzenie: jak publikowanie oferty w portalu Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="806f1-113">Getting started: How to publish an offer to the Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)
* [<span data-ttu-id="806f1-114">Tworzenie obrazu maszyny wirtualnej dla witryny Marketplace</span><span class="sxs-lookup"><span data-stu-id="806f1-114">Creating a virtual machine image for the Marketplace</span></span>](marketplace-publishing-vm-image-creation.md)

