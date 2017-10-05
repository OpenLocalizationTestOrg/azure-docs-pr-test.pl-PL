---
title: "Grupy komputerów w analizy dzienników dziennika wyszukiwania | Dokumentacja firmy Microsoft"
description: "Grupy komputerów w analizy dzienników umożliwiają zakres wyszukiwania dziennika do określonego zestawu komputerów.  W tym artykule opisano różne metody używanej do tworzenia grup komputerów i sposobu ich używania w wyszukiwaniu dziennika."
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
ms.openlocfilehash: a2ddc932343d54963a378ee27dc962a790326b2a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="computer-groups-in-log-analytics-log-searches"></a>Zaloguj się wyszukiwanie grup komputerów w analizy dzienników

>[!NOTE]
> W tym artykule opisano korzystanie z grup komputerów przy użyciu języka bieżącego zapytania Anayltics dziennika.    Jeśli został uaktualniony do obszaru roboczego [języka zapytań nowe analizy dzienników](log-analytics-log-search-upgrade.md), grup komputerów działać inaczej.  Informacje są dostępne w tym artykule z inną składnię i zachowanie dla nowy język kwerendy.  


Grupy komputerów w analizy dzienników umożliwiają zakresu [dziennika wyszukiwania](log-analytics-log-searches.md) do określonego zestawu komputerów.  Każda grupa jest wypełniana z komputerami za pomocą zapytanie, które należy zdefiniować lub importując grup z różnych źródeł.  Podczas wyszukiwania dziennika zawiera grupy, wyniki są ograniczone do rekordów, które spełniają komputerów w grupie.

## <a name="creating-a-computer-group"></a>Tworzenie grupy komputerów
Można utworzyć grupę komputerów w analizy dzienników przy użyciu dowolnej z metod w poniższej tabeli.  W poniższych sekcjach znajdują się szczegółowe informacje o każdej z metod. 

| Metoda | Opis |
|:--- |:--- |
| Wyszukiwanie w dzienniku |Utwórz wyszukiwania dziennika, które zwraca listę komputerów i Zapisz wyniki jako grupę komputerów. |
| Interfejs API wyszukiwania w dzienniku |Programowe tworzenie grupy komputerów, na podstawie wyników wyszukiwania dziennika za pomocą interfejsu API wyszukiwania dziennika. |
| Usługa Active Directory |Automatyczne skanowanie członkostwo w grupie na wszystkich komputerach agenta, które są członkami domeny usługi Active Directory i utworzyć grupę w analizy dzienników dla każdej grupy zabezpieczeń. |
| PROGRAM WSUS |Skanowanie serwerów WSUS lub klientów do użycia z grup i automatycznie utworzyć grupę w analizy dzienników dla każdego. |

### <a name="log-search"></a>Wyszukiwanie w dzienniku
Grupy komputerów utworzone na podstawie wyszukiwania dziennika zawiera wszystkie komputery zwróconych przez zapytanie wyszukiwania, który należy zdefiniować.  To zapytanie jest uruchamiane za każdym razem, grupa komputerów jest używany tak, aby wszelkie zmiany, ponieważ grupa została utworzona ta jest uwzględniana.

Poniższa procedura umożliwia utworzenie grupy komputerów z wyszukiwania dziennika.

1. [Tworzenie wyszukiwania dziennika](log-analytics-log-searches.md) które zwraca listę komputerów.  Wyszukiwanie musi zwracać różne zestaw komputerów przy użyciu przypominać **Distinct Computer** lub **miar count() przez komputer** w zapytaniu.  
2. Kliknij przycisk **zapisać** przycisk w górnej części ekranu.
3. Wybierz **tak** do **Zapisz to zapytanie jako grupę komputerów**.
4. Wpisz w **nazwa** i **kategorii** dla grupy.  Jeśli wyszukiwanie o tej samej nazwie i kategorii już istnieje, następnie należy monit go zastąpić.  Może mieć wiele wyszukiwanie o tej samej nazwie w różnych kategoriach. 

