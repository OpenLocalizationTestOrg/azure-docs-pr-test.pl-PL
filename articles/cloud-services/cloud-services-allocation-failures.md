---
title: "Błąd alokacji usługi w chmurze aaaTroubleshooting | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów z błędami alokacji podczas wdrażania usługi Cloud Services na platformie Azure"
services: azure-service-management, cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 529157eb-e4a1-4388-aa2b-09e8b923af74
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: dfd5cc4663ccc6ed1b27ca9df579182737363b0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-allocation-failure-when-you-deploy-cloud-services-in-azure"></a>Rozwiązywanie problemów z błędami alokacji podczas wdrażania usługi Cloud Services na platformie Azure
## <a name="summary"></a>Podsumowanie
Podczas wdrażania tooa wystąpień usługi w chmurze lub dodać nową sieć web lub wystąpień roli procesu roboczego, Microsoft Azure przydziela zasoby obliczeniowe. Czasami może pojawić błędy podczas przeprowadzania tych operacji nawet zanim przejdziesz hello limity subskrypcji platformy Azure. W tym artykule opisano niektóre typowe błędy alokacji hello hello przyczyny, a także sugeruje możliwe korygowania. Planując wdrożenie hello usług Hello informacje mogą być również przydatne.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

### <a name="background--how-allocation-works"></a>Tło — jak działa alokacji
Witaj serwerach w centrach danych platformy Azure są dzielone w klastrach. Nowe żądanie alokacji usługi chmury nastąpiła w wielu klastrach. Po pierwszym wystąpieniu hello jest tooa wdrożonej usługi w chmurze (w albo tymczasowym czy produkcyjnym), usługa w chmurze pobiera przypiętych tooa klastra. Dla usługi w chmurze hello nastąpi w hello sam żadnego dalszego wdrożenia klastra. W tym artykule firma Microsoft będzie odwoływać się toothis jako "przypiętych tooa klastra". Diagram 1 poniżej przedstawia hello przypadku normalnych alokacji, w której nastąpiła w wielu klastrach; Diagram 2 przedstawia przypadku hello alokacji to jest przypięty tooCluster 2 ponieważ, który jest gdzie hello istniejących CS_1 usługi w chmurze jest obsługiwana.

![Diagram alokacji](./media/cloud-services-allocation-failure/Allocation1.png)

### <a name="why-allocation-failure-happens"></a>Dlaczego sytuacji błąd alokacji
Żądanie alokacji jest przypięty tooa klastra, ma wyższy stopień niepowodzeniem toofind zwolnić zasoby, ponieważ pula zasobów dostępnych hello jest ograniczona tooa klastra. Ponadto jeśli żądanie alokacji jest przypięty tooa klastra, ale hello typ zasobu, która miała nie jest obsługiwany przez ten klaster, żądanie zakończy się niepowodzeniem nawet wtedy, gdy klaster hello ma bezpłatnego zasobu. Diagram 3 poniżej przedstawia przypadku hello gdzie przypiętych alokacja nie powiedzie się, ponieważ hello candidate tylko klastra nie ma wolnego zasobów. Diagram 4 przedstawia przypadku hello których alokacji przypiętych nie powiedzie się, ponieważ hello tylko candidate klastra nie obsługuje hello żądany rozmiar maszyny Wirtualnej, nawet jeśli klaster hello ma zwolnić zasoby.

![Błąd alokacji przypiętych](./media/cloud-services-allocation-failure/Allocation2.png)

## <a name="troubleshooting-allocation-failure-for-cloud-services"></a>Rozwiązywanie problemów z błędami alokacji dla usług w chmurze
### <a name="error-message"></a>Komunikat o błędzie
Może zostać wyświetlony następujący komunikat o błędzie hello:

    "Azure operation '{operation id}' failed with code Compute.ConstrainedAllocationFailed. Details: Allocation failed; unable toosatisfy constraints in request. hello requested new service deployment is bound tooan Affinity Group, or it targets a Virtual Network, or there is an existing deployment under this hosted service. Any of these conditions constrains hello new deployment toospecific Azure resources. Please retry later or try reducing hello VM size or number of role instances. Alternatively, if possible, remove hello aforementioned constraints or try deploying tooa different region."

