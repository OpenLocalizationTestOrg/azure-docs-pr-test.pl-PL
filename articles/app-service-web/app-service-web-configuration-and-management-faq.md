---
title: "aaaConfiguration — często zadawane pytania dotyczące aplikacji sieci web platformy Azure | Dokumentacja firmy Microsoft"
description: "Uzyskaj odpowiedzi toofrequently zadawane pytania dotyczące konfiguracji i problemów z zarządzaniem funkcji Web Apps hello Azure App Service."
services: app-service\web
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 5aa405582813291a4aaf144d2f821ecb20a5edcb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configuration-and-management-faqs-for-web-apps-in-azure"></a>Konfigurowanie i zarządzanie często zadawane pytania dotyczące aplikacji sieci Web na platformie Azure

Ten artykuł zawiera odpowiedzi toofrequently zadawane pytania (FAQ) dotyczące problemów dotyczących konfiguracji i zarządzania dla hello [funkcja Web Apps usługi Azure App Service](https://azure.microsoft.com/services/app-service/web/).

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="are-there-limitations-i-should-be-aware-of-if-i-want-toomove-app-service-resources"></a>Czy istnieją ograniczenia I należy zwrócić uwagę aby toomove zasobów usługi aplikacji?

Jeśli planujesz toomove usługi aplikacji — zasoby tooa nową grupę zasobów lub subskrypcji, istnieje kilka ograniczeń toobe znane. Aby uzyskać więcej informacji, zobacz [ograniczenia usługi aplikacji](../azure-resource-manager/resource-group-move-resources.md#app-service-limitations).

## <a name="how-do-i-use-a-custom-domain-name-for-my-web-app"></a>Jak używać niestandardowej nazwy domeny dla mojej aplikacji sieci web?

Aby toocommon odpowiedzi na pytania dotyczące korzystania z niestandardowej nazwy domeny z aplikacji sieci web platformy Azure, zobacz nasze 7 minutowy film wideo [Dodawanie niestandardowej nazwy domeny](https://channel9.msdn.com/blogs/Azure-App-Service-Self-Help/Add-a-Custom-Domain-Name). przewodnik oferuje Hello wideo tooadd niestandardowej nazwy domeny. Opisuje sposób toouse własnego adresu URL zamiast hello *. azurewebsites.net adresu URL aplikacji sieci web usługi aplikacji. Również widoczne szczegółowe wskazówki dotyczące [jak toomap niestandardowej nazwy domeny](web-sites-custom-domain-name.md).


## <a name="how-do-i-purchase-a-new-custom-domain-for-my-web-app"></a>Jak kupić nowej domeny niestandardowej dla mojej aplikacji sieci web?

jak toopurchase i skonfiguruj niestandardową domenę na potrzeby aplikacji sieci web usługi aplikacji, zobacz toolearn [kupowanie i konfigurowanie niestandardowej nazwy domeny w usłudze App Service](custom-dns-web-site-buydomains-web-app.md).


## <a name="how-do-i-upload-and-configure-an-existing-ssl-certificate-for-my-web-app"></a>Jak przekazać i skonfigurować certyfikat SSL dla mojej aplikacji sieci web?

jak tooupload i konfigurowanie niestandardowych istniejącego certyfikatu SSL, zobacz toolearn [Powiąż istniejący niestandardowy SSL certyfikatu tooan aplikacji sieci web Azure](app-service-web-tutorial-custom-ssl.md#upload).


## <a name="how-do-i-purchase-and-configure-a-new-ssl-certificate-in-azure-for-my-web-app"></a>Jak kupić i skonfigurować nowy certyfikat SSL dla mojej aplikacji sieci web na platformie Azure?

jak toopurchase i skonfigurować certyfikat SSL dla aplikacji sieci web usługi aplikacji, zobacz toolearn [dodać tooyour certyfikatu SSL aplikacji usługi app Service](web-sites-purchase-ssl-web-site.md).


## <a name="how-do-i-move-application-insights-resources"></a>Jak przenieść zasobów usługi Application Insights?

Obecnie usługa Azure Application Insights nie obsługuje operacji przenoszenia hello. Jeśli oryginalną grupę zasobów zawiera zasób usługi Application Insights, nie można przenieść tego zasobu. Jeśli dołączysz zasobu usługi Application Insights hello podczas próby toomove aplikacji usługi app Service, hello całego Przenieś operacja kończy się niepowodzeniem. Jednak usługa Application Insights i hello niepotrzebne toobe w planie usługi aplikacji hello poprawnie tej samej grupie zasobów co aplikacja hello dla toofunction aplikacji hello.

Aby uzyskać więcej informacji, zobacz [ograniczenia usługi aplikacji](../azure-resource-manager/resource-group-move-resources.md#app-service-limitations).

## <a name="where-can-i-find-a-guidance-checklist-and-learn-more-about-resource-move-operations"></a>Gdzie można znaleźć listę kontrolną wskazówki i Dowiedz się więcej na temat zasobów operacje są przenoszone?

[Ograniczenia usługi aplikacji](../azure-resource-manager/resource-group-move-resources.md#app-service-limitations) pokazuje, jak toomove tooeither zasobów nowej subskrypcji lub tooa nowy zasób grupy w hello sam subskrypcji. Możesz uzyskać informacje na temat listy kontrolnej przenoszenia zasobów hello, Dowiedz się więcej usług, które obsługują operacji przenoszenia hello i Dowiedz się więcej na temat ograniczeń usługi aplikacji i innych tematach.

## <a name="how-do-i-set-hello-server-time-zone-for-my-web-app"></a>Jak ustawić strefy czasowej serwera hello do mojej aplikacji sieci web?

tooset powitania serwera strefę czasową dla aplikacji sieci web:

1. W portalu Azure w ramach subskrypcji usługi aplikacji hello Przejdź toohello **ustawienia aplikacji** menu.
2. W obszarze **ustawień aplikacji**, Dodaj następujące ustawienie:
    * Klucz = WEBSITE_TIME_ZONE
    * Wartość = *hello strefa czasowa ma*
3. Wybierz pozycję **Zapisz**.

## <a name="why-do-my-continuous-webjobs-sometimes-fail"></a>Dlaczego moje ciągłe zadania Webjob czasami nie powiodło się?

Domyślnie aplikacje sieci web są usuwane, jeśli są one bezczynności na wybrany okres czasu. Dzięki temu system hello zaoszczędzenia zasobów. W planie Basic i Standard, możesz włączyć hello **zawsze na** ustawienie aplikacji sieci web hello tookeep załadować cały czas hello. Jeśli aplikacja sieci web jest uruchomiony ciągłe zadania Webjob, należy włączyć **zawsze na**, lub hello zadania Webjob może nie działać prawidłowo. Aby uzyskać więcej informacji, zobacz [tworzenie stale uruchomione zadania WebJob](web-sites-create-web-jobs.md#CreateContinuous).

## <a name="how-do-i-get-hello-outbound-ip-address-for-my-web-app"></a>Jak uzyskać hello wychodzący adres IP dla mojej aplikacji sieci web?

Lista hello tooget wychodzących adresów IP dla aplikacji sieci web:

1. W portalu Azure, w bloku aplikacja sieci web, hello Przejdź toohello **właściwości** menu.
2. Wyszukaj **adresy ip wychodzących**.

zostanie wyświetlona lista Hello wychodzących adresów IP.

Jeżeli witryny sieci Web znajduje się w środowisku usługi aplikacji dla rozwiązania PowerApps, toolearn jak tooget wychodzący adres IP, zobacz [adresów sieciowych wychodzących](app-service-app-service-environment-network-architecture-overview.md#outbound-network-addresses).

## <a name="how-do-i-get-a-reserved-or-dedicated-inbound-ip-address-for-my-web-app"></a>Jak uzyskać zarezerwowany lub jest dedykowany dla ruchu przychodzącego adresu IP dla mojej aplikacji sieci web?

tooset się dedykowanej lub zastrzeżony adres IP dla ruchu przychodzącego wywołania tooyour Azure aplikacji witryny sieci Web, zainstalować i skonfigurować certyfikat SSL opartego na protokole IP.

Należy pamiętać, że toouse dedykowana lub zastrzeżonego adresu IP dla połączeń przychodzących, planu usługi aplikacji musi mieć w planie usługi podstawowe lub nowszej.

## <a name="can-i-export-my-app-service-certificate-toouse-outside-azure-such-as-for-a-website-hosted-elsewhere"></a>Moje toouse certyfikatu usługi aplikacji poza Azure, można wyeksportować takie jak witryny sieci Web hostowaną w innym miejscu? 

Certyfikaty usługi aplikacji są traktowane jako zasobów platformy Azure. Nie są one przeznaczone toouse poza usługami Azure. Nie można wyeksportować je toouse poza Azure. Aby uzyskać więcej informacji, zobacz [— często zadawane pytania dotyczące certyfikaty usługi aplikacji i domen niestandardowych](https://social.msdn.microsoft.com/Forums/azure/f3e6faeb-5ed4-435a-adaa-987d5db43b80/faq-on-app-service-certificates-and-custom-domains?forum=windowsazurewebsitespreview).

## <a name="can-i-export-my-app-service-certificate-toouse-with-other-azure-cloud-services"></a>Można wyeksportować Mój toouse certyfikatu usługi aplikacji z innymi usługami w chmurze Azure?

Hello portal zapewnia najwyższej jakości środowisko do wdrażania certyfikatów usługi aplikacji za pośrednictwem usługi Azure Key Vault tooApp usługi aplikacji. Jednak firma Microsoft odbierała ona żądania od klientów toouse tych certyfikatów poza hello usługi aplikacji platformy, na przykład z maszyn wirtualnych platformy Azure. toolearn jak toocreate PFX kopię lokalną usługą aplikacji certyfikatu, dzięki czemu można użyć certyfikatu hello z innych zasobów platformy Azure, zobacz [utworzyć kopię lokalną PFX certyfikatu usługi aplikacji](https://blogs.msdn.microsoft.com/appserviceteam/2017/02/24/creating-a-local-pfx-copy-of-app-service-certificate/).

Aby uzyskać więcej informacji, zobacz [— często zadawane pytania dotyczące certyfikaty usługi aplikacji i domen niestandardowych](https://social.msdn.microsoft.com/Forums/azure/f3e6faeb-5ed4-435a-adaa-987d5db43b80/faq-on-app-service-certificates-and-custom-domains?forum=windowsazurewebsitespreview).


## <a name="why-do-i-see-hello-message-partially-succeeded-when-i-try-tooback-up-my-web-app"></a>Dlaczego widzę wiadomości powitania "Częściowo powiodła się" podczas próby tooback zapasową mojej aplikacji sieci web?

Częstą przyczyną niepowodzenia wykonywania kopii zapasowej jest, że niektóre pliki są używane przez aplikację hello. Pliki, które są używane są zablokowane, gdy wykonanie kopii zapasowej hello. To zapobiega tworzona kopia zapasowa tych plików i może spowodować stanem "Częściowo powiodła się". Użytkownik może potencjalnie temu zapobiec przez wykluczanie plików z hello procesu tworzenia kopii zapasowej. Możesz wybrać tooback się tylko co jest potrzebne. Aby uzyskać więcej informacji, zobacz [kopii zapasowej tylko hello ważne części swoją witrynę przy użyciu aplikacji sieci web platformy Azure](http://www.zainrizvi.io/2015/06/05/creating-partial-backups-of-your-site-with-azure-web-apps/).

## <a name="how-do-i-remove-a-header-from-hello-http-response"></a>Jak usunąć nagłówek z hello odpowiedzi HTTP?

tooremove hello nagłówków z hello odpowiedzi HTTP, zaktualizuj plik web.config witryny sieci. Aby uzyskać więcej informacji, zobacz [usunąć nagłówki standard server na witryny sieci Web Azure](https://azure.microsoft.com/blog/removing-standard-server-headers-on-windows-azure-web-sites/).

## <a name="is-app-service-compliant-with-pci-standard-30-and-31"></a>Usługi aplikacji jest zgodne z PCI standardowe 3.0 i 3.1?

Funkcja Web Apps hello Azure App Service jest obecnie zgodnie z PCI danych zabezpieczeń Standard (DSS) w wersji 3.0 poziomu 1. PCI DSS w wersji 3.1 znajduje się w naszej plan. Planowanie trwa już sposób wdrożenia standardu najnowsze hello będzie kontynuowana.

PCI DSS wersji 3.1 certyfikacji wymaga wyłączenie zabezpieczeń TLS (Transport Layer) 1.0. Obecnie wyłączenie protokołu TLS 1.0 nie jest opcją dla większości planów usługi aplikacji. Jednak jeśli Użyj środowiska usługi aplikacji lub są ujawniane toomigrate Twojego tooApp obciążenia środowiska usługi, możesz uzyskać większą kontrolę nad środowiska. Obejmuje to wyłączenie protokołu TLS 1.0, kontaktując się z pomocą techniczną platformy Azure. W hello Najbliższa przyszłość planujemy toomake toousers dostępny tych ustawień.

Aby uzyskać więcej informacji, zobacz [zgodności aplikacji sieci web Microsoft Azure App Service z PCI standardowe 3.0 i 3.1](https://support.microsoft.com/help/3124528).

## <a name="how-do-i-use-hello-staging-environment-and-deployment-slots"></a>Jak używać hello przemieszczania środowiska i miejsc wdrożenia?

W planie Standard i Premium usługi aplikacji podczas wdrażania tooApp aplikacji sieci web usługi, można wdrożyć miejsce wdrożenia oddzielnych tooa zamiast miejsca produkcji toohello domyślne. Miejsca wdrożenia są aplikacje sieci web, które mają własne nazwy hosta. Elementy zawartości i konfiguracji aplikacji sieci Web może być zamieniona między dwóch miejsc wdrożenia, w tym hello miejsca produkcji.

Aby uzyskać więcej informacji na temat używania miejsc wdrożenia, zobacz [Konfigurowanie środowiska przemieszczania w usłudze App Service](web-sites-staged-publishing.md).

## <a name="how-do-i-access-and-review-webjob-logs"></a>Jak uzyskać dostęp i przejrzyj dzienniki zadania WebJob?

Dzienniki zadania WebJob tooreview:

1. Zaloguj się tooyour [Kudu witryny sieci Web](https://*yourwebsitename*.scm.azurewebsites.net).
2. Wybierz hello zadania WebJob.
3. Wybierz hello **dane wyjściowe Przełącz** przycisku.
4. Plik wyjściowy hello toodownload, wybierz opcję hello **Pobierz** łącza.
5. Dla poszczególnych przebiegów wybierz **wywołania poszczególnych**.
6. Wybierz hello **dane wyjściowe Przełącz** przycisku.
7. Wybierz hello łącze.

## <a name="im-trying-toouse-hybrid-connections-with-sql-server-why-do-i-see-hello-message-systemoverflowexception-arithmetic-operation-resulted-in-an-overflow"></a>Próbuję połączeń hybrydowych toouse z programem SQL Server. Dlaczego Zobacz wiadomości powitania "System.OverflowException: operacji arytmetycznej nastąpiło przepełnienie w czasie"?

Jeśli korzystasz z połączeń hybrydowych tooaccess programu SQL Server, aktualizacja programu Microsoft .NET, na 10 maja 2016 może spowodować toofail połączenia. Ten komunikat może zostać wyświetlony:

```
Exception: System.Data.Entity.Core.EntityException: hello underlying provider failed on Open. —> System.OverflowException: Arithmetic operation resulted in an overflow. or (64 bit Web app) System.OverflowException: Array dimensions exceeded supported range, at System.Data.SqlClient.TdsParser.ConsumePreLoginHandshake
```

### <a name="resolution"></a>Rozwiązanie

Pracujemy nad tooupdate toofix Menedżera połączeń hybrydowych ten problem. Aby obejść, zobacz [połączeń hybrydowych błąd z programem SQL Server: System.OverflowException: operacji arytmetycznej nastąpiło przepełnienie w czasie](https://blogs.msdn.microsoft.com/waws/2016/05/17/hybrid-connection-error-with-sql-server-system-overflowexception-arithmetic-operation-resulted-in-an-overflow/).

## <a name="how-do-i-add-or-edit-a-url-rewrite-rule"></a>Jak dodać lub edytować reguły ponownego zapisywania adresów URL?

tooadd lub edytowanie reguły ponownego zapisywania adresów URL:

1. Skonfiguruj Menedżera usług Internet Information Services (IIS), aby łączy tooyour aplikacji sieci web usługi aplikacji. toolearn tooconnect usługi tooApp Menedżera usług IIS, zobacz temat [zdalne administrowanie Azure witryn sieci Web za pomocą Menedżera usług IIS](https://azure.microsoft.com/blog/remote-administration-of-windows-azure-websites-using-iis-manager/).
2. W Menedżerze usług IIS, dodawanie lub edytowanie reguły ponownego zapisywania adresów URL. toolearn jak tooadd lub ponowne zapisywanie adresów URL edycji reguły, zobacz [Utwórz reguły ponownego zapisywania dla adresu URL hello przepisywania moduł](https://www.iis.net/learn/extensions/url-rewrite-module/creating-rewrite-rules-for-the-url-rewrite-module).

## <a name="how-do-i-control-inbound-traffic-tooapp-service"></a>Jak kontrolować ruch przychodzący tooApp usługi?

Na poziomie witryny hello masz dwie opcje umożliwiające sterowanie tooApp ruch przychodzący usługi:

* Włącz ograniczenia dynamicznego adresu IP. toolearn tooturn na dynamiczne ograniczenia adresów IP, zobacz temat [ograniczenia adresów IP i domen dla witryn sieci Web Azure](https://azure.microsoft.com/blog/ip-and-domain-restrictions-for-windows-azure-web-sites/).
* Włącz moduł zabezpieczeń. toolearn tooturn na modułu zabezpieczeń, zobacz temat [ModSecurity zapory aplikacji sieci web w witrynach sieci Web Azure](https://azure.microsoft.com/blog/modsecurity-for-azure-websites/).

Jeśli używasz środowiska usługi aplikacji, możesz użyć [zapory Barracuda](https://azure.microsoft.com/blog/configuring-barracuda-web-application-firewall-for-azure-app-service-environment/).

## <a name="how-do-i-block-ports-in-an-app-service-web-app"></a>Jak zablokować portów w aplikacji sieci web usługi aplikacji?

W hello usługi aplikacji udostępnionych środowiska dzierżawy, nie jest możliwe tooblock określonych portów z powodu hello rodzaj hello infrastruktury. Również porty TCP 4016, 4018 i 4020 może być otwarty dla zdalnego debugowania programu Visual Studio.

W środowisku usługi aplikacji należy mieć pełną kontrolę nad ruchu przychodzącego i wychodzącego. Możesz użyć grup zabezpieczeń sieci toorestrict lub blok określone porty. Aby uzyskać więcej informacji dotyczących środowiska usługi aplikacji, zobacz [wprowadzenie do środowiska usługi aplikacji](https://azure.microsoft.com/blog/introducing-app-service-environment/).

## <a name="how-do-i-capture-an-f12-trace"></a>Jak przechwycić śledzenia F12?

Masz dwie opcje do przechwytywania śledzenia F12:

* F12 HTTP śledzenia
* Dane wyjściowe konsoli F12

### <a name="f12-http-trace"></a>F12 HTTP śledzenia

1. W programie Internet Explorer przejdź tooyour witryny sieci Web. Jest ważne toosign przed hello następnych kroków. W przeciwnym razie hello śledzenia F12 przechwytuje poufne dane logowania.
2. Naciśnij klawisz F12.
3. Sprawdź, że hello **sieci** karta jest zaznaczone, a następnie wybierz hello zielony **odtwarzanie** przycisku.
4. Witaj kroki, które odtworzyć problem hello.
5. Wybierz hello red **zatrzymać** przycisku.
6. Wybierz hello **zapisać** przycisk (ikona dysku) i Zapisz plik HAR hello (w programie Internet Explorer i krawędzi) *lub* kliknij prawym przyciskiem myszy plik HAR hello, a następnie wybierz **Zapisz jako HAR z zawartością** () w przeglądarce Chrome).

### <a name="f12-console-output"></a>Dane wyjściowe konsoli F12

1. Wybierz hello **konsoli** kartę.
2. Dla każdej karty, która zawiera kilka elementów, wybierz kartę hello (**błąd**, **ostrzeżenie**, lub **informacji**). Jeśli karta hello nie jest zaznaczone, ikona kartę hello jest czarnego lub szarego po przeniesieniu kursora powitania od tego.
3. Kliknij prawym przyciskiem myszy w obszarze wiadomość hello hello okienka, a następnie wybierz **skopiuj wszystkie**.
4. Witaj Wklej skopiowany tekst w pliku, a następnie zapisz plik hello.

tooview pliku HAR, można użyć hello [HAR podglądu](http://www.softwareishard.com/har/viewer/).

## <a name="why-do-i-get-an-error-when-i-try-tooconnect-an-app-service-web-app-tooa-virtual-network-that-is-connected-tooexpressroute"></a>Dlaczego jest zgłaszany błąd przy próbie tooconnect usługę aplikacji sieci web aplikacji tooa sieć wirtualna, która jest połączonych tooExpressRoute?

Jeśli spróbujesz tooconnect sieci web platformy Azure aplikacji tooa sieć wirtualna ma podłączony tooAzure ExpressRoute jej nie powiedzie się. Witaj zostanie wyświetlony następujący komunikat: "Brama nie jest brama sieci VPN."

Obecnie nie może mieć punkt lokacja sieci VPN połączeń tooa sieć wirtualna, która jest tooExpressRoute połączonych. Punkt do lokacji sieci VPN i ExpressRoute nie mogą współistnieć na powitania sam sieci wirtualnej. Aby uzyskać więcej informacji, zobacz [ExpressRoute i sieci VPN typu lokacja lokacja połączeń limity i ograniczenia](../expressroute/expressroute-howto-coexist-classic.md#limits-and-limitations).

## <a name="how-do-i-connect-an-app-service-web-app-tooa-virtual-network-that-has-a-static-routing-policy-based-gateway"></a>Jak połączyć z usługi aplikacji sieci web aplikacji tooa sieć wirtualną mającą statycznego routingu bramy (oparte na zasadach)

Łączenie aplikacji usługi sieci web aplikacji tooa sieć wirtualną mającą statycznego routingu bramy (oparte na zasadach) nie jest obecnie obsługiwane. Jeśli sieci wirtualnej docelowy już istnieje, musi on mieć włączone z bramą routingu dynamicznego, aby można było tooan połączonych aplikacji VPN punkt lokacja. Jeśli brama ustawiono toostatic routingu, nie można włączyć sieć VPN punkt lokacja. 

Aby uzyskać więcej informacji, zobacz [integracji aplikacji z sieci wirtualnej platformy Azure](web-sites-integrate-with-vnet.md#getting-started).

## <a name="in-my-app-service-environment-why-can-i-create-only-one-app-service-plan-even-though-i-have-two-workers-available"></a>W moich środowiska usługi aplikacji, dlaczego można utworzyć tylko jeden plan usługi aplikacji, nawet jeśli użytkownik ma dwa procesy robocze, które są dostępne?

tooprovide odporność na uszkodzenia, środowiska usługi aplikacji wymaga, że każdego procesu roboczego puli wymaga co najmniej jeden zasób dodatkowe zasoby obliczeniowe. Hello dodatkowe zasoby obliczeniowe zasobu nie można przypisać obciążenia.

Aby uzyskać więcej informacji, zobacz [jak toocreate środowiska usługi aplikacji](app-service-web-how-to-create-an-app-service-environment.md).

## <a name="why-do-i-see-timeouts-when-i-try-toocreate-an-app-service-environment"></a>Dlaczego widzę przekroczeń limitu czasu podczas próby toocreate środowiska usługi aplikacji?

Czasami tworzenie środowiska usługi aplikacji nie powiedzie się. W takim przypadku zostanie wyświetlony następujący błąd w hello Dzienniki aktywności hello:
```
ResourceID: /subscriptions/{SubscriptionID}/resourceGroups/Default-Networking/providers/Microsoft.Web/hostingEnvironments/{ASEname}
Error:{"error":{"code":"ResourceDeploymentFailure","message":"hello resource provision operation did not complete within hello allowed timeout period.”}}
```

tooresolve, upewnij się, że żaden z hello następujące warunki są spełnione:
* podsieć Hello jest za mały.
* Witaj podsieci nie jest pusty.
* ExpressRoute zapobiega hello wymaganiami dotyczącymi łączności sieciowej środowiska usługi aplikacji.
* Nieprawidłowa grupa zabezpieczeń sieci uniemożliwia hello wymaganiami dotyczącymi łączności sieciowej środowiska usługi aplikacji.
* Wymuszanie tunelowania jest włączona.

Aby uzyskać więcej informacji, zobacz [częste problemy podczas wdrażania (Tworzenie) nowego środowiska usługi aplikacji Azure](https://blogs.msdn.microsoft.com/waws/2016/05/13/most-frequent-issues-when-deploying-creating-a-new-azure-app-service-environment-ase/).

## <a name="why-cant-i-delete-my-app-service-plan"></a>Dlaczego nie można usunąć planu usługi aplikacji?

Nie można usunąć planu usługi App Service, jeśli wszystkie aplikacje usługi aplikacji są skojarzone z hello planu usługi aplikacji. Przed usunięciem plan usługi aplikacji, Usuń wszystkie skojarzone aplikacje usługi aplikacji z hello planu usługi aplikacji.

## <a name="how-do-i-schedule-a-webjob"></a>Jak zaplanować zadanie WebJob?

Zaplanowane zadania WebJob można utworzyć za pomocą usługi Cron wyrażeń:

1. Utwórz plik settings.job.
2. W tym pliku JSON obejmują właściwości harmonogramu przy użyciu wyrażenia Cron: 
    ```
    { "schedule": "{second}
    {minute} {hour} {day}
    {month} {day of hello week}" }
    ```

Aby uzyskać więcej informacji na temat zaplanowane zadania Webjob, zobacz [utworzyć zaplanowane zadanie WebJob przy użyciu wyrażenia Cron](web-sites-create-web-jobs.md#CreateScheduledCRON).

## <a name="how-do-i-perform-penetration-testing-for-my-app-service-app"></a>Jak wykonać penetracji testowania dla mojej aplikacji usługi app Service?

Testowanie penetracji tooperform [Prześlij żądanie](https://security-forms.azure.com/penetration-testing/terms).

## <a name="how-do-i-configure-a-custom-domain-name-for-an-app-service-web-app-that-uses-traffic-manager"></a>Jak skonfigurować niestandardową nazwę domeny dla aplikacji sieci web usługi aplikacji, który używa Menedżera ruchu?

toolearn toouse niestandardowej nazwy domeny w aplikacji usługi App Service, która używa usługi Azure Traffic Manager w programie Równoważenie obciążenia, zobacz temat [Konfigurowanie niestandardowej nazwy domeny dla aplikacji sieci web platformy Azure z usługą Traffic Manager](web-sites-traffic-manager-custom-domain-name.md).

## <a name="my-app-service-certificate-is-flagged-for-fraud-how-do-i-resolve-this"></a>Certyfikatu usługi aplikacji jest oznaczona flagą oszustw. Jak rozwiązać ten problem?

Podczas weryfikacji domeny hello zakupu certyfikatów usługi aplikacji można napotkać następujące wiadomość hello:

"Certyfikat ma została oznaczona flagą możliwym oszustwie. Żądanie hello jest obecnie w ramach przeglądu. Jeśli certyfikat hello nie można używać w ciągu 24 godzin, skontaktuj się z pomocą techniczną platformy Azure."

Jak wiadomość hello wskazuje, ten proces sprawdzania poprawności oszustwa może potrwać too24 toocomplete godzin. W tym czasie nastąpi przejście wiadomość hello toosee.

Jeśli certyfikat usługi aplikacji nadal tooshow ten komunikat po 24 godzinach, uruchom hello następującego skryptu programu PowerShell. Witaj Witaj kontaktów skryptu [dostawcę certyfikatów](https://www.godaddy.com/) bezpośrednio tooresolve hello problem.

```
Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId <subId>
$actionProperties = @{
    "Name"= "<Customer Email Address>"
    };
Invoke-AzureRmResourceAction -ResourceGroupName "<App Service Certificate Resource Group Name>" -ResourceType Microsoft.CertificateRegistration/certificateOrders -ResourceName "<App Service Certificate Resource Name>" -Action resendRequestEmails -Parameters $actionProperties -ApiVersion 2015-08-01 -Force   
```

## <a name="how-do-authentication-and-authorization-work-in-app-service"></a>Jak uwierzytelnianie i autoryzacja działają w usłudze App Service?

Szczegółowa dokumentacja uwierzytelniania i autoryzacji w usłudze App Service, zobacz [zabezpieczeń usługi aplikacji](../app-service/app-service-security-readme.md). dokumentacji Hello zawiera także informacje o konfigurowaniu usługi aplikacji toouse różnych zidentyfikować dostawcy logowania:
* [Azure Active Directory](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)
* [Facebook](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md)
* [Google](../app-service-mobile/app-service-mobile-how-to-configure-google-authentication.md)
* [Konto Microsoft](../app-service-mobile/app-service-mobile-how-to-configure-microsoft-authentication.md)
* [Twitter](../app-service-mobile/app-service-mobile-how-to-configure-twitter-authentication.md)

## <a name="how-do-i-redirect-hello-default-azurewebsitesnet-domain-toomy-azure-web-apps-custom-domain"></a>Jak przekierować domyślne hello *. azurewebsites.net domeny toomy aplikacji sieci web Azure dla domeny niestandardowej?

Podczas tworzenia nowej witryny sieci Web za pomocą aplikacji sieci Web na platformie Azure, domyślny *sitename*. azurewebsites.net domeny są przypisane tooyour witryny. Jeśli Dodawanie witryny tooyour nazwy hosta niestandardowego i stanie tooaccess toobe użytkownicy nie mają domyślnej *. azurewebsites.net domeny, można przekierowywać hello domyślny adres URL. toolearn tooredirect wszystkie ruchu z witryny sieci Web domyślnej domeny tooyour domeny niestandardowej, zobacz [hello domyślnej domeny tooyour niestandardowej domeny przekierowania w aplikacji sieci web platformy Azure](http://www.zainrizvi.io/2016/04/07/block-default-azure-websites-domain/).

## <a name="how-do-i-determine-which-version-of-net-version-is-installed-in-app-service"></a>Jak ustalić, która wersja programu .NET jest zainstalowana wersja w usłudze App Service?

Witaj najszybszy sposób toofind hello wersję platformy Microsoft .NET zainstalowanym w usłudze App Service jest za pomocą konsoli Kudu hello. Z hello portalu lub przy użyciu adresu URL hello aplikację usługi aplikacji można uzyskać dostępu do hello Kudu konsoli. Aby uzyskać szczegółowe instrukcje, zobacz [określić hello zainstalowana wersja platformy .NET w usłudze App Service](https://blogs.msdn.microsoft.com/waws/2016/11/02/how-to-determine-the-installed-net-version-in-azure-app-services/).

## <a name="why-isnt-autoscale-working-as-expected"></a>Dlaczego skalowania automatycznego nie działa zgodnie z oczekiwaniami?

Jeśli Azure skalowania automatycznego nie skalować w lub skalowana w poziomie wystąpienie aplikacji sieci web hello zgodnie z oczekiwaniami, użytkownik może być uruchomiona w scenariuszu, w którym firma Microsoft celowo wybrać nie tooscale tooavoid nieskończoną pętlę powodu zbyt "niestabilny." Zazwyczaj dzieje się tak, gdy nie ma odpowiedni poziom między hello progi skalowalnego w poziomie i w skali. jak tooavoid "niestabilny" i tooread dotyczące innych najlepszych rozwiązań skalowania automatycznego, zobacz toolearn [najlepsze rozwiązania w zakresie skalowania automatycznego](../monitoring-and-diagnostics/insights-autoscale-best-practices.md#autoscale-best-practices).

## <a name="why-does-autoscale-sometimes-scale-only-partially"></a>Dlaczego skalowania automatycznego czasami skalowany tylko częściowo?

Skalowania automatycznego jest wyzwalane, gdy metryki przekroczą wstępnie skonfigurowanych granicach. Czasami można zauważyć, że pojemność hello jest tylko częściowo wypełnione porównaniu toowhat, które miały. Taka sytuacja może wystąpić, gdy hello liczba wystąpień, które mają nie są dostępne. W tym scenariuszu skalowania automatycznego częściowo wypełnia się przy użyciu hello dostępna liczba wystąpień. Skalowania automatycznego jest następnie uruchamia hello Zrównoważ logiki tooget większej pojemności. Przydzielania hello pozostałych wystąpień. Należy pamiętać, że może to potrwać kilka minut.

Jeśli nie widzisz hello oczekiwana liczba wystąpień po upływie kilku minut, może to być ponieważ uzupełnienia częściowe hello jest za mało metryki hello toobring w granicach hello. Lub skalowania automatycznego może mieć skalowany w dół, ponieważ osiągnął hello dolna granica metryki.

Jeśli żaden z tych warunków, a hello problem będzie się powtarzał, należy przesłać żądanie pomocy technicznej.

## <a name="how-do-i-turn-on-http-compression-for-my-content"></a>Jak włączyć kompresję HTTP zawartości Moje?

tooturn na kompresji zarówno statycznych i dynamicznych typów zawartości, należy dodać hello następującego pliku web.config na poziomie aplikacji toohello kodu:

```
<system.webServer>
<urlCompression doStaticCompression="true" doDynamicCompression="true" />
< /system.webServer>
```

Można również określić hello określonych dynamiczne i typy MIME statycznych, które mają toocompress. Aby uzyskać więcej informacji, zobacz nasze odpowiedzi tooa forum pytanie [httpCompression ustawień na prosty witryny sieci Web Azure](https://social.msdn.microsoft.com/Forums/azure/890b6d25-f7dd-4272-8970-da7798bcf25d/httpcompression-settings-on-a-simple-azure-website?forum=windowsazurewebsitespreview).

## <a name="how-do-i-migrate-from-an-on-premises-environment-tooapp-service"></a>Jak przeprowadzić migrację z lokalnymi tooApp środowiska usługi?

toomigrate witryny z systemami Windows i Linux tooApp serwerów sieci web usługi, możesz użyć Asystenta migracji usługi aplikacji Azure. Narzędzie migracji Hello tworzy aplikacje sieci web i baz danych na platformie Azure, zgodnie z potrzebami i publikuje następnie hello zawartości. Aby uzyskać więcej informacji, zobacz [Asystenta migracji usługi aplikacji Azure](https://www.movemetothecloud.net/).
