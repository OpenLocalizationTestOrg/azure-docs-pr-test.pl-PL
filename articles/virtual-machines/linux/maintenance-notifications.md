---
title: "Obsługa powiadomień dotyczących konserwacji dla maszyn wirtualnych systemu Linux na platformie Azure | Dokumentacja firmy Microsoft"
description: "Wyświetlanie powiadomień konserwacji dla maszyn wirtualnych systemu Linux działających na platformie Azure i uruchomić samoobsługi konserwacji."
services: virtual-machines-linux
documentationcenter: 
author: zivraf
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 12/15/2017
ms.author: zivr
ms.openlocfilehash: d551a62a59e0a7f63f5fd4862680a271de659a19
ms.sourcegitcommit: 7d4b3cf1fc9883c945a63270d3af1f86e3bfb22a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/08/2018
---
# <a name="handling-planned-maintenance-notifications-for-linux-virtual-machines"></a>Obsługa planowanych konserwacji powiadomienia dla maszyn wirtualnych systemu Linux

Azure wykonuje okresowo aktualizacje do poprawy niezawodności, wydajności i zabezpieczeń infrastruktury hosta dla maszyny wirtualnej. Aktualizacje są zmiany, takie jak stosowanie poprawek do środowiska macierzystego lub uaktualnianie i likwidowaniu sprzętu. Większość tych aktualizacji są wykonywane bez wpływu na maszyny wirtualne. Istnieją jednak przypadki, w których aktualizacje mają wpływ:

- Jeśli konserwacji nie wymaga ponownego uruchomienia systemu, platforma Azure korzysta migracji w miejscu wstrzymanie maszyny Wirtualnej, gdy host jest aktualizowany.

- Jeśli konserwacji wymaga ponownego uruchomienia, możesz uzyskać zawiadomienia o podczas jest planowanych konserwacji. W takich przypadkach podano przedział czasu, w którym można uruchomić obsługi samodzielnie, gdy jest używany dla Ciebie.


Planowana konserwacja, która wymaga ponownego uruchomienia zaplanowano etapami. Każdy wave ma inny zakres (regiony).

- Wave rozpoczyna się od powiadomienia do klientów. Domyślnie powiadomienia są wysyłane do subskrypcji właściciel i współwłaściciele. Można dodać więcej adresatów i opcje obsługi wiadomości, takie jak wiadomości e-mail, SMS i elementów webhook, do powiadomienia za pomocą usługi Azure [alertów dotyczących działań w dzienniku](../../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).  
- W tym czasie powiadomienia *samoobsługi okna* ma zostać udostępnione. W tym oknie można znaleźć, który maszyn wirtualnych znajdują się w tym wave i aktywnego start konserwacji zgodnie z własnych wymagań dotyczących planowania.
- Po oknie samoobsługi *zaplanowanego okna obsługi* rozpoczyna się. W pewnym momencie podczas tego okna Azure harmonogramy i stosuje obsługi wymaganych do maszyny wirtualnej. 

Celem o dwa okna jest zapewniają wystarczająco dużo czasu, aby uruchomić konserwacji i ponownego uruchamiania maszyny wirtualnej, a Azure automatycznie rozpoczęcia konserwacji.


Portalu Azure, programu PowerShell, interfejsu API REST i interfejsu wiersza polecenia umożliwia zapytania dla okna obsługi dla maszyn wirtualnych i uruchomić samoobsługi konserwacji.

 > [!NOTE]
 > Jeśli użytkownik próbuje uruchomić konserwacji i żądanie kończy się niepowodzeniem, Azure oznacza maszyny Wirtualnej jako **pominięte**. Nie można użyć opcji obsługi zainicjował klienta. Maszyny Wirtualnej musi zostać uruchomiony ponownie przez platformę Azure w fazie zaplanowanej konserwacji.


 
## <a name="should-you-start-maintenance-using-during-the-self-service-window"></a>Należy rozpocząć konserwacji przy użyciu podczas okna samoobsługi?  

Poniższe wskazówki powinny pomóc zdecydować, czy należy używać tej funkcji i uruchomione konserwacji w czasie własnego.

> [!NOTE] 
> Konserwacja samoobsługi nie mogą być dostępne dla wszystkich maszyn wirtualnych. Aby ustalić, czy aktywnego ponownego wdrażania jest dostępna dla maszyny Wirtualnej, należy wyszukać **teraz uruchomić** w stanie konserwacji. Samoobsługowe konserwacji jest obecnie niedostępna dla usługi w chmurze (rola sieci Web/proces roboczy), usługi Service Fabric i zestawy skalowania maszyny wirtualnej.


