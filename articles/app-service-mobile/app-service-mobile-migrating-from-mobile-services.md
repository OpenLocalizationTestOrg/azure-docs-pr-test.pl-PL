---
title: "aaaMigrate z usługi Mobile Services tooan aplikację usługi Mobile aplikacji"
description: "Dowiedz się, jak tooeasily migracji z tooan aplikacji usługi Mobile Services aplikację usługi Mobile aplikacji"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 07507ea2-690f-4f79-8776-3375e2adeb9e
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile
ms.devlang: na
ms.topic: article
ms.date: 10/03/2016
ms.author: glenga
ms.openlocfilehash: cd2e8d98595703389300b79da9bf51cdcefe7b40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="article-top"></a>Migrowanie istniejących tooAzure usługi mobilnej Azure App Service
Z hello [ogólnej dostępności usługi Azure App Service], mogą być łatwo witryny usług Azure Mobile Services migracji w miejscu tootake zaletą wszystkich funkcji hello Azure App Service.  W tym dokumencie opisano jakie tooexpect podczas migracji lokacji z usług Azure Mobile Services tooAzure usługi aplikacji.

## <a name="what-does-migration-do"></a>Migracja czego tooyour lokacji
Migracja usługi mobilnej Azure włącza usługi mobilnej do [usłudze Azure App Service] aplikacji bez wpływu na powitania kodu.  Centra powiadomień, połączenie danych SQL, ustawień uwierzytelniania, zaplanowane zadania i nazwy domeny pozostają niezmienione.  Klientów mobilnych za pomocą usługi mobilnej Azure nadal toooperate normalnie.  Migracja powoduje ponowne uruchomienie usługi po przekazanych tooAzure usługi aplikacji.

[!INCLUDE [app-service-mobile-migrate-vs-upgrade](../../includes/app-service-mobile-migrate-vs-upgrade.md)]

## <a name="why-migrate"></a>Dlaczego należy dokonanie migracji lokacji
Microsoft jest rekomendowania dokonać migracji z usługi mobilnej Azure tootake z zalet hello funkcji Azure App Service, w tym:

* Nowe funkcje hosta, w tym [Webjob] i [niestandardowych nazw domen].
* Łączność tooyour zasobów lokalnych za pomocą [sieci wirtualnej] dodatkowo zbyt[połączeń hybrydowych].
* Monitorowanie i rozwiązywanie problemów z usługi New Relic lub [usługi Application Insights].
* Wbudowane narzędzia DevOps, łącznie z [przemieszczania miejsc], wycofywania i w środowisku produkcyjnym testowania.
* [Automatyczne skalowanie], równoważenie obciążenia, a [monitorowania wydajności].

Aby uzyskać więcej informacji na powitania świadczenia usługi Azure App Service, zobacz hello [vs usług Mobile Services. Usługi aplikacji] tematu.

## <a name="before-you-begin"></a>Przed rozpoczęciem
Przed rozpoczęciem głównych pracę, witryny, należy kopię zapasową skryptów usługi mobilnej i bazy danych SQL.

## <a name="migrating-site"></a>Migrowanie witryn
Witaj zostaną zmigrowane wszystkie lokacje w jednym regionie Azure.

toomigrate witryny:

1. Zaloguj się za toohello [klasycznego portalu Azure].
2. Wybierz usługi mobilnej w regionie hello mają toomigrate.
3. Kliknij przycisk hello **migracji tooApp usługi** przycisku.

   ![Witaj przycisk migracji][0]
4. Przeczytaj hello migracji tooApp usługi w oknie dialogowym.
5. Wprowadź nazwę hello usługi mobilnej w polu hello.  Na przykład, jeśli nazwa domeny to contoso.azure mobile.net, wprowadź *contoso* w polu hello.
6. Przycisk hello znaczników.

Monitorowanie stanu hello migracji hello w hello Monitora aktywności. Witryna jest wymienione jako *Migrowanie* w hello klasycznego portalu Azure.

  ![Monitorowanie aktywności migracji][1]

Każdy migracji może potrwać od 3 minuty too15 na migrowanym usługi mobilnej.  Witryna jest nadal dostępny w trakcie migracji hello.
Witryna zostanie ponownie na końcu hello hello procesu migracji.  Witryna Hello jest niedostępna podczas hello ponownego uruchomienia procesu, który może trwać kilka sekund.

