---
title: "błędy artefaktu aaaDiagnose w maszynie Wirtualnej platformy Azure DevTest Labs | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak błędy artefaktu tootroubleshoot w usłudze DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 115e0086-3293-4adf-8738-9f639f31f918
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: tarcher
ms.openlocfilehash: 40b3cea72cf071cc5d9a6d002d309d923c3d3084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-artifact-failures-in-hello-lab"></a><span data-ttu-id="5e326-103">Diagnozowanie błędów artefaktów w laboratorium hello</span><span class="sxs-lookup"><span data-stu-id="5e326-103">Diagnose artifact failures in hello lab</span></span> 
<span data-ttu-id="5e326-104">Po utworzeniu artefaktu, można sprawdzić toosee, jeśli zakończyło się pomyślnie, lub nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="5e326-104">After you have created an artifact, you can check toosee if it succeeded or failed.</span></span> <span data-ttu-id="5e326-105">Dzienniki artefaktów w usłudze DevTest Labs zawierają informacje, których można użyć toodiagnose błąd artefaktu.</span><span class="sxs-lookup"><span data-stu-id="5e326-105">Artifact logs in DevTest Labs provide information you can use toodiagnose an artifact failure.</span></span> <span data-ttu-id="5e326-106">Istnieje kilka sposobów, można wyświetlić informacje dziennika hello artefaktu maszyny Wirtualnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="5e326-106">There are a couple different ways you can view hello artifact log information for a Windows VM.</span></span>

> [!NOTE]
> <span data-ttu-id="5e326-107">tooensure błędy są poprawnie zidentyfikowane i wyjaśniono, należy pamiętać, że tego artefaktu hello jest nieprawidłową strukturę.</span><span class="sxs-lookup"><span data-stu-id="5e326-107">tooensure that failures are correctly identified and explained, it is important that hello artifact is properly structured.</span></span> <span data-ttu-id="5e326-108">Aby dowiedzieć się jak toocorrectly tworzenia artefaktu, zobacz [Tworzenie niestandardowych artefaktów](devtest-lab-artifact-author.md).</span><span class="sxs-lookup"><span data-stu-id="5e326-108">For information about how toocorrectly construct an artifact, see [Create custom artifacts](devtest-lab-artifact-author.md).</span></span> <span data-ttu-id="5e326-109">I toosee przykładem prawidłowo strukturalnych artefaktu, zapoznaj się z tym [typy parametrów testu](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts/windows-test-paramtypes) artefaktu.</span><span class="sxs-lookup"><span data-stu-id="5e326-109">And toosee an example of a properly structured artifact, check out this [Test Parameter Types](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts/windows-test-paramtypes) artifact.</span></span>

## <a name="troubleshoot-artifact-failures-using-hello-azure-portal"></a><span data-ttu-id="5e326-110">Rozwiązywanie problemów z awariami artefaktów przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="5e326-110">Troubleshoot artifact failures using hello Azure portal</span></span>
<span data-ttu-id="5e326-111">toouse hello Azure toodiagnose portalu błędów podczas tworzenia artefaktu, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="5e326-111">toouse hello Azure portal toodiagnose failures during artifact creation, follow these steps:</span></span>

1. <span data-ttu-id="5e326-112">Z listy hello zasobów wybierz laboratorium.</span><span class="sxs-lookup"><span data-stu-id="5e326-112">From hello list of resources, select your lab.</span></span>

2. <span data-ttu-id="5e326-113">Wybierz maszynę Wirtualną systemu Windows, która obejmuje hello artefaktu ma tooinvestigate hello.</span><span class="sxs-lookup"><span data-stu-id="5e326-113">Choose hello Windows VM that includes hello artifact you want tooinvestigate.</span></span>

3. <span data-ttu-id="5e326-114">W lewym panelu hello w obszarze **ogólne**, wybierz **artefakty**.</span><span class="sxs-lookup"><span data-stu-id="5e326-114">In hello left panel under **GENERAL**, choose **Artifacts**.</span></span> <span data-ttu-id="5e326-115">Artefakty skojarzone z tej maszyny Wirtualnej zostanie wyświetlona lista, wskazujące nazwę hello hello artefaktów i jego stan.</span><span class="sxs-lookup"><span data-stu-id="5e326-115">A list of artifacts associated with that VM appears, indicating hello name of hello artifact and its status.</span></span>

   ![Przykład repozytorium git artefaktów](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifacts-failure.png)

4. <span data-ttu-id="5e326-117">Wybierz artefaktu, który zawiera stan ****.</span><span class="sxs-lookup"><span data-stu-id="5e326-117">Choose an artifact that shows a status of **Failed**.</span></span> <span data-ttu-id="5e326-118">artefaktu Hello otwiera i pokazuje rozszerzenie komunikat o błędzie zawiera szczegóły dotyczące błędu hello hello artefaktu.</span><span class="sxs-lookup"><span data-stu-id="5e326-118">hello artifact opens and shows an extension message that includes details about hello failure of hello artifact.</span></span>

   ![Przykład repozytorium git artefaktów](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifact-error.png)


## <a name="troubleshoot-artifact-failures-from-within-hello-vm"></a><span data-ttu-id="5e326-120">Rozwiązywanie błędów artefaktów z wewnątrz hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="5e326-120">Troubleshoot artifact failures from within hello VM</span></span>
<span data-ttu-id="5e326-121">tooview hello artefaktu dzienników z poziomu maszyny wirtualnej hello, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="5e326-121">tooview hello artifact logs from within hello virtual machine, follow these steps:</span></span>

1. <span data-ttu-id="5e326-122">Zaloguj się za toohello maszynę Wirtualną, która zawiera hello artefaktu ma toodiagnose.</span><span class="sxs-lookup"><span data-stu-id="5e326-122">Log in toohello VM that contains hello artifact you want toodiagnose.</span></span>

2. <span data-ttu-id="5e326-123">Przejdź tooC:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.9\Status gdzie "1.9 jest numer wersji hello rozszerzenie klienta.</span><span class="sxs-lookup"><span data-stu-id="5e326-123">Navigate tooC:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.9\Status where "1.9 is hello CSE version number.</span></span>

   ![Przykład repozytorium git artefaktów](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifact-error-vm-status.png)

3. <span data-ttu-id="5e326-125">Otwórz hello **stan** pliku tooview informacje, że ułatwia diagnozowanie błędów artefaktu dla tej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5e326-125">Open hello **status** file tooview information that helps diagnose artifact failures for that VM.</span></span>




[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="5e326-126">Wpisy na blogu pokrewne</span><span class="sxs-lookup"><span data-stu-id="5e326-126">Related blog posts</span></span>
* [<span data-ttu-id="5e326-127">Dołącz do maszyny Wirtualnej tooexisting domeny AD przy użyciu szablonu usługi resource manager w usłudze Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="5e326-127">Join a VM tooexisting AD Domain using a resource manager template in Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a><span data-ttu-id="5e326-128">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5e326-128">Next steps</span></span>
* <span data-ttu-id="5e326-129">Dowiedz się, jak za[Dodawanie laboratorium tooa repozytorium Git](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="5e326-129">Learn how too[add a Git repository tooa lab](devtest-lab-add-artifact-repo.md).</span></span>

