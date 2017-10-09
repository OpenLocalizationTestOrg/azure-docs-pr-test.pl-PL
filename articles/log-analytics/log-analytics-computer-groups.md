---
title: "grupy aaaComputer w analizy dzienników dziennika wyszukiwania | Dokumentacja firmy Microsoft"
description: "Grupy komputerów w analizy dzienników pozwalają tooscope dziennik wyszukiwania tooa określonego zestawu komputerów.  W tym artykule opisano różne metody hello można użyć grupy komputerów toocreate i jak toouse je w dzienniku wyszukiwania."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: a28b9e8a-6761-4ead-aa61-c8451ca90125
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: bwren
ms.openlocfilehash: 7dafea9829e541f5582a1d855fafb82aa4d94430
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="computer-groups-in-log-analytics-log-searches"></a>Zaloguj się wyszukiwanie grup komputerów w analizy dzienników

>[!NOTE]
> W tym artykule opisano hello używanie grup komputerów przy użyciu hello bieżący język kwerendy Anayltics dziennika.    Jeśli obszaru roboczego został uaktualniony toohello [języka zapytań nowe analizy dzienników](log-analytics-log-search-upgrade.md), grup komputerów działać inaczej.  Informacje o znajdują się w tym artykule i hello inną składnię i zachowanie hello nowy język kwerendy.  


Grupy komputerów w analizy dzienników pozwalają tooscope [dziennika wyszukiwania](log-analytics-log-searches.md) tooa określonego zestawu komputerów.  Każda grupa jest wypełniana z komputerami za pomocą zapytanie, które należy zdefiniować lub importując grup z różnych źródeł.  Podczas wyszukiwania dziennika zawiera grupy hello, hello wyniki są ograniczone toorecords, odpowiadających hello komputerów w grupie hello.

## <a name="creating-a-computer-group"></a>Tworzenie grupy komputerów
Można utworzyć grupę komputerów w analizy dzienników przy użyciu dowolnej z metod hello w hello w poniższej tabeli.  Szczegółowe informacje o poszczególnych metod znajdują się w poniższych sekcjach hello. 

| Metoda | Opis |
|:--- |:--- |
| Wyszukiwanie w dzienniku |Utwórz wyszukiwania dziennika, które zwraca listę komputerów i Zapisz wyniki hello jako grupę komputerów. |
| Interfejs API wyszukiwania w dzienniku |Użyj hello interfejs API dziennika wyszukiwania tooprogrammatically Tworzenie grupy komputerów, na podstawie wyników hello wyszukiwania dziennika. |
| Usługa Active Directory |Automatyczne skanowanie hello członkostwo w grupie na wszystkich komputerach agenta, które są członkami domeny usługi Active Directory i utworzyć grupę w analizy dzienników dla każdej grupy zabezpieczeń. |
| PROGRAM WSUS |Skanowanie serwerów WSUS lub klientów do użycia z grup i automatycznie utworzyć grupę w analizy dzienników dla każdego. |

### <a name="log-search"></a>Wyszukiwanie w dzienniku
Grupy komputerów utworzone na podstawie wyszukiwania dziennika zawiera wszystkie komputery hello zwróconych przez zapytanie wyszukiwania, który należy zdefiniować.  To zapytanie jest uruchamiane za każdym razem, gdy grupy komputerów hello jest używany, aby wszelkie zmiany od czasu utworzenia grupy hello jest odzwierciedlone.

Użyj poniższych toocreate procedury grupy komputerów z wyszukiwania dziennika hello.

1. [Tworzenie wyszukiwania dziennika](log-analytics-log-searches.md) które zwraca listę komputerów.  Witaj wyszukiwania musi zwracać różne zestaw komputerów przy użyciu wyglądać mniej więcej tak **Distinct Computer** lub **miar count() przez komputer** hello zapytania.  
2. Kliknij przycisk hello **zapisać** przycisk u góry hello hello ekranu.
3. Wybierz **tak** za**Zapisz to zapytanie jako grupę komputerów**.
4. Wpisz w **nazwa** i **kategorii** hello grupy.  Jeśli wyszukiwanie na podstawie hello samą nazwą i kategorią już istnieje, a następnie można toooverwrite zostanie wyświetlony monit o jej.  Może mieć wiele wyszukiwania za pomocą hello takie same nazwy w różnych kategoriach. 

