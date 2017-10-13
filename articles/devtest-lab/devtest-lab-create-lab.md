---
title: "Tworzenie laboratorium w usłudze Azure DevTest Labs | Microsoft Docs"
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
ms.date: 09/07/2017
ms.author: tarcher
ms.openlocfilehash: 9657a4681f6bd9cc126de50883ce7a66357156e0
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="create-a-lab-in-azure-devtest-labs"></a>Tworzenie laboratorium w usłudze Azure DevTest Labs
Azure DevTest Labs to infrastruktura, która obejmuje wiele różnych zasobów (np. maszyn wirtualnych) i umożliwia lepsze zarządzanie tymi zasobami przez określenie ograniczeń i przydziałów. W tym artykule szczegółowo omówiono proces tworzenia laboratorium przy użyciu witryny Azure Portal.

## <a name="prerequisites"></a>Wymagania wstępne
Aby utworzyć laboratorium, potrzebne są:

* Subskrypcja platformy Azure. Aby zapoznać się z opcjami zakupu platformy Azure, zobacz [Jak kupić system Azure](https://azure.microsoft.com/pricing/purchase-options/) lub [Bezpłatna miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/). Aby utworzyć laboratorium, trzeba być właścicielem subskrypcji.

## <a name="steps-to-create-a-lab-in-azure-devtest-labs"></a>Procedura tworzenia laboratorium w usłudze Azure DevTest Labs
Następujące kroki ilustrują tworzenie laboratorium w usłudze Azure DevTest Labs przy użyciu witryny Azure Portal. 

1. Zaloguj się w witrynie [Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Z menu głównego po lewej stronie wybierz pozycję **Więcej usług** (w dolnej części listy).

    ![Opcja menu Więcej usług](./media/devtest-lab-create-lab/more-services-menu-option.png)

1. Z listy dostępnych usług wybierz pozycję **DevTest Labs**.
1. W obszarze **DevTest Labs** wybierz pozycję **Dodaj**.
   
    ![Dodawanie laboratorium](./media/devtest-lab-create-lab/add-lab-button.png)

1. W obszarze **Tworzenie laboratorium DevTest Lab**:
   
    1. W polu **Nazwa laboratorium** wprowadź nazwę dla nowego laboratorium.
    2. W pozycji **Subskrypcja** wybierz subskrypcję do skojarzenia z laboratorium.
    3. W pozycji **Lokalizacja** wybierz lokalizację do przechowywania laboratorium.
    4. Wybierz pozycję **Automatyczne zamykanie**, aby włączyć opcję i określić parametry automatycznego zamykania wszystkich maszyn wirtualnych laboratorium. Funkcja automatycznego zamykania służy głównie do osiągnięcia oszczędności. Pozwala określić, kiedy ma dojść do automatycznego zamknięcia maszyny wirtualnej. Ustawienia automatycznego zamykania można zmienić po utworzeniu laboratorium, wykonując czynności opisane w artykule [Manage all policies for a lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md#set-auto-shutdown) (Zarządzanie wszystkimi zasadami dla laboratorium w usłudze Azure DevTest Labs).
    1. Wprowadź informacje w polach **NAZWA** i **WARTOŚĆ** w obszarze **Tagi**, jeśli chcesz utworzyć niestandardowe tagowanie, które będzie dodawane do każdego zasobu utworzonego w laboratorium. Tagi są przydatne do porządkowania zasobów laboratorium według kategorii i zarządzania nimi. Aby uzyskać więcej informacji na temat tagów, w tym na temat sposobu dodawania tagów po utworzeniu laboratorium, zobacz [Dodawanie tagów do laboratorium](devtest-lab-add-tag.md).
    5. Wybierz pozycję **Przypnij do pulpitu nawigacyjnego**, jeśli chcesz, aby na pulpicie nawigacyjnym portalu był wyświetlany skrót do laboratorium.
    6. Wybierz pozycję **Opcje automatyzacji**, aby uzyskać szablony usługi Azure Resource Manager dotyczące automatyzacji konfiguracji. 
    7. Wybierz pozycję **Utwórz**. Stan procesu tworzenia laboratorium można monitorować, obserwując obszar **Powiadomienia**. Po ukończeniu odśwież stronę, aby wyświetlić nowo utworzone laboratorium na liście laboratoriów.  
    
    ![Tworzenie sekcji laboratorium usługi DevTest Labs](./media/devtest-lab-create-lab/create-devtestlab-blade.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Następne kroki
Po utworzeniu laboratorium warto rozważyć poniższe kroki:

* [Secure access to a lab](devtest-lab-add-devtest-user.md) (Zabezpieczanie dostępu do laboratorium).
* [Set lab policies](devtest-lab-set-lab-policy.md) (Ustawianie zasad laboratorium).
* [Create a lab template](devtest-lab-create-template.md) (Tworzenie szablonu laboratorium).
* [Create custom artifacts for your VMs](devtest-lab-artifact-author.md) (Tworzenie niestandardowych artefaktów dla maszyn wirtualnych).
* [Add a VM with artifacts to a lab](https://azure.microsoft.com/resources/videos/how-to-create-vms-with-artifacts-in-a-devtest-lab/) (Dodawanie maszyny wirtualnej z artefaktami do laboratorium).

