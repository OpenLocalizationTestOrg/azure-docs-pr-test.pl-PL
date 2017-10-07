---
title: aaaCreate niestandardowego obrazu z maszyny Wirtualnej Azure DevTest Labs | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toocreate obraz niestandardowy w usłudze Azure DevTest Labs używającego zainicjowana VM hello portalu Azure"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 7dccb79d3db4aae676c7bd2f6b800301210491e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-from-a-vm"></a>Tworzenie niestandardowego obrazu z maszyny Wirtualnej

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

## <a name="step-by-step-instructions"></a>Instrukcje krok po kroku

Utworzyć niestandardowy obraz z elastycznie maszyny Wirtualnej, a następnie użyć tej toocreate niestandardowego obrazu identycznych maszyn wirtualnych. Witaj, wykonaj czynności ilustrują sposób toocreate niestandardowego obrazu z maszyny Wirtualnej:

1. Zaloguj się toohello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Wybierz **więcej usług**, a następnie wybierz **DevTest Labs** z listy hello.

1. Z listy hello labs wybierz żądany laboratorium hello.  

1. W bloku hello laboratorium, wybierz **Moje maszyny wirtualne**.
 
1. Na powitania **Moje maszyny wirtualne** bloku, wybierz hello maszyny Wirtualnej, z którego mają zostać toocreate hello niestandardowego obrazu.

1. W bloku hello wirtualna wybierz **Tworzenie niestandardowego obrazu (VHD)**.

    ![Tworzenie niestandardowego obrazu elementu menu](./media/devtest-lab-create-template/create-custom-image.png)

1. Na powitania **Utwórz obraz** bloku, wprowadź nazwę i opis dla niestandardowego obrazu. Te informacje są wyświetlane na liście hello baz podczas tworzenia maszyny Wirtualnej.

    ![Tworzenie niestandardowego obrazu bloku](./media/devtest-lab-create-template/create-custom-image-blade.png)

1. Określ, czy program sysprep zostało uruchomione na powitania maszyny Wirtualnej. Jeśli hello sysprep nie zostało uruchomione na powitania maszyny Wirtualnej, określ, czy program sysprep uruchamiany po utworzeniu maszyny Wirtualnej z tego obrazu niestandardowego.

1. Wybierz **OK** po toocreate Zakończono hello niestandardowego obrazu.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>Wpisy na blogu pokrewne

- [Niestandardowe obrazy lub formuł?](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [Kopiowanie obrazów niestandardowych między Azure DevTest Labs](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a>Następne kroki

- [Dodawanie laboratorium tooyour maszyny Wirtualnej](./devtest-lab-add-vm-with-artifacts.md)
