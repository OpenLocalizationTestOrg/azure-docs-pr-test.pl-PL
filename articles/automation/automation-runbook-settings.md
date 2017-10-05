---
title: Ustawienia elementu Runbook | Dokumentacja firmy Microsoft
description: "W tym artykule opisano ustawienia konfiguracji dla elementu runbook w automatyzacji Azure oraz sposobu zmiany ich za pomocą portalu zarządzania Azure i programu Windows PowerShell."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: a726f20c-a952-48b8-88ee-36d76aa3ac61
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/11/2016
ms.author: bwren
ms.openlocfilehash: 20ecbc270e61d234e026e6ba2634c7aad63b3355
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="runbook-settings"></a><span data-ttu-id="86893-103">Ustawienia elementu Runbook</span><span class="sxs-lookup"><span data-stu-id="86893-103">Runbook settings</span></span>
<span data-ttu-id="86893-104">Każdy element runbook automatyzacji Azure ma wiele ustawień, które ułatwiają jego identyfikację i zmianę jego zachowania rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="86893-104">Each runbook in Azure Automation has multiple settings that help it to be identified and to change its logging behavior.</span></span> <span data-ttu-id="86893-105">Każde z tych ustawień opisano poniżej; dołączono instrukcji na temat sposobu ich modyfikacji.</span><span class="sxs-lookup"><span data-stu-id="86893-105">Each of these settings is described below followed by procedures on how to modify them.</span></span>

## <a name="settings"></a><span data-ttu-id="86893-106">Ustawienia</span><span class="sxs-lookup"><span data-stu-id="86893-106">Settings</span></span>
### <a name="name-and-description"></a><span data-ttu-id="86893-107">Nazwa i opis</span><span class="sxs-lookup"><span data-stu-id="86893-107">Name and description</span></span>
<span data-ttu-id="86893-108">Nie można zmienić nazwy elementu runbook, po jego utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="86893-108">You cannot change the name of a runbook after it has been created.</span></span> <span data-ttu-id="86893-109">Opis jest opcjonalny i może zawierać maksymalnie 512 znaków.</span><span class="sxs-lookup"><span data-stu-id="86893-109">The Description is optional and can be up to 512 characters.</span></span>

