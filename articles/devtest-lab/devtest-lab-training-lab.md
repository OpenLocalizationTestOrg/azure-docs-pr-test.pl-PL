---
title: aaaUse Azure DevTest Labs szkolenia | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toouse Azure DevTest Labs w scenariuszach szkolenia."
services: devtest-lab,virtual-machines
documentationcenter: na
author: steved0x
manager: douge
editor: 
ms.assetid: 57ff4e30-7e33-453f-9867-e19b3fdb9fe2
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/12/2016
ms.author: sdanie
ms.openlocfilehash: 4a5f44a282d8f6a58849c730ff89237ccff39ca8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-devtest-labs-for-training"></a>Użyć do trenowania Azure DevTest Labs
Azure DevTest Labs mogą być używane tooimplement wiele scenariuszy klucza w dodanie toodev i testowanie. Jest jednym z tych scenariuszy tooset się laboratorium szkolenia. Azure DevTest Labs umożliwia toocreate laboratorium, w którym można podać szablonów niestandardowych każdego szkoleniowych można użyć środowiska identyczne i izolowane toocreate szkolenia. Można zastosować zasady tooensure środowisk szkolenia czy szkoleniowych tooeach dostępne tylko wtedy, gdy są potrzebne i zawiera za mało zasobów — takich jak maszyny wirtualne - wymagane do trenowania hello. Na koniec można łatwo udostępniać laboratorium hello z uczestnikom, które mogą uzyskiwać dostęp do za pomocą jednego kliknięcia.

![Użyć do trenowania DevTest Labs](./media/devtest-lab-training-lab/devtest-lab-training.png)

Azure DevTest Labs spełnia następujące wymagania, które są wymagane tooconduct szkolenia w dowolnym środowisku wirtualnym hello: 

* Stażyści nie widzi maszyn wirtualnych utworzonych przez inne stażyści
* Każdym komputerze szkolenia powinny być identyczne
* Stażyści można szybko ustanowić środowiskami szkolenia
* Kontrolowanie kosztów przez zapewnienie, że stażyści nie można pobrać więcej maszyn wirtualnych, niż jest to wymagane dla hello szkolenia, a także zamykania maszyn wirtualnych nie używają ich
* Można łatwo udostępnić laboratorium szkolenia hello każdego szkoleniowych
* Ponowne użycie hello szkolenia laboratorium wielokrotnie

W tym artykule należy informacje o różnych funkcji w usłudze Azure DevTest Labs, których można użyć toomeet hello opisane wcześniej wymagania szkolenia i szczegółowy opis kroków, wykonać tooset się laboratorium szkolenia.  

## <a name="implementing-training-with-azure-devtest-labs"></a>Implementowanie szkolenia Azure DevTest Labs
1. **Tworzenie laboratorium hello** 
   
    Laboratoria są hello punkt początkowy w usłudze Azure DevTest Labs. Po utworzeniu laboratorium, można wykonywać zadania, takie jak dodawanie użytkowników (stażyści) toohello laboratorium, ustawianie zasad toocontrol kosztów, zdefiniuj obrazów maszyn wirtualnych, które można szybko utworzyć i inne.   
   
    Dowiedz się więcej, klikając łącza hello w hello w poniższej tabeli:
   
   | Zadanie | Omawiane zagadnienia |
   | --- | --- |
   | [Tworzenie laboratorium w usłudze Azure DevTest Labs](devtest-lab-create-lab.md) |Dowiedz się, jak toocreate a laboratorium w usłudze Azure DevTest Labs w hello portalu Azure. |
2. **Tworzenie maszyn wirtualnych szkolenia w kilka minut przy użyciu gotowych marketplace obrazów i niestandardowych obrazów** 
   
    Można pobrania gotowych obrazów z szerokiej gamy obrazów w portalu Azure Marketplace hello i udostępnić je stażystów hello w laboratorium hello. Jeśli obrazy gotowe hello nie spełniają wymagań, można utworzyć niestandardowy obraz przez utworzenie maszyny Wirtualnej przy użyciu gotowych obrazu z portalu Azure Marketplace, instalowanie całe oprogramowanie hello potrzebnym do trenowania hello i zapisywanie hello maszyny Wirtualnej jako obraz niestandardowy w laboratorium hello laboratorium. 
   
    Dowiedz się więcej, klikając łącza hello w hello w poniższej tabeli:
   
   | Zadanie | Omawiane zagadnienia |
   | --- | --- |
   | [Konfigurowanie portalu Azure Marketplace obrazów](devtest-lab-configure-marketplace-images.md) |Dowiedz się, jak obrazy portalu Azure Marketplace listy dozwolonych adresów IP; Udostępnianie do wyboru tylko obrazy hello ma hello szkolenia. |
   | [Tworzenie niestandardowego obrazu](devtest-lab-create-template.md) |Tworzenie niestandardowego obrazu wstępnie instalując oprogramowanie hello, potrzebne do trenowania hello tak, aby stażyści może szybko utworzyć Maszynę wirtualną przy użyciu hello niestandardowego obrazu. |
