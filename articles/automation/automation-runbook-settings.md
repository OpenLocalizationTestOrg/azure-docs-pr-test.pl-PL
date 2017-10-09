---
title: Ustawienia aaaRunbook | Dokumentacja firmy Microsoft
description: "W tym artykule opisano hello ustawienia konfiguracji dla elementu runbook automatyzacji Azure i w jaki sposób toochange je za pomocą obu hello portalu zarządzania Azure i programu Windows PowerShell."
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
ms.openlocfilehash: 6f0ef09c148355a351464424c22c33df9300f0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-settings"></a><span data-ttu-id="fa93d-103">Ustawienia elementu Runbook</span><span class="sxs-lookup"><span data-stu-id="fa93d-103">Runbook settings</span></span>
<span data-ttu-id="fa93d-104">Każdy element runbook automatyzacji Azure ma wiele ustawień, które ułatwiają toobe zidentyfikowane i toochange jego zachowania podczas rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="fa93d-104">Each runbook in Azure Automation has multiple settings that help it toobe identified and toochange its logging behavior.</span></span> <span data-ttu-id="fa93d-105">Każde z tych ustawień opisano poniżej; dołączono przez procedury dotyczące toomodify je.</span><span class="sxs-lookup"><span data-stu-id="fa93d-105">Each of these settings is described below followed by procedures on how toomodify them.</span></span>

## <a name="settings"></a><span data-ttu-id="fa93d-106">Ustawienia</span><span class="sxs-lookup"><span data-stu-id="fa93d-106">Settings</span></span>
### <a name="name-and-description"></a><span data-ttu-id="fa93d-107">Nazwa i opis</span><span class="sxs-lookup"><span data-stu-id="fa93d-107">Name and description</span></span>
<span data-ttu-id="fa93d-108">Nie można zmienić nazwy hello elementu runbook, po jego utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="fa93d-108">You cannot change hello name of a runbook after it has been created.</span></span> <span data-ttu-id="fa93d-109">Hello opis jest opcjonalny i może być zapasowej too512 znaków.</span><span class="sxs-lookup"><span data-stu-id="fa93d-109">hello Description is optional and can be up too512 characters.</span></span>

