---
title: "aaaMigrate enterprise tooAzure aplikacji sieci web usługi aplikacji"
description: "Pokazuje, jak tooquickly Asystenta migracji aplikacji sieci Web toouse migracji istniejącej tooAzure witryn sieci Web usług IIS aplikacji usługi sieci Web aplikacji"
services: app-service
documentationcenter: 
author: cephalin
writer: cephalin
manager: erikre
editor: 
ms.assetid: 2e846fc0-37cc-42e6-ac57-ff442ef16e85
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/01/2016
ms.author: cephalin
ms.openlocfilehash: 7d66c5b799f0eefe85cbd9ba596ee0a05167f295
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-an-enterprise-web-app-tooazure-app-service"></a>Migrowanie enterprise tooAzure aplikacji sieci web usługi aplikacji
Możesz łatwo przeprowadzić migrację istniejącej witryny sieci Web uruchomionymi na Internet Information Service (IIS) 6 lub nowszej zbyt[aplikacji usługi sieci Web aplikacji](http://go.microsoft.com/fwlink/?LinkId=529714). 

> [!IMPORTANT]
> Windows Server 2003 osiągnięto koniec pomocy technicznej na 14 lipca 2015 r. Jeśli są obecnie obsługuje witryny sieci Web na serwerze IIS, Windows Server 2003, aplikacje sieci Web jest sposób niskiego ryzyka, niskich kosztach i niskim tarcia tookeep witryn internetowych online i Asystenta migracji aplikacji sieci Web mogą pomóc zautomatyzować proces migracji hello. 
> 
> 

[Web Apps migracji Asystenta](https://www.movemetothecloud.net/) można analizować instalacji serwera IIS, identyfikowanie witryn, które mogą być tooApp zmigrowane usługi, zaznacz wszystkie elementy, które nie mogą być migrowane lub nieobsługiwane na platformie hello a następnie przeprowadzić migrację witryny sieci Web i tooAzure skojarzonych bazach danych.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="elements-verified-during-compatibility-analysis"></a>Elementy zweryfikowana podczas analizy zgodności
Witaj Asystenta migracji tworzy tooidentify Raport gotowości, wszelkie potencjalne przyczyny problemu lub problemy z blokowaniem, które mogą uniemożliwić pomyślną migrację z lokalnej usługi IIS tooAzure aplikacji usługi sieci Web aplikacji. Niektóre znane toobe kluczowych elementów hello są:

* Port powiązania — aplikacji sieci Web obsługuje tylko Port 80 dla protokołu HTTP i portu 443 dla ruchu HTTPS. Konfiguracje innego portu zostanie zignorowany, a ruch zostanie too80 routingiem i 443. 
* Uwierzytelnianie — aplikacji sieci Web obsługuje uwierzytelnianie anonimowe domyślnie i uwierzytelnianie oparte na formularzach w przypadku, gdy określony przez aplikację. Dzięki integracji z usługą Azure Active Directory i usług AD FS tylko jest używane uwierzytelnianie systemu Windows. Wszystkie inne formy uwierzytelniania — na przykład uwierzytelnianie podstawowe — nie są obecnie obsługiwane. 
* Globalnej pamięci podręcznej zestawów (GAC) — Witaj pamięci podręcznej GAC nie jest obsługiwane w aplikacjach sieci Web. Jeśli aplikacja odwołuje się do zestawów które zwykle wdrażanie toohello pamięci podręcznej GAC, konieczne będzie folder bin toodeploy toohello aplikacji w aplikacji sieci Web. 
* Wersją IIS5 Tryb zgodności — nie jest to obsługiwane w aplikacjach sieci Web. 
* Pule aplikacji — w aplikacjach sieci Web, każdej lokacji i jej podrzędne aplikacje uruchamiane w hello tej samej puli aplikacji. Jeśli witryna ma wiele aplikacji podrzędnych przy użyciu wielu pul aplikacji, umożliwi to ich skonsolidowanie tooa jednej puli aplikacji z typowymi ustawieniami lub migracji każdej aplikacji sieci web w osobnych tooa aplikacji.
* COM — składniki — aplikacji sieci Web nie zezwala na powitania rejestracji składników COM na platformie hello. Jeśli z witryn sieci Web lub aplikacji wykorzystać wszystkie składniki modelu COM, należy ponownie zapisuje je w kodzie zarządzanym i wdrażać je hello witryny sieci Web lub aplikacji.
* Rozszerzenia ISAPI — aplikacji sieci Web mogą obsługiwać hello korzystanie z rozszerzeń interfejsu ISAPI. Potrzebne są następujące hello toodo:
  
  * Wdrażanie hello dll z aplikacji sieci web 
  * Zarejestruj hello biblioteki DLL przy użyciu [pliku Web.config](http://www.iis.net/configreference/system.webserver/isapifilters)
  * Umieść plik applicationHost.xdt w katalogu głównym witryny hello z zawartością hello opisane w "Stosowanie toobe rozszerzenia ISAPI arbitrart załadowany" [sekcji tego artykułu](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples) 
    
  
    
    Aby uzyskać więcej przykładów toouse transformacji dokumentów XML z witryny sieci Web, zobacz [przekształcenie witryny sieci Web Microsoft Azure](http://blogs.msdn.com/b/waws/archive/2014/06/17/transform-your-microsoft-azure-web-site.aspx).
* Inne składniki, takich jak SharePoint, rozszerzenia serwera FrontPage (FPSE), FTP, certyfikaty SSL nie zostaną zmigrowane.

## <a name="how-toouse-hello-web-apps-migration-assistant"></a>Jak toouse hello Asystenta migracji aplikacji sieci Web
W tej sekcji przechodzi przez tootoomigrate przykład kilka witryn sieci Web używające bazy danych programu SQL Server i uruchomiona na lokalnym komputerze z systemem Windows Server 2003 R2 (IIS 6.0):

1. Na powitania IIS serwerze lub komputerze klienckim Przejdź zbyt[https://www.movemetothecloud.net/](https://www.movemetothecloud.net/) 
   
   ![](./media/web-sites-migration-from-iis-server/migration-tool-homepage.png)
2. Instalowanie Asystenta migracji aplikacji sieci Web, klikając hello **serwera IIS w wersji dedykowanej** przycisku. Więcej opcji będzie opcje w hello Najbliższa przyszłość. 
3. Kliknij przycisk hello **Zainstaluj narzędzie** przycisk tooinstall Asystenta migracji aplikacji sieci Web na tym komputerze.
   
   ![](./media/web-sites-migration-from-iis-server/install-page.png)
   
   > [!NOTE]
   > Możesz również kliknąć **Pobierz instalacji w trybie offline** toodownload ZIP pliku dla nie instalowanie na serwerach połączonych toohello internet. Możesz też kliknąć przycisk **przekazać istniejący raport gotowości migracji**, która jest toowork zaawansowanej opcji z istniejącej migracji Raport gotowości wcześniej generowany (co omówiono później).
   > 
   > 
4. W hello **instalacji aplikacji** kliknij **zainstalować** tooinstall na tym komputerze. Spowoduje także zainstalowanie odpowiednich zależności, takie jak narzędzie Web Deploy, DacFX i IIS, jeśli to konieczne. 
   
   ![](./media/web-sites-migration-from-iis-server/install-progress.png)
   
   Po zakończeniu instalacji Asystenta migracji aplikacji sieci Web jest uruchamiana automatycznie.
5. Wybierz **migracji lokacji i bazy danych z tooAzure serwera zdalnego**. Wprowadź poświadczenia administracyjne hello powitania serwera zdalnego i kliknij przycisk **Kontynuuj**. 
   
   ![](./media/web-sites-migration-from-iis-server/migrate-from-remote.png)
   
   Oczywiście można toomigrate powitania serwera lokalnego. Opcja zdalnego Hello jest przydatna, jeśli chcesz toomigrate witryn sieci Web z produkcyjnym serwerem usługi IIS.
   
   W tym momencie będzie przeprowadzał inspekcję narzędzia migracji hello hello konfiguracji serwer usług IIS, takie jak witryny, aplikacji, pul aplikacji i zależności tooidentify candidate witryn sieci Web do migracji. 
6. Poniższy zrzut ekranu Hello zawiera trzy witryn sieci Web — **domyślna witryna sieci Web**, **TimeTracker**, i **CommerceNet4**. Wszystkie mają skojarzone bazy danych, że chcemy toomigrate. Wybierz wszystkie lokacje hello zostaną tooassess, takich jak, a następnie kliknij przycisk **dalej**.
   
   ![](./media/web-sites-migration-from-iis-server/select-migration-candidates.png)
7. Kliknij przycisk **przekazać** Raport gotowości hello tooupload. Jeśli klikniesz przycisk **Zapisz plik lokalnie**, można uruchomić narzędzia migracji hello później i przekazywania hello zapisano Raport gotowości, jak wspomniano wcześniej.
   
   ![](./media/web-sites-migration-from-iis-server/upload-readiness-report.png)
   
   Po przekazaniu Raport gotowości hello Azure wykonuje analizy gotowości i pokazuje hello wyników. Odczytać hello szczegółów oceny dla każdej witryny sieci Web i upewnij się, że rozumie, lub usunąć wszystkie problemy przed kontynuowaniem. 
   
   ![](./media/web-sites-migration-from-iis-server/readiness-assessment.png)
8. Kliknij przycisk **rozpocząć migrację** toostart hello migracji. Teraz można toolog tooAzure przekierowane do swojego konta. Jest ważne, aby zalogować się przy użyciu konta, które ma aktywną subskrypcją platformy Azure. Jeśli nie masz konta platformy Azure, można założyć bezpłatnej wersji próbnej [tutaj](https://azure.microsoft.com/pricing/free-trial/?WT.srch=1&WT.mc_ID=SEM_). 
9. Wybierz konta dzierżawy hello, subskrypcji platformy Azure i region toouse baz danych i aplikacji sieci web platformy Azure zmigrowane, a następnie kliknij przycisk **Start migracji**. Możesz wybrać toomigrate witryn sieci Web hello później.
   
   ![](./media/web-sites-migration-from-iis-server/choose-tenant-account.png)
10. Na następnym ekranie powitania można zmieniać toohello domyślnych migracji ustawień, takich jak:
    
    * Użyj istniejącej bazy danych SQL Azure lub Utwórz nową bazę danych SQL Azure i skonfigurować jej poświadczenia
    * Wybierz hello toomigrate witryn sieci Web
    * Definiowanie nazw dla aplikacji sieci web platformy Azure hello i ich połączonej bazy danych SQL
    * Dostosuj ustawienia globalne hello i ustawienia na poziomie witryny
    
    Witaj Poniższy zrzut ekranu przedstawia wszystkich witryn hello wybrana do migracji z ustawieniami domyślnymi hello.
    
    ![](./media/web-sites-migration-from-iis-server/migration-settings.png)
    
    > [!NOTE]
    > Witaj **włączyć usługi Azure Active Directory** wyboru w niestandardowych ustawieniach integruje hello aplikacji sieci web platformy Azure z [usługi Azure Active Directory](../active-directory/active-directory-whatis.md) (hello **katalog domyślny**). Aby uzyskać więcej informacji o synchronizacji usługi Azure Active Directory z lokalnej usługi Active Directory, zobacz [integracji katalogów](http://msdn.microsoft.com/library/jj573653).
    > 
    > 
11. Po wprowadzeniu wszystkich zmian hello żądanego kliknij **Utwórz** procesu migracji hello toostart. Narzędzie migracji Hello zostanie tworzenie aplikacji sieci web hello Azure SQL Database i Azure, a następnie opublikuj hello zawartości witryny sieci Web i baz danych. Postęp migracji Hello wyraźnie jest wyświetlany w obszarze narzędzia migracji hello i zostanie wyświetlony ekran podsumowania w celu hello, które witryny hello szczegóły migracji, czy zostały one pomyślnie, łącza toohello nowo utworzony Azure aplikacje sieci web. 
    
    Jeśli dowolne wystąpienia błędu w trakcie migracji, wyraźnie hello będzie narzędzia migracji wskazywać hello błędu i wycofywania hello zmiany. Będzie również raportu o błędach hello toosend może bezpośrednia Inżynieria toohello zespołu, klikając hello **Wyślij raport o błędach** przycisk ze stosu wywołań przechwycony błąd hello i kompilacji treści wiadomości. 
    
    ![](./media/web-sites-migration-from-iis-server/migration-error-report.png)
    
    Jeśli migracja powiedzie się bez błędów, możesz również kliknąć hello **Przekaż opinię** przycisk tooprovide opinię bezpośrednio. 
12. Kliknij aplikacje sieci web Azure toohello łącza hello i sprawdź, czy migracja hello zakończyła się pomyślnie.
13. Możesz teraz zarządzać hello migracji aplikacji sieci web w usłudze Azure App Service. toodo, zaloguj się do hello [Azure Portal](https://portal.azure.com).
14. Hello portalu Azure, otwórz toosee bloku aplikacji sieci Web hello migrowanych witryny sieci Web (wyświetlane jako aplikacje sieci web), a następnie kliknij na jednym z nich toostart Zarządzanie hello aplikacji sieci web, takich jak skonfigurowanie ciągłego publikowania, tworzenie kopii zapasowych, skalowanie automatyczne i monitorowanie wykorzystania lub wydajność.
    
    ![](./media/web-sites-migration-from-iis-server/TimeTrackerMigrated.png)

> [!NOTE]
> Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service. Bez kart kredytowych i bez zobowiązań.
> 
> 

## <a name="whats-changed"></a>Co zostało zmienione
* Toohello przewodnik zmiany z tooApp witryn sieci Web usługi dla: [usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