## <a name="finalizing-migration"></a>Finalizowanie hello migracji
Planowanie tootest witryny z klienta mobilnego po zakończeniu hello hello procesu migracji.  Sprawdź, czy można wykonać wszystkich typowych akcji klienta bez klientów urządzeń przenośnych toohello zmiany.  

### <a name="update-app-service-tier"></a>Wybierz odpowiednią usługę aplikacji warstwy cenowej
Uzyskuje się większą elastyczność w cennik po przeprowadzeniu migracji tooAzure usługi aplikacji.

1. Zaloguj się za toohello [portalu Azure].
2. Wybierz **wszystkie zasoby** lub **usługi aplikacji** następnie kliknij nazwę hello zmigrowane usługi mobilnej.
3. Domyślnie zostanie otwarty blok ustawień Hello.
4. Kliknij przycisk **planu usługi App Service** w menu Ustawienia hello.
5. Kliknij przycisk hello **warstwy cenowej** kafelka.
6. Kliknij hello kafelka tooyour odpowiednie wymagania, a następnie kliknij przycisk **wybierz**.  Może być konieczne tooClick **Wyświetl wszystkie** toosee hello dostępnych warstw cenowych.

Jako punkt początkowy zaleca się hello następujące warstwy:

| Warstwy cenowej usługi mobilnej | Usługi aplikacji warstwy cenowej |
|:--- |:--- |
| Bezpłatna |Bezpłatna F1 |
| Podstawowa |B1 Basic |
| Standardowa |Standardowa S1 |

Brak dużą elastyczność w wyborze hello prawo warstwę cenową dla aplikacji.  Odwołuje się zbyt[App Service — ceny] Aby uzyskać szczegółowe informacje o cenach hello nowej usługi aplikacji.

> [!TIP]
> Witaj warstwy standardowa usługi aplikacji zawiera funkcje toomany dostępu, które mogą podlegać toouse, łącznie z [przemieszczania miejsc], automatycznego tworzenia kopii zapasowej i automatyczne skalowanie.  Zapoznaj się hello nowe możliwości, gdy istnieje!
>
>

### <a name="review-migration-scheduler-jobs"></a>Przejrzyj zadania harmonogramu migracji hello
Harmonogram zadań nie będą widoczne dopiero po zakończeniu migracji około 30 minut.  Zaplanowane zadania nadal toorun w tle hello.
tooview Twoje zaplanowane zadania po są widoczne ponownie:

1. Zaloguj się za toohello [portalu Azure].
2. Wybierz **Przeglądaj >**, wprowadź **harmonogram** w hello *filtru* polu, a następnie wybierz **kolekcje harmonogramu**.

Istnieje ograniczona liczba wolnych harmonogram zadania dostępne po migracji.  Przejrzyj użycia i hello [plany harmonogramu Azure].

### <a name="configure-cors"></a>Konfigurowanie mechanizmu CORS w razie potrzeby
Współużytkowanie zasobów między źródłami to technika tooallow tooaccess witryny sieci Web interfejs API sieci Web w innej domenie.  Jeśli korzystasz z usług Azure Mobile Services z witryny sieci Web skojarzony, należy tooconfigure CORS w ramach migracji hello.  Jeśli uzyskują dostęp do usług Azure Mobile Services wyłącznie z urządzeń przenośnych, CORS nie musi toobe skonfigurowany z wyjątkiem w rzadkich przypadkach.

Zmigrowane ustawienia mechanizmu CORS są dostępne jako hello **MS_CrossDomainWhitelist** ustawienia aplikacji.  toomigrate Twojego toohello lokacji zakładzie mechanizmu CORS usługi App Service:

1. Zaloguj się za toohello [portalu Azure].
2. Wybierz **wszystkie zasoby** lub **usługi aplikacji** następnie kliknij nazwę hello zmigrowane usługi mobilnej.
3. Domyślnie zostanie otwarty blok ustawień Hello.
4. Kliknij przycisk **CORS** w menu hello interfejsu API.
5. Wprowadź wszelkie dozwolone źródła w polu hello pod warunkiem, naciskając klawisz Enter po każdym.
6. Po liście dozwolone źródła jest poprawny, kliknij przycisk Zapisz hello.

