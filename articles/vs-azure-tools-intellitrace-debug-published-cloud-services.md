---
title: "aaaDebugging opublikowane usługi Azure usługę w chmurze z programu Visual Studio i IntelliTrace | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak usługa toodebug chmurę z programu Visual Studio i IntelliTrace"
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5e6662fc-b917-43ea-bf2b-4f2fc3d213dc
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 60734a71d5499de72e1ca81a3ab0ab9f34bc303a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="debugging-a-published-azure-cloud-service-with-visual-studio-and-intellitrace"></a>Debugowanie usługi opublikowana chmura Azure za pomocą programu Visual Studio i IntelliTrace
Przy użyciu funkcji IntelliTrace można rejestrować szeroką gamę informacji o debugowaniu dla wystąpienia roli, po uruchomieniu na platformie Azure. Toofind hello przyczynę problemu, należy tak, jakby były uruchomione w systemie Azure można użyć toostep dzienniki IntelliTrace hello za pomocą kodu w programie Visual Studio. W rezultacie rekordy kod klucza wykonywania i środowiska danych IntelliTrace, gdy aplikacja Azure działa jako usługa w chmurze na platformie Azure i umożliwia powtarzania hello rejestrowane dane z programu Visual Studio. 

Można użyć funkcji IntelliTrace, jeśli masz zainstalowany program Visual Studio Enterprise i celów aplikacji Azure .NET Framework 4 lub nowszy. IntelliTrace zbiera informacje dotyczące poszczególnych ról platformy Azure. Hello maszyny wirtualnej dla tych ról są zawsze uruchamiane w 64-bitowych systemach operacyjnych.

Alternatywnie, można użyć [zdalnego debugowania](http://go.microsoft.com/fwlink/p/?LinkId=623041) tooattach bezpośrednio tooa usługi w chmurze jest uruchomiona na platformie Azure.

> [!IMPORTANT]
> IntelliTrace jest przeznaczona tylko w scenariuszach debugowania i nie powinna być używana w przypadku wdrożenia produkcyjnego.
> 

## <a name="configure-an-azure-application-for-intellitrace"></a>Skonfigurować aplikację Azure dla funkcji IntelliTrace
tooenable IntelliTrace aplikacji platformy Azure, musisz utworzyć i opublikować aplikacji hello z projektu programu Visual Studio Azure. Przed opublikowaniem tooAzure, należy skonfigurować funkcji IntelliTrace dla aplikacji platformy Azure. W przypadku publikowania aplikacji bez konfigurowania funkcji IntelliTrace, należy toorepublish hello projektu. Aby uzyskać więcej informacji, zobacz [publikowania Azure cloud services projektów przy użyciu programu Visual Studio](http://go.microsoft.com/fwlink/p/?LinkId=623012).

1. Jeśli jesteś gotowe toodeploy aplikacji platformy Azure, sprawdź, czy elementy docelowe kompilacji projektu są zbyt**debugowania**.

1. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt i wybierz z menu kontekstowego hello **publikowania**.
   
1. W hello **publikowanie aplikacji platformy Azure** okno dialogowe, wybierz opcję hello subskrypcji platformy Azure i wybierz **dalej**.

1. W hello **ustawienia** strona, wybierz hello **Zaawansowane ustawienia** kartę.

1. Włącz hello **włączyć IntelliTrace** opcję toocollect dzienniki IntelliTrace dla aplikacji po opublikowaniu go w chmurze hello.
   
1. toocustomize hello IntelliTrace konfiguracji podstawowej, wybierz opcję **ustawienia** dalej zbyt**włączyć IntelliTrace**.

    ![Łącze Ustawienia funkcji IntelliTrace](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/intellitrace-settings-link.png)
   
1. W hello **ustawienia IntelliTrace** okna dialogowego, można określić toolog zdarzenia, które, czy toocollect informacji o wywołaniach, które toocollect moduły i procesy w dziennikach i rejestrowania toohello tooallocate ilość miejsca. Aby uzyskać więcej informacji o funkcji IntelliTrace, zobacz [debugowanie przy użyciu funkcji IntelliTrace](http://go.microsoft.com/fwlink/?LinkId=214468).
   
    ![Ustawienia funkcji IntelliTrace](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC519063.png)

dziennika IntelliTrace Hello jest cyklicznego pliku dziennika hello maksymalny rozmiar określony w ustawieniach IntelliTrace hello (hello domyślny rozmiar to 250 MB). Dzienniki IntelliTrace są zbierane tooa pliku w systemie plików hello hello maszyny wirtualnej. W przypadku żądania hello dzienniki, migawki są podejmowane w danym momencie i pobrać tooyour komputera lokalnego.

Po hello usługi w chmurze Azure została opublikowana tooAzure, można określić, jeśli włączono IntelliTrace z hello Azure w węźle **Eksploratora serwera**, jak pokazano w powitania po obrazu:

![Eksplorator serwera - IntelliTrace włączone](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC744134.png)

## <a name="download-intellitrace-logs-for-a-role-instance"></a>Pobierz dzienniki IntelliTrace dla wystąpienia roli
Za pomocą programu Visual Studio, możesz pobrać dzienniki IntelliTrace dla wystąpienia roli wykonaj następujące czynności:

1. W **Eksploratora serwera**, rozwiń węzeł hello **usługi w chmurze** węzeł i Znajdź wystąpienia roli dzienniki, których chcesz toodownload. 

1. Kliknij prawym przyciskiem myszy hello wystąpienia roli, a następnie wybierz z menu kontekstowego hello s, **Wyświetl dzienniki IntelliTrace**. 

    ![Wyświetlanie opcji menu Dzienniki IntelliTrace](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/view-intellitrace-logs.png)

1. Dzienniki IntelliTrace Hello są tooa pobranego pliku w katalogu na komputerze lokalnym. Zawsze zażądania hello dzienników IntelliTrace, utworzyć nową migawkę. Podczas pobierania dzienników hello Visual Studio Wyświetla hello postęp operacji hello hello **dziennika aktywności platformy Azure** okna. Jak pokazano na następującej ilustracji hello, możesz rozszerzyć hello pozycji dla toosee operacji hello więcej szczegółów.

![VST_IntelliTraceDownloadProgress](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC745551.png)

Podczas pobierania dzienników IntelliTrace hello, możesz kontynuować toowork w programie Visual Studio. Dziennik hello zakończył pobieranie, zostanie otwarty w programie Visual Studio.

> [!NOTE]
> Witaj dzienniki IntelliTrace może zawierać wyjątki tego framework hello generuje i obsługuje później. Kod wewnętrzny framework generuje tych wyjątków w ramach normalnego uruchamiania roli, więc można je bezpiecznie zignorować.
> 
> 

## <a name="next-steps"></a>Następne kroki
- [Opcje debugowania usług w chmurze Azure](vs-azure-tools-debugging-cloud-services-overview.md)
- [Publikowanie usługi w chmurze platformy Azure przy użyciu programu Visual Studio](vs-azure-tools-publishing-a-cloud-service.md)