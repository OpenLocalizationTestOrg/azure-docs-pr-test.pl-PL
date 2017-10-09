---
title: "aaaManage usługi Azure Key Vault przy użyciu automatyzacji Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat sposobu hello usługi Automatyzacja Azure może być używane toomanage usługi Azure Key Vault."
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
ms.openlocfilehash: 7f46ecc1206a96e8aeb1d086285461cb5b205472
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-key-vault-using-azure-automation"></a><span data-ttu-id="40ab2-103">Zarządzanie usługą Azure Key Vault za pomocą usługi Automatyzacja Azure</span><span class="sxs-lookup"><span data-stu-id="40ab2-103">Managing Azure Key Vault using Azure Automation</span></span>
<span data-ttu-id="40ab2-104">W tym przewodniku przedstawiono usługi Automatyzacja Azure toohello i jak mogą być używane toosimplify zarządzania kluczy i kluczy tajnych w magazynie kluczy Azure.</span><span class="sxs-lookup"><span data-stu-id="40ab2-104">This guide will introduce you toohello Azure Automation service and how it can be used toosimplify management of your keys and secrets in Azure Key Vault.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="40ab2-105">Co to jest Azure Automation?</span><span class="sxs-lookup"><span data-stu-id="40ab2-105">What is Azure Automation?</span></span>
<span data-ttu-id="40ab2-106">[Automatyzacja Azure](../automation/automation-intro.md) jest usługą platformy Azure, dla uproszczenia zarządzania chmurą za pośrednictwem automatyzacji procesu i konfiguracji żądanego stanu.</span><span class="sxs-lookup"><span data-stu-id="40ab2-106">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation and desired state configuration.</span></span> <span data-ttu-id="40ab2-107">Zadania ręczne, powtarzane długotrwałe i podatne na błędy przy użyciu usługi Automatyzacja Azure, może być automatycznych tooincrease niezawodności, wydajności i toovalue czasu dla Twojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="40ab2-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="40ab2-108">Automatyzacja Azure umożliwia aparatowi wykonywania przepływów pracy wysoce niezawodne, wysokiej dostępności, która może obsłużyć toomeet potrzeb.</span><span class="sxs-lookup"><span data-stu-id="40ab2-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales toomeet your needs.</span></span> <span data-ttu-id="40ab2-109">W automatyzacji Azure procesów może być rozpoczęte ręcznie, przez systemy 3rd firmy lub w zaplanowanych odstępach czasu tak, aby zadania stanie dokładnie w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="40ab2-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="40ab2-110">Obniżenie kosztów operacyjnych i zwolnić IT i toofocus personelu DevOps pracy dodającego wartość biznesową, przenosząc toobe zadań zarządzania z chmury uruchamiane automatycznie przez usługi Automatyzacja Azure.</span><span class="sxs-lookup"><span data-stu-id="40ab2-110">Reduce operational overhead and free up IT and DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-key-vault"></a><span data-ttu-id="40ab2-111">Jak usługi Automatyzacja Azure ułatwia zarządzanie usługą Azure Key Vault?</span><span class="sxs-lookup"><span data-stu-id="40ab2-111">How can Azure Automation help manage Azure Key Vault?</span></span>
<span data-ttu-id="40ab2-112">Magazyn kluczy można zarządzać w automatyzacji Azure za pomocą hello [poleceń cmdlet usługi Key Vault AzureRM](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) i [poleceń cmdlet klasycznej usługi Azure Key Vault](https://msdn.microsoft.com/library/azure/dn868052.aspx).</span><span class="sxs-lookup"><span data-stu-id="40ab2-112">Key Vault can be managed in Azure Automation by using hello [AzureRM Key Vault cmdlets](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) and [Azure Classic Key Vault cmdlets](https://msdn.microsoft.com/library/azure/dn868052.aspx).</span></span> <span data-ttu-id="40ab2-113">Hello Azure modułu Zarządzanie klasycznym usługi Key Vault jest dostępny automatycznie w automatyzacji Azure i zaimportować hello [AzureRM KeyVault modułu](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) w automatyzacji Azure tak, aby można było wykonać wiele zarządzania infrastrukturą usługi Key Vault zadania w ramach usługi hello.</span><span class="sxs-lookup"><span data-stu-id="40ab2-113">hello Azure module for managing classic Key Vault is available automatically in Azure Automation, and you can import hello [AzureRM-KeyVault module](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) into Azure Automation, so that you can perform many of your Key Vault management tasks within hello service.</span></span> <span data-ttu-id="40ab2-114">Tych poleceń cmdlet usługi Automatyzacja Azure, za pomocą poleceń cmdlet powitania dla innych usług platformy Azure, tooautomate złożone zadania może również łączyć 3 systemów firm i usług Azure.</span><span class="sxs-lookup"><span data-stu-id="40ab2-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="40ab2-115">Za pomocą poleceń cmdlet usługi Azure Key Vault hello można wykonać te zadania, między innymi:</span><span class="sxs-lookup"><span data-stu-id="40ab2-115">With hello Azure Key Vault cmdlets you can perform these tasks among others:</span></span> 

* <span data-ttu-id="40ab2-116">Tworzenie i Konfigurowanie magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="40ab2-116">Create and configure a key vault</span></span>
* <span data-ttu-id="40ab2-117">Tworzenie lub Importowanie klucza</span><span class="sxs-lookup"><span data-stu-id="40ab2-117">Create or import a key</span></span>
* <span data-ttu-id="40ab2-118">Utwórz lub zaktualizuj klucz tajny</span><span class="sxs-lookup"><span data-stu-id="40ab2-118">Create or update a secret</span></span>
* <span data-ttu-id="40ab2-119">Atrybuty aktualizacji klucza</span><span class="sxs-lookup"><span data-stu-id="40ab2-119">Update attributes of a key</span></span>
* <span data-ttu-id="40ab2-120">Pobierz klucz lub klucz tajny</span><span class="sxs-lookup"><span data-stu-id="40ab2-120">Get a key or secret</span></span>
* <span data-ttu-id="40ab2-121">Usuwanie klucza lub klucza tajnego</span><span class="sxs-lookup"><span data-stu-id="40ab2-121">Delete a key or secret</span></span>

<span data-ttu-id="40ab2-122">Oto kilka przykładów przy użyciu programu PowerShell toomanage Key Vault:</span><span class="sxs-lookup"><span data-stu-id="40ab2-122">Here are some examples of using PowerShell toomanage Key Vault:</span></span>  

* [<span data-ttu-id="40ab2-123">Usługi Azure Key Vault - krok po kroku</span><span class="sxs-lookup"><span data-stu-id="40ab2-123">Azure Key Vault - Step by Step</span></span>](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step)
* [<span data-ttu-id="40ab2-124">Instalowanie i konfigurowanie usługi Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="40ab2-124">Setting Up and Configuring an Azure Key Vault</span></span>](https://www.simple-talk.com/cloud/platform-as-a-service/setting-up-and-configuring-an-azure-key-vault)

## <a name="next-steps"></a><span data-ttu-id="40ab2-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="40ab2-125">Next steps</span></span>
<span data-ttu-id="40ab2-126">Teraz, kiedy znasz już podstawy hello usługi Automatyzacja Azure i jak mogą być używane toomanage usługi Azure Key Vault, wykonaj te toolearn łącza więcej informacji na temat automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="40ab2-126">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure Key Vault, follow these links toolearn more about Azure Automation.</span></span>

* <span data-ttu-id="40ab2-127">Zobacz hello usługi Automatyzacja Azure [Wprowadzenie — samouczek](../automation/automation-first-runbook-graphical.md).</span><span class="sxs-lookup"><span data-stu-id="40ab2-127">See hello Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md).</span></span>
* <span data-ttu-id="40ab2-128">Zobacz hello [skryptów programu PowerShell magazynu kluczy Azure](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5).</span><span class="sxs-lookup"><span data-stu-id="40ab2-128">See hello [Azure Key Vault PowerShell scripts](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5).</span></span>

