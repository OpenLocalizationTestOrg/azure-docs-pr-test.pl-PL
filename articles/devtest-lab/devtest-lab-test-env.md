---
title: "aaaUse Azure DevTest Labs dla maszyny Wirtualnej i PaaS test środowisk | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse Azure DevTest Labs dla maszyny Wirtualnej i PaaS przetestować scenariusze środowiska."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: d4e2c334-643a-40c9-9051-625b8f39fc86
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: tarcher
ms.openlocfilehash: 9285090da768491e1275942318b094fae89e3273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-devtest-labs-for-vm-and-paas-test-environments"></a>Użyj Azure DevTest Labs dla maszyny Wirtualnej i PaaS test środowisk

Azure DevTest Labs tooimplement można używać wielu różnych kluczowych scenariuszy, ale podstawowego scenariusza polega na użyciu DevTest Labs toohost maszyny dla testerów. 

W tym scenariuszu DevTest Labs zapewnia następujące korzyści:

- Testerów przetestować najnowszą wersję aplikacji hello szybkie Inicjowanie obsługi środowisk systemu Windows i Linux za pomocą szablonów wielokrotnego użytku i artefaktów.
- Testerów można zwiększać ich przez Inicjowanie obsługi wielu agentów testowych do testowania obciążenia.
- Administratorzy mogą kontrolować koszty przez zapewnienie, że:
  - Testerów nie można pobrać więcej maszyn wirtualnych, niż jest to wymagane.
  - Maszyny wirtualne są zamknięte podczas nieużywany.

![Użyć do trenowania DevTest Labs](./media/devtest-lab-developer-lab/devtest-lab-developer-lab.png)

W tym artykule informacje o różnych wymaganiach tester toomeet funkcji Azure DevTest Labs i hello tooset toofollow szczegółowy opis kroków, tworząc laboratorium.

## <a name="implementing-test-environments-with-azure-devtest-labs"></a>Implementowanie środowiska testowego o usłudze Azure DevTest Labs
1. **Tworzenie laboratorium hello** 
   
    Laboratoria są hello punkt początkowy w usłudze Azure DevTest Labs. Po utworzeniu laboratorium, można wykonać zadania, takie jak dodawanie laboratorium toohello użytkowników (testerów), ustawienia zasad toocontrol kosztów, definiowanie obrazów maszyn wirtualnych, które można szybko utworzyć i inne.  
   
    Dowiedz się więcej, klikając łącza hello w hello w poniższej tabeli:
   
   | Zadanie | Omawiane zagadnienia |
   | --- | --- |
   | [Tworzenie laboratorium w usłudze Azure DevTest Labs](devtest-lab-create-lab.md) |Dowiedz się, jak toocreate a laboratorium w usłudze Azure DevTest Labs w hello portalu Azure. |
