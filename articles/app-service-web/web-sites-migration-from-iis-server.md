---
title: "Migrowanie aplikacji sieci Web przedsiębiorstwa do usługi Azure App Service"
description: "Przedstawia sposób użycia Asystenta migracji aplikacji sieci Web szybko migrację istniejących witryn sieci Web usług IIS do aplikacji sieci Web usługi aplikacji Azure"
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
ms.openlocfilehash: 18d6a8da38b42dcf5c1500f7fc26638aea26a809
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="migrate-an-enterprise-web-app-to-azure-app-service"></a>Migrowanie aplikacji sieci Web przedsiębiorstwa do usługi Azure App Service
Możesz łatwo przeprowadzić migrację istniejących uruchomionymi na Internet Information Service (IIS) 6 lub nowszej do witryny sieci Web [aplikacji usługi sieci Web aplikacji](http://go.microsoft.com/fwlink/?LinkId=529714). 

> [!IMPORTANT]
> Windows Server 2003 osiągnięto koniec pomocy technicznej na 14 lipca 2015 r. Obecnie obsługując witryny sieci Web na serwerze IIS to Windows Server 2003, aplikacje sieci Web jest niskiego ryzyka, niskich kosztach i niskim tarcia sposobem utrzymywania witryn w trybie online i Asystenta migracji aplikacji sieci Web pomaga zautomatyzować proces migracji. 
> 
> 

[Web Apps migracji Asystenta](https://www.movemetothecloud.net/) można analizować instalacji serwera IIS, które witryny można poddać migracji do usługi App Service, zaznacz wszystkie elementy, które nie mogą być migrowane lub nieobsługiwane na platformie, a następnie przeprowadzić migrację witryny sieci Web i skojarzone bazy danych do platformy Azure.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="elements-verified-during-compatibility-analysis"></a>Elementy zweryfikowana podczas analizy zgodności
Asystent migracji tworzy raport gotowości, aby zidentyfikować wszelkie potencjalnych przyczyn problemu lub problemy z blokowaniem, które mogą uniemożliwić pomyślną migrację z lokalnej usługi IIS do aplikacji sieci Web usługi aplikacji Azure. Niektóre z kluczowych elementów pod uwagę są:

* Port powiązania — aplikacji sieci Web obsługuje tylko Port 80 dla protokołu HTTP i portu 443 dla ruchu HTTPS. Konfiguracje innego portu zostanie zignorowany, a ruch będą kierowane do 80 i 443. 
* Uwierzytelnianie — aplikacji sieci Web obsługuje uwierzytelnianie anonimowe domyślnie i uwierzytelnianie oparte na formularzach w przypadku, gdy określony przez aplikację. Dzięki integracji z usługą Azure Active Directory i usług AD FS tylko jest używane uwierzytelnianie systemu Windows. Wszystkie inne formy uwierzytelniania — na przykład uwierzytelnianie podstawowe — nie są obecnie obsługiwane. 
* Globalnej pamięci podręcznej zestawów (GAC) — pamięci podręcznej GAC nie jest obsługiwany w aplikacji sieci Web. Jeśli aplikacja odwołuje się do zestawów, które zwykle wdrażasz do pamięci podręcznej GAC, należy wdrożyć na folder bin aplikacji w aplikacji sieci Web. 
* Wersją IIS5 Tryb zgodności — nie jest to obsługiwane w aplikacjach sieci Web. 
* Pule aplikacji — w aplikacji sieci Web, każdej lokacji i jej podrzędne aplikacje uruchomione w tej samej puli aplikacji. Jeśli witryna ma wiele aplikacji podrzędnych przy użyciu wielu pul aplikacji, konsolidować je do jednej puli aplikacji z typowymi ustawieniami lub migracji poszczególnych aplikacji w aplikacji sieci web w osobnych.
* COM — składniki — aplikacji sieci Web nie zezwala na rejestracji składników COM na platformie. Jeśli z witryn sieci Web lub aplikacji wykorzystać wszystkie składniki modelu COM, musi ponownie zapisuje je w kodzie zarządzanym i wdrażać je z witryny sieci Web lub aplikacji.
* Rozszerzenia ISAPI — aplikacji sieci Web obsługuje używanie rozszerzenia ISAPI. Należy wykonać następujące czynności:
  
  * Wdróż biblioteki dll z aplikacji sieci web 
  * Zarejestruj za pomocą bibliotek DLL [pliku Web.config](http://www.iis.net/configreference/system.webserver/isapifilters)
  * Umieść plik applicationHost.xdt w katalogu głównym witryny z zawartością opisane w "Zezwalanie arbitrart rozszerzeń ISAPI do załadowania" [sekcji tego artykułu](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples) 
    
  
    
    Aby uzyskać więcej przykładów do transformacji dokumentów XML za pomocą witryny sieci Web, zobacz [przekształcenie witryny sieci Web Microsoft Azure](http://blogs.msdn.com/b/waws/archive/2014/06/17/transform-your-microsoft-azure-web-site.aspx).
* Inne składniki, takich jak SharePoint, rozszerzenia serwera FrontPage (FPSE), FTP, certyfikaty SSL nie zostaną zmigrowane.

## <a name="how-to-use-the-web-apps-migration-assistant"></a>Sposób korzystania z Asystenta migracji aplikacji sieci Web
Ta procedura sekcji za pośrednictwem przykład w celu migracji kilka witryn sieci Web, że korzystanie z bazy danych programu SQL Server i uruchomiona na lokalnym komputerze z systemem Windows Server 2003 R2 (IIS 6.0):

1. Na serwerze IIS serwerze lub komputerze klienckim przejdź do [https://www.movemetothecloud.net/](https://www.movemetothecloud.net/) 
   
   ![](./media/web-sites-migration-from-iis-server/migration-tool-homepage.png)
2. Instalowanie Asystenta migracji aplikacji sieci Web, klikając **serwera IIS w wersji dedykowanej** przycisku. Aby wyświetlić więcej opcji będzie opcje w najbliższej przyszłości. 
3. Kliknij przycisk **Zainstaluj narzędzie** przycisk, aby zainstalować Asystenta migracji aplikacji sieci Web na tym komputerze.
   
   ![](./media/web-sites-migration-from-iis-server/install-page.png)
   
   > [!NOTE]
   > Możesz również kliknąć **Pobierz instalacji w trybie offline** Aby pobrać plik ZIP do instalowania na serwerach nie jest połączony z Internetem. Możesz też kliknąć przycisk **przekazać istniejący raport gotowości migracji**, która jest opcją zaawansowaną do pracy z istniejących migracji Raport gotowości wcześniej generowany (co omówiono później).
   > 
   > 
4. W **instalacji aplikacji** kliknij **zainstalować** do zainstalowania na tym komputerze. Spowoduje także zainstalowanie odpowiednich zależności, takie jak narzędzie Web Deploy, DacFX i IIS, jeśli to konieczne. 
   
   ![](./media/web-sites-migration-from-iis-server/install-progress.png)
   
   Po zakończeniu instalacji Asystenta migracji aplikacji sieci Web jest uruchamiana automatycznie.
5. Wybierz **migracji lokacji i bazy danych z serwera zdalnego Azure**. Wprowadź poświadczenia administracyjne dla serwera zdalnego, a następnie kliknij przycisk **Kontynuuj**. 
   
   ![](./media/web-sites-migration-from-iis-server/migrate-from-remote.png)
   
   Oczywiście można migrować z lokalnego serwera. Zdalne opcja jest przydatna, gdy użytkownik chce migrować witryn sieci Web z produkcyjnym serwerem usługi IIS.
   
   W tym momencie będzie przeprowadzał inspekcję narzędzie do migracji konfiguracji serwera IIS, np. witryny, aplikacji, pul aplikacji i zależności, do identyfikowania candidate witryn sieci Web do migracji. 
6. Poniższy zrzut ekranu przedstawia trzy witryn sieci Web — **domyślna witryna sieci Web**, **TimeTracker**, i **CommerceNet4**. Wszystkie mają skojarzonej bazy danych, która ma być migracji. Wybierz wszystkie witryny, które chcesz ocenić, a następnie kliknij przycisk **dalej**.
   
   ![](./media/web-sites-migration-from-iis-server/select-migration-candidates.png)
7. Kliknij przycisk **przekazać** przekazać Raport gotowości. Jeśli klikniesz przycisk **Zapisz plik lokalnie**, można ponownie uruchomić narzędzie do migracji i przekaż Raport gotowości zapisanych, jak wspomniano wcześniej.
   
   ![](./media/web-sites-migration-from-iis-server/upload-readiness-report.png)
   
   Po przekazaniu Raport gotowości Azure przeprowadza analizę gotowości i pokazuje wyniki. Przeczytaj szczegóły oceny dla każdej witryny sieci Web i upewnij się, że rozumie, lub usunąć wszystkie problemy przed kontynuowaniem. 
   
   ![](./media/web-sites-migration-from-iis-server/readiness-assessment.png)
8. Kliknij przycisk **rozpocząć migrację** aby rozpocząć migrację. Nastąpi przekierowanie do platformy Azure, aby zalogować się do swojego konta. Jest ważne, aby zalogować się przy użyciu konta, które ma aktywną subskrypcją platformy Azure. Jeśli nie masz konta platformy Azure, można założyć bezpłatnej wersji próbnej [tutaj](https://azure.microsoft.com/pricing/free-trial/?WT.srch=1&WT.mc_ID=SEM_). 
9. Wybierz region baz danych i aplikacji sieci web platformy Azure zmigrowane, a następnie kliknij przycisk konta dzierżawy, subskrypcji platformy Azure i **Start migracji**. Możesz wybrać witryn sieci Web, aby przeprowadzić migrację później.
   
   ![](./media/web-sites-migration-from-iis-server/choose-tenant-account.png)
10. Na następnym ekranie można można zmienić domyślne ustawienia migracji, takie jak:
    
    * Użyj istniejącej bazy danych SQL Azure lub Utwórz nową bazę danych SQL Azure i skonfigurować jej poświadczenia
    * Wybierz witryny sieci Web do migracji
    * Definiowanie nazw dla aplikacji sieci web platformy Azure i ich połączonej bazy danych SQL
    * Dostosuj ustawienia globalne i ustawienia na poziomie witryny
    
    Poniższy zrzut ekranu przedstawia wszystkich witryn sieci Web wybrana do migracji z ustawieniami domyślnymi.
    
    ![](./media/web-sites-migration-from-iis-server/migration-settings.png)
    
    > [!NOTE]
    > **włączyć usługi Azure Active Directory** wyboru w niestandardowych ustawieniach integruje się w aplikacji sieci web platformy Azure przy użyciu [usługi Azure Active Directory](../active-directory/active-directory-whatis.md) ( **katalog domyślny**). Aby uzyskać więcej informacji o synchronizacji usługi Azure Active Directory z lokalnej usługi Active Directory, zobacz [integracji katalogów](http://msdn.microsoft.com/library/jj573653).
    > 
    > 
11. Po wprowadzeniu wszystkich odpowiednich zmian, kliknij przycisk **Utwórz** do rozpoczęcia procesu migracji. Narzędzie do migracji tworzenie bazy danych SQL Azure i aplikacji sieci web platformy Azure, a następnie opublikować zawartości witryny sieci Web i baz danych. Postęp migracji wyraźnie jest wyświetlany w narzędziu do migracji, a następnie zostanie wyświetlony ekran podsumowania na końcu szczegóły Lokacje migracji, czy zostały one pomyślnie, linki do aplikacji nowo utworzone sieci web platformy Azure. 
    
    W przypadku błędu podczas migracji, narzędzie do migracji zostanie wyraźnie wskazuje błędu i wycofywania zmian. Ponadto można wysłać raport o błędach bezpośrednio do zespołu inżynieryjnego, klikając **Wyślij raport o błędach** przycisku, z błędem przechwyconych stos wywołań i kompilacji treści wiadomości. 
    
    ![](./media/web-sites-migration-from-iis-server/migration-error-report.png)
    
    Jeśli migracja powiedzie się bez błędów, możesz również kliknąć **Przekaż opinię** przycisk, aby zapewnić opinię bezpośrednio. 
12. Kliknij łącza do aplikacji sieci web platformy Azure i sprawdź, czy migracja zakończyła się pomyślnie.
13. Możesz teraz zarządzać aplikacji sieci web zmigrowane w usłudze Azure App Service. Aby to zrobić, zaloguj się do [Azure Portal](https://portal.azure.com).
14. W portalu Azure otwarcie bloku aplikacji sieci Web, aby zobaczyć migrowanych witryny sieci Web (wyświetlane jako aplikacje sieci web), a następnie kliknij na jednym z nich, aby rozpocząć zarządzanie aplikacją sieci web, takich jak konfigurowanie ciągłej publikowania, tworzenia kopii zapasowych, skalowanie automatyczne i monitorowania użycia i wydajności.
    
    ![](./media/web-sites-migration-from-iis-server/TimeTrackerMigrated.png)

> [!NOTE]
> Jeśli chcesz zacząć korzystać z usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź do artykułu [Try App Service](https://azure.microsoft.com/try/app-service/) (Wypróbuj usługę App Service), w którym wyjaśniono, jak od razu utworzyć początkową aplikację sieci Web o krótkim okresie istnienia w usłudze App Service. Bez kart kredytowych i bez zobowiązań.
> 
> 

## <a name="whats-changed"></a>Co zostało zmienione
* Przewodnik dotyczący przejścia od usługi Witryny sieci Web do usługi App Service można znaleźć w temacie [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714) (Usługa Azure App Service i jej wpływ na istniejące usługi platformy Azure).

