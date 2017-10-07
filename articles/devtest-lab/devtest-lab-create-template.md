---
title: aaaCreate niestandardowego obrazu z pliku VHD Azure DevTest Labs | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toocreate obraz niestandardowy w usłudze Azure DevTest Labs od pliku wirtualnego dysku twardego za pomocą hello portalu Azure"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: b795bc61-7c28-40e6-82fc-96d629ee0568
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 80af8ea1cb72380f868df0a76c4a0dcd92e63cf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-from-a-vhd-file"></a>Tworzenie niestandardowego obrazu z pliku VHD

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a>Instrukcje krok po kroku

Witaj następujących krokach objaśniono sposób tworzenia niestandardowego obrazu z pliku VHD za pomocą hello portalu Azure:

1. Zaloguj się toohello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Wybierz **więcej usług**, a następnie wybierz **DevTest Labs** z listy hello.

1. Z listy hello labs wybierz żądany laboratorium hello.  

1. W bloku hello laboratorium, wybierz **konfiguracji**. 

1. W laboratorium hello **konfiguracji** bloku, wybierz opcję **niestandardowych obrazów (VHD)**.

1. Na powitania **niestandardowych obrazów** bloku, wybierz opcję **+ Dodaj**.

    ![Dodaj niestandardowy obraz](./media/devtest-lab-create-template/add-custom-image.png)

1. Wprowadź nazwę hello hello niestandardowego obrazu. Ta nazwa będzie wyświetlana na liście hello podstawowej obrazów, podczas tworzenia maszyny Wirtualnej.

1. Wprowadź opis hello hello niestandardowego obrazu. Ten opis jest wyświetlany w hello listy obrazów podstawowej podczas tworzenia maszyny Wirtualnej.

1. Wybierz **wirtualnego dysku twardego**.

1. Z hello **wirtualnego dysku twardego** bloku, hello wybierz żądany plik wirtualnego dysku twardego.

1. Wybierz **OK** tooclose hello **wirtualnego dysku twardego** bloku.

1. Wybierz **Konfiguracja systemu operacyjnego**.

1. Na powitania **Konfiguracja systemu operacyjnego** , a następnie wybierz opcję **Windows** lub **Linux**.

1. Jeśli **Windows** jest zaznaczone, określ za pomocą pola wyboru hello czy *Sysprep* zostało uruchomione na maszynie hello. 

1. Wybierz **OK** tooclose hello **Konfiguracja systemu operacyjnego** bloku.

1. Wybierz **OK** toocreate hello niestandardowego obrazu.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>Wpisy na blogu pokrewne

- [Niestandardowe obrazy lub formuł?](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [Kopiowanie obrazów niestandardowych między Azure DevTest Labs](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a>Następne kroki

- [Dodawanie laboratorium tooyour maszyny Wirtualnej](./devtest-lab-add-vm-with-artifacts.md)
