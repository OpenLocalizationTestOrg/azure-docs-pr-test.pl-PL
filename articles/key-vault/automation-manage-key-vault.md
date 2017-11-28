---
title: "Zarządzanie usługą Azure Key Vault przy użyciu automatyzacji Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat sposobu usługi Automatyzacja Azure może służyć do zarządzania usługi Azure Key Vault."
services: Key-Vault, automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 4e780762-19b6-4ca6-b894-ebb44c538f35
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: magoedte;csand
ms.openlocfilehash: dee39662472fe54776b591977f2b1ecb39d15b00
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-key-vault-using-azure-automation"></a><span data-ttu-id="467da-103">Zarządzanie usługą Azure Key Vault za pomocą usługi Automatyzacja Azure</span><span class="sxs-lookup"><span data-stu-id="467da-103">Managing Azure Key Vault using Azure Automation</span></span>
<span data-ttu-id="467da-104">W tym przewodniku przedstawiono usługi Automatyzacja Azure oraz jak on używany w celu uproszczenia zarządzania kluczy i kluczy tajnych w magazynie kluczy Azure.</span><span class="sxs-lookup"><span data-stu-id="467da-104">This guide will introduce you to the Azure Automation service and how it can be used to simplify management of your keys and secrets in Azure Key Vault.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="467da-105">Co to jest Azure Automation?</span><span class="sxs-lookup"><span data-stu-id="467da-105">What is Azure Automation?</span></span>
<span data-ttu-id="467da-106">[Automatyzacja Azure](../automation/automation-intro.md) jest usługą platformy Azure, dla uproszczenia zarządzania chmurą za pośrednictwem automatyzacji procesu i konfiguracji żądanego stanu.</span><span class="sxs-lookup"><span data-stu-id="467da-106">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation and desired state configuration.</span></span> <span data-ttu-id="467da-107">Przy użyciu automatyzacji Azure, ręczne, powtarzane, długotrwałe i podatne na błędy zadań można zautomatyzować, aby zwiększyć niezawodność, wydajność i wartość czasu dla Twojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="467da-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span></span>