3. **Tworzenie szablonów wielokrotnego użytku maszyn szkolenia** 
   
    Formuła w usłudze Azure DevTest Labs jest lista domyślnych wartości właściwości używanych toocreate maszyny Wirtualnej. Wybieranie obrazu, rozmiar maszyny Wirtualnej (kombinacja Procesora i pamięci RAM) i sieć wirtualną można utworzyć formuły w laboratorium hello. Każdy szkoleniowych można Zobacz hello formuły w laboratorium hello i użyć toocreate maszyny Wirtualnej. 
   
    Dowiedz się więcej, klikając łącza hello w hello w poniższej tabeli:
   
   | Zadanie | Omawiane zagadnienia |
   | --- | --- |
   | [Zarządzanie DevTest Labs formuły toocreate maszyny wirtualne](devtest-lab-manage-formulas.md) |Dowiedz się, jak utworzyć formuły przez przechwycenie obrazu, rozmiar maszyny Wirtualnej (kombinację procesora CPU i pamięci RAM) i sieci wirtualnej. |
4. **Kontrolę kosztów**
   
    Azure DevTest Labs umożliwia tooset zasady w hello laboratorium toospecify hello maksymalną liczbę maszyn wirtualnych, które mogą być tworzone przez szkoleniowych w laboratorium hello. 
   
    Jest przeprowadzenie szkolenia wielodniowego i toostop wszystkich hello maszyn wirtualnych o określonej godzinie dnia hello, a następnie automatycznie uruchomić je ponownie hello dnia, można łatwo realizacji tego przez ustawienie automatyczne zamykanie i zasady w laboratorium hello automatycznego uruchamiania. 
   
    Na koniec po zakończeniu szkolenia można usunąć wszystkich hello maszyn wirtualnych jednocześnie za pomocą jednego skryptu środowiska PowerShell. 
   
    Dowiedz się więcej, klikając łącza hello w hello w poniższej tabeli:
   
   | Zadanie | Omawiane zagadnienia |
   | --- | --- |
   | [Definiowanie zasad laboratorium](devtest-lab-set-lab-policy.md) |Kontrolę kosztów przez ustawienie zasad w laboratorium hello. |
   | [Usuń wszystkie laboratorium hello maszyn wirtualnych za pomocą skryptu programu PowerShell](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |Po zakończeniu hello szkolenia, należy usunąć wszystkie laboratoria hello w jednej operacji. |
5. **Udostępnij laboratorium hello każdego szkoleniowych**
   
    Laboratoria są bezpośrednio dostępne przy użyciu łącza, które możesz udostępniać stażyści Twojego. Twoje stażyści nie muszą nawet być toohave konta platformy Azure, jak długo mają [konta Microsoft](devtest-lab-faq.md#what-is-a-microsoft-account). Stażyści nie widzi utworzonych przez inne stażyści maszyn wirtualnych.  
   
    Dowiedz się więcej, klikając łącza hello w hello w poniższej tabeli:
   
   | Zadanie | Omawiane zagadnienia |
   | --- | --- |
   | [Dodawanie laboratorium tooa szkoleniowych w usłudze Azure DevTest Labs](devtest-lab-add-devtest-user.md) |Użyj hello Azure tooadd portalu stażyści tooyour szkolenia laboratorium. |
   | [Dodawanie laboratorium toohello stażyści przy użyciu skryptu programu PowerShell](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |Użyj Dodawanie laboratorium szkolenia tooyour stażyści tooautomate środowiska PowerShell. |
   | [Uzyskaj link toohello laboratorium](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |Dowiedz się, jak laboratorium jest bezpośrednio dostępny za pośrednictwem hiperłącza. |
6. **Ponowne użycie hello wielokrotnie laboratorium** 
   
    Można zautomatyzować tworzenie laboratorium, ustawienia niestandardowe, w tym tworzenia szablonu usługi Resource Manager i używając jej labs identyczne toocreate wielokrotnie. 
   
    Dowiedz się więcej, klikając łącza hello w hello w poniższej tabeli:
   
   | Zadanie | Omawiane zagadnienia |
   | --- | --- |
   | [Tworzenie laboratorium przy użyciu szablonu usługi Resource Manager](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |Utwórz laboratoriów w usłudze Azure DevTest Labs za pomocą szablonów usługi Resource Manager. |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

