---
title: "aaaComparing niestandardowych obrazów i formuły w usłudze DevTest Labs | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o hello różnice między niestandardowych obrazów i formuły jako baz maszyn wirtualnych może zdecydować, który najlepiej odpowiada środowisku."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: a3cb259a-7d80-40ec-8ee8-45105704d589
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: tarcher
ms.openlocfilehash: 3c1d88dfe0ff94b8e825bb7a0b4aca3341c9330d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="comparing-custom-images-and-formulas-in-devtest-labs"></a>Porównywanie niestandardowych obrazów i formuły w usłudze DevTest Labs
Zarówno [niestandardowych obrazów](devtest-lab-create-template.md) i [formuły](devtest-lab-manage-formulas.md) mogą być używane jako podstawy [utworzone nowe maszyny wirtualne](devtest-lab-add-vm-with-artifacts.md). Jednak rozróżnienia klucza hello niestandardowych obrazów i formuły jest obraz niestandardowy po prostu obraz oparty na dysku VHD, gdy formuła jest obraz oparty na dysku VHD *oprócz* wstępnie skonfigurowane ustawienia — takich jak rozmiar maszyny Wirtualnej, sieci wirtualnej podsieć, a artefaktów. Te wstępnie skonfigurowane ustawienia są skonfigurowane z wartościami domyślnymi, które mogą zostać zastąpione w czasie hello tworzenia maszyny Wirtualnej. W tym artykule opisano niektóre zalety hello (specjalistów) wady i zalety (wad) toousing niestandardowych obrazów i przy użyciu formuły.

## <a name="custom-image-pros-and-cons"></a>Obraz niestandardowy zalet i wad
Niestandardowe obrazy zapewniają toocreate statycznych, niezmienne sposób maszyn wirtualnych z wymagane środowisko. 

**Specjaliści**

* Obsługi z niestandardowego obrazu maszyny Wirtualnej jest szybkie, ponieważ nic nie zmieni się po powitalne przejścia maszyny Wirtualnej z obrazu hello. Innymi słowy nie ma żadnych tooapply ustawienia jako obraz niestandardowy hello jest tylko obraz bez ustawień. 
* Maszyny wirtualne utworzone za pomocą pojedynczego obrazu niestandardowego są identyczne.

**Cons**

* Należy tooupdate pewien aspekt niestandardowy obraz powitania obraz powitania muszą zostać ponownie utworzone.  

## <a name="formula-pros-and-cons"></a>Formuły zalet i wad
Formuły zapewniają toocreate dynamiczny sposób maszyn wirtualnych z ustawienia konfiguracji hello potrzebne.

**Specjaliści**

* Zmiany w środowisku hello można przechwycić na bieżąco hello za pośrednictwem artefaktów. Na przykład, jeśli mają zainstalowane najnowsze bitów hello z potoku sieci wersji maszyny Wirtualnej lub zarejestrować hello najnowsze kodu z repozytorium, można po prostu określić artefaktu, który wdraża bitów najnowsze hello lub rejestruje hello najnowsze kodu w formule hello razem z docelowy obrazu podstawowego. Zawsze, gdy w tej formule jest używany toocreate maszyn wirtualnych, hello najnowsze bity/kodu są wdrożone pozyskać toohello maszyny Wirtualnej. 
* Formuły można zdefiniować ustawienia domyślne, których nie może dostarczyć niestandardowe obrazy — takich jak ustawienia sieci wirtualnej i rozmiarów maszyn wirtualnych. 
* Ustawienia Hello zapisane w formule są wyświetlane jako wartości domyślne, ale można zmodyfikować po utworzeniu hello maszyny Wirtualnej. 

**Cons**

* Tworzenie maszyny Wirtualnej na podstawie formuły może zająć więcej czasu niż tworzenia maszyny Wirtualnej z obrazu niestandardowego.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>Wpisy na blogu pokrewne
* [Niestandardowe obrazy lub formuł?](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a>Następne kroki
- [DevTest Labs — często zadawane pytania](devtest-lab-faq.md)