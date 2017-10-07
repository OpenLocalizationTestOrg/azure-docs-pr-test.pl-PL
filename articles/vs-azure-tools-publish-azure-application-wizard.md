---
title: Witaj aaaUsing programu Visual Studio Azure Kreator publikowania aplikacji | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooconfigure hello różnych ustawień w Visual Studio Azure Kreator publikowania aplikacji hello"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 7d8f1ac9-e439-47e0-a183-0642c4ea1920
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 3f0b580d0054cc246372597660d8ae317d9b8686
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-visual-studio-publish-azure-application-wizard"></a>Za pomocą programu Visual Studio Azure Kreator publikowania aplikacji hello
Po opracowywanie aplikacji sieci web w programie Visual Studio, tooan tej aplikacji usługi w chmurze Azure można opublikować za pomocą hello **publikowanie aplikacji platformy Azure** kreatora. 

> [!NOTE]
> Ten temat dotyczy wdrażania usług toocloud, nie tooweb witryny. Informacje o wdrażaniu witryny tooweb, zobacz [jak tooDeploy witryny sieci Web Azure](https://social.msdn.microsoft.com/Search/windowsazure?query=How%20to%20Deploy%20an%20Azure%20Web%20Site&Refinement=138&ac=4#refinementChanges=117&pageNumber=1&showMore=false).
> 
> 

## <a name="accessing-hello-publish-azure-application-wizard"></a>Uzyskiwanie dostępu do hello Kreator publikowania aplikacji Azure

Kreator publikowania aplikacji Azure hello na dwa sposoby w zależności od typu hello projektu programu Visual Studio, których masz są dostępne.

**Jeśli masz projekt usługi w chmurze platformy Azure:**

1. Utwórz lub Otwórz projekt usługi w chmurze platformy Azure w programie Visual Studio.

1. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt hello i wybierz z menu kontekstowego hello **publikowania**.

**Jeśli masz projektu aplikacji sieci web, która nie jest włączona dla platformy Azure:**

1. Utwórz lub Otwórz projekt usługi w chmurze platformy Azure w programie Visual Studio.

1. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt hello i wybierz z menu kontekstowego hello **przekonwertować** > **przekonwertować tooAzure projekt usługi w chmurze**. 

1. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy nowo utworzony hello Azure projektu i wybierz z menu kontekstowego hello **publikowania**.

## <a name="sign-in-page"></a>Strona logowania

![Strona logowania](./media/vs-azure-tools-publish-azure-application-wizard/sign-in.png)

**Konto** — wybierz konto lub **Dodaj konto** liście rozwijanej hello konta.

**Wybierz subskrypcję** — wybierz hello toouse subskrypcji dla danego wdrożenia.
   
## <a name="settings-page---common-settings-tab"></a>Ustawienia strony — karta typowe ustawienia   

![Typowe ustawienia](./media/vs-azure-tools-publish-azure-application-wizard/settings-common-settings.png)

**Usługi w chmurze** — za pomocą listy rozwijanej hello, albo wybierz istniejący chmurę usługi lub wybierz  **&lt;Utwórz nowy >**i Utwórz usługę w chmurze. Wyświetla Hello centrum danych w nawiasach dla każdej usługi w chmurze. Zaleca się, że lokalizacja centrum danych hello hello usługi w chmurze być hello takie same jako hello lokalizacji centrum danych dla konta magazynu hello (Zaawansowane ustawienia).  

**Środowisko** — wybierz opcję **produkcji** lub **przemieszczania**. Wybierz hello środowiska przemieszczania, jeśli chcesz, aby toodeploy aplikacji w środowisku testowym. 

**Konfiguracja kompilacji** — wybierz opcję **debugowania** lub **wersji**.

**Konfiguracja usługi** — wybierz opcję **chmury** lub **lokalnego**.
   
**Włącz pulpit zdalny dla wszystkich ról** -wyboru tej opcji, jeśli chcesz, aby mogli tooremotely toobe połączyć toohello usługi. Ta opcja jest używana głównie do rozwiązywania problemów. Po zaznaczeniu tego pola wyboru hello **konfigurację usług pulpitu zdalnego** zostanie wyświetlone okno dialogowe. Wybierz hello **ustawienia** Konfiguracja hello toochange łącza.
   
**Włącz dla wszystkich ról w sieci web narzędzia Web Deploy** -Sprawdź tę opcję, tooenable wdrożenie w hello usługi sieci web. Musisz wybrać hello **Włącz pulpit zdalny dla wszystkich ról** opcję toouse tej funkcji. Aby uzyskać więcej informacji, zobacz [ [publikowania usługi w chmurze platformy Azure przy użyciu programu Visual Studio](https://msdn.microsoft.com/library/azure/ff683672.aspx)](https://msdn.microsoft.com/library/azure/ff683672.aspx). 

## <a name="settings-page---advanced-settings-tab"></a>Ustawienia strony — karta Zaawansowane ustawienia

![Ustawienia zaawansowane](./media/vs-azure-tools-publish-azure-application-wizard/settings-advanced-settings.png)

**Etykieta wdrożenia** — zaakceptuj nazwę domyślną hello lub wprowadź nazwę. tooappend hello Data toohello etykieta wdrożenia, pozostaw hello jest zaznaczone pole wyboru. 
   
**Konto magazynu** — wybierz tę opcję hello toouse konta magazynu dla tego wdrożenia, **&lt;Utwórz nowy > toocreate konta magazynu. Wyświetla Hello centrum danych w nawiasach dla każdego konta magazynu. Zaleca się, że lokalizacja centrum danych hello hello konta magazynu być hello sam jako hello lokalizacji centrum danych dla usługi w chmurze hello (typowe ustawienia).  
   
Witaj kontem magazynu platformy Azure przechowuje hello pakietu dla wdrożenia aplikacji hello. Po wdrożeniu aplikacji hello pakietów hello jest usuwany z hello konta magazynu.

**Usuń wdrożenie w przypadku niepowodzenia** — wybierz to wdrożenie hello toohave opcji usunięte, jeśli nie zostaną napotkane błędy podczas publikowania. To powinno być niezaznaczone, jeśli chcesz toomaintain stałego wirtualnego adresu IP dla usługi w chmurze.

**Wdrożenia aktualizacji** — wybierz tę opcję, jeśli chcesz toodeploy tylko zaktualizowane składniki. Ten typ wdrożenia może być szybsza niż pełne wdrożenie. To sprawdzić, jeśli chcesz toomaintain stałego wirtualnego adresu IP dla usługi w chmurze. 

**Wdrożenia aktualizacji - ustawienia** -służy w tym oknie dialogowym toofurther określ w jaki sposób toobe ról hello zaktualizowane. Jeśli wybierzesz **aktualizacji przyrostowej**, każde wystąpienie aplikacji jest zaktualizowane jeden po drugim, więc tej aplikacji hello jest zawsze dostępna. Jeśli wybierzesz **jednoczesne aktualizowanie**, wszystkich wystąpień aplikacji są aktualizowane na powitania tym samym czasie. Jednoczesne aktualizowanie jest szybsze, ale z usługą mogą być niedostępne podczas procesu aktualizacji hello. 

![Ustawienia wdrożenia](./media/vs-azure-tools-publish-azure-application-wizard/deployment-settings.png)

**Włącz IntelliTrace** — Określ, czy tooenable IntelliTrace. Przy użyciu funkcji IntelliTrace można rejestrować szeroką gamę informacji o debugowaniu dla wystąpienia roli, po uruchomieniu na platformie Azure. Toofind hello przyczynę problemu, należy tak, jakby były uruchomione w systemie Azure można użyć toostep dzienniki IntelliTrace hello za pomocą kodu w programie Visual Studio. Aby uzyskać więcej informacji o korzystaniu z funkcji IntelliTrace, zobacz [debugowania usługi opublikowana chmura Azure za pomocą programu Visual Studio i IntelliTrace](./vs-azure-tools-intellitrace-debug-published-cloud-services.md). 

**Włącz profilowanie** — Określ, czy tooenable profilowanie wydajności. Witaj profilera Visual Studio umożliwia tooget dokładnych analiz hello obliczeniową aspektów sposób uruchamiania usługi w chmurze. Aby uzyskać więcej informacji na temat używania hello profilera Visual Studio, zobacz [testowanie wydajności usługi w chmurze Azure hello](./vs-azure-tools-performance-profiling-cloud-services.md).

**Włącz zdalny debuger dla wszystkich ról** — Określ, czy tooenable zdalnego debugowania. Aby uzyskać więcej informacji dotyczących debugowania usługi w chmurze przy użyciu programu Visual Studio, zobacz [debugowania usługi w chmurze Azure lub maszyny wirtualnej w programie Visual Studio](./vs-azure-tools-debug-cloud-services-virtual-machines.md).

## <a name="diagnostics-settings-page"></a>Strona Ustawienia diagnostyki

![Ustawienia diagnostyczne](./media/vs-azure-tools-publish-azure-application-wizard/diagnostic-settings.png)

Diagnostyka umożliwia tootroubleshoot usługi w chmurze Azure (lub maszyny wirtualnej platformy Azure). Aby uzyskać informacje diagnostyczne, zobacz [Konfigurowanie diagnostyki dla usług Azure Cloud Services i maszyn wirtualnych](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md). Uzyskać informacji na temat usługi Application Insights, zobacz [co to jest usługa Application Insights?](./application-insights/app-insights-overview.md).

## <a name="summary-page"></a>Strona podsumowania

![Podsumowanie](./media/vs-azure-tools-publish-azure-application-wizard/summary.png)

**Docelowy profil** — można wybrać toocreate profilu publikowania hello wybrane ustawienia. Na przykład utworzyć jeden profil dla środowiska testowego i drugą w środowisku produkcyjnym. toosave ten profil, wybierz hello **zapisać** ikony. Kreator Hello tworzy profil hello i zapisze go w hello projektu Visual Studio. Nazwa profilu hello toomodify, otwórz hello **docelowego profilu** listy, a następnie wybierz pozycję **< Zarządzaj >**.
   
   > [!NOTE]
   > profil publikowania Hello zostanie wyświetlony w Eksploratorze rozwiązań w programie Visual Studio, a ustawienia profilu hello są zapisywane tooa plik z rozszerzeniem .azurePubxml. Ustawienia są zapisywane jako atrybutami tagów XML.
   > 
   > 

## <a name="publishing-your-application"></a>Publikowanie aplikacji

Po skonfigurowaniu wszystkich hello projektu wdrożenia, wybierz **publikowania** u dołu okna dialogowego hello hello. Można monitorować stan procesu hello w hello **dane wyjściowe** okna w programie Visual Studio.

## <a name="next-steps"></a>Następne kroki
- [Migrowanie i publikowanie aplikacji sieci Web tooan usługi w chmurze Azure w programie Visual Studio](./vs-azure-tools-migrate-publish-web-app-to-cloud-service.md)
- [Dowiedz się, jak usługa w chmurze toouse Visual Studio toopublish platformy Azure](./vs-azure-tools-publishing-a-cloud-service.md)
- [Debugowanie usługi opublikowana chmura Azure za pomocą programu Visual Studio i IntelliTrace](./vs-azure-tools-intellitrace-debug-published-cloud-services.md)
- [Testowanie wydajności hello usługi w chmurze Azure](./vs-azure-tools-performance-profiling-cloud-services.md)
- [Konfigurowanie diagnostyki dla usług w chmurze Azure i maszyn wirtualnych](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md). 
- [Co to jest Application Insights?](./application-insights/app-insights-overview.md)