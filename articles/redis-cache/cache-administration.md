---
title: "tooadminister aaaHow pamięć podręczna Redis Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak ponownie takich jak tooperform zadań administracyjnych i Zaplanuj aktualizacje dla pamięci podręcznej Redis Azure"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 8c915ae6-5322-4046-9938-8f7832403000
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 07/05/2017
ms.author: sdanie
ms.openlocfilehash: eb24668a3f6264444e7d4daf1ac43b41b12dfe66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadminister-azure-redis-cache"></a>Jak tooadminister Azure pamięci podręcznej Redis
W tym temacie opisano, jak administracja tooperform zadań takich jak [ponowny rozruch](#reboot) i [Planowanie aktualizacji](#schedule-updates) dla swoich wystąpień w pamięci podręcznej Redis Azure.

## <a name="reboot"></a>Ponowne uruchamianie
Witaj **ponowny rozruch** bloku umożliwia tooreboot co najmniej jeden węzeł z pamięci podręcznej. Ta możliwość ponownego uruchomienia umożliwia tootest możesz aplikacji zapewnia odporność na awarie w przypadku awarii węzła pamięci podręcznej.

![Ponowne uruchamianie](./media/cache-administration/redis-cache-administration-reboot.png)

Wybierz hello tooreboot węzłów, a następnie kliknij przycisk **ponowny rozruch**.

![Ponowne uruchamianie](./media/cache-administration/redis-cache-reboot.png)

Jeśli pamięć podręczna premium z włączoną funkcją klastrowania, można wybrać, które odłamków hello tooreboot pamięci podręcznej.

![Ponowne uruchamianie](./media/cache-administration/redis-cache-reboot-cluster.png)

tooreboot co najmniej jeden węzeł z pamięci podręcznej, wybierz węzeł hello potrzebne i kliknij przycisk **ponowny rozruch**. Jeśli masz usługi pamięć podręczna premium z włączoną funkcją klastrowania, wybierz tooreboot odłamków hello potrzebne, a następnie kliknij przycisk **ponowny rozruch**. Po kilku minutach hello ponownego uruchomienia wybranych węzłów i jest znowu w trybie online później za kilka minut.

Witaj wpływ na aplikacje klienckie różni się w zależności od węzły, które, ponowne uruchomienie.

* **Wzorzec** — w przypadku węzła głównego hello jest kończy się niepowodzeniem po ponownym rozruchu, Azure pamięć podręczna Redis nad węzłem repliki toohello i zamienia ją toomaster. Podczas tego trybu failover może być przez krótki czas, w którym połączenia może zakończyć się niepowodzeniem toohello pamięci podręcznej.
* **Podrzędny** — po ponownym uruchomieniu węzła podrzędna hello jest zwykle ma wpływ toocache klientów.
* **Zarówno i podrzędna** — w przypadku obu węzłów pamięci podręcznej są ponownie uruchamiane, wszystkie dane zostaną utracone w hello połączenia i pamięci podręcznej toohello pamięci podręcznej kończyć się niepowodzeniem, dopóki węzła podstawowego hello wraca do trybu online. Jeśli skonfigurowano [trwałości danych](cache-how-to-premium-persistence.md), hello najnowszej kopii zapasowej jest przywracany pamięci podręcznej hello wraca do trybu online, ale wszystkie zapisy pamięci podręcznej, które wystąpiły po utworzeniu ostatniej kopii zapasowej hello zostaną utracone.
* **Węzły w warstwie premium pamięci podręcznej z włączoną funkcją klastrowania** — w przypadku ponownego uruchamiania jednego lub więcej węzłów z klastra usługi pamięć podręczna premium włączone, hello zachowanie hello wybrane węzły są takie same hello jako po ponownym uruchomieniu węzła odpowiedniego hello lub w węzłach nieklastrowanych pamięć podręczna.

> [!IMPORTANT]
> Ponowne uruchomienie jest teraz dostępna dla wszystkich warstw cenowych.
> 
> 

## <a name="reboot-faq"></a>Ponowny rozruch — często zadawane pytania
* [Wybór węzła powinna I ponowny rozruch tootest Moja aplikacja?](#which-node-should-i-reboot-to-test-my-application)
* [Czy można ponownie połączeń klienckich tooclear hello w pamięci podręcznej?](#can-i-reboot-the-cache-to-clear-client-connections)
* [Spowoduje utratę danych z mojej pamięci podręcznej, jeśli I wykonaj ponowny rozruch?](#will-i-lose-data-from-my-cache-if-i-do-a-reboot)
* [Czy można ponownie moje pamięci podręcznej przy użyciu programu PowerShell, interfejsu wiersza polecenia lub innych narzędzi do zarządzania?](#can-i-reboot-my-cache-using-powershell-cli-or-other-management-tools)
* [Warstw cenowych, jakie może korzystać z funkcji ponownego uruchomienia hello?](#what-pricing-tiers-can-use-the-reboot-functionality)

### <a name="which-node-should-i-reboot-tootest-my-application"></a>Wybór węzła powinna I ponowny rozruch tootest Moja aplikacja?
odporności hello tootest aplikację przed awarią węzła podstawowego hello pamięci podręcznej, ponowne uruchomienie hello **wzorca** węzła. odporność hello tootest aplikację przed awariami hello węzła pomocniczego, ponowne uruchomienie hello **podrzędna** węzła. odporność hello tootest aplikacji przed całkowitą awarią hello pamięci podręcznej, ponowny rozruch **zarówno** węzłów.

### <a name="can-i-reboot-hello-cache-tooclear-client-connections"></a>Czy można ponownie połączeń klienckich tooclear hello w pamięci podręcznej?
Tak, jeśli ponowne uruchomienie z pamięci podręcznej hello wszystkich połączeń klientów zostały wyczyszczone. Może być przydatne w przypadku hello gdzie wszystkich połączeń klientów wyczerpaniu błąd logiczny tooa lub błędem w aplikacji klienckiej hello ponowny rozruch. Każda warstwa cenowa ma inną [limitów połączeń klienta](cache-configure.md#default-redis-server-configuration) dla hello różnych rozmiarach i po osiągnięciu tych limitów nie więcej połączeń klienta są akceptowane. Ponowny rozruch hello pamięci podręcznej zawiera tooclear sposób wszystkich połączeń klientów.

> [!IMPORTANT]
> Jeśli ponowne uruchomienie połączenia klienta pamięci podręcznej tooclear programie StackExchange.Redis automatycznie ponownie nawiąże połączenie po powrocie do trybu online hello węzeł pamięci podręcznej Redis. Gdy hello podstawowy problem nie zostanie rozwiązany, hello połączenia klienckie może nadal toobe wykorzystane.
> 
> 

### <a name="will-i-lose-data-from-my-cache-if-i-do-a-reboot"></a>Spowoduje utratę danych z mojej pamięci podręcznej, jeśli I wykonaj ponowny rozruch?
Jeśli ponowne uruchomienie obu hello **wzorca** i **podrzędna** węzłów, wszystkie dane w pamięci podręcznej hello (lub w tym niezależnych korzystania z usługi pamięć podręczna premium z włączoną funkcją klastrowania) zostaną utracone. Jeśli skonfigurowano [trwałości danych](cache-how-to-premium-persistence.md), hello najnowszej kopii zapasowej zostanie przywrócone, kiedy pamięci podręcznej hello wraca do trybu online, ale wszystkie zapisy pamięci podręcznej, które wystąpiły po kopii zapasowej hello zostaną utracone.

Jeśli ponowne uruchomienie tylko jednego z węzłów hello, dane nie są zwykle utracone, ale nadal może być. Na przykład, jeśli jest ponowny rozruch węzła głównego hello i pamięć podręczna zapisu jest w toku, hello danych z hello pamięć podręczna zapisu jest utracone. Będzie inny scenariusz utraty danych, jeśli ponownie jeden węzeł i innych hello węzła sytuacji toogo dół powodu niepowodzenia tooa na powitania tym samym czasie. Aby uzyskać więcej informacji na temat możliwych przyczyn utraty danych, zobacz [wystąpił toomy danych w pamięci podręcznej Redis?](https://gist.github.com/JonCole/b6354d92a2d51c141490f10142884ea4#file-whathappenedtomydatainredis-md)

### <a name="can-i-reboot-my-cache-using-powershell-cli-or-other-management-tools"></a>Czy można ponownie moje pamięci podręcznej przy użyciu programu PowerShell, interfejsu wiersza polecenia lub innych narzędzi do zarządzania?
Tak, dla środowiska PowerShell instrukcje można znaleźć [tooreboot pamięci podręcznej Redis](cache-howto-manage-redis-cache-powershell.md#to-reboot-a-redis-cache).

### <a name="what-pricing-tiers-can-use-hello-reboot-functionality"></a>Warstw cenowych, jakie może korzystać z funkcji ponownego uruchomienia hello?
Ponowne uruchomienie jest dostępna dla wszystkich warstw cenowych.

## <a name="schedule-updates"></a>Aktualizacje harmonogramu
Witaj **Zaplanuj aktualizacje** bloku umożliwia toodesignate okno obsługi pamięci podręcznej warstwy Premium. Okna obsługi hello jest określona, wszystkie aktualizacje serwera Redis są wprowadzane podczas tego okna. 

> [!NOTE] 
> okna obsługi Hello stosuje tylko aktualizacje serwera tooRedis i nie tooany Azure aktualizacji lub aktualizacji systemu operacyjnego toohello hello maszyn wirtualnych, obsługujące hello pamięci podręcznej.
> 
> 

![Aktualizacje harmonogramu](./media/cache-administration/redis-schedule-updates.png)

Sprawdź dni hello potrzeby toospecify okna konserwacji i określ hello godzina rozpoczęcia okna konserwacji dla każdego dnia i kliknij **OK**. Należy pamiętać, że czas okna obsługi hello jest w formacie UTC. 

> [!NOTE]
> Witaj oknie domyślnej konserwacji aktualizacji jest pięć godzin. Ta wartość nie jest konfigurowalne z hello portalu Azure, ale można go skonfigurować w programie PowerShell przy użyciu hello `MaintenanceWindow` parametru hello [AzureRmRedisCacheScheduleEntry nowy](/powershell/module/azurerm.rediscache/new-azurermrediscachescheduleentry) polecenia cmdlet. Aby uzyskać więcej informacji, zobacz [zaplanowanych aktualizacji przy użyciu programu PowerShell, interfejsu wiersza polecenia lub innych narzędzi do zarządzania można zarządzać?](#can-i-manage-scheduled-updates-using-powershell-cli-or-other-management-tools)
> 
> 

## <a name="schedule-updates-faq"></a>Zaplanuj aktualizacje — często zadawane pytania
* [Gdy aktualizacje wystąpić, jeśli nie jest używany hello harmonogram aktualizacji funkcji?](#when-do-updates-occur-if-i-dont-use-the-schedule-updates-feature)
* [Jakiego rodzaju aktualizacje są wprowadzane podczas hello zaplanowane okna obsługi?](#what-type-of-updates-are-made-during-the-scheduled-maintenance-window)
* [Zaplanowane aktualizacje przy użyciu programu PowerShell, interfejsu wiersza polecenia lub innych narzędzi do zarządzania można zarządzać?](#can-i-managed-scheduled-updates-using-powershell-cli-or-other-management-tools)
* [Warstw cenowych, jakie może korzystać z funkcji aktualizacji harmonogram hello?](#what-pricing-tiers-can-use-the-schedule-updates-functionality)

### <a name="when-do-updates-occur-if-i-dont-use-hello-schedule-updates-feature"></a>Gdy aktualizacje wystąpić, jeśli nie jest używany hello harmonogram aktualizacji funkcji?
Jeśli nie określisz okna obsługi, aktualizacje mogą być dokonywane w dowolnym momencie.

### <a name="what-type-of-updates-are-made-during-hello-scheduled-maintenance-window"></a>Jakiego rodzaju aktualizacje są wprowadzane podczas hello zaplanowane okna obsługi?
Tylko pamięci podręcznej Redis serwera wprowadzone aktualizacje hello zaplanowanym oknie obsługi. okna obsługi Hello aktualizacji systemu operacyjnego maszyny Wirtualnej toohello lub nie ma zastosowania aktualizacji tooAzure.

### <a name="can-i-managed-scheduled-updates-using-powershell-cli-or-other-management-tools"></a>Czy mogę zarządzanego, zaplanowanych aktualizacji przy użyciu programu PowerShell, interfejsu wiersza polecenia lub innych narzędzi do zarządzania?
Tak, można zarządzać za pomocą następującego polecenia cmdlet programu PowerShell hello zaplanowane aktualizacje:

* [Get-AzureRmRedisCachePatchSchedule](/powershell/module/azurerm.rediscache/get-azurermrediscachepatchschedule)
* [Nowe AzureRmRedisCachePatchSchedule](/powershell/module/azurerm.rediscache/new-azurermrediscachepatchschedule)
* [Nowe AzureRmRedisCacheScheduleEntry](/powershell/module/azurerm.rediscache/new-azurermrediscachescheduleentry)
* [Usuń AzureRmRedisCachePatchSchedule](/powershell/module/azurerm.rediscache/remove-azurermrediscachepatchschedule)

### <a name="what-pricing-tiers-can-use-hello-schedule-updates-functionality"></a>Warstw cenowych, jakie może korzystać z funkcji aktualizacji harmonogram hello?
Witaj **Zaplanuj aktualizacje** funkcja jest dostępna tylko w warstwie cenowej premium hello.

## <a name="next-steps"></a>Następne kroki
* Poznaj więcej [warstwy premium usługi pamięć podręczna Redis Azure](cache-premium-tier-intro.md) funkcji.