> [!TIP]
> Jest jedną z zalet hello przy użyciu usługi Azure App Service można uruchamiać witryn sieci web i usługi mobilnej w na powitania tej samej lokacji.  Aby uzyskać więcej informacji, zobacz hello [następne kroki](#next-steps) sekcji.
>
>

### <a name="download-publish-profile"></a>Pobierz nowy profil publikowania
Hello profilu publikowania witryny jest zmieniany, gdy migracja tooAzure usługi aplikacji.  Jeśli planujesz toopublish witryny z poziomu programu Visual Studio, konieczne jest nowy profil publikowania.  toodownload hello nowy profil publikowania:

1. Zaloguj się za toohello [portalu Azure].
2. Wybierz **wszystkie zasoby** lub **usługi aplikacji** następnie kliknij nazwę hello zmigrowane usługi mobilnej.
3. Kliknij przycisk **profilu publikowania Get**.

Plik ustawień publikacji Hello jest pobrany tooyour komputera.  Jest to zwykle *sitename*. Ustawień publikacji.  Importuj hello opublikować ustawienia do istniejącego projektu:

1. Otwórz program Visual Studio i projekt usługi mobilnej Azure.
2. Kliknij prawym przyciskiem myszy projekt w hello **Eksploratora rozwiązań** i wybierz **publikowania...**
3. Kliknij przycisk **importu**
4. Kliknij przycisk **Przeglądaj** i wybierz z pobranego pliku ustawień publikowania.  Kliknij przycisk **OK**.
5. Kliknij przycisk **sprawdzania poprawności połączenia** tooensure hello opublikować ustawienia pracę.
6. Kliknij przycisk **publikowania** toopublish witryny.

## <a name="working-with-your-site"></a>Praca z Twojej lokacji po migracji
Rozpocząć pracę z usługą nowych aplikacji w hello [portalu Azure] po migracji.  Witaj poniżej przedstawiono niektóre informacje o na określonych operacji używane tooperform w hello [klasycznego portalu Azure], wraz z ich odpowiedniki usługi aplikacji.

### <a name="publishing-your-site"></a>Pobieranie i publikowanie migrowanych witryny
Witryna jest dostępna za pośrednictwem git i ftp i należy ponownie opublikować z różnych mechanizmów różne, w tym WebDeploy, TFS Mercurial, GitHub i FTP.  poświadczenia wdrożenia Hello są migrowane z pozostałą hello witryny.  Jeśli nie określono poświadczeń wdrożenia lub nie pamiętać, można zresetować je:

1. Zaloguj się za toohello [portalu Azure].
2. Wybierz **wszystkie zasoby** lub **usługi aplikacji** następnie kliknij nazwę hello zmigrowane usługi mobilnej.
3. Domyślnie zostanie otwarty blok ustawień Hello.
4. Kliknij przycisk **poświadczenia wdrażania** w hello publikowania menu.
5. Wprowadź nowe poświadczenia wdrożenia hello w dostępnych polach hello, a następnie kliknij przycisk Zapisz hello.

Można używać tych poświadczeń tooclone hello lokacji za pomocą narzędzia git lub konfigurowanie zautomatyzowanych wdrożeń z usługi GitHub, TFS lub Mercurial.  Aby uzyskać więcej informacji, zobacz hello [dokumentacja wdrażania usługi aplikacji Azure].

### <a name="appsettings"></a>Ustawienia aplikacji
Większość ustawień zmigrowanych usługi mobilnej są dostępne za pośrednictwem ustawień aplikacji.  Lista ustawień aplikacji hello można uzyskać z hello [portalu Azure].
tooview lub zmienić ustawienia aplikacji:

1. Zaloguj się za toohello [portalu Azure].
2. Wybierz **wszystkie zasoby** lub **usługi aplikacji** następnie kliknij nazwę hello zmigrowane usługi mobilnej.
3. Domyślnie zostanie otwarty blok ustawień Hello.
4. Kliknij przycisk **ustawienia aplikacji** hello ogólne menu.
5. Przewiń w sekcji Ustawienia aplikacji toohello i znaleźć ustawienia aplikacji.
6. Kliknij wartość hello hello aplikacji ustawienie tooedit hello wartości.  Kliknij przycisk **zapisać** toosave hello wartość.

Można zaktualizować wiele ustawień aplikacji na powitania tym samym czasie.

> [!TIP]
> Istnieją dwa ustawienia aplikacji z hello tę samą wartość.  Na przykład może zostać wyświetlony *ApplicationKey* i *MS\_ApplicationKey*.  Aktualizowanie ustawień aplikacji, zarówno na powitania tym samym czasie.
>
>

### <a name="authentication"></a>Uwierzytelnianie
Wszystkie ustawienia uwierzytelniania są dostępne jako ustawienia aplikacji w witrynie zmigrowane.  tooupdate ustawienia uwierzytelniania, należy zmienić ustawienia odpowiedniej aplikacji.  Witaj poniższej tabeli przedstawiono hello ustawień aplikacji właściwe dla dostawcy uwierzytelniania:

| Dostawca | Identyfikator klienta | Klucz tajny klienta | Inne ustawienia |
|:--- |:--- |:--- |:--- |
| Konto Microsoft |**MS\_MicrosoftClientID** |**MS\_MicrosoftClientSecret** |**MS\_MicrosoftPackageSID** |
| Facebook |**MS\_FacebookAppID** |**MS\_FacebookAppSecret** | |
| Twitter |**MS\_TwitterConsumerKey** |**MS\_TwitterConsumerSecret** | |
| Google |**MS\_GoogleClientID** |**MS\_GoogleClientSecret** | |
| Azure AD |**MS\_AadClientID** | |**MS\_AadTenants** |

Uwaga: **MS\_AadTenants** jest przechowywane w postaci listy rozdzielanej przecinkami domen dzierżawy (pola "Dozwolone dzierżaw" hello w portalu usługi Mobile Services hello).

> [!WARNING]
> **Nie używaj hello mechanizmów uwierzytelniania w menu Ustawienia hello**
>
> Usługa aplikacji Azure zapewnia osobne "bez kodu" uwierzytelnianie i autoryzacja system w obszarze hello *uwierzytelniania / autoryzacji* hello (przestarzałe) i ustawień menu *uwierzytelniania Mobile* Opcja menu Ustawienia hello.  Te opcje są niezgodne z migrowanych usługi mobilnej Azure.  Możesz [uaktualniania lokacji](app-service-mobile-net-upgrading-from-mobile-services.md) tootake zaletą hello uwierzytelniania usługi Azure App Service.
>
>

### <a name="easytables"></a>Dane
Hello *danych* karty w usłudze Mobile Services została zastąpiona przez *łatwe tabel* w hello portalu Azure.  tooaccess łatwe tabel:

1. Zaloguj się za toohello [portalu Azure].
2. Wybierz **wszystkie zasoby** lub **usługi aplikacji** następnie kliknij nazwę hello zmigrowane usługi mobilnej.
3. Domyślnie zostanie otwarty blok ustawień Hello.
4. Kliknij przycisk **łatwe tabel** hello przenośnych menu.

Tabelę można dodać, klikając hello **Dodaj** przycisk lub dostępu do istniejących tabel, klikając nazwę tabeli.  Istnieją różne operacje, które można wykonać z poziomu tego bloku, w tym:

* Zmienianie uprawnień tabeli
* Edytowanie hello operacyjne skryptów
* Zarządzanie schematem tabeli hello
* Usuwanie tabeli hello
* Wyczyszczenie hello spisu treści
* Usuwanie określonych wierszy w tabeli hello

### <a name="easyapis"></a>INTERFEJS API
Witaj *interfejsu API* karty w usłudze Mobile Services została zastąpiona przez *łatwe interfejsów API* w hello portalu Azure.  tooaccess łatwe interfejsów API:

1. Zaloguj się za toohello [portalu Azure].
2. Wybierz **wszystkie zasoby** lub **usługi aplikacji** następnie kliknij nazwę hello zmigrowane usługi mobilnej.
3. Domyślnie zostanie otwarty blok ustawień Hello.
4. Kliknij przycisk **łatwe interfejsów API** hello przenośnych menu.

Swoje migrowanych interfejsy API są już na liście hello bloku.  Można również dodać interfejsu API z poziomu tego bloku.  toomanage określonego interfejsu API, kliknij przycisk hello interfejsu API.
Na nowy blok hello można dostosować uprawnienia hello i edytować hello skryptów na potrzeby hello interfejsu API.

### <a name="on-demand-jobs"></a>Zadania harmonogramu
Wszystkie zadania harmonogramu są dostępne za pośrednictwem hello sekcji kolekcji zadań harmonogramu.  tooaccess harmonogramu zadań:

1. Zaloguj się za toohello [portalu Azure].
2. Wybierz **Przeglądaj >**, wprowadź **harmonogram** w hello *filtru* polu, a następnie wybierz **kolekcje harmonogramu**.
3. Wybierz hello kolekcji zadań dla witryny.  Szablon ma nazwę *sitename*-zadania.
4. Kliknij przycisk **ustawienia**.
5. Kliknij przycisk **zadania harmonogramu** w obszarze Zarządzanie.

Zaplanowane zadania są wyświetlane z częstotliwością hello, określone przed migracją.  Zadania na żądanie są wyłączone.  toorun zadanie na żądanie:

1. Wybierz zadanie hello mają toorun.
2. W razie potrzeby kliknij **włączyć** tooenable hello zadania.
3. Kliknij przycisk **ustawienia**, następnie **harmonogram**.
4. Wybierz opcję ponownego **raz**, następnie kliknij przycisk **Zapisz**

Twoje zadania na żądanie znajdują się w `App_Data/config/scripts/scheduler post-migration`.  Firma Microsoft zaleca przekonwertować wszystkie zadania na żądanie za[Webjob] lub [funkcji].  Zapisać nowe zadania harmonogramu jako [Webjob] lub [funkcji].

### <a name="notification-hubs"></a>Centra powiadomień
Mobile Services używa centra powiadomień dla powiadomień wypychanych.  następujące ustawienia aplikacji Hello są używane toolink hello tooyour Centrum powiadomień usługi mobilnej po migracji:

| Ustawienia aplikacji | Opis |
|:--- |:--- |
| **MS\_PushEntityNamespace** |Witaj Namespace Centrum powiadomień |
| **MS\_NotificationHubName** |Witaj nazwę Centrum powiadomień |
| **MS\_NotificationHubConnectionString** |Witaj parametry połączenia Centrum powiadomień |
| **MS\_nazwa przestrzeni nazw** |Alias MS_PushEntityNamespace |

Centrum powiadomień jest zarządzana za pomocą hello [portalu Azure].  Zanotuj nazwę Centrum powiadomień hello (można go znaleźć za pomocą ustawień aplikacji hello):

1. Zaloguj się za toohello [portalu Azure].
2. Wybierz **Przeglądaj**>, a następnie wybierz pozycję **centra powiadomień**
3. Kliknij nazwę Centrum powiadomień hello skojarzony z usługą mobilną hello.

> [!NOTE]
> Jeśli Centrum powiadomień jest typu "Mixed", nie jest widoczne.  "Mieszany" wpisz powiadomień koncentratory wykorzystywać zarówno usługi Notification Hubs i starszych funkcji usługi Service Bus.  [Konwertuj mieszanych obszary nazw] przed kontynuowaniem.  Po ukończeniu konwersji hello Centrum powiadomień zostanie wyświetlony w hello [portalu Azure].
>
>

Aby uzyskać więcej informacji, przejrzyj hello [usługi Notification Hubs] dokumentacji.

> [!TIP]
> Funkcje zarządzania centra powiadomień w hello [portalu Azure] są nadal w wersji zapoznawczej.  Witaj [klasycznego portalu Azure] pozostaje dostępna, zarządzanie centrów powiadomień.
>
>

### <a name="legacy-push"></a>Ustawienia starszych wypychania
Skonfigurowanie na usługi mobilnej przed wprowadzeniem hello na centra powiadomień wypychanych, czy używasz *starszych wypychania*.  Jeśli używasz wypychania i nie ma na liście konfiguracji centrum powiadomień, a następnie prawdopodobnie używasz *starszych wypychania*.  Ta funkcja jest migrowana z innymi funkcjami.  Jednak zaleca się uaktualnienie koncentratory tooNotification zaraz po zakończeniu migracji hello.

W hello tymczasowe wszystkie ustawienia starszych wypychania hello (z wyjątkiem zauważalne hello certyfikatu APNS hello) są dostępne w ustawień aplikacji.  Zaktualizuj certyfikat usługi APN hello zastępując hello odpowiedniego pliku na powitania systemu plików.

### <a name="app-settings"></a>Inne ustawienia aplikacji
następujące ustawienia dodatkowe aplikacji Hello są migrowane z usługi mobilnej i dostępnych w ramach *ustawienia* > *ustawień aplikacji*:

| Ustawienia aplikacji | Opis |
|:--- |:--- |
| **MS\_MobileServiceName** |Nazwa aplikacji Hello |
| **MS\_MobileServiceDomainSuffix** |Prefiks domeny Hello. tj Azure mobile.net |
| **MS\_ApplicationKey** |Klucz aplikacji |
| **MS\_umożliwia** |Klucz główny aplikacji |

Klucz aplikacji Hello i klucz główny są identyczne toohello kluczy aplikacji z oryginalnego usługi mobilnej.  W szczególności hello klucz aplikacji jest wysyłane przez klientów mobilnych toovalidate ich stosowania hello przenośnych interfejsu API.

### <a name="cliequivalents"></a>Odpowiedniki wiersza polecenia
Można już używać hello *azure przenośnych* polecenia toomanage witryny usług Azure Mobile Services.  Zamiast tego wiele funkcji zostało zastąpione hello *usługi azure site* polecenia.  Użyj poniższej hello tabeli toofind odpowiedniki Typowe polecenia:

| *Azure Mobile* polecenia | Odpowiednik *usługi Azure Site* polecenia |
|:--- |:--- |
| lokalizacje przenośnych |Lista lokalizacji lokacji |
| listy dla urządzeń przenośnych |Lista witryn |
| Pokaż przenośnych *nazwy* |Pokaż lokacji *nazwy* |
| ponowne uruchomienie przenośnych *nazwy* |ponowne uruchomienie witryny *nazwy* |
| Wdróż go ponownie przenośnych *nazwy* |Wdróż go ponownie wdrożenia lokacji *commitId* *nazwy* |
| przenośne zestawu kluczy *nazwa* *typu* *wartości* |Usuń appsetting lokacji *klucza* *nazwy* <br/> Dodaj witrynę appsetting *klucza*=*wartość* *nazwy* |
| Lista przenośnych konfiguracji *nazwy* |Lista appsetting lokacji *nazwy* |
| Pobierz przenośnych config *nazwa* *klucza* |Pokaż appsetting lokacji *klucza* *nazwy* |
| zestaw przenośnych config *nazwa* *klucza* |Usuń appsetting lokacji *klucza* *nazwy* <br/> Dodaj witrynę appsetting *klucza*=*wartość* *nazwy* |
| Lista przenośnych domeny *nazwy* |Lista domeny lokacji *nazwy* |
| Dodawanie domeny przenośnych *nazwa* *domeny* |Dodawanie domeny lokacji *domeny* *nazwy* |
| Usuń domeny przenośnych *nazwy* |Usuwanie domeny witryny *domeny* *nazwy* |
| Pokaż przenośnych skali *nazwy* |Pokaż lokacji *nazwy* |
| Zmiana skali przenośnych *nazwy* |Tryb skali witryn *tryb* *nazwy* <br /> lokacji wystąpień skali *wystąpień* *nazwy* |
| Lista przenośnych appsetting *nazwy* |Lista appsetting lokacji *nazwy* |
| Dodaj przenośnych appsetting *nazwa* *klucza* *wartości* |Dodaj witrynę appsetting *klucza*=*wartość* *nazwy* |
| Usuń przenośnych appsetting *nazwa* *klucza* |Usuń appsetting lokacji *klucza* *nazwy* |
| Pokaż przenośnych appsetting *nazwa* *klucza* |Usuń appsetting lokacji *klucza* *nazwy* |

Zaktualizuj uwierzytelniania lub wypychanej powiadomienie o ustawienia aktualizując hello odpowiednie ustawienie aplikacji.
Edytowanie plików i opublikować swoją witrynę przy użyciu protokołu ftp lub git.

### <a name="diagnostics"></a>Rejestrowanie i Diagnostyka
Rejestrowanie diagnostyczne zwykle jest wyłączony w usłudze Azure App Service.  tooenable rejestrowania diagnostycznego:

1. Zaloguj się za toohello [portalu Azure].
2. Wybierz **wszystkie zasoby** lub **usługi aplikacji** następnie kliknij nazwę hello zmigrowane usługi mobilnej.
3. Domyślnie zostanie otwarty blok ustawień Hello.
4. Wybierz **dzienników diagnostycznych** hello funkcje menu.
5. Kliknij przycisk **ON** dla hello następujące dzienniki: **rejestrowania aplikacji (systemu plików)**, **szczegółowe komunikaty o błędach**, i **śledzenie nieudanych żądań**
6. Kliknij przycisk **systemu plików** dla rejestrowania serwera sieci Web
7. Kliknij przycisk **Zapisz**

Dzienniki hello tooview:

1. Zaloguj się za toohello [portalu Azure].
2. Wybierz **wszystkie zasoby** lub **usługi aplikacji** następnie kliknij nazwę hello zmigrowane usługi mobilnej.
3. Kliknij przycisk hello **narzędzia** przycisku
4. Wybierz **strumienia dziennika** hello OBSERVE menu.

Dzienniki są wyświetlane w oknie hello, ponieważ są one generowane.  Możesz również pobrać dzienniki hello potrzeby późniejszej analizy przy użyciu poświadczeń wdrożenia. Aby uzyskać więcej informacji, zobacz hello [rejestrowanie] dokumentacji.

## <a name="known-issues"></a>Znane problemy
### <a name="deleting-a-migrated-mobile-app-clone-causes-a-site-outage"></a>Usuwanie klon migracji aplikacji mobilnej powoduje awarii lokacji
Jeśli klonowanie zmigrowane usługi mobilnej przy użyciu programu Azure PowerShell, a następnie usuń hello klonowania, hello wpis DNS dla usługi produkcji zostaną usunięte.  Witryny jest już dostępny z Internetu hello.  

Rozwiązanie: W razie potrzeby tooclone lokacji to zrobić za pośrednictwem portalu hello.

### <a name="changing-webconfig-does-not-work"></a>Zmienianie pliku Web.config nie działa
Jeśli masz witryny ASP.NET zmieni się toohello `Web.config` pliku nie zostać zastosowane.  Hello Azure App Service kompilacje odpowiedniej `Web.config` pliku podczas uruchamiania toosupport hello usług Mobile Services w czasie wykonywania.  Można zastąpić niektórych ustawień (np. nagłówki niestandardowe) przy użyciu pliku transformacji XML.  Utwórz plik w nazwie `applicationHost.xdt` — ten plik musi kończyć w hello `D:\home\site` katalogu na powitania usługi platformy Azure.  Przekaż `applicationHost.xdt` plików za pomocą skryptu wdrażania niestandardowych lub bezpośrednio za pomocą Kudu.  Witaj poniżej pokazano przykładowy dokument:

```
<?xml version="1.0" encoding="utf-8"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
  <system.webServer>
    <httpProtocol>
      <customHeaders>
        <add name="X-Frame-Options" value="DENY" xdt:Transform="Replace" />
        <remove name="X-Powered-By" xdt:Transform="Insert" />
      </customHeaders>
    </httpProtocol>
    <security>
      <requestFiltering removeServerHeader="true" xdt:Transform="SetAttributes(removeServerHeader)" />
    </security>
  </system.webServer>
</configuration>
```

Aby uzyskać więcej informacji, zobacz hello [przykłady przekształcenie XDT] dokumentacji w witrynie GitHub.

### <a name="migrated-mobile-services-cannot-be-added-tootraffic-manager"></a>Nie można dodać zmigrowane usługi mobilnej tooTraffic Manager
Podczas tworzenia profilu usługi Traffic Manager nie może bezpośrednio wybierz profil toohello zmigrowane usługi mobilnej.  Użyj "zewnętrznego punktu końcowego."  Zewnętrznego punktu końcowego można dodawać tylko za pomocą programu PowerShell.  Aby uzyskać więcej informacji, zobacz [samouczek Menedżera ruchu](https://azure.microsoft.com/blog/azure-traffic-manager-external-endpoints-and-weighted-round-robin-via-powershell/).

## <a name="next-steps"></a>Następne kroki
Teraz, że aplikacja jest tooApp zmigrowane usługi, istnieją nawet więcej funkcji, których można użyć:

* Wdrożenie [przemieszczania miejsc] pozwalają toostage zmiany tooyour lokacji i wykonywania A / B testowania.
* [Webjob] zapewnieniu jej zamiennika dla zadania zaplanowane na żądanie.
* Możesz [stale wdrażanie] witryny przez łączenie z witryny tooGitHub, TFS lub Mercurial.
* Można użyć [usługi Application Insights] toomonitor witryny.
* Służą a witryny sieci Web i interfejs API Mobile z hello tego samego kodu.

### <a name="upgrading-your-site"></a>Uaktualnianie tooAzure lokacji z usług Mobile Services zestaw SDK usługi Mobile Apps
* Dla projektów serwera opartego na Node.js hello nowych [zestaw SDK usługi Mobile Apps Node.js] udostępnia kilka nowych funkcji. Na przykład można teraz nie lokalne działania projektowe i debugowanie, użyj dowolnej wersji środowiska Node.js powyżej 0.10 i dostosować za pomocą wszystkich programów pośredniczących Express.js.
* Aby uzyskać. Projekty oparte na sieci serwera hello nowych [pakietów NuGet zestawu SDK aplikacji mobilnych](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) zależności NuGet uzyskuje się większą elastyczność.  Te pakiety obsługuje hello nowej aplikacji usługi uwierzytelniania i tworzą z żadnym projektem platformy ASP.NET. Aby dowiedzieć się więcej na temat uaktualniania, zobacz [uaktualnić istniejącą tooApp usługi mobilnej platformy .NET usługi](app-service-mobile-net-upgrading-from-mobile-services.md).

<!-- Images -->
[0]: ./media/app-service-mobile-migrating-from-mobile-services/migrate-to-app-service-button.PNG
[1]: ./media/app-service-mobile-migrating-from-mobile-services/migration-activity-monitor.png
[2]: ./media/app-service-mobile-migrating-from-mobile-services/triggering-job-with-postman.png

<!-- Links -->
[Cennik usługi aplikacji]: https://azure.microsoft.com/en-us/pricing/details/app-service/
[usługi Application Insights]: ../application-insights/app-insights-overview.md
[Automatyczne skalowanie]: ../app-service-web/web-sites-scale.md
[usłudze Azure App Service]: ../app-service/app-service-value-prop-what-is.md
[dokumentacja wdrażania usługi aplikacji Azure]: ../app-service-web/web-sites-deploy.md
[klasycznego portalu Azure]: https://manage.windowsazure.com
[portalu Azure]: https://portal.azure.com
[Azure Region]: https://azure.microsoft.com/en-us/regions/
[plany harmonogramu Azure]: ../scheduler/scheduler-plans-billing.md
[stale wdrażanie]: ../app-service-web/app-service-continuous-deployment.md
[Konwertuj mieszanych obszary nazw]: https://azure.microsoft.com/en-us/blog/updates-from-notification-hubs-independent-nuget-installation-model-pmt-and-more/
[curl]: http://curl.haxx.se/
[niestandardowych nazw domen]: ../app-service-web/web-sites-custom-domain-name.md
[Fiddler]: http://www.telerik.com/fiddler
[ogólnej dostępności usługi Azure App Service]: https://azure.microsoft.com/blog/announcing-general-availability-of-app-service-mobile-apps/
[połączeń hybrydowych]: ../app-service-web/web-sites-hybrid-connection-get-started.md
[rejestrowanie]: ../app-service-web/web-sites-enable-diagnostic-log.md
[zestaw SDK usługi Mobile Apps Node.js]: https://github.com/azure/azure-mobile-apps-node
[vs usług Mobile Services. Usługi aplikacji]: app-service-mobile-value-prop-migration-from-mobile-services.md
[usługi Notification Hubs]: ../notification-hubs/notification-hubs-push-notification-overview.md
[monitorowania wydajności]: ../app-service-web/web-sites-monitor.md
[Postman]: http://www.getpostman.com/
[przemieszczania miejsc]: ../app-service-web/web-sites-staged-publishing.md
[sieci wirtualnej]: ../app-service-web/web-sites-integrate-with-vnet.md
[Webjob]: ../app-service-web/websites-webjobs-resources.md
[przykłady przekształcenie XDT]: https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples
[funkcji]: ../azure-functions/functions-overview.md