### <a name="tags"></a><span data-ttu-id="86893-110">Tagi</span><span class="sxs-lookup"><span data-stu-id="86893-110">Tags</span></span>
<span data-ttu-id="86893-111">Znaczniki umożliwiają przypisywanie unikatowych słów i wyrażeń w celu ułatwienia identyfikacji elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="86893-111">Tags allow you to assign distinct words and phrases to help identify a runbook.</span></span> <span data-ttu-id="86893-112">Na przykład gdy przesłać elementu runbook [galerii programu PowerShell](https://www.powershellgallery.com/), określ określonego znaczniki, aby zidentyfikować elementu runbook powinien być wyświetlany w kategorii.</span><span class="sxs-lookup"><span data-stu-id="86893-112">For example, when you submit a runbook to the [PowerShell Gallery](https://www.powershellgallery.com/), you specify particular tags to identify which categories the runbook should be listed in.</span></span> <span data-ttu-id="86893-113">Można określić wiele znaczników elementu runbook, oddzielając je przecinkami.</span><span class="sxs-lookup"><span data-stu-id="86893-113">You can specify multiple tags for a runbook by separating them with commas.</span></span>

### <a name="logging"></a><span data-ttu-id="86893-114">Rejestrowanie</span><span class="sxs-lookup"><span data-stu-id="86893-114">Logging</span></span>
<span data-ttu-id="86893-115">Domyślnie rekordy pełne i postępu nie są zapisywane w historii zadań.</span><span class="sxs-lookup"><span data-stu-id="86893-115">By default, Verbose and Progress records are not written to job history.</span></span> <span data-ttu-id="86893-116">Można zmienić ustawienia określonego elementu runbook, aby zapisywać te rekordy.</span><span class="sxs-lookup"><span data-stu-id="86893-116">You can change the settings for a particular runbook to log these records.</span></span> <span data-ttu-id="86893-117">Aby uzyskać więcej informacji o tych rekordów, zobacz [Runbook dane wyjściowe i komunikaty](automation-runbook-output-and-messages.md).</span><span class="sxs-lookup"><span data-stu-id="86893-117">For more information on these records, see [Runbook Output and Messages](automation-runbook-output-and-messages.md).</span></span>

## <a name="changing-runbook-settings"></a><span data-ttu-id="86893-118">Zmiana ustawień elementu runbook</span><span class="sxs-lookup"><span data-stu-id="86893-118">Changing runbook settings</span></span>

### <a name="changing-runbook-settings-with-the-azure-portal"></a><span data-ttu-id="86893-119">Zmiana ustawień elementu runbook w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="86893-119">Changing runbook settings with the Azure portal</span></span>
<span data-ttu-id="86893-120">Możesz zmienić ustawienia dla elementu runbook w portalu Azure z **ustawienia** bloku dla elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="86893-120">You can change settings for a runbook in the Azure portal from the **Settings** blade for the runbook.</span></span>

1. <span data-ttu-id="86893-121">W portalu Azure wybierz **automatyzacji** , a następnie kliknij nazwę konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="86893-121">In the Azure portal, select **Automation** and then then click the name of an automation account.</span></span>
2. <span data-ttu-id="86893-122">Wybierz **elementów Runbook** kartę.</span><span class="sxs-lookup"><span data-stu-id="86893-122">Select the **Runbooks** tab.</span></span>
3. <span data-ttu-id="86893-123">Kliknij nazwę elementu runbook i użytkownik jest kierowany do bloku ustawienia dla elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="86893-123">Click the name of a runbook and you are directed to the settings blade for the runbook.</span></span> <span data-ttu-id="86893-124">W tym miejscu można określić lub Zmień tagi, opis elementu runbook, konfigurowanie ustawień śledzenia i rejestrowania, a także dostęp do narzędzia obsługi, aby pomóc w rozwiązywaniu problemów.</span><span class="sxs-lookup"><span data-stu-id="86893-124">From here you can specify or modify tags, the runbook description, configure logging and tracing settings, and access support tools to help you solve problems.</span></span>     

### <a name="changing-runbook-settings-with-windows-powershell"></a><span data-ttu-id="86893-125">Zmiana ustawień elementu runbook przy użyciu programu Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="86893-125">Changing runbook settings with Windows PowerShell</span></span>
<span data-ttu-id="86893-126">Można użyć [AzureRmAutomationRunbook zestaw](https://msdn.microsoft.com/library/mt603786.aspx) polecenia cmdlet, aby zmienić ustawienia dla elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="86893-126">You can use the [Set-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603786.aspx) cmdlet to change the settings for a runbook.</span></span> <span data-ttu-id="86893-127">Jeśli chcesz określić wiele znaczników można albo udostępnić tablica lub jeden ciąg rozdzielany przecinkami wartości do parametru tagów.</span><span class="sxs-lookup"><span data-stu-id="86893-127">If you want to specify multiple tags, you can either provide an array or a single string with comma delimited values to the Tags parameter.</span></span> <span data-ttu-id="86893-128">Możesz uzyskać bieżące znaczniki z [Get-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603728.aspx).</span><span class="sxs-lookup"><span data-stu-id="86893-128">You can get the current tags with the [Get-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603728.aspx).</span></span>

<span data-ttu-id="86893-129">Następujące przykładowe polecenia pokazują, jak można ustawić właściwości dla elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="86893-129">The following sample commands show how to set the properties for a runbook.</span></span> <span data-ttu-id="86893-130">W tym przykładzie dodaje trzy znaczniki do istniejących tagów i określa, że powinny być rejestrowane rekordów pełnych.</span><span class="sxs-lookup"><span data-stu-id="86893-130">This sample adds three tags to the existing tags and specifies that verbose records should be logged.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $tags = (Get-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName).Tags
    $tags += "Tag1,Tag2,Tag3"
    Set-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName –LogVerbose $true –Tags $tags

## <a name="next-steps"></a><span data-ttu-id="86893-131">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="86893-131">Next steps</span></span>
* <span data-ttu-id="86893-132">Aby dowiedzieć się, jak utworzyć i pobrać dane wyjściowe i komunikaty o błędach z elementów runbook, zobacz [Runbook dane wyjściowe i komunikaty](automation-runbook-output-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="86893-132">To learn how to create and retrieve output and error messages from runbooks, see [Runbook Output and Messages](automation-runbook-output-and-messages.md)</span></span> 
* <span data-ttu-id="86893-133">Zrozumienie, jak można dodać elementu runbook, który już został opracowany przez społeczność lub inne źródło lub utworzyć własne można znaleźć elementu runbook [Tworzenie lub importowanie elementu Runbook](automation-creating-importing-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="86893-133">To understand how to add a runbook that was already developed by the community or other source, or to create your own runbook see [Creating or Importing a Runbook](automation-creating-importing-runbook.md)</span></span> 

