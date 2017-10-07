---
title: aaa "lekcji samouczka usług Azure Analysis Services 13: Wdrażanie | Opis elementu Microsoft Docs": w tym artykule opisano, jak samouczek hello toodeploy projektu tooAzure Analysis Services.
usługi: documentationcenter usług analysis services: "Autor: minewiskan Menedżera: Edytor erikre:" tagów: "

MS.AssetID: ms.service: ms.devlang usług analysis services: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: ms.author 2017-07/17: owend
---
# <a name="lesson-13-deploy"></a>Lekcja 13. Wdrażanie

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

W tej lekcji można skonfigurować właściwości wdrożenia; Określanie tooand toodeploy nazwę modelu hello Azure Analysis Services serwera. Następnie możesz wdrożyć hello modelu toothat wystąpienia. Po wdrożeniu modelu, użytkownicy mogą łączyć tooit przy użyciu raportowania aplikacji klienckiej. toolearn więcej, zobacz [wdrażanie usług Analysis Services tooAzure](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy).  
  
Szacowany czas toocomplete tej lekcji: **5 minut**  
  
## <a name="prerequisites"></a>Wymagania wstępne  
Ten temat stanowi część samouczka modelowania tabelarycznego, który należy wykonać w podanej kolejności. Przed wykonaniem zadania hello w tej lekcji, powinno mieć ukończone poprzedniej lekcji hello: [lekcji 12: analizować w programie Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).  

> [!IMPORTANT]  
> Musi mieć [uprawnienia administratora](../analysis-services-server-admins.md) na powitania zdalnego usług Analysis Services serwera w kolejności toodeploy tooit.  

> [!IMPORTANT]  
> Jeśli hello AdventureWorksDW2014 przykładowa baza danych jest zainstalowana na lokalnym serwerze SQL i jest instalowany serwer usług Azure Analysis Services modelu tooan [bramy danych lokalnych](../analysis-services-gateway.md) jest wymagana.
  
## <a name="deploy-hello-model"></a>Wdróż hello model  
  
#### <a name="tooconfigure-deployment-properties"></a>Właściwości wdrożenia tooconfigure  

  
1.  W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy hello **sprzedaży Internet AW** projektu, a następnie kliknij przycisk **właściwości**.  
  
2.  W hello **strony właściwości sprzedaży Internet AW** okna dialogowego, w obszarze **serwera wdrażania**, w hello **serwera** właściwości, wprowadź hello całego serwera.  

    ![aas-lesson13-deploy-property](../tutorials/media/aas-lesson13-deploy-property.png)
  
3.  W hello **bazy danych** właściwości, typ **Adventure Works Internet sprzedaży**.  
  
4.  W hello **Nazwa modelu** właściwości, typ **Adventure Works Internet sprzedaży modelu**.  
  
5.  Sprawdź wybrane opcje, a następnie kliknij przycisk **OK**.  
  
#### <a name="toodeploy-hello-adventure-works-internet-sales"></a>Witaj toodeploy sprzedaży Internet Adventure Works
  
1.  W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy hello **sprzedaży Internet AW** projektu > **kompilacji**.  

2.  Kliknij prawym przyciskiem myszy hello **sprzedaży Internet AW** projektu > **Wdróż**.

    W przypadku wdrażania tooAzure Analysis Services, może być zostanie wyświetlony monit o tooenter Twojego konta. Wprowadź swoje konto organizacyjne i hasło, na przykład nancy@adventureworks.com. To konto musi być w Administratorzy na powitania serwera.
  
    okno dialogowe wdrażanie Hello pojawia się i wyświetla stan wdrożenia hello hello metadanych i każdej tabeli objęte hello modelu.  
    
    ![aas-lesson13-deploy-status](../tutorials/media/aas-lesson13-deploy-status.png)
  
3. Po pomyślnym zakończeniu wdrażania kliknij przycisk **Zamknij**.  
  
## <a name="conclusion"></a>Podsumowanie  
Gratulacje! Tworzenie i wdrażanie pierwszego modelu tabelarycznego usług Analysis Services zostało ukończone. W tym samouczku pomogła informacje pomocne przy zakończeniu hello najbardziej typowych zadań tworzenia modelu tabelarycznego. Teraz, gdy jest wdrażana modelu sprzedaży Internet Adventure Works, można użyć programu SQL Server Management Studio toomanage hello modelu; Tworzenie planu tworzenia kopii zapasowych i skrypty procesu. Użytkownicy mogą teraz również łączyć modelu toohello raportowania aplikacji klienckiej, takich jak program Microsoft Excel lub Power BI.  

![aas-lesson13-ssms](../tutorials/media/aas-lesson13-ssms.png)
  
  
  
## <a name="whats-next"></a>Co dalej?
[Łączenie z programem Power BI Desktop](../analysis-services-connect-pbi.md)   
[Lekcja uzupełniająca — zabezpieczenia dynamiczne](../tutorials/aas-supplemental-lesson-dynamic-security.md)   
[Lekcja uzupełniająca — wiersze szczegółów](../tutorials/aas-supplemental-lesson-detail-rows.md)   
[Lekcja uzupełniająca — niewyrównane hierarchie](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)   