Samoobsługowe obsługi nie jest zalecane w przypadku wdrożeń za pomocą **zestawów dostępności** ponieważ są to ustawienia wysokiej dostępności, których wpływ na tylko jedną aktualizację domeny w danym momencie. 
    - Let Azure wyzwalacza obsługi, ale należy pamiętać, że kolejność domen aktualizacji jest w pełni funkcjonalne nie zawsze odbywa się po kolei i czy przerwie 30-minutowych między domenami aktualizacji.
    - Jeśli do tymczasowej utraty niektórych wydajność (liczba domen aktualizacji/1) jest istotny, jego można łatwo skompensować przez rozdzielenie Dodawanie wystąpień w okresie konserwacji. 

**Nie** użycia samoobsługi konserwacji w następujących scenariuszach: 
    - Jeśli wyłączysz maszyn wirtualnych, albo ręcznie, przy użyciu DevTest labs, przy użyciu automatycznego zamykania lub według harmonogramu, go można przywrócić stan konserwacji i w związku z tym spowodować przestój dodatkowe.
    - W krótkim okresie maszyn wirtualnych, które znasz zostaną usunięte przed upływem wave konserwacji. 
    - W przypadku obciążeń o dużych stanie przechowywane w dysk lokalny (efemeryczne), który jest pożądane, aby zachować przy aktualizacji. 
    - W przypadkach, gdy rozmiar maszyny Wirtualnej często ponieważ można przywrócić stan konserwacji. 
    - Jeśli wdrożyły zaplanowanego zdarzenia, które Włącz aktywne pracy awaryjnej lub łagodne zamykanie obciążenie, 15 minut przed rozpoczęciem obsługi zamykania

**Użyj** samoobsługi konserwacji, jeśli jest planowane uruchamianie maszyny Wirtualnej przerwana podczas fazy zaplanowanej konserwacji i żadna wskazań liczników określonych powyżej nie ma zastosowania. 

Najlepiej użyć samoobsługi konserwacji w następujących przypadkach:
    - Musisz przekazać okna obsługi dokładnie do zarządzania lub odbiorcy końcowego. 
    - Trzeba wykonać konserwacji przed upływem określonego terminu. 
    - Należy kontrolować sekwencji konserwacji, np. aplikację wielowarstwową zagwarantowanie bezpieczne odzyskiwanie.
    - Potrzebujesz więcej niż 30 minut czasu odzyskiwania maszyny Wirtualnej między dwiema domenami aktualizacji (UDs). Aby kontrolować czas między domenami aktualizacji, użytkownik zainicjuje obsługi na maszyny wirtualne jednej domeny aktualizacji (UD) w czasie.



## <a name="find-vms-scheduled-for-maintenance-using-cli"></a>Znajdź maszyny wirtualne według harmonogramu konserwacji przy użyciu interfejsu wiersza polecenia

