---
title: Application Insights Lejki aaaAzure
description: "Dowiedz się, jak używasz toodiscover Lejki jak klienci są interakcji z aplikacją."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: cfreeman
ms.openlocfilehash: 3a90cfd11cb193e303136504df44008ffd04a290
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="discover-how-customers-are-using-your-application-with-hello-application-insights-funnels"></a>Wykryj, jak klienci za pomocą aplikacji hello Lejki Insights aplikacji

Opis klientów są hello największe znaczenie tooyour działalności. Jeśli aplikacja obejmuje kilka etapów, konieczne będzie tooknow Jeśli większość klientów postępu są przez cały proces hello lub jeśli ich kończą się proces hello w pewnym momencie. postęp Hello na kolejnych czynności w aplikacji sieci web nazywa się "lejka". Możesz użyć hello Application Insights Lejki toogain wgląd w użytkowników i monitor kursy wymiany krok po kroku. 

## <a name="get-started-with-hello-funnels-blade"></a>Rozpoczynanie pracy z bloku Lejki hello
Hello Najprostszym sposobem toolearn o Lejki jest toowalk, jednak w przykładzie. Hello poniższych ilustracjach pokazują, że hello kroki właściciele firm handlu elektronicznego zajmie toolearn sposób interakcji klientów z aplikacją sieci web.  

### <a name="create-your-funnel"></a>Utwórz użytkownika lejka.
Przed utworzeniem sieci lejka należy toodecide na pytanie hello ma tooanswer. Na przykład można tooknow ilu użytkowników Wyświetlanie przez stronę główną, kliknij na anonsu. W tym przykładzie hello właścicieli hello firmy Fabrikam Fiber mają tooknow hello odsetek klientów, którzy dokonać zakupu po dodaniu elementów tootheir koszyku podczas hello ostatniego miesiąca.

Poniżej przedstawiono kroki hello podejmują toocreate ich lejka.

1. Kliknij przycisk Nowy hello na powitania Lejki bloku.
1. Wybierz przedział czasu hello "Ostatni miesiąc" z hello **zakres czasu** listy rozwijanej. 
1. Wybierz hello **stronę produktu** zdarzenia z hello **krok 1** listy rozwijanej. 
1. Wybierz hello **koszyka tooshopping Dodaj** zdarzenia z hello **krok 2** listy rozwijanej.
1. Wybierz hello **kliknij zakupu** zdarzenia z hello **kroku 3** listy rozwijanej.
1. Dodaj lejka toohello nazwę, a następnie kliknij przycisk **zapisać**.

Witaj poniższej ilustracji przedstawiono generuje hello danych hello Lejki bloku. Z tutaj hello właścicieli Fabrikam widoczny podczas hello ostatniego tygodnia, 22.7% dla klientów, którzy dodany element tootheir zakupy koszyka zakupu hello ukończone. Można również sprawdzić 1% klientom Witaj kliknięty anonsu, aby odwiedzić stronę produktu hello i 20% klientów wylogowany po zakończeniu ich zakupu.


![Blok Lejki z danymi](./media/app-insights-understand-usage-patterns/funnel1.png)

## <a name="next-steps"></a>Następne kroki
- Dowiedz się więcej o [analizy użycia](app-insights-usage-overview.md). 
