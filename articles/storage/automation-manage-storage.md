---
title: "aaaManage usługi Azure Storage za pomocą usługi Automatyzacja Azure"
description: "Więcej informacji na temat sposobu hello usługi Automatyzacja Azure może być używane toomanage magazynu Azure na dużą skalę."
services: storage, automation
documentationcenter: 
author: jodoglevy
manager: eamono
editor: 
ms.assetid: bac41c39-1d95-46aa-a481-ec17bbb21b40
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: eamono
ms.openlocfilehash: 15e34128ffb0ba3315b5260442f628b5978c5197
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-storage-using-azure-automation"></a><span data-ttu-id="1c455-103">Zarządzanie magazynem Azure za pomocą usługi Automatyzacja Azure</span><span class="sxs-lookup"><span data-stu-id="1c455-103">Managing Azure Storage using Azure Automation</span></span>
<span data-ttu-id="1c455-104">W tym przewodniku przedstawiono usługi Automatyzacja Azure toohello i jak mogą być używane toosimplify zarządzania obiektów blob magazynu Azure, tabel i kolejek.</span><span class="sxs-lookup"><span data-stu-id="1c455-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of your Azure Storage blobs, tables, and queues.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="1c455-105">Co to jest Azure Automation?</span><span class="sxs-lookup"><span data-stu-id="1c455-105">What is Azure Automation?</span></span>
<span data-ttu-id="1c455-106">[Automatyzacja Azure](https://azure.microsoft.com/services/automation/) jest usługą platformy Azure, dla uproszczenia zarządzania chmurą za pomocą automatyzacji procesu.</span><span class="sxs-lookup"><span data-stu-id="1c455-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="1c455-107">Przy użyciu usługi Automatyzacja Azure, długotrwałe, ręczne, podatne na błędy i często powtarzane zadania można automatycznych tooincrease niezawodności i wydajności i zmniejszyć czas toovalue dla Twojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="1c455-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated tooincrease reliability and efficiency, and reduce time toovalue for your organization.</span></span>

<span data-ttu-id="1c455-108">Automatyzacja Azure umożliwia aparatowi wykonywania przepływów pracy wysoce niezawodne i wysokiej dostępności, która może obsłużyć toomeet potrzeb miarę rozwoju organizacji.</span><span class="sxs-lookup"><span data-stu-id="1c455-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales toomeet your needs as your organization grows.</span></span> <span data-ttu-id="1c455-109">W automatyzacji Azure procesów może być rozpoczęte ręcznie, przez systemy 3rd firmy lub w zaplanowanych odstępach czasu tak, aby zadania stanie dokładnie w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="1c455-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="1c455-110">Obniżyć koszty operacyjne i zwolnić IT / toofocus personelu DevOps pracy dodającego wartość biznesową, przenosząc toobe zadań zarządzania z chmury uruchamiane automatycznie przez usługi Automatyzacja Azure.</span><span class="sxs-lookup"><span data-stu-id="1c455-110">Lower operational overhead and free up IT / DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-storage"></a><span data-ttu-id="1c455-111">Jak usługi Automatyzacja Azure ułatwia zarządzanie magazynem Azure?</span><span class="sxs-lookup"><span data-stu-id="1c455-111">How can Azure Automation help manage Azure Storage?</span></span>
<span data-ttu-id="1c455-112">Magazyn Azure można zarządzać w automatyzacji Azure za pomocą poleceń cmdlet programu PowerShell hello, które są dostępne w [programu Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="1c455-112">Azure Storage can be managed in Azure Automation by using hello PowerShell cmdlets that are available in [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="1c455-113">Automatyzacja Azure ma tych poleceń cmdlet programu PowerShell magazynu fabrycznej hello tak, aby można było wykonać wszystkich obiektów blob, tabel i kolejki zadań zarządzania w ramach usługi hello.</span><span class="sxs-lookup"><span data-stu-id="1c455-113">Azure Automation has these Storage PowerShell cmdlets available out of hello box, so that you can perform all of your blob, table, and queue management tasks within hello service.</span></span> <span data-ttu-id="1c455-114">Tych poleceń cmdlet usługi Automatyzacja Azure, za pomocą poleceń cmdlet powitania dla innych usług platformy Azure, tooautomate złożone zadania może również łączyć 3 systemów firm i usług Azure.</span><span class="sxs-lookup"><span data-stu-id="1c455-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="1c455-115">Witaj [galerię elementów runbook usługi Automatyzacja Azure](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) zawiera szereg produktu zespołu i społeczność elementów runbook tooget pracy automatyzacji zarządzania usługi Azure Storage, innych usług platformy Azure i systemów firm 3.</span><span class="sxs-lookup"><span data-stu-id="1c455-115">hello [Azure Automation runbook gallery](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contains a variety of product team and community runbooks tooget started automating management of Azure Storage, other Azure services, and 3rd party systems.</span></span> <span data-ttu-id="1c455-116">Galeria elementów runbook obejmują:</span><span class="sxs-lookup"><span data-stu-id="1c455-116">Gallery runbooks include:</span></span>

* [<span data-ttu-id="1c455-117">Usuwanie obiektów blob magazynu Azure, które są niektórych dni starego przy użyciu automatyzacji usługi</span><span class="sxs-lookup"><span data-stu-id="1c455-117">Remove Azure Storage Blobs that are Certain Days Old Using Automation Service</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Remove-Storage-Blobs-that-aae4b761)
* [<span data-ttu-id="1c455-118">Pobieranie obiektu Blob z usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="1c455-118">Download a Blob from Azure Storage</span></span>](https://gallery.technet.microsoft.com/scriptcenter/a-Blob-from-Azure-Storage-6bc13745)
* [<span data-ttu-id="1c455-119">Wykonaj kopię zapasową wszystkich dysków dla jednej maszyny Wirtualnej platformy Azure lub dla wszystkich maszyn wirtualnych w usłudze w chmurze</span><span class="sxs-lookup"><span data-stu-id="1c455-119">Backup all disks for a single Azure VM or for all VMs in a Cloud Service</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Backup-all-disks-for-a-ede940d5)

## <a name="next-steps"></a><span data-ttu-id="1c455-120">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1c455-120">Next Steps</span></span>
<span data-ttu-id="1c455-121">Teraz, kiedy znasz już podstawy hello usługi Automatyzacja Azure i jak może być używana toomanage, które obiekty BLOB magazynu Azure, tabel i kolejek, wykonaj te toolearn łącza więcej informacji na temat automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="1c455-121">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure Storage blobs, tables, and queues, follow these links toolearn more about Azure Automation.</span></span>

<span data-ttu-id="1c455-122">Zobacz samouczek usługi Automatyzacja Azure hello [Tworzenie lub importowanie elementu runbook automatyzacji Azure](../automation/automation-creating-importing-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="1c455-122">See hello Azure Automation tutorial [Creating or importing a runbook in Azure Automation](../automation/automation-creating-importing-runbook.md).</span></span>