Informacje o zaplanowanej konserwacji można wyświetlić, korzystając [maszyna wirtualna platformy azure w Pobierz widok wystąpienia](/cli/azure/vm?view=azure-cli-latest#az_vm_get_instance_view).
 
Informacje konserwacji są zwracane tylko wtedy, gdy planowanych konserwacji. Jeśli zdefiniowano żadnej konserwacji zaplanowane tej wpływa na Maszynie wirtualnej, polecenie nie zwraca żadnych informacji konserwacji. 

```azure-cli
az vm get-instance-view -g rgName -n vmName
```

Następujące wartości są zwracane w obszarze MaintenanceRedeployStatus: 

| Wartość | Opis   |
|-------|---------------|
| IsCustomerInitiatedMaintenanceAllowed | Wskazuje, czy w tej chwili można wykonać obsługi maszyny Wirtualnej ||
| PreMaintenanceWindowStartTime         | Na początku samoobsługi oknem obsługi po rozpoczęciu konserwacji na maszynie Wirtualnej ||
| PreMaintenanceWindowEndTime           | Koniec samoobsługi oknem obsługi po rozpoczęciu konserwacji na maszynie Wirtualnej ||
| MaintenanceWindowStartTime            | Na początku zaplanowanego okna obsługi w którym Azure inicjuje konserwacji na maszynie Wirtualnej ||
| MaintenanceWindowEndTime              | Koniec zaplanowanego okna obsługi w którym Azure inicjuje konserwacji na maszynie Wirtualnej ||
| LastOperationResultCode               | Wynik ostatniej próby zainicjowanie obsługi w maszynie Wirtualnej ||




## <a name="start-maintenance-on-your-vm-using-cli"></a>Obsługa uruchamiania na maszynie Wirtualnej za pomocą interfejsu wiersza polecenia

Następujące wywołanie spowoduje zainicjowanie obsługi na maszynie Wirtualnej, jeśli `IsCustomerInitiatedMaintenanceAllowed` jest ustawiona na true.

```azure-cli
az vm perform-maintenance rgName vmName 
```

[!INCLUDE [virtual-machines-common-maintenance-notifications](../../../includes/virtual-machines-common-maintenance-notifications.md)]

## <a name="classic-deployments"></a>W przypadku wdrożeń klasycznych

Jeśli nadal masz starszych maszyn wirtualnych, które zostały wdrożone przy użyciu klasycznego modelu wdrażania, można używać 1.0 interfejsu wiersza polecenia do zapytania dla maszyn wirtualnych i inicjowania obsługi.

Upewnij się, że jesteś w tryb pracy z klasycznym maszyny Wirtualnej, wpisując:

```
azure config mode asm
```

Stan konserwacji maszyny wirtualnej o nazwie *myVM*, wpisz:

```
azure vm show myVM 
``` 

Aby uruchomić konserwacji na klasycznej maszyny Wirtualnej o nazwie *myVM* w *Moja_usługa* usługi i *myDeployment* wdrożenia, wpisz:

```
azure compute virtual-machine initiate-maintenance --service-name myService --name myDeployment --virtual-machine-name myVM
```


## <a name="faq"></a>Często zadawane pytania


**Pytanie: Dlaczego należy przeprowadzić ponowny rozruch teraz moje maszyny wirtualne?**

**Odpowiedź:** podczas większość aktualizacji i uaktualnień do platformy Azure nie wpływają na dostępność maszyn wirtualnych, istnieją przypadki, w którym firma Microsoft nie należy unikać ponownego uruchamiania maszyn wirtualnych hostowanych na platformie Azure. Firma Microsoft współdzielenia kilka zmian, które wymagają firmie Microsoft w celu ponownego uruchomienia nasze serwery, które spowoduje ponowne uruchomienie maszyn wirtualnych.

**Pytanie: czy wykonać zalecenia wysokiej dostępności przy użyciu zestawu dostępności, mogę awaryjnym?**

**Odpowiedź:** ustawić maszyn wirtualnych wdrożonych w dostępności lub zestawy skalowania maszyny wirtualnej mają podstawowe pojęcie w zakresie domen aktualizacji (UD). Podczas przeprowadzania konserwacji, Azure będzie honorować ograniczenia UD i nie zostanie wykonany ponowny rozruch maszyny wirtualne z różnych UD (w tym samym zestawie dostępności).  Azure również oczekuje na co najmniej 30 minut przed przejściem do następnej grupy maszyn wirtualnych. 

Aby uzyskać więcej informacji o wysokiej dostępności, zobacz [dostępności dla maszyn wirtualnych na platformie Azure i regiony](regions-and-availability.MD).

**Pytanie: jak otrzymywać powiadomienia o zaplanowanej konserwacji?**

**Odpowiedź:** wave zaplanowanej konserwacji rozpoczyna się przez ustawienie harmonogramu co najmniej jeden regiony platformy Azure. Wkrótce po powiadomienie e-mail są wysyłane do właścicieli subskrypcji (jeden adres e-mail dla subskrypcji). Dodatkowych kanałów oraz odbiorców to powiadomienie może zostać skonfigurowany za pomocą alertów dotyczących działań w dzienniku. W przypadku, gdy należy wdrożyć maszynę wirtualną w regionie, w którym jest już zaplanowana zaplanowanej konserwacji, nie będą otrzymywać powiadomienia, ale raczej muszą sprawdzać stan konserwacji maszyny wirtualnej.

**Pytanie: nie widzę wskazania zaplanowanej konserwacji w portalu, programu Powershell lub interfejsu wiersza polecenia, na czym polega problem?**

**Odpowiedź:** informacje powiązane z zaplanowanej konserwacji jest dostępna podczas wave zaplanowanej konserwacji, tylko dla maszyn wirtualnych, które będą mieć wpływ go. Innymi słowy Jeśli dane nie są wyświetlane, możliwe że wave konserwacji ma już wykonane (lub nie jest uruchomiony) lub że maszyna wirtualna już znajduje się w zaktualizowany serwer.

**Pytanie: czy istnieje sposób informacji, aby dokładnie Moja maszyna wirtualna jest ograniczona?**

**Odpowiedź:** przy ustalaniu harmonogramu, definiujemy okno czasu kilka dni. Jednak dokładne sekwencjonowania serwerów (i maszyn wirtualnych), w tym przedziale czasu jest nieznany. Klienci, którzy wiedzieć dokładny czas ich maszyn wirtualnych można użyć [zaplanowane zdarzenia](scheduled-events.md) zapytania z poziomu maszyny wirtualnej i otrzymasz powiadomienie 15 minut przed ponownym maszyny Wirtualnej.

**Pytanie: jak długo ponownego uruchomienia Moja maszyna wirtualna Trwa?**

**Odpowiedź:** w zależności od rozmiaru maszyny Wirtualnej, ponowne uruchomienie komputera może potrwać kilka minut w oknie konserwacji samoobsługi. Podczas Azure zainicjował ponowne uruchomienia w oknie zaplanowanej konserwacji ponownego rozruchu zwykle zajmie około 25 minut. Należy pamiętać, że w przypadku, gdy używasz usługi w chmurze (rola sieci Web/proces roboczy), zestawy skalowania maszyny wirtualnej lub zestawów dostępności, będziesz mieć możliwość 30 minut między wszystkimi grupami z maszyn wirtualnych (UD) podczas czasu zaplanowanego okna obsługi.

**Pytanie: co to jest środowisko w przypadku usługi w chmurze (rola sieci Web/proces roboczy), usługi Service Fabric i zestawy skalowania maszyny wirtualnej?**

**Odpowiedź:** podczas zaplanowanej konserwacji wpływ na tych platformach, klienci korzystający z tych platform są uznawane za bezpieczne podane tego tylko maszyny wirtualne w jednej uaktualnienia domeny (UD) jest ograniczona w danym momencie. Samoobsługowe konserwacji jest obecnie niedostępna dla usługi w chmurze (rola sieci Web/proces roboczy), usługi Service Fabric i zestawy skalowania maszyny wirtualnej.

**Pytanie: czy mogę zostać odebrana wiadomość e-mail na temat likwidowania sprzętu, jest to taka sama jak zaplanowanej konserwacji?**

**Odpowiedź:** podczas likwidowania sprzętu jest zdarzeń planowanych konserwacji, mamy jeszcze nie został załadowany ten przypadek użycia do nowego środowiska.  

**Pytanie: nie widzę żadnych informacji konserwacji na moich maszynach wirtualnych. Co poszło źle?**

**Odpowiedź:** istnieje kilka przyczyn, dlaczego czasie nie widać żadnych informacji konserwacji na maszyny wirtualne:
1.  Używane są oznaczone jako Microsoft wewnętrzny subskrypcji.
2.  Maszyny wirtualne nie są zaplanowane do obsługi. Możliwe, że wave obsługi zostało zakończone, anulowane lub zmodyfikować tak, aby maszyny wirtualne są nie wpływa już go.
3.  Nie masz **konserwacji** kolumny dodanej do widoku listy maszyny Wirtualnej. Gdy ta kolumna dodano widok domyślny, klientów, którzy skonfigurowany tak, aby zobaczyć kolumn innych niż domyślne należy ręcznie dodać **konserwacji** kolumny do widoku listy ich maszyny Wirtualnej.

**Pytanie: czy Moje maszyny Wirtualnej jest zaplanowane do obsługi po raz drugi. Dlaczego?**

**Odpowiedź:** istnieje kilka przypadków użycia, gdy pojawi się zaplanowane do obsługi po ukończeniu już konserwacji-ponownego wdrażania maszyny Wirtualnej:
1.  Firma Microsoft ma anulowane wave konserwacji i ponownie uruchomić go z różnych ładunku. Możliwe, że wykryliśmy błędnej ładunku i po prostu należy wdrożyć dodatkowe ładunku.
2.  Maszyna wirtualna została *usługi zabliźnione* do innego węzła z powodu awarii sprzętowej
3.  Wybrano opcję zatrzymania (deallocate) i uruchom ponownie maszynę Wirtualną
4.  Masz **automatycznego zamykania** włączony dla maszyny Wirtualnej


**Pytanie: utrzymanie zestawu dostępności zajmuje dużo czasu, a teraz widoczne "pominięte" stan w przypadku niektórych Moje dostępność wystąpień. Dlaczego?** 

**Odpowiedź:** po kliknięciu zaktualizować wiele wystąpień w zestawie w krótkim odstępie czasu dostępności, Azure może umieścić w kolejce te żądania i uruchamia można zaktualizować tylko maszyn wirtualnych w domenie jedną aktualizację (UD) w czasie. Jednak ponieważ może to być Wstrzymaj między domenami aktualizacji, aktualizacja wydaje się trwać dłużej. Kolejki aktualizacji trwa dłużej niż 60 minut, niektórych wystąpień wyświetli **pominięte** stanu, nawet jeśli zostały one pomyślnie zaktualizowane. Aby uniknąć tego niewłaściwy stan, ustawia jego dostępność, klikając ich wystąpienia w obrębie jednej dostępności aktualizacji ustawić i poczekać na aktualizację na danej maszynie Wirtualnej, aby zakończyć przed kliknięciem przycisku Dalej maszyny wirtualnej w domenie innej aktualizacji.


## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak można zarejestrować obsługi zdarzeń z wewnątrz maszynę Wirtualną przy użyciu [zaplanowane zdarzenia](scheduled-events.md).