2. **Tworzenie maszyn wirtualnych w kilka minut przy użyciu gotowych marketplace obrazów i niestandardowych obrazów** 
   
    Możesz pobrania gotowych obrazów z szerokiej gamy obrazów w portalu Azure Marketplace hello i udostępnić je w laboratorium hello. Jeśli obrazy gotowe hello nie spełniają wymagań, można utworzyć niestandardowy obraz przez utworzenie maszyny Wirtualnej przy użyciu gotowych obrazu z portalu Azure Marketplace, instalowanie całe oprogramowanie hello, które są potrzebne, i zapisywanie hello maszyny Wirtualnej jako obraz niestandardowy w laboratorium hello laboratorium.

    Jeśli będziesz używać niestandardowych obrazów, należy rozważyć użycie toocreate fabryki obrazu i dystrybucji obrazów. Fabryka obrazu jest rozwiązanie konfiguracji jako kod, który regularnie tworzy i rozpowszechnia obrazy skonfigurowany automatycznie. Ta zapisuje hello czas toomanually skonfigurować system powitania po utworzeniu maszyny Wirtualnej z hello podstawowego systemu operacyjnego.
  
    Dowiedz się więcej, klikając łącza hello w hello w poniższej tabeli:
   
   | Zadanie | Omawiane zagadnienia |
   | --- | --- |
   | [Konfigurowanie portalu Azure Marketplace obrazów](devtest-lab-configure-marketplace-images.md) |Informacje na temat dozwolonych obrazów Azure Marketplace, udostępniając wybór tylko hello obrazów dla testerów hello.|
   | [Tworzenie niestandardowego obrazu](devtest-lab-create-template.md) |Tworzenie niestandardowego obrazu wstępnie instalując oprogramowanie hello, potrzebne, aby testerów może szybko utworzyć Maszynę wirtualną przy użyciu hello niestandardowego obrazu.|
   | [Więcej informacji na temat fabryki obrazu](https://blogs.msdn.microsoft.com/devtestlab/2017/04/17/video-custom-image-factory-with-azure-devtest-labs/) |Obejrzyj klip wideo, który opisuje sposób tooset Konfigurowanie i użyj fabrykę obrazu.|

3. **Tworzenie szablonów wielokrotnego użytku dla maszyny testowe** 
   
    Formuła w usłudze Azure DevTest Labs jest lista domyślnych wartości właściwości używanych toocreate maszyny Wirtualnej. Wybieranie obrazu, rozmiar maszyny Wirtualnej (kombinacja Procesora i pamięci RAM) i sieć wirtualną można utworzyć formuły w laboratorium hello. Każdy tester można Zobacz hello formuły w laboratorium hello i użyć toocreate maszyny Wirtualnej. 
   
    Dowiedz się więcej, klikając łącza hello w hello w poniższej tabeli:
   
   | Zadanie | Omawiane zagadnienia |
   | --- | --- |
   | [Zarządzanie DevTest Labs formuły toocreate maszyny wirtualne](devtest-lab-manage-formulas.md) |Dowiedz się, jak utworzyć formuły przez przechwycenie obrazu, rozmiar maszyny Wirtualnej (kombinację procesora CPU i pamięci RAM) i sieci wirtualnej.|

3. **Tworzenie wielu maszyn wirtualnych środowisk testowych.** 
   
    Można użyć usługi Azure Resource Manager szablony toodefine hello infrastrukturze i konfiguracji rozwiązania Azure i wielokrotnie wdrażać testu wiele maszyn wirtualnych w spójnym stanie.

    Zasoby platformy Azure PaaS można udostępnić w środowisku z szablonem usługi Resource Manager i widoczny w śledzenie kosztów. Jednak maszyna wirtualna automatycznego zamykania nie ma zastosowania tooPaaS zasobów.

    Dowiedz się więcej, klikając łącza hello w hello w poniższej tabeli:
   
   | Zadanie | Omawiane zagadnienia |
   | --- | --- |
   | [Tworzenie środowisk z wieloma maszynami wirtualnymi i zasobów PaaS za pomocą szablonów usługi Azure Resource Manager](devtest-lab-create-environment-from-arm.md) |Dowiedz się, jak można wdrożyć wiele maszyn wirtualnych w spójnym stanie dla danego środowiska testowego.|

4. **Tworzenie artefaktów tooenable elastyczne dostosowanie maszyny Wirtualnej**

   Artefakty są używane toodeploy i konfigurowania aplikacji po zainicjowaniu obsługi maszyny Wirtualnej. Artefaktami mogą być:

   - Narzędzia, które mają tooinstall na powitania maszyny Wirtualnej — np. agenci, program Fiddler i program Visual Studio.
   - Akcje, które mają toorun na powitania maszyny Wirtualnej — np. klonowanie repozytorium.
   - Aplikacje, które mają tootest.

   Wiele artefakty są już dostępne out-of--box. Ale jeśli chcesz więcej dostosowania do określonych potrzeb, możesz utworzyć własne niestandardowe artefakty.

   Dowiedz się więcej, klikając łącza hello w hello w poniższej tabeli:
   
   | Zadanie | Omawiane zagadnienia |
   | --- | --- |
   | [Tworzenie niestandardowych artefaktów dla maszyny Wirtualnej DevTest Labs](devtest-lab-artifact-author.md) |Tworzenie własnych niestandardowych artefaktów dla maszyn wirtualnych hello w laboratorium.|
   | [Dodaj Git artefakty niestandardowych toostore repozytorium i szablony usługi Azure Resource Manager do użycia w usłudze Azure DevTest Labs](devtest-lab-add-artifact-repo.md) |Dowiedz się, jak toostore Twojego niestandardowe artefakty w własne prywatne repozytorium Git.|

5. **Kontrolę kosztów**
   
    Azure DevTest Labs umożliwia tooset zasady w hello laboratorium toospecify hello maksymalną liczbę maszyn wirtualnych, które mogą być tworzone przez tester w laboratorium hello. 
   
    Jeśli zespół testu ma zestaw harmonogram pracy i mają toostop wszystkich hello maszyn wirtualnych o określonej godzinie dnia hello, a następnie automatycznie uruchomić je ponownie hello dnia, można łatwo wykonywać który przez ustawienie automatyczne zamykanie automatyczne uruchamianie zasad i w laboratorium hello. 
   
    Na koniec po zakończeniu tworzenia aplikacji można usunąć wszystkich hello maszyn wirtualnych jednocześnie za pomocą jednego skryptu środowiska PowerShell. 
   
    Dowiedz się więcej, klikając łącza hello w hello w poniższej tabeli:
   
   | Zadanie | Omawiane zagadnienia |
   | --- | --- |
   | [Definiowanie zasad laboratorium](devtest-lab-set-lab-policy.md) |Kontrolę kosztów przez ustawienie zasad w laboratorium hello. |
   | [Usuń wszystkie laboratorium hello maszyn wirtualnych za pomocą skryptu programu PowerShell](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |Po zakończeniu testowania, należy usunąć wszystkie laboratoria hello w jednej operacji.|

1. **Dodaj tooa sieci wirtualnej laboratorium** 
   
    DevTest Labs tworzy nową sieć wirtualną (VNET), przy każdym utworzeniu laboratorium. Jeśli skonfigurowano własnych sieci Wirtualnej — np. za pomocą programu ExpressRoute lub sieci VPN typu lokacja lokacja — można dodać tej sieci Wirtualnej laboratorium tooyour ustawień sieci wirtualnej, aby była dostępna podczas tworzenia maszyn wirtualnych.

    Ponadto jest usługa Azure Active Directory domeny sprzężenia artefaktu dostępne której jest przyłączany do domeny tooa maszyny Wirtualnej po utworzeniu hello maszyny Wirtualnej. 
   
    Dowiedz się więcej, klikając łącza hello w hello w poniższej tabeli:
   
   | Zadanie | Omawiane zagadnienia |
   | --- | --- |
   | [Konfigurowanie sieci wirtualnej w usłudze Azure DevTest Labs](devtest-lab-configure-vnet.md) |Dowiedz się, jak tooconfigure sieci wirtualnej w usłudze Azure DevTest Labs przy użyciu hello portalu Azure.|

6. **Udostępnij laboratorium hello każdego tester**
   
    Laboratoria są bezpośrednio dostępne przy użyciu łącza, które są udostępniane z testerów. Ich nie muszą nawet być toohave konta platformy Azure, jak długo mają [konta Microsoft](devtest-lab-faq.md#what-is-a-microsoft-account). Testerów nie widzi maszyny wirtualne utworzone przez inne testerów.  
   
    Dowiedz się więcej, klikając łącza hello w hello w poniższej tabeli:
   
   | Zadanie | Omawiane zagadnienia |
   | --- | --- |
   | [Dodawanie laboratorium tooa tester w usłudze Azure DevTest Labs](devtest-lab-add-devtest-user.md) |Użyj hello Azure tooadd portalu testerów tooyour laboratorium.|
   | [Dodawanie laboratorium toohello testerów przy użyciu skryptu programu PowerShell](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |Za pomocą programu PowerShell tooautomate Dodawanie laboratorium tooyour testerów. |
   | [Uzyskaj link toohello laboratorium](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |Dowiedz się, jak testerów bezpośrednio uzyskać dostęp za pośrednictwem hiperłącze laboratorium.|

7. **Zautomatyzować tworzenie laboratorium więcej zespołów** 
   
    Można zautomatyzować tworzenie laboratorium, ustawienia niestandardowe, w tym tworzenia szablonu usługi Resource Manager i używając jej labs identyczne toocreate wielokrotnie. 
   
    Dowiedz się więcej, klikając łącza hello w hello w poniższej tabeli:
   
   | Zadanie | Omawiane zagadnienia |
   | --- | --- |
   | [Tworzenie laboratorium przy użyciu szablonu usługi Resource Manager](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |Utwórz laboratoriów w usłudze Azure DevTest Labs za pomocą szablonów usługi Resource Manager. |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

