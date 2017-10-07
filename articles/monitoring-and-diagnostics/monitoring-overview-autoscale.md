---
title: "aaaOverview automatycznego skalowania w maszynach wirtualnych platformy Azure firmy Microsoft, usługi w chmurze i aplikacje sieci Web | Dokumentacja firmy Microsoft"
description: "Omówienie automatycznego skalowania na platformie Microsoft Azure. Stosuje tooVirtual maszyny, Cloud Services i aplikacji sieci Web."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 74bf03be-e658-4239-a214-c12424b53e4c
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/02/2016
ms.author: robb
ms.openlocfilehash: ef68b722ea22c4149a7d7a89c5855ba761db9247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-autoscale-in-microsoft-azure-virtual-machines-cloud-services-and-web-apps"></a>Omówienie automatycznego skalowania w maszynach wirtualnych platformy Azure firmy Microsoft, usługi w chmurze i aplikacje sieci Web
W tym artykule opisano jest jakie skalowania automatycznego Microsoft Azure, jego zalety i sposób tooget uruchamiania, przy jej użyciu.  

Azure Monitor skalowania automatycznego ma zastosowanie tylko zbyt[zestawy skalowania maszyny wirtualnej](https://azure.microsoft.com/services/virtual-machine-scale-sets/), [usługi w chmurze](https://azure.microsoft.com/services/cloud-services/), i [usługi aplikacji — aplikacje sieci Web](https://azure.microsoft.com/services/app-service/web/).

> [!NOTE]
> Platforma Azure ma dwie metody automatycznego skalowania. Starsza wersja programu skalowania automatycznego ma zastosowanie tooVirtual maszyny (zestawy dostępności). Ta funkcja ma ograniczony pomocy technicznej i zaleca się migrowanie skalowania maszyny toovirtual ustawia obsługi automatycznego skalowania szybszy i bardziej niezawodny. Łącze w sposób toouse hello starszych technologii znajduje się w tym artykule.  
>
>

## <a name="what-is-autoscale"></a>Co to jest funkcja automatycznego skalowania?
Skalowania automatycznego umożliwia toohave hello ilości zasobów obciążenia hello toohandle w swojej aplikacji. Pozwala ona zasoby tooadd zwiększa toohandle w obciążeniu, a także oszczędzić pieniądze przez usunięcie zasobów, które są obecne w stanie bezczynności. Określ minimalną i maksymalną liczbę wystąpień toorun i dodać lub usunąć maszyny wirtualnej automatycznie na podstawie zestawu reguł. O minimalnej sprawia, że czy aplikacja zawsze działa nawet w przypadku obciążenia. O maksymalnej ogranicza łącznym możliwy koszt co godzinę. Automatycznie skalować między te dwie wartości graniczne przy użyciu utworzone reguły.

 ![Wyjaśniono skalowania automatycznego. Dodawanie i usuwanie maszyny wirtualne](./media/monitoring-overview-autoscale/AutoscaleConcept.png)

Gdy warunki reguły są spełnione, co najmniej jednej akcji skalowania automatycznego są wyzwalane. Można dodać i usunąć maszyny wirtualnej lub wykonywać inne akcje. Witaj następujący diagram koncepcyjny ten proces został przedstawiony.  

 ![Diagram przepływu skalowania automatycznego](./media/monitoring-overview-autoscale/Autoscale_Overview_v4.png)

Witaj wyjaśnienia poniżej dotyczy toohello części hello poprzedni diagram.   

## <a name="resource-metrics"></a>Metryki dla zasobu
Zasoby Emituj metryki, te metryki są później przetwarzane przez zasady. Metryki dostarczane za pomocą różnych metod.
Zestawy skalowania maszyny wirtualnej Użyj danych telemetrycznych z agentów diagnostyki Azure, natomiast dane telemetryczne dla aplikacji sieci Web i usługi w chmurze pochodzi bezpośrednio z hello infrastruktury platformy Azure. Niektóre często używane dane statystyczne obejmują użycie procesora CPU, pamięć liczników wątków, długość kolejki i użycie dysku. Aby uzyskać listę danych telemetrycznych można użyć, zobacz [wspólnej metryki automatycznego skalowania](insights-autoscale-common-metrics.md).

## <a name="custom-metrics"></a>Metryki niestandardowe
Można również wykorzystać własne niestandardowe metryki, które mogą być emitowanie Twojej aplikacji. Jeśli skonfigurowano tooApplication metryki Insights mogą korzystać z tych decyzji toomake metryki od tego, czy Twoje aplikacje toosend tooscale lub nie. 

## <a name="time"></a>Time
Reguły na podstawie harmonogramu są oparte na czas UTC. Należy poprawnie ustawić strefy czasowej podczas konfigurowania reguł.  

## <a name="rules"></a>Reguły
Witaj diagram przedstawia tylko jedną regułę automatycznego skalowania, ale można mieć wiele z nich. Można utworzyć złożone zasady nakładające się odpowiednio do potrzeb.  Typy reguł  

* **Na podstawie Metryka** — na przykład, wykonaj tę akcję, gdy wykorzystanie Procesora jest powyżej 50%.
* **Na podstawie czasu** — na przykład wyzwalacza elementu webhook co 8 am w sobotę danego strefy czasowej.

Reguły metryki pomiaru obciążenia aplikacji i Dodaj lub usuń maszyny wirtualne oparte na tym obciążenia. Zasady oparte na harmonogramie Zezwalaj tooscale podczas Zobacz wzorce czasu w obciążenia i mają tooscale przed wzrostu obciążenia można lub zmniejszenie.  

## <a name="actions-and-automation"></a>Akcje i automatyzacji
Reguły może wyzwolić co najmniej jeden typ akcji.

* **Skala** -VMs skali przychodzący lub wychodzący
* **Wiadomości e-mail** — Wyślij e-mail toosubscription Administratorzy, co Administratorzy i/lub dodatkowy adres e-mail użytkownika
* **Zautomatyzować za pomocą elementów webhook** -Wywołaj elementów webhook, co może uruchamiać wiele złożonych akcji wewnątrz lub na zewnątrz Azure. Wewnątrz Azure można uruchomić elementu runbook usługi Automatyzacja Azure, funkcji platformy Azure lub aplikacji logiki platformy Azure. Przykładowy adres URL innych firm poza Azure obejmują usług takich jak zapas czasu i usługi Twilio.

## <a name="autoscale-settings"></a>Ustawienia skalowania automatycznego
Skalowania automatycznego Użyj następujących hello terminologii i struktury.

- **Ustawieniu skalowania automatycznego** jest odczytywany przez hello skalowania automatycznego aparatu toodetermine czy tooscale w górę lub w dół. Zawiera jeden lub więcej profilów, informacje dotyczące zasobu docelowego hello i ustawień powiadomień.

    - **Profilów skalowania automatycznego** jest kombinacją a:

        - **Ustawienia pojemności**, co oznacza hello minimalna, maksymalna i domyślne wartości dla wielu wystąpień.
        - **zestaw reguł**, z których każdy zawiera wyzwalacz (czas lub Metryka) oraz akcję skalowania (w górę lub w dół).
        - **Cykl**, co oznacza, że podczas skalowania automatycznego powinien obowiązywać tego profilu.

        Może mieć wiele profilów, umożliwiających tootake nad wymagania nakładające się różnią. Na przykład może mieć profilów skalowania automatycznego różne dla różnych porach dnia lub dni tygodnia hello.

    - A **ustawienie powiadomień o** definiuje, jakie powiadomień powinna wystąpić, gdy wystąpi zdarzenie skalowania automatycznego oparte na spełniających kryteria hello jednego ustawienia skalowania automatycznego hello profilów. Skalowania automatycznego można powiadomić co najmniej jeden adres e-mail lub tooone wywołania lub więcej elementów webhook.


![Ustawienia skalowania automatycznego Azure, profilu i struktury reguły](./media/monitoring-overview-autoscale/AzureResourceManagerRuleStructure3.png)

Witaj pełną listę można konfigurować pól i opisy jest dostępna w hello [interfejsu API REST skalowania automatycznego](https://msdn.microsoft.com/library/dn931928.aspx).

Aby uzyskać przykłady kodu zobacz

* [Zestawy skalowania maszyny Wirtualnej za pomocą szablonów usługi Resource Manager konfiguracji zaawansowanej skalowania automatycznego](insights-advanced-autoscale-virtual-machine-scale-sets.md)  
* [Interfejs API REST skalowania automatycznego](https://msdn.microsoft.com/library/dn931953.aspx)

## <a name="horizontal-vs-vertical-scaling"></a>Pionowy skalowanie w poziomie vs
Skalowania automatycznego tylko skalowanie w poziomie, wzrost ("out") lub spadek ("") w hello liczba wystąpień maszyn wirtualnych.  Poziomy jest bardziej elastyczna w sytuacji, w chmurze, ponieważ pozwala toorun tysięcy obciążenia toohandle maszyn wirtualnych.

Z kolei skalowanie w pionie różni się. Ją zachowuje hello tej samej liczby maszyn wirtualnych, ale powoduje, że hello maszyn wirtualnych więcej ("w górę") lub mniej ("wyłączone") zaawansowane. Power jest mierzony w pamięci, szybkości Procesora, miejsca na dysku itp.  Skalowanie w pionie ma więcej ograniczeń. Jest on zależny od dostępności hello większych sprzętu, która szybko trafienia górny limit i zależą od regionu. Pionowego, skalowania również zwykle wymaga toostop maszyny Wirtualnej i uruchom ponownie.

Aby uzyskać więcej informacji, zobacz [skalowanie w pionie maszyny wirtualnej platformy Azure w usłudze Automatyzacja Azure](../virtual-machines/linux/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="methods-of-access"></a>Metody dostępu
Możesz skonfigurować automatycznego skalowania za pomocą

* [Witryna Azure Portal](insights-how-to-scale.md)
* [PowerShell](insights-powershell-samples.md#create-and-manage-autoscale-settings)
* [Interfejs wiersza polecenia i platform (CLI)](insights-cli-samples.md#autoscale)
* [Interfejs API REST Azure monitora](https://msdn.microsoft.com/library/azure/dn931953.aspx)

## <a name="supported-services-for-autoscale"></a>Obsługiwane usługi do skalowania automatycznego
| Usługa | Schemat & dokumentów |
| --- | --- |
| Web Apps |[Skalowanie aplikacji sieci Web](insights-how-to-scale.md) |
| Cloud Services |[Funkcja automatycznego skalowania usługi w chmurze](../cloud-services/cloud-services-how-to-scale.md) |
| Maszyny wirtualne: klasycznym |[Skalowanie zestawów dostępności klasyczne maszyny wirtualnej](https://blogs.msdn.microsoft.com/kaevans/2015/02/20/autoscaling-azurevirtual-machines/) |
| Maszyn wirtualnych: Zestawy skalowania systemu Windows |[Ustawia skalowanie skalowania maszyny wirtualnej w systemie Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) |
| Maszyn wirtualnych: Ustawia Linux skalowania |[Ustawia skalowanie skalowania maszyny wirtualnej w systemie Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) |
| Maszyny wirtualnej: Przykład systemu Windows |[Zestawy skalowania maszyny Wirtualnej za pomocą szablonów usługi Resource Manager konfiguracji zaawansowanej skalowania automatycznego](insights-advanced-autoscale-virtual-machine-scale-sets.md) |

## <a name="next-steps"></a>Następne kroki
toolearn więcej informacji na temat skalowania automatycznego, użyj powitalne wskazówki skalowania automatycznego wymienionymi wcześniej, lub można znaleźć toohello następujące zasoby:

* [Azure metryki wspólnej skalowania automatycznego monitora](insights-autoscale-common-metrics.md)
* [Najlepsze praktyki dotyczące skalowania automatycznego Azure Monitor](insights-autoscale-best-practices.md)
* [Użyj automatycznego skalowania akcje toosend poczty e-mail i elementu webhook powiadomień o alertach](insights-autoscale-to-webhook-email.md)
* [Interfejs API REST skalowania automatycznego](https://msdn.microsoft.com/library/dn931953.aspx)
* [Rozwiązywania problemów skalowania automatycznego zestawy skalowania maszyny wirtualnej](../virtual-machine-scale-sets/virtual-machine-scale-sets-troubleshoot.md)