Poniżej przedstawiono przykładowe wyszukiwania, które można zapisać jako grupę komputerów.

    Computer="Computer1" OR Computer="Computer2" | distinct Computer 
    Computer=*srv* | measure count() by Computer

>[!NOTE]
> Jeśli obszaru roboczego został uaktualniony toohello [języka zapytań nowe analizy dzienników](log-analytics-log-search-upgrade.md) , a następnie hello są następujące zmiany wykonane toohello procedury toocreate Nowa grupa komputerów.
>  
> - Witaj toocreate zapytania musi zawierać grupę komputerów `distinct Computer`.  Poniżej przedstawiono przykład toocreate zapytania grupy komputerów.<br>`Heartbeat | where Computer contains "srv" `
> - Podczas tworzenia nowej grupy komputerów, należy określić w nazwie toohello dodanie aliasu.  Hello alias jest używany, gdy przy użyciu hello grupy komputerów w zapytaniu, zgodnie z poniższym opisem.  

### <a name="log-search-api"></a>Dziennik wyszukiwania interfejsu API
Grupy komputerów utworzone za pomocą hello interfejs API dziennika wyszukiwania są hello same wyszukiwania utworzonych za pomocą wyszukiwania dziennika.

Szczegółowe informacje na temat tworzenia grupy komputerów przy użyciu hello interfejs API dziennika wyszukiwania można znaleźć [grup komputerów w dzienniku analizy dzienników wyszukiwania interfejsu API REST](log-analytics-log-search-api.md#computer-groups).

### <a name="active-directory"></a>Usługa Active Directory
Podczas konfigurowania członkostwa w grupach usługi Active Directory tooimport Log Analytics analizuje hello członkostwa w grupie komputerów przyłączonych do domeny z agentem pakietu OMS hello.  Grupa komputerów jest tworzony w analizy dzienników dla każdej grupy zabezpieczeń w usłudze Active Directory, a każdy komputer został dodany odpowiadającego toohello grup zabezpieczeń, które są członkami grup komputerów toohello.  To członkostwo jest stale aktualizowany co 4 godziny.  

Konfigurowanie grup zabezpieczeń usługi Active Directory tooimport analizy dzienników z hello **grup komputerów** menu analizy dzienników **ustawienia**.  Wybierz **automatyzacji** , a następnie **członkostwa w grupach usługi Active Directory importu z komputerów**.  Nie są wymagane żadne dalsze czynności konfiguracyjne.

![Grupy komputerów z usługi Active Directory](media/log-analytics-computer-groups/configure-activedirectory.png)

Gdy grupy zostały zaimportowane, hello menu listy hello liczba komputerów z członkostwem grupy wykrywane i hello wiele grup zaimportowane.  Możesz kliknąć jeden z tych hello tooreturn łącza **Grupa_komputerów** rekordy z tymi informacjami.

### <a name="windows-server-update-service"></a>Windows Server Update Service
Po skonfigurowaniu członkostw tooimport analizy dzienników usług WSUS, analizę hello przeznaczonych dla wszystkie komputery z agentem pakietu OMS hello członkostwo w grupie.  Jeśli używasz klienta przeznaczonych dla dowolnego komputera, który jest połączony tooOMS i jest częścią żadnych WSUS przypisywania grup członkostwa w grupie zaimportował tooLog Analytics. Jeśli używasz po stronie serwera celem hello, który powinien być zainstalowany agent pakietu OMS na powitania WSUS serwera toobe informacji członkostwa grupy hello zaimportowane tooOMS.  To członkostwo jest stale aktualizowany co 4 godziny. 

Konfigurowanie grup zabezpieczeń usługi Active Directory tooimport analizy dzienników z hello **grup komputerów** menu analizy dzienników **ustawienia**.  Wybierz **usługi Active Directory** , a następnie **członkostwa w grupach usługi Active Directory importu z komputerów**.  Nie są wymagane żadne dalsze czynności konfiguracyjne.

![Grupy komputerów z usługi Active Directory](media/log-analytics-computer-groups/configure-wsus.png)

Gdy grupy zostały zaimportowane, hello menu listy hello liczba komputerów z członkostwem grupy wykrywane i hello wiele grup zaimportowane.  Możesz kliknąć jeden z tych hello tooreturn łącza **Grupa_komputerów** rekordy z tymi informacjami.

## <a name="managing-computer-groups"></a>Zarządzanie grupami komputerów
Możesz wyświetlić grupy komputerów, które zostały utworzone na podstawie wyszukiwania dziennika lub hello interfejs API dziennika wyszukiwania z hello **grup komputerów** menu analizy dzienników **ustawienia**.  Kliknij przycisk hello **x** w hello **Usuń** grupy komputerów hello toodelete kolumny.  Kliknij przycisk hello **Wyświetlanie członków** ikony wyszukiwania dziennika grupy hello toorun grupy, które zwraca jej elementów członkowskich. 

![Grupy komputerów zapisane](media/log-analytics-computer-groups/configure-saved.png)

toomodify hello grupy, Utwórz nową grupy z hello sam **kategorii** i **nazwa** toooverwrite hello oryginalnej grupy.

## <a name="using-a-computer-group-in-a-log-search"></a>W wyszukiwaniu dziennika przy użyciu grupy komputerów
Możesz użyć hello następujące grupy komputerów tooa toorefer składni wyszukiwania dziennika.  Określanie hello **kategorii** jest opcjonalny i tylko wymagane, jeśli masz grup komputerów z hello takie same nazwy w różnych kategoriach. 

    $ComputerGroups[Category: Name]

Po uruchomieniu wyszukiwania, najpierw zostaną rozpoznane hello członkami grupy komputera wyszukiwania hello uwzględniane.  Jeśli grupa hello jest oparta na wyszukiwania dziennika, tego wyszukiwania jest uruchamiane tooreturn hello członkami grupy hello przed wykonaniem hello wyszukiwania najwyższego poziomu dziennika.

Grupy komputerów są zazwyczaj używane z hello **IN** klauzuli hello dziennik wyszukiwania jak hello poniższy przykład:

    Type=UpdateSummary Computer IN $ComputerGroups[My Computer Group]

>[!NOTE]
> Jeśli obszaru roboczego został uaktualniony toohello [języka zapytań nowe analizy dzienników](log-analytics-log-search-upgrade.md), a następnie użyć grupy komputerów w zapytaniu, traktując jej aliasem jako funkcja jak hello poniższy przykład:
> 
>  `UpdateSummary | where Computer IN (MyComputerGroup)`

## <a name="computer-group-records"></a>Rekordów grupy komputerów
Zostaje utworzony rekord w hello OMS repozytorium dla każdego członkostwa grup komputerów utworzone na podstawie usługi Active Directory lub usług WSUS.  Te rekordy mieć typu **Grupa_komputerów** i mają właściwości hello w hello w poniższej tabeli.  Rekordy nie są tworzone dla grup komputerów opartych na dziennik wyszukiwania.

| Właściwość | Opis |
|:--- |:--- |
| Typ |*Grupa_komputerów* |
| SourceSystem |*SourceSystem* |
| Computer (Komputer) |Nazwa komputera członkowskiego hello. |
| Grupa |Nazwa grupy hello. |
| GroupFullName |Pełna ścieżka grupy toohello tym hello źródło i nazwa źródła. |
| GroupSource |Źródło tej grupy zostały zebrane z. <br><br>Polecenie cmdlet<br>PROGRAM WSUS<br>WSUSClientTargeting |
| GroupSourceName |Nazwa źródła hello hello grupy zostały zebrane.  Dla usługi Active Directory to hello nazwy domeny. |
| ManagementGroupName |Nazwa grupy zarządzania hello agentów programu SCOM.  W przypadku innych agentów jest AOI -\<identyfikator obszaru roboczego\> |
| TimeGenerated |Grupa komputerów hello Data i godzina utworzenia lub aktualizacji. |

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o [dziennika wyszukiwania](log-analytics-log-searches.md) tooanalyze hello dane zebrane ze źródeł danych i rozwiązań.  