Poniżej przedstawiono przykładowe wyszukiwania, które można zapisać jako grupę komputerów.

    Computer="Computer1" OR Computer="Computer2" | distinct Computer 
    Computer=*srv* | measure count() by Computer

>[!NOTE]
> Jeśli obszaru roboczego został uaktualniony do [języka zapytań nowe analizy dzienników](log-analytics-log-search-upgrade.md) , a następnie następujące zmiany zostały wprowadzone procedury można utworzyć nowej grupy komputerów.
>  
> - Zapytanie w celu utworzenia grupy komputerów musi zawierać `distinct Computer`.  Poniżej przedstawiono przykład kwerendy można utworzyć grupę komputerów.<br>`Heartbeat | where Computer contains "srv" `
> - Podczas tworzenia nowej grupy komputerów, należy określić alias oprócz nazwy.  Alias jest używany, gdy za pomocą grupy komputerów w zapytaniu, zgodnie z poniższym opisem.  

### <a name="log-search-api"></a>Dziennik wyszukiwania interfejsu API
Grupy komputerów utworzone za pomocą interfejsu API Search dziennika są takie same jak wyszukiwania utworzonych za pomocą wyszukiwania dziennika.

Aby uzyskać więcej informacji na temat tworzenia grupy komputerów przy użyciu interfejsu API Search dziennika zobacz [grup komputerów w dzienniku analizy dzienników wyszukiwania interfejsu API REST](log-analytics-log-search-api.md#computer-groups).

### <a name="active-directory"></a>Usługa Active Directory
Podczas konfigurowania analizy dzienników do zaimportowania członkostwa w grupach usługi Active Directory, analizuje członkostwo w grupie komputerów przyłączonych do domeny z agentem pakietu OMS.  Grupa komputerów jest tworzony w analizy dzienników dla każdej grupy zabezpieczeń w usłudze Active Directory, a każdy komputer jest dodawany do odpowiadającego do grupy zabezpieczeń, które są oni członkami grupy komputerów.  To członkostwo jest stale aktualizowany co 4 godziny.  

Konfigurowanie analizy dzienników do zaimportowania grup zabezpieczeń usługi Active Directory z **grup komputerów** menu analizy dzienników **ustawienia**.  Wybierz **automatyzacji** , a następnie **członkostwa w grupach usługi Active Directory importu z komputerów**.  Nie są wymagane żadne dalsze czynności konfiguracyjne.

![Grupy komputerów z usługi Active Directory](media/log-analytics-computer-groups/configure-activedirectory.png)

Grupy zostały zaimportowane, menu znajdują się liczba komputerów z członkostwem grupy wykryte i liczby grup zaimportowane.  Możesz kliknąć jeden z poniższych linków, aby zwrócić **Grupa_komputerów** rekordy z tymi informacjami.

### <a name="windows-server-update-service"></a>Windows Server Update Service
Podczas konfigurowania analizy dzienników do zaimportowania członkostwa w grupach usług WSUS, analizuje docelowych członkostwo w grupie komputerów z agentem pakietu OMS.  Jeśli używasz klienta przeznaczonych dla dowolnego komputera, który jest połączony z usługą OMS i jest częścią żadnych WSUS przypisywania grup ma jego przynależność zaimportowany do analizy dzienników. Jeśli używasz po stronie serwera celem OMS powinien być zainstalowany agent na serwerze programu WSUS w taki sposób, aby informacje o członkostwie grupy do zaimportowania z usługą OMS.  To członkostwo jest stale aktualizowany co 4 godziny. 

Konfigurowanie analizy dzienników do zaimportowania grup zabezpieczeń usługi Active Directory z **grup komputerów** menu analizy dzienników **ustawienia**.  Wybierz **usługi Active Directory** , a następnie **członkostwa w grupach usługi Active Directory importu z komputerów**.  Nie są wymagane żadne dalsze czynności konfiguracyjne.

![Grupy komputerów z usługi Active Directory](media/log-analytics-computer-groups/configure-wsus.png)

Grupy zostały zaimportowane, menu znajdują się liczba komputerów z członkostwem grupy wykryte i liczby grup zaimportowane.  Możesz kliknąć jeden z poniższych linków, aby zwrócić **Grupa_komputerów** rekordy z tymi informacjami.

## <a name="managing-computer-groups"></a>Zarządzanie grupami komputerów
Możesz wyświetlić grupy komputerów, które zostały utworzone na podstawie wyszukiwania dziennika lub interfejsu API dziennika wyszukiwania z **grup komputerów** menu analizy dzienników **ustawienia**.  Kliknij przycisk **x** w **Usuń** kolumna usunąć grupę komputerów.  Kliknij przycisk **Wyświetlanie członków** ikona grupy do uruchamiania grupy dziennik wyszukiwania, które zwraca jej elementów członkowskich. 

![Grupy komputerów zapisane](media/log-analytics-computer-groups/configure-saved.png)

Aby zmodyfikować grupę, należy utworzyć nową grupę o tej samej **kategorii** i **nazwa** zastąpić oryginalnej grupy.

## <a name="using-a-computer-group-in-a-log-search"></a>W wyszukiwaniu dziennika przy użyciu grupy komputerów
Następująca składnia jest używana do odwoływania się do grupy komputerów w wyszukiwaniu dziennika.  Określanie **kategorii** jest opcjonalny i tylko wymagane, jeśli masz grupy komputerów o takiej samej nazwie w różnych kategoriach. 

    $ComputerGroups[Category: Name]

Po uruchomieniu wyszukiwania, najpierw zostaną rozpoznane członków grup komputerów, uwzględniany w wyszukiwaniu.  Jeśli grupa jest oparta na wyszukiwania dziennika, do zwrócenia członków grupy, przed przeprowadzeniem wyszukiwania najwyższego poziomu dziennika jest uruchamiane tego wyszukiwania.

Grupy komputerów są zazwyczaj używane z **IN** klauzuli w wyszukiwania dziennika, jak w poniższym przykładzie:

    Type=UpdateSummary Computer IN $ComputerGroups[My Computer Group]

>[!NOTE]
> Jeśli obszaru roboczego został uaktualniony do [języka zapytań nowe analizy dzienników](log-analytics-log-search-upgrade.md), a następnie użyć grupy komputerów w zapytaniu, traktując jej aliasem jako funkcja jak w poniższym przykładzie:
> 
>  `UpdateSummary | where Computer IN (MyComputerGroup)`

## <a name="computer-group-records"></a>Rekordów grupy komputerów
Zostaje utworzony rekord w repozytorium OMS dla każdego członkostwa grup komputerów utworzone na podstawie usługi Active Directory lub usług WSUS.  Te rekordy mieć typu **Grupa_komputerów** i mieć właściwości w poniższej tabeli.  Rekordy nie są tworzone dla grup komputerów opartych na dziennik wyszukiwania.

| Właściwość | Opis |
|:--- |:--- |
| Typ |*Grupa_komputerów* |
| SourceSystem |*SourceSystem* |
| Computer (Komputer) |Nazwa komputera członkowskiego. |
| Grupa |Nazwa grupy. |
| GroupFullName |Pełna ścieżka do grupy, takie jak źródło i nazwa źródła. |
| GroupSource |Źródło tej grupy zostały zebrane z. <br><br>Polecenie cmdlet<br>PROGRAM WSUS<br>WSUSClientTargeting |
| GroupSourceName |Nazwa źródła, które zostały zebrane grupy.  Dla usługi Active Directory jest to nazwa domeny. |
| ManagementGroupName |Nazwa grupy zarządzania agentów SCOM.  W przypadku innych agentów jest AOI -\<identyfikator obszaru roboczego\> |
| TimeGenerated |Data i godzina utworzenia lub aktualizacji grupy komputerów. |

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o [dziennika wyszukiwania](log-analytics-log-searches.md) analizować dane zebrane ze źródeł danych i rozwiązania.  

