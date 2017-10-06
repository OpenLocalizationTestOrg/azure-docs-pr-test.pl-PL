---
title: "aaaCreate laboratorium w usłudze Azure DevTest Labs | Dokumentacja firmy Microsoft"
description: "Tworzenie laboratorium w usłudze Azure DevTest Labs na potrzeby maszyn wirtualnych"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 8b6d3e70-6528-42a4-a2ef-449575d0f928
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/30/2017
ms.author: tarcher
ms.openlocfilehash: 2ec5498f10e0cc06a196a71e319e340937abb1a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-lab-in-azure-devtest-labs"></a>Tworzenie laboratorium w usłudze Azure DevTest Labs
Laboratorium w usłudze Azure DevTest Labs jest hello infrastruktury, który obejmuje grupy zasobów, takich jak maszyn wirtualnych (VM), które umożliwiają lepsze zarządzanie tych zasobów, określając ograniczenia i limity przydziału. Ten artykuł przeprowadzi Cię przez proces tworzenia laboratorium przy użyciu portalu Azure hello hello.

## <a name="prerequisites"></a>Wymagania wstępne
toocreate laboratorium, potrzebne są:

* Subskrypcja platformy Azure. toolearn o opcjami zakupu platformy Azure, zobacz [jak toobuy Azure](https://azure.microsoft.com/pricing/purchase-options/) lub [bezpłatna miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/). Musi być właścicielem hello hello subskrypcji toocreate hello laboratorium.

## <a name="steps-toocreate-a-lab-in-azure-devtest-labs"></a>Kroki toocreate laboratorium w usłudze Azure DevTest Labs
Witaj następujące kroki pokazują, jak toouse hello Azure toocreate portalu laboratorium w usłudze Azure DevTest Labs. 

1. Zaloguj się toohello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Wybierz z menu głównego powitania po lewej stronie powitania, **więcej usług** (u dołu hello hello listy).

    ![Opcja menu Więcej usług](./media/devtest-lab-create-lab/more-services-menu-option.png)

1. Z listy dostępnych usług, hello **DevTest Labs**.
1. Na powitania **DevTest Labs** bloku, wybierz opcję **Dodaj**.
   
    ![Dodawanie laboratorium](./media/devtest-lab-create-lab/add-lab-button.png)

1. Na powitania **Utwórz laboratorium DevTest Lab** bloku:
   
    1. Wprowadź **Nazwa laboratorium** dla nowego laboratorium hello.
    2. Wybierz hello **subskrypcji** tooassociate z hello laboratorium.
    3. Wybierz **lokalizacji** w których toostore hello laboratorium.
    4. Wybierz **automatyczne zamykanie** toospecify tooenable - i definiować parametry hello — Witaj, automatyczne zamykanie hello laboratorium wszystkich maszyn wirtualnych. Witaj automatyczne zamykanie funkcja jest głównie funkcji oszczędności zgodnie z którymi można określić, kiedy zechcesz hello wirtualna tooautomatically można zamknąć. Ustawienia automatycznego zamykania można zmienić po utworzeniu laboratorium hello hello wykonaj czynności opisane w artykule hello [zarządzanie wszystkimi zasadami dla laboratorium w usłudze Azure DevTest Labs](./devtest-lab-set-lab-policy.md#set-auto-shutdown).
    5. Wybierz **tooDashboard numeru Pin** Jeśli skrót tooappear laboratorium hello na powitania pulpitu nawigacyjnego portalu.
    6. Wybierz **opcje automatyzacji** tooget szablonów usługi Azure Resource Manager dla konfiguracji usługi Automatyzacja. 
    7. Wybierz pozycję **Utwórz**. Po wybraniu **Utwórz**, hello **DevTest Labs** wyświetla bloku. Możesz monitorować stan hello procesu tworzenia laboratorium hello obserwując hello **powiadomienia** obszaru. Po ukończeniu odświeżania hello strony toosee hello nowo utworzony w hello lista labs laboratorium.  
    
    ![Blok tworzenia laboratorium](./media/devtest-lab-create-lab/create-devtestlab-blade.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Następne kroki
Po utworzeniu laboratorium, poniżej przedstawiono niektóre dalej tooconsider kroki:

* [Bezpieczny dostęp tooa laboratorium](devtest-lab-add-devtest-user.md).
* [Set lab policies](devtest-lab-set-lab-policy.md) (Ustawianie zasad laboratorium).
* [Create a lab template](devtest-lab-create-template.md) (Tworzenie szablonu laboratorium).
* [Create custom artifacts for your VMs](devtest-lab-artifact-author.md) (Tworzenie niestandardowych artefaktów dla maszyn wirtualnych).
* [Dodawanie maszyny Wirtualnej z laboratorium tooa artefakty](https://azure.microsoft.com/resources/videos/how-to-create-vms-with-artifacts-in-a-devtest-lab/).

