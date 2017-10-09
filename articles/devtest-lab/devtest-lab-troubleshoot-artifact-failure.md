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
# <a name="diagnose-artifact-failures-in-hello-lab"></a>Diagnozowanie błędów artefaktów w laboratorium hello 
Po utworzeniu artefaktu, można sprawdzić toosee, jeśli zakończyło się pomyślnie, lub nie powiodło się. Dzienniki artefaktów w usłudze DevTest Labs zawierają informacje, których można użyć toodiagnose błąd artefaktu. Istnieje kilka sposobów, można wyświetlić informacje dziennika hello artefaktu maszyny Wirtualnej systemu Windows.

> [!NOTE]
> tooensure błędy są poprawnie zidentyfikowane i wyjaśniono, należy pamiętać, że tego artefaktu hello jest nieprawidłową strukturę. Aby dowiedzieć się jak toocorrectly tworzenia artefaktu, zobacz [Tworzenie niestandardowych artefaktów](devtest-lab-artifact-author.md). I toosee przykładem prawidłowo strukturalnych artefaktu, zapoznaj się z tym [typy parametrów testu](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts/windows-test-paramtypes) artefaktu.

## <a name="troubleshoot-artifact-failures-using-hello-azure-portal"></a>Rozwiązywanie problemów z awariami artefaktów przy użyciu hello portalu Azure
toouse hello Azure toodiagnose portalu błędów podczas tworzenia artefaktu, wykonaj następujące kroki:

1. Z listy hello zasobów wybierz laboratorium.

2. Wybierz maszynę Wirtualną systemu Windows, która obejmuje hello artefaktu ma tooinvestigate hello.

3. W lewym panelu hello w obszarze **ogólne**, wybierz **artefakty**. Artefakty skojarzone z tej maszyny Wirtualnej zostanie wyświetlona lista, wskazujące nazwę hello hello artefaktów i jego stan.

   ![Przykład repozytorium git artefaktów](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifacts-failure.png)

4. Wybierz artefaktu, który zawiera stan ****. artefaktu Hello otwiera i pokazuje rozszerzenie komunikat o błędzie zawiera szczegóły dotyczące błędu hello hello artefaktu.

   ![Przykład repozytorium git artefaktów](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifact-error.png)


## <a name="troubleshoot-artifact-failures-from-within-hello-vm"></a>Rozwiązywanie błędów artefaktów z wewnątrz hello maszyny Wirtualnej
tooview hello artefaktu dzienników z poziomu maszyny wirtualnej hello, wykonaj następujące kroki:

1. Zaloguj się za toohello maszynę Wirtualną, która zawiera hello artefaktu ma toodiagnose.

2. Przejdź tooC:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.9\Status gdzie "1.9 jest numer wersji hello rozszerzenie klienta.

   ![Przykład repozytorium git artefaktów](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifact-error-vm-status.png)

3. Otwórz hello **stan** pliku tooview informacje, że ułatwia diagnozowanie błędów artefaktu dla tej maszyny Wirtualnej.




[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>Wpisy na blogu pokrewne
* [Dołącz do maszyny Wirtualnej tooexisting domeny AD przy użyciu szablonu usługi resource manager w usłudze Azure DevTest Labs](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a>Następne kroki
* Dowiedz się, jak za[Dodawanie laboratorium tooa repozytorium Git](devtest-lab-add-artifact-repo.md).

