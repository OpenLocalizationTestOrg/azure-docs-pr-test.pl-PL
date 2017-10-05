---
title: "Zarządzanie magazynem Azure za pomocą usługi Automatyzacja Azure"
description: "Więcej informacji na temat jak usługa Automatyzacja Azure może służyć do zarządzania magazynem Azure na dużą skalę."
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
ms.openlocfilehash: 4649e42a628307e15f8b067503e4e8e13f16f1af
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="managing-azure-storage-using-azure-automation"></a><span data-ttu-id="59e3e-103">Zarządzanie magazynem Azure za pomocą usługi Automatyzacja Azure</span><span class="sxs-lookup"><span data-stu-id="59e3e-103">Managing Azure Storage using Azure Automation</span></span>
<span data-ttu-id="59e3e-104">W tym przewodniku przedstawiono usługi Automatyzacja Azure oraz jak on używany w celu uproszczenia zarządzania obiektów blob magazynu Azure, tabel i kolejek.</span><span class="sxs-lookup"><span data-stu-id="59e3e-104">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of your Azure Storage blobs, tables, and queues.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="59e3e-105">Co to jest Azure Automation?</span><span class="sxs-lookup"><span data-stu-id="59e3e-105">What is Azure Automation?</span></span>
<span data-ttu-id="59e3e-106">[Automatyzacja Azure](https://azure.microsoft.com/services/automation/) jest usługą platformy Azure, dla uproszczenia zarządzania chmurą za pomocą automatyzacji procesu.</span><span class="sxs-lookup"><span data-stu-id="59e3e-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="59e3e-107">Przy użyciu usługi Automatyzacja Azure, można zautomatyzować, aby zwiększyć niezawodność i wydajność długotrwałe, ręcznych, podatnych i często powtarzanych zadań i skrócić czas wartości dla Twojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="59e3e-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated to increase reliability and efficiency, and reduce time to value for your organization.</span></span>

<span data-ttu-id="59e3e-108">Automatyzacja Azure umożliwia aparatowi wykonywania przepływów pracy wysoce niezawodne i wysokiej dostępności, która może obsłużyć do własnych potrzeb miarę rozwoju organizacji.</span><span class="sxs-lookup"><span data-stu-id="59e3e-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales to meet your needs as your organization grows.</span></span> <span data-ttu-id="59e3e-109">W automatyzacji Azure procesów może być rozpoczęte ręcznie, przez systemy 3rd firmy lub w zaplanowanych odstępach czasu tak, aby zadania stanie dokładnie w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="59e3e-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="59e3e-110">Obniżyć koszty operacyjne i zwolnić IT / personel DevOps skupić się na pracy, który dodaje biznesowych wartość przez przeniesienie zadań zarządzania chmury do automatycznego uruchamiania przez usługi Automatyzacja Azure.</span><span class="sxs-lookup"><span data-stu-id="59e3e-110">Lower operational overhead and free up IT / DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-storage"></a><span data-ttu-id="59e3e-111">Jak usługi Automatyzacja Azure ułatwia zarządzanie magazynem Azure?</span><span class="sxs-lookup"><span data-stu-id="59e3e-111">How can Azure Automation help manage Azure Storage?</span></span>
<span data-ttu-id="59e3e-112">Magazyn Azure można zarządzać w automatyzacji Azure za pomocą poleceń cmdlet programu PowerShell, które są dostępne w [programu Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="59e3e-112">Azure Storage can be managed in Azure Automation by using the PowerShell cmdlets that are available in [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="59e3e-113">Usługi Automatyzacja Azure ma tych poleceń cmdlet programu PowerShell magazynu fabrycznej, umożliwiając wykonanie wszystkich obiektów blob, tabel i kolejki zadań zarządzania w ramach usługi.</span><span class="sxs-lookup"><span data-stu-id="59e3e-113">Azure Automation has these Storage PowerShell cmdlets available out of the box, so that you can perform all of your blob, table, and queue management tasks within the service.</span></span> <span data-ttu-id="59e3e-114">Można również skojarzyć te polecenia cmdlet usługi Automatyzacja Azure, za pomocą poleceń cmdlet dla innych usług Azure, aby zautomatyzować złożone zadania 3 systemów firm i usług Azure.</span><span class="sxs-lookup"><span data-stu-id="59e3e-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="59e3e-115">[Galerię elementów runbook usługi Automatyzacja Azure](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) zawiera szereg produktu zespołu i społeczność elementy runbook, aby rozpocząć automatyzacji zarządzania usługi Azure Storage, innych usług platformy Azure i systemów firm 3.</span><span class="sxs-lookup"><span data-stu-id="59e3e-115">The [Azure Automation runbook gallery](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contains a variety of product team and community runbooks to get started automating management of Azure Storage, other Azure services, and 3rd party systems.</span></span> <span data-ttu-id="59e3e-116">Galeria elementów runbook obejmują:</span><span class="sxs-lookup"><span data-stu-id="59e3e-116">Gallery runbooks include:</span></span>

* [<span data-ttu-id="59e3e-117">Usuwanie obiektów blob magazynu Azure, które są niektórych dni starego przy użyciu automatyzacji usługi</span><span class="sxs-lookup"><span data-stu-id="59e3e-117">Remove Azure Storage Blobs that are Certain Days Old Using Automation Service</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Remove-Storage-Blobs-that-aae4b761)
* [<span data-ttu-id="59e3e-118">Pobieranie obiektu Blob z usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="59e3e-118">Download a Blob from Azure Storage</span></span>](https://gallery.technet.microsoft.com/scriptcenter/a-Blob-from-Azure-Storage-6bc13745)
* [<span data-ttu-id="59e3e-119">Wykonaj kopię zapasową wszystkich dysków dla jednej maszyny Wirtualnej platformy Azure lub dla wszystkich maszyn wirtualnych w usłudze w chmurze</span><span class="sxs-lookup"><span data-stu-id="59e3e-119">Backup all disks for a single Azure VM or for all VMs in a Cloud Service</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Backup-all-disks-for-a-ede940d5)

## <a name="next-steps"></a><span data-ttu-id="59e3e-120">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="59e3e-120">Next Steps</span></span>
<span data-ttu-id="59e3e-121">Teraz, kiedy znasz już podstawy usługi Automatyzacja Azure i jak może służyć do zarządzania obiektów blob, tabel i kolejek usługi Azure Storage, skorzystaj z poniższych linków, aby dowiedzieć się więcej na temat automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="59e3e-121">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure Storage blobs, tables, and queues, follow these links to learn more about Azure Automation.</span></span>

<span data-ttu-id="59e3e-122">Zobacz samouczek usługi Automatyzacja Azure [Tworzenie lub importowanie elementu runbook automatyzacji Azure](../../automation/automation-creating-importing-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="59e3e-122">See the Azure Automation tutorial [Creating or importing a runbook in Azure Automation](../../automation/automation-creating-importing-runbook.md).</span></span>