### <a name="common-issues"></a>Typowe problemy
Poniżej przedstawiono hello typowych alokacji scenariuszy, które powodują alokacji żądania toobe przypiętych tooa jednego klastra.

* Wdrażanie tooStaging miejsca — Jeśli usługa w chmurze ma wdrożenia w każdym miejscu, następnie usługa w chmurze całego hello jest przypięty tooa konkretnego klastra.  Oznacza to, że jeśli wdrożenia już istnieje w gnieździe produkcyjnym hello, następnie nowe wdrożenie przemieszczania może zostać przydzielone tylko w hello sam klastra jako hello miejsca produkcji. Jeśli klaster hello zbliża się do pojemności, Żądanie hello może zakończyć się niepowodzeniem.
* Skalowanie — Dodawanie nowych wystąpień tooan istniejącą usługę w chmurze musi przydzielić w hello sam klastra.  Zazwyczaj można przydzielić pomniejszonego skalowanie żądania, ale nie zawsze. Jeśli klaster hello zbliża się do pojemności, Żądanie hello może zakończyć się niepowodzeniem.
* Grupa koligacji — nową usługę chmury pusty tooan wdrożenia mogą zostać przydzieleni przez sieć szkieletowa hello w dowolnego klastra w danym regionie, chyba, że usługa w chmurze hello jest przypięty tooan grupy koligacji. Toohello wdrożeń w tej samej grupie koligacji, zostanie podjęta na powitania tego samego klastra. Jeśli klaster hello zbliża się do pojemności, Żądanie hello może zakończyć się niepowodzeniem.
* Grupy koligacji vNet - starszych sieci wirtualnych zostały wiązanej tooaffinity grupy zamiast regionów, a usługi w chmurze w tych sieciach wirtualnych będzie przypiętych toohello grupy koligacji klastra. Sieć wirtualna wdrożeń toothis typu będą podejmowane w klastrze hello przypięty. Jeśli klaster hello zbliża się do pojemności, Żądanie hello może zakończyć się niepowodzeniem.

## <a name="solutions"></a>Rozwiązania
1. Ponownego wdrażania tooa nową usługę w chmurze — to rozwiązanie jest prawdopodobnie toobe najbardziej popularnych umożliwia toochoose platformy hello ze wszystkich klastrów w tym regionie.

   * Wdrażanie hello obciążenia tooa nową usługę w chmurze  
   * Zaktualizuj hello CNAME i A rekordów toopoint ruchu toohello nową usługę w chmurze
   * Po zero ruch będzie toohello starej lokacji, możesz usunąć hello starego usługi w chmurze. To rozwiązanie powinno spowodować przestojów.
2. Usuń zarówno produkcyjne i przejściowe miejsc — to rozwiązanie zachowa istniejącą nazwę DNS, ale zostanie utworzona aplikacja tooyour przestoju.

   * Usuń hello produkcyjne i przejściowe miejsc istniejącą usługę w chmurze, dzięki czemu usługa w chmurze hello jest pusty, a następnie
   * Utwórz nowe wdrożenie hello istniejących w usłudze w chmurze. Spowoduje to ponowne podjęcie próby tooallocation na wszystkich klastrach w regionie hello. Upewnij się, że usługa w chmurze hello nie jest związany tooan grupy koligacji.
3. Zastrzeżony adres IP — to rozwiązanie zachowa IP istniejącego rozwiązania, ale zostanie utworzona aplikacja tooyour przestoju.  

   * Tworzenie zastrzeżonego adresu IP istniejącego wdrożenia przy użyciu programu Powershell

     ```
     New-AzureReservedIP -ReservedIPName {new reserved IP name} -Location {location} -ServiceName {existing service name}
     ```
   * Wykonaj #2 powyższego, co się toospecify hello nowy zastrzeżony adres IP w CSCFG hello usługi.
4. Usuń grupę koligacji dla nowych wdrożeń - grup koligacji nie są zalecane. Wykonaj kroki &#1; powyżej toodeploy nową usługę w chmurze. Upewnij się, usługa w chmurze nie jest w grupie koligacji.
5. Konwertuj tooa regionalną sieć wirtualną — zobacz [jak toomigrate z grup koligacji tooa regionalną sieć wirtualną (VNet)](../virtual-network/virtual-networks-migrate-to-regional-vnet.md).