### <a name="tags"></a><span data-ttu-id="fa93d-110">Tagi</span><span class="sxs-lookup"><span data-stu-id="fa93d-110">Tags</span></span>
<span data-ttu-id="fa93d-111">Tagi dopuszczać możesz tooassign unikatowych słów i wyrażeń toohelp identyfikacji elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="fa93d-111">Tags allow you tooassign distinct words and phrases toohelp identify a runbook.</span></span> <span data-ttu-id="fa93d-112">Na przykład podczas przesyłania runbook toohello [galerii programu PowerShell](https://www.powershellgallery.com/), należy określić tooidentify tagi określonej kategorii hello runbook powinien być wyświetlany w.</span><span class="sxs-lookup"><span data-stu-id="fa93d-112">For example, when you submit a runbook toohello [PowerShell Gallery](https://www.powershellgallery.com/), you specify particular tags tooidentify which categories hello runbook should be listed in.</span></span> <span data-ttu-id="fa93d-113">Można określić wiele znaczników elementu runbook, oddzielając je przecinkami.</span><span class="sxs-lookup"><span data-stu-id="fa93d-113">You can specify multiple tags for a runbook by separating them with commas.</span></span>

### <a name="logging"></a><span data-ttu-id="fa93d-114">Rejestrowanie</span><span class="sxs-lookup"><span data-stu-id="fa93d-114">Logging</span></span>
<span data-ttu-id="fa93d-115">Domyślnie rekordy pełne i postępu nie są zapisywane toojob historii.</span><span class="sxs-lookup"><span data-stu-id="fa93d-115">By default, Verbose and Progress records are not written toojob history.</span></span> <span data-ttu-id="fa93d-116">Ustawienia hello toolog określonego elementu runbook można zmienić tych rekordów.</span><span class="sxs-lookup"><span data-stu-id="fa93d-116">You can change hello settings for a particular runbook toolog these records.</span></span> <span data-ttu-id="fa93d-117">Aby uzyskać więcej informacji o tych rekordów, zobacz [Runbook dane wyjściowe i komunikaty](automation-runbook-output-and-messages.md).</span><span class="sxs-lookup"><span data-stu-id="fa93d-117">For more information on these records, see [Runbook Output and Messages](automation-runbook-output-and-messages.md).</span></span>

## <a name="changing-runbook-settings"></a><span data-ttu-id="fa93d-118">Zmiana ustawień elementu runbook</span><span class="sxs-lookup"><span data-stu-id="fa93d-118">Changing runbook settings</span></span>

### <a name="changing-runbook-settings-with-hello-azure-portal"></a><span data-ttu-id="fa93d-119">Zmiana ustawień elementu runbook z hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="fa93d-119">Changing runbook settings with hello Azure portal</span></span>
<span data-ttu-id="fa93d-120">Możesz zmienić ustawienia elementu runbook w portalu Azure hello w hello **ustawienia** bloku hello elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="fa93d-120">You can change settings for a runbook in hello Azure portal from hello **Settings** blade for hello runbook.</span></span>

1. <span data-ttu-id="fa93d-121">Hello portalu Azure, wybierz **automatyzacji** , a następnie kliknij nazwę hello konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="fa93d-121">In hello Azure portal, select **Automation** and then then click hello name of an automation account.</span></span>
2. <span data-ttu-id="fa93d-122">Wybierz hello **elementów Runbook** kartę.</span><span class="sxs-lookup"><span data-stu-id="fa93d-122">Select hello **Runbooks** tab.</span></span>
3. <span data-ttu-id="fa93d-123">Kliknij nazwę hello elementu runbook i są bloku ustawienia ukierunkowanej toohello hello elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="fa93d-123">Click hello name of a runbook and you are directed toohello settings blade for hello runbook.</span></span> <span data-ttu-id="fa93d-124">W tym miejscu można określić lub zmodyfikować tagi, hello opis elementu runbook, konfigurowanie rejestrowania i ustawień śledzenia i dostęp do pomocy technicznej toohelp narzędzia do rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="fa93d-124">From here you can specify or modify tags, hello runbook description, configure logging and tracing settings, and access support tools toohelp you solve problems.</span></span>     

### <a name="changing-runbook-settings-with-windows-powershell"></a><span data-ttu-id="fa93d-125">Zmiana ustawień elementu runbook przy użyciu programu Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="fa93d-125">Changing runbook settings with Windows PowerShell</span></span>
<span data-ttu-id="fa93d-126">Można użyć hello [AzureRmAutomationRunbook zestaw](https://msdn.microsoft.com/library/mt603786.aspx) polecenia cmdlet toochange hello ustawienia elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="fa93d-126">You can use hello [Set-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603786.aspx) cmdlet toochange hello settings for a runbook.</span></span> <span data-ttu-id="fa93d-127">Jeśli chcesz toospecify wiele tagów można albo udostępnić tablica lub jeden ciąg parametr tagi toohello wartości rozdzielone przecinkami.</span><span class="sxs-lookup"><span data-stu-id="fa93d-127">If you want toospecify multiple tags, you can either provide an array or a single string with comma delimited values toohello Tags parameter.</span></span> <span data-ttu-id="fa93d-128">Możesz uzyskać bieżące znaczniki hello z hello [Get-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603728.aspx).</span><span class="sxs-lookup"><span data-stu-id="fa93d-128">You can get hello current tags with hello [Get-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603728.aspx).</span></span>

<span data-ttu-id="fa93d-129">Witaj następujące przykładowe polecenia pokazują, jak tooset hello właściwości elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="fa93d-129">hello following sample commands show how tooset hello properties for a runbook.</span></span> <span data-ttu-id="fa93d-130">W tym przykładzie dodaje trzy znaczniki istniejących toohello znaczniki i określa, że powinny być rejestrowane rekordów pełnych.</span><span class="sxs-lookup"><span data-stu-id="fa93d-130">This sample adds three tags toohello existing tags and specifies that verbose records should be logged.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $tags = (Get-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName).Tags
    $tags += "Tag1,Tag2,Tag3"
    Set-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName –LogVerbose $true –Tags $tags

## <a name="next-steps"></a><span data-ttu-id="fa93d-131">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fa93d-131">Next steps</span></span>
* <span data-ttu-id="fa93d-132">toolearn toocreate i pobrać dane wyjściowe i komunikaty o błędach z elementami runbook, zobacz temat [Runbook dane wyjściowe i komunikaty](automation-runbook-output-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="fa93d-132">toolearn how toocreate and retrieve output and error messages from runbooks, see [Runbook Output and Messages](automation-runbook-output-and-messages.md)</span></span> 
* <span data-ttu-id="fa93d-133">toounderstand jak wyświetlić tooadd elementu runbook, który został już opracowany przez społeczność hello lub inne źródło lub toocreate własne runbook [Tworzenie lub importowanie elementu Runbook](automation-creating-importing-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="fa93d-133">toounderstand how tooadd a runbook that was already developed by hello community or other source, or toocreate your own runbook see [Creating or Importing a Runbook](automation-creating-importing-runbook.md)</span></span> 