<span data-ttu-id="467da-108">Automatyzacja Azure umożliwia aparatowi wykonywania przepływów pracy wysoce niezawodne, wysokiej dostępności, która może obsłużyć do własnych potrzeb.</span><span class="sxs-lookup"><span data-stu-id="467da-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales to meet your needs.</span></span> <span data-ttu-id="467da-109">W automatyzacji Azure procesów może być rozpoczęte ręcznie, przez systemy 3rd firmy lub w zaplanowanych odstępach czasu tak, aby zadania stanie dokładnie w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="467da-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="467da-110">Obniżenie kosztów operacyjnych i zwolnić IT i pracownicy DevOps skupić się na pracy dodającego wartość biznesową przez przeniesienie zadań zarządzania chmury do automatycznego uruchamiania przez usługi Automatyzacja Azure.</span><span class="sxs-lookup"><span data-stu-id="467da-110">Reduce operational overhead and free up IT and DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-key-vault"></a><span data-ttu-id="467da-111">Jak usługi Automatyzacja Azure ułatwia zarządzanie usługą Azure Key Vault?</span><span class="sxs-lookup"><span data-stu-id="467da-111">How can Azure Automation help manage Azure Key Vault?</span></span>
<span data-ttu-id="467da-112">Za pomocą można zarządzać w automatyzacji Azure Key Vault [poleceń cmdlet usługi Key Vault AzureRM](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) i [poleceń cmdlet klasycznej usługi Azure Key Vault](https://msdn.microsoft.com/library/azure/dn868052.aspx).</span><span class="sxs-lookup"><span data-stu-id="467da-112">Key Vault can be managed in Azure Automation by using the [AzureRM Key Vault cmdlets](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) and [Azure Classic Key Vault cmdlets](https://msdn.microsoft.com/library/azure/dn868052.aspx).</span></span> <span data-ttu-id="467da-113">Moduł Azure do zarządzania klasycznym usługi Key Vault jest dostępna automatycznie w automatyzacji Azure i można zaimportować [AzureRM KeyVault modułu](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) w automatyzacji Azure tak, aby można było wykonać wiele zadań zarządzania w ramach usługi Key Vault.</span><span class="sxs-lookup"><span data-stu-id="467da-113">The Azure module for managing classic Key Vault is available automatically in Azure Automation, and you can import the [AzureRM-KeyVault module](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) into Azure Automation, so that you can perform many of your Key Vault management tasks within the service.</span></span> <span data-ttu-id="467da-114">Można również skojarzyć te polecenia cmdlet usługi Automatyzacja Azure, za pomocą poleceń cmdlet dla innych usług Azure, aby zautomatyzować złożone zadania 3 systemów firm i usług Azure.</span><span class="sxs-lookup"><span data-stu-id="467da-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="467da-115">Za pomocą poleceń cmdlet usługi Azure Key Vault może wykonać te zadania, między innymi:</span><span class="sxs-lookup"><span data-stu-id="467da-115">With the Azure Key Vault cmdlets you can perform these tasks among others:</span></span> 

* <span data-ttu-id="467da-116">Tworzenie i Konfigurowanie magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="467da-116">Create and configure a key vault</span></span>
* <span data-ttu-id="467da-117">Tworzenie lub Importowanie klucza</span><span class="sxs-lookup"><span data-stu-id="467da-117">Create or import a key</span></span>
* <span data-ttu-id="467da-118">Utwórz lub zaktualizuj klucz tajny</span><span class="sxs-lookup"><span data-stu-id="467da-118">Create or update a secret</span></span>
* <span data-ttu-id="467da-119">Atrybuty aktualizacji klucza</span><span class="sxs-lookup"><span data-stu-id="467da-119">Update attributes of a key</span></span>
* <span data-ttu-id="467da-120">Pobierz klucz lub klucz tajny</span><span class="sxs-lookup"><span data-stu-id="467da-120">Get a key or secret</span></span>
* <span data-ttu-id="467da-121">Usuwanie klucza lub klucza tajnego</span><span class="sxs-lookup"><span data-stu-id="467da-121">Delete a key or secret</span></span>

<span data-ttu-id="467da-122">Oto kilka przykładów przy użyciu programu PowerShell do zarządzania usługi Key Vault:</span><span class="sxs-lookup"><span data-stu-id="467da-122">Here are some examples of using PowerShell to manage Key Vault:</span></span>  

* [<span data-ttu-id="467da-123">Usługi Azure Key Vault - krok po kroku</span><span class="sxs-lookup"><span data-stu-id="467da-123">Azure Key Vault - Step by Step</span></span>](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step)
* [<span data-ttu-id="467da-124">Instalowanie i konfigurowanie usługi Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="467da-124">Setting Up and Configuring an Azure Key Vault</span></span>](https://www.simple-talk.com/cloud/platform-as-a-service/setting-up-and-configuring-an-azure-key-vault)

## <a name="next-steps"></a><span data-ttu-id="467da-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="467da-125">Next steps</span></span>
<span data-ttu-id="467da-126">Teraz, kiedy znasz już podstawy usługi Automatyzacja Azure i jak może służyć do zarządzania usługą Azure Key Vault, skorzystaj z poniższych linków, aby dowiedzieć się więcej na temat automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="467da-126">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure Key Vault, follow these links to learn more about Azure Automation.</span></span>

* <span data-ttu-id="467da-127">Zobacz automatyzacji Azure [Wprowadzenie — samouczek](../automation/automation-first-runbook-graphical.md).</span><span class="sxs-lookup"><span data-stu-id="467da-127">See the Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md).</span></span>
* <span data-ttu-id="467da-128">Zobacz [skryptów programu PowerShell magazynu kluczy Azure](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5).</span><span class="sxs-lookup"><span data-stu-id="467da-128">See the [Azure Key Vault PowerShell scripts](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5).</span></span>

