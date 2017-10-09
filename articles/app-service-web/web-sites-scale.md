---
title: "aaaScale się aplikacji na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooscale zapasowej aplikacji w usłudze Azure App Service tooadd pojemności i funkcje."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: f7091b25-b2b6-48da-8d4a-dcf9b7baccab
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2016
ms.author: cephalin
ms.openlocfilehash: 97f46f77aeef95aec90d38e8396a023820e3caeb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-up-an-app-in-azure"></a>Skalowanie w górę aplikacji na platformie Azure
W tym artykule opisano sposób tooscale aplikacji w usłudze Azure App Service. Istnieją dwa przepływy pracy do skalowania, skalowania w górę i skalowania w poziomie i w tym artykule opisano hello skalowania w górę przepływu pracy.

* [Skalowanie w górę](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Pobierz więcej Procesora, pamięci, miejsca na dysku i dodatkowych funkcji, takich jak dedykowanych maszynach wirtualnych (VM), niestandardowe domeny i certyfikaty, przemieszczania miejsc, skalowanie automatyczne i inne. Skalowanie w górę, zmieniając hello cenowym planu usługi aplikacji — należącego do aplikacji.
* [Skalowanie w poziomie](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Zwiększ hello liczba wystąpień maszyn wirtualnych, których uruchamianie aplikacji.
  Możesz skalować w poziomie tooas wiele jako 20 wystąpień, w zależności od warstwy cenowej. [Środowiska usługi App Service](../app-service/app-service-app-service-environments-readme.md) w **Premium** warstwy będzie zwiększyć swoich wystąpień too50 liczba skalowalnego w poziomie. Aby uzyskać więcej informacji na temat skalowania, zobacz [skalowanie liczby wystąpień ręcznie lub automatycznie](../monitoring-and-diagnostics/insights-how-to-scale.md). Można znaleźć poza jak toouse Skalowanie automatyczne, który jest automatycznie tooscale liczba wystąpień na podstawie wstępnie zdefiniowanych reguł i harmonogramy.

Witaj skali ustawienia zajmuje tylko sekund tooapply i wpływają na wszystkie aplikacje w sieci [planu usługi aplikacji](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
Nie wymagają możesz toochange kodu lub ponownego wdrażania aplikacji.

Uzyskać informacje o cenach hello i funkcjach poszczególnych planów usługi aplikacji, zobacz [szczegóły cennika usługi App](https://azure.microsoft.com/pricing/details/web-sites/).  

> [!NOTE]
> Przed przejściem plan usługi aplikacji z hello **wolne** warstwy, należy najpierw usunąć hello [limitów wydatków](https://azure.microsoft.com/pricing/spending-limits/) w miejscu dla subskrypcji platformy Azure. tooview lub zmień opcje subskrypcji Microsoft Azure App Service, zobacz [subskrypcji platformy Microsoft Azure][azuresubscriptions].
> 
> 

<a name="scalingsharedorbasic"></a>
<a name="scalingstandard"></a>

## <a name="scale-up-your-pricing-tier"></a>Skalowanie w górę warstwę cenową
1. W przeglądarce otwórz hello [portalu Azure][portal].
2. W bloku aplikacji kliknij **wszystkie ustawienia**, a następnie kliknij przycisk **Skaluj w górę**.
   
    ![Przejdź tooscale zapasowej swojej aplikacji Azure.][ChooseWHP]
3. Wybierz warstwę, a następnie kliknij przycisk **wybierz**.
   
    Witaj **powiadomienia** kartę będzie flash zielona **Powodzenie** po zakończeniu operacji hello.

<a name="ScalingSQLServer"></a>

## <a name="scale-related-resources"></a>Powiązane zasoby są skalowane
Jeśli aplikacja jest zależny od innych usług, takich jak bazy danych SQL Azure lub usługi Azure Storage, można również skalować tych zasobów na podstawie Twoich potrzeb. Te zasoby nie mogą być skalowane z hello planu usługi aplikacji i musi być skalowane niezależnie.

1. W **Essentials**, kliknij przycisk hello **grupy zasobów** łącza.
   
    ![Skalowanie w górę powiązane zasoby aplikacji Azure](./media/web-sites-scale/RGEssentialsLink.png)
2. W hello **Podsumowanie** częścią hello **grupy zasobów** bloku, kliknij zasobów, które mają tooscale. powitania po zrzut ekranu przedstawia zasobów bazy danych SQL i zasobów magazynu Azure.
   
    ![Przejdź tooscale bloku grupy tooresource zapasowej swojej aplikacji Azure](./media/web-sites-scale/ResourceGroup.png)
3. Dla zasobów bazy danych SQL, kliknij przycisk **ustawienia** > **warstwa cenowa** hello tooscale warstwy cenowej.
   
    ![Skalowanie w górę hello bazy danych SQL wewnętrznej bazy danych dla aplikacji Azure](./media/web-sites-scale/ScaleDatabase.png)
   
    Można też włączyć [— replikacja geograficzna](../sql-database/sql-database-geo-replication-overview.md) dla swojego wystąpienia bazy danych SQL.
   
    Dla zasobu usługi Magazyn Azure, kliknij przycisk **ustawienia** > **konfiguracji** tooscale Twojego opcji magazynu.
   
    ![Skalowanie w górę hello Azure Storage konto używane przez aplikację Azure](./media/web-sites-scale/ScaleStorage.png)

<a name="devfeatures"></a>

## <a name="learn-about-developer-features"></a>Dowiedz się więcej o funkcje programistyczne
W zależności od warstwy cenowej hello hello zorientowane na developer są dostępne następujące funkcje:

### <a name="bitness"></a>Liczba bitów
* Hello **podstawowe**, **standardowe**, i **Premium** warstwy obsługi aplikacji 64-bitowe i 32-bitowych.
* Witaj **wolne** i **Shared** planu warstwami obsługuje tylko 32-bitowych aplikacji.

### <a name="debugger-support"></a>Obsługa debugera
* Obsługa debugera jest dostępna dla hello **wolne**, **Shared**, i **podstawowe** tryby w jedno połączenie dla danego planu usługi aplikacji.
* Obsługa debugera jest dostępna dla hello **standardowe** i **Premium** tryby na pięć równoczesnych połączeń na plan usługi aplikacji.

<a name="OtherFeatures"></a>

## <a name="learn-about-other-features"></a>Dowiedz się więcej o innych funkcjach
* Aby uzyskać szczegółowe informacje o wszystkich pozostałych funkcji w hello usługi aplikacji hello planów, włącznie z ceny i funkcje zainteresowania użytkowników tooall (w tym deweloperzy), zobacz [szczegóły cennika usługi App](https://azure.microsoft.com/pricing/details/web-sites/).

> [!NOTE]
> Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/) gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service. Bez kart kredytowych są wymagane i nie bez zobowiązań.
> 
> 

<a name="Next Steps"></a>

## <a name="next-steps"></a>Następne kroki
* tooget korzystać z platformy Azure, zobacz [bezpłatna wersja próbna programu Microsoft Azure](https://azure.microsoft.com/pricing/free-trial/).
* Aby uzyskać informacje o cenach pomocy technicznej i umowy dotyczącej poziomu usług, odwiedź hello następującego łącza.
  
    [Informacje o cenach transferu danych](https://azure.microsoft.com/pricing/details/data-transfers/)
  
    [Plany pomocy technicznej platformy Azure firmy Microsoft](https://azure.microsoft.com/support/plans/)
  
    [Umowy dotyczące poziomu usług](https://azure.microsoft.com/support/legal/sla/)
  
    [Szczegóły cennika bazy danych SQL](https://azure.microsoft.com/pricing/details/sql-database/)
  
    [Maszyny wirtualnej i rozmiary usługi chmury Microsoft Azure][vmsizes]
  
    [Szczegóły cennika usługi aplikacji](https://azure.microsoft.com/pricing/details/app-service/)
  
    [Usługi aplikacji — cennik szczegóły - połączeń SSL](https://azure.microsoft.com/pricing/details/web-sites/#ssl-connections)
* Informacje o usłudze Azure App Service najlepszych rozwiązań, w tym tworzenie skalowalnych i elastyczne architektury, zobacz [najlepsze rozwiązania: aplikacje sieci Web usługi aplikacji Azure](http://blogs.msdn.com/b/windowsazure/archive/2014/02/10/best-practices-windows-azure-websites-waws.aspx).
* Temat skalowania aplikacji usługi App Service można obejrzeć hello następujące zasoby:
  
  * [Gdy tooScale Azure Websites — Stefan Schackow](https://azure.microsoft.com/resources/videos/azure-web-sites-free-vs-standard-scaling/)
  * [Automatyczne skalowanie witryn sieci Web Azure, procesora CPU lub zaplanowane — z Stefan Schackow](https://azure.microsoft.com/resources/videos/auto-scaling-azure-web-sites/)
  * [Jak Azure skalowalność witryn sieci Web - Stefan Schackow](https://azure.microsoft.com/resources/videos/how-azure-web-sites-scale/)

<!-- LINKS -->
[vmsizes]:/pricing/details/app-service/
[SQLaccountsbilling]:http://go.microsoft.com/fwlink/?LinkId=234930
[azuresubscriptions]:http://go.microsoft.com/fwlink/?LinkID=235288
[portal]: https://portal.azure.com/

<!-- IMAGES -->
[ChooseWHP]: ./media/web-sites-scale/scale1ChooseWHP.png
[ChooseBasicInstances]: ./media/web-sites-scale/scale2InstancesBasic.png
[SaveButton]: ./media/web-sites-scale/05SaveButton.png
[BasicComplete]: ./media/web-sites-scale/06BasicComplete.png
[ScaleStandard]: ./media/web-sites-scale/scale3InstancesStandard.png
[Autoscale]: ./media/web-sites-scale/scale4AutoScale.png
[SetTargetMetrics]: ./media/web-sites-scale/scale5AutoScaleTargetMetrics.png
[SetFirstRule]: ./media/web-sites-scale/scale6AutoScaleFirstRule.png
[SetSecondRule]: ./media/web-sites-scale/scale7AutoScaleSecondRule.png
[SetThirdRule]: ./media/web-sites-scale/scale8AutoScaleThirdRule.png
[SetRulesFinal]: ./media/web-sites-scale/scale9AutoScaleFinal.png
[ResourceGroup]: ./media/web-sites-scale/scale10ResourceGroup.png
[ScaleDatabase]: ./media/web-sites-scale/scale11SQLScale.png
[GeoReplication]: ./media/web-sites-scale/scale12SQLGeoReplication.png
