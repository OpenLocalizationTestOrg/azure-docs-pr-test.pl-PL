---
title: aaaAdd funkcji tooyour pierwszej aplikacji sieci web | Dokumentacja firmy Microsoft
description: "Dodaj ciekawe funkcje tooyour pierwszej aplikacji sieci web w ciągu kilku minut."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 542671c2-22f0-4f20-8b4b-fa477264c492
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2016
ms.author: cephalin
ms.openlocfilehash: 46c9b118c2c188508cb0a369c691a79073b7d7b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-functionality-tooyour-first-web-app"></a>Dodawanie funkcji tooyour pierwszej aplikacji sieci web
W [wdrażanie Twojego pierwszego tooAzure aplikacji sieci web w ciągu pięciu minut](app-service-web-get-started-dotnet.md), wdrożono przykładową aplikację sieci web do [usłudze Azure App Service](../app-service/app-service-value-prop-what-is.md). W tym artykule będzie szybko dodać niektóre ciekawe funkcje tooyour wdrożone sieci web aplikacji. W ciągu kilku minut:

* wymusisz uwierzytelnianie użytkowników,
* przeprowadzisz automatyczne skalowanie aplikacji,
* odbierzesz alerty dotyczące wydajności hello aplikacji.

Niezależnie od tego, która Przykładowa aplikacja została wdrożona w poprzednim artykule hello możesz kontynuować pracę w samouczku hello.

Witaj trzy czynności przedstawione w tym samouczek są tylko kilka przykładów hello wielu przydatnych funkcji, które użytkownik otrzymuje po przekazaniu aplikacji sieci web w usłudze App Service. Wiele funkcji hello są dostępne w hello **wolne** warstwy (czyli pierwszej aplikacji sieci web działa na), i korzystania z wersji próbnej środków tootry funkcje, które wymagają wyższych warstw cenowych. Pewność, że aplikacja sieci web pozostanie w **wolne** warstwy, chyba że wyraźnie zmienisz tooa inną warstwa cenowa.

> [!NOTE]
> Aplikacja sieci web Hello zostały utworzone z wiersza polecenia platformy Azure jest uruchamiana w **wolne** warstwy, który zezwala tylko jednego wystąpienia udostępnionej maszyny Wirtualnej z przydziałami zasobów. Aby uzyskać więcej informacji o ofercie warstwy **Bezpłatna**, zobacz temat [App Service limits](../azure-subscription-service-limits.md#app-service-limits) (Limity usługi App Service).
> 
> 

## <a name="authenticate-your-users"></a>Uwierzytelnianie użytkowników
Teraz zobaczmy, jak łatwo jest tooadd uwierzytelniania tooyour aplikacji (dalsze informacje na [uwierzytelniania/autoryzacji dla aplikacji usługi](https://azure.microsoft.com/blog/announcing-app-service-authentication-authorization/)).

1. W hello bloku portalu aplikacji, który został właśnie otwarty, kliknij przycisk **ustawienia** > **uwierzytelniania / autoryzacji**.  
    ![Uwierzytelnianie — blok ustawień](./media/app-service-web-get-started/aad-login-settings.png)
2. Kliknij przycisk **na** tooturn na uwierzytelniania.  
3. W sekcji **Dostawcy uwierzytelniania** kliknij pozycję **Azure Active Directory**.  
    ![Uwierzytelnianie — wybieranie usługi Azure AD](./media/app-service-web-get-started/aad-login-config.png)
4. W hello **ustawień usługi Azure Active Directory** bloku, kliknij przycisk **Express**, następnie kliknij przycisk **OK**. Witaj domyślne ustawienia spowodują utworzenie nowej aplikacji usługi Azure AD w katalogu domyślnym.  
    ![Uwierzytelnianie — konfiguracja ekspresowa](./media/app-service-web-get-started/aad-login-express.png)
5. Kliknij pozycję **Zapisz**.  
    ![Uwierzytelnianie — zapisywanie konfiguracji](./media/app-service-web-get-started/aad-login-save.png)
   
    Po pomyślnym zmiany hello zobaczysz hello dzwonka powiadomień zielony oraz przyjazny komunikat.
6. W hello bloku portalu aplikacji kliknij hello **adres URL** link (lub **Przeglądaj** na pasku menu hello). Witaj link jest adresem HTTP.  
    ![Uwierzytelnianie — przejście tooURL](./media/app-service-web-get-started/aad-login-browse-click.png)  
    Jednak po otwarciu aplikacji hello na nowej karcie Tekst hello przekierowuje pole adresu URL i zakończeniu w aplikacji z adresem HTTPS. Co jest wyświetlane jest jest już zalogowany tooyour subskrypcji platformy Azure i automatycznie uwierzytelniony w aplikacji hello.  
    ![Uwierzytelnianie — zalogowany](./media/app-service-web-get-started/aad-login-browse-http-postclick.png)  
    Dlatego jeśli teraz otworzysz nieuwierzytelnioną sesję w innej przeglądarce, zobaczysz ekran logowania po przejściu toohello tego samego adresu URL.  
    <!-- ![Authenticate - login page](./media/app-service-web-get-started/aad-login-browse.png)  -->
    Jeśli nigdy nie wykonywano żadnych czynności w usłudze Azure Active Directory, katalog domyślny może nie zawierać żadnych użytkowników usługi Azure AD. W takim przypadku prawdopodobnie jedynym kontem hello w jest tekst hello konta Microsoft z subskrypcją platformy Azure. Który ma Dlaczego zostały automatycznie zalogowany toohello aplikacji w hello sam wcześniej przeglądarki.
    Na tej stronie logowania, można użyć tego samego toolog konta Microsoft w.

Gratulacje, są uwierzytelniani wszystkich aplikacji sieci web tooyour ruchu.

Można zauważyć w hello **uwierzytelniania / autoryzacji** bloku, które można wykonać wiele innych, takie jak:

* Włączyć logowanie za pomocą danych z serwisów społecznościowych
* Włączyć wiele opcji logowania
* Zmień hello domyślne zachowanie podczas pierwszego przechodzenia użytkowników tooyour aplikacji

Usługa App Service zawiera gotowe rozwiązanie dla niektórych typowych uwierzytelniania hello musi, więc nie trzeba logika uwierzytelniania hello tooprovide samodzielnie.
Aby uzyskać więcej informacji, zobacz [App Service Authentication/Authorization](https://azure.microsoft.com/blog/announcing-app-service-authentication-authorization/) (Uwierzytelnianie/autoryzacja usługi App Service).

## <a name="scale-your-app-automatically-based-on-demand"></a>Automatyczne skalowanie aplikacji na podstawie zapotrzebowania
Następnie Załóżmy skalowania automatycznego aplikację, aby automatycznie dostosowywała pojemności toorespond toouser żądanie (dalsze informacje na [skalować aplikację w usłudze Azure](web-sites-scale.md) i [skalowanie liczby wystąpień ręcznie lub automatycznie](../monitoring-and-diagnostics/insights-how-to-scale.md)).

Krótko mówiąc, skalowanie aplikacji sieci Web można przeprowadzić na dwa sposoby:

* [Skalowanie w górę](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): większa wydajność procesora CPU, więcej pamięci, miejsca na dysku i dodatkowych funkcji, np. dedykowane maszyny wirtualne, niestandardowe domeny i certyfikaty, miejsca przejściowe, skalowanie automatyczne i wiele innych. Skalowanie w górę, zmieniając hello cenowym planu usługi aplikacji, który należy aplikacja.
* [Skalowanie w poziomie](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): zwiększanie hello liczba wystąpień maszyn wirtualnych, które Uruchom aplikację.
  Możesz skalować w poziomie tooas wiele jako 50 wystąpień, w zależności od warstwy cenowej.

Nie przedłużając, skonfigurujmy skalowanie automatyczne.

1. Najpierw Przeprowadź skalowanie w górę tooenable Skalowanie automatyczne. W hello bloku portalu aplikacji kliknij **ustawienia** > **Skaluj w górę (Plan usługi App Service)**.  
    ![Skalowanie w górę — blok ustawień](./media/app-service-web-get-started/scale-up-settings.png)
2. Przewiń i wybierz hello **standardowe S1** warstwy, hello najniższej warstwy, która obsługuje funkcję skalowania automatycznego (zaznaczona kółkiem na zrzucie ekranu), a następnie kliknij przycisk **wybierz**.  
    ![Skalowanie w górę — wybieranie warstwy](./media/app-service-web-get-started/scale-up-select.png)
   
    To już koniec skalowania w górę.
   
   > [!IMPORTANT]
   > Ta warstwa rozszerza środki do wykorzystania w bezpłatnej wersji próbnej. Jeśli masz płatności na koncie wiąże konta tooyour opłat.
   > 
   > 
3. Teraz skonfigurujmy funkcję skalowania automatycznego. W hello bloku portalu aplikacji kliknij **ustawienia** > **Skaluj w poziomie (Plan usługi App Service)**.  
    ![Skalowanie w poziomie — blok ustawień](./media/app-service-web-get-started/scale-out-settings.png)
4. Zmień **skalowanie przez** za**procent użycia procesora CPU**. odpowiednio zaktualizować Hello suwaków pod hello listy rozwijanej. Następnie zdefiniuj zakres wartości pól **Wystąpienia** (od **1** do **2**) oraz **Zakres docelowy** (od **40** do **80**). To zrobić, wpisując w polach hello lub Przesuń suwaki hello.  
    ![Skalowanie w poziomie —konfigurowanie skalowania automatycznego](./media/app-service-web-get-started/scale-out-configure.png)
   
    Na podstawie tej konfiguracji aplikacja automatycznie jest skalowana w poziomie, gdy użycie procesora CPU przekracza 80% i gdy spada poniżej 40%.
5. Kliknij przycisk **zapisać** na pasku menu hello.

Gratulacje. Twoja aplikacja jest automatycznie.

Można zauważyć w hello **ustawienia skali** bloku, które można wykonać wiele innych, takie jak:

* Skalować ręcznie tooa określonej liczby wystąpień
* Skalować według innych metryk wydajności (np. procentowego zużycia pamięci lub przydziału dysku)
* Dostosowywać zachowanie skalowania w przypadku wyzwolenia reguły dotyczącej wydajności
* Skalować automatycznie zgodnie z harmonogramem
* Określać zachowanie funkcji skalowania automatycznego wobec przyszłych zdarzeń

Aby uzyskać więcej informacji na temat skalowania aplikacji w górę, zobacz temat [Scale up your app in Azure](web-sites-scale.md) (Skalowanie aplikacji w górę na platformie Azure). Aby uzyskać więcej informacji na temat skalowania w poziomie, zobacz [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md) (Ręczne lub automatyczne skalowanie liczby wystąpień).

## <a name="receive-alerts-for-your-app"></a>Otrzymywanie alertów dotyczących aplikacji
Teraz, Twoja aplikacja jest automatycznie, co się dzieje, gdy osiągnie hello maksymalnej liczby wystąpień (2), a użycie procesora CPU przekroczy żądany poziom (80%)?
Możesz skonfigurować alert (dalsze informacje na [otrzymywać powiadomienia o alertach](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)) tooinform tę sytuację, więc możesz skalowanie w górę/w poziomie aplikacji, np. Teraz szybko skonfigurujemy alert dla tego scenariusza.

1. W hello bloku portalu aplikacji kliknij **narzędzia** > **alerty**.  
    ![Alerty — blok ustawień](./media/app-service-web-get-started/alert-settings.png)
2. Kliknij przycisk **Dodaj alert**. Następnie w hello **zasobów** polu hello wybierz zasób, który kończy się wyrazem **(serverfarms)**. Jest to Twój plan usługi App Service.  
    ![Alerty — dodawanie alertu dla planu usługi App Service](./media/app-service-web-get-started/alert-add.png)
3. Ustaw pozycję **Nazwa** na `CPU Maxed`, **Metryka** na **Procent użycia procesora CPU** oraz **Próg** na `90`, a następnie wybierz pozycję **Właściciele, współautorzy i czytelnicy poczty e-mail** i kliknij przycisk **OK**.   
    ![Alerty — konfigurowanie alertu](./media/app-service-web-get-started/alert-configure.png)
   
    Gdy platforma Azure zakończy tworzenie alertu hello, zobaczysz go w hello **alerty** bloku.  
    ![Alerty — widok po zakończeniu](./media/app-service-web-get-started/alert-done.png)

Gratulacje. Teraz otrzymujesz alerty.

To ustawienie alertów sprawdza użycie procesora CPU co pięć minut. Jeśli ta wartość przekracza 90%, otrzymasz alert e-mail. Otrzymają go również wszystkie autoryzowane osoby. toosee, każdego, kto jest autoryzowany tooreceive hello alertów, przejdź kopii toohello bloku portalu aplikacji i kliknij przycisk hello **dostępu** przycisku.  
![Zobacz, kto otrzymuje alerty](./media/app-service-web-get-started/alert-rbac.png)

Powinny pojawić się który **Administratorzy subskrypcji** są już hello **właściciela** aplikacji hello. Jeśli jesteś administratorem konta subskrypcji platformy Azure (np. subskrypcji wersji próbnej) hello będzie zawierać tej grupy. Aby uzyskać więcej informacji dotyczących kontroli dostępu opartej na rolach platformy Azure, zobacz temat [Azure Role-Based Access Control](../active-directory/role-based-access-control-configure.md) (Kontrola dostępu do platformy Azure oparta na rolach).

> [!NOTE]
> Reguły alertów to nowa funkcja platformy Azure. Aby uzyskać więcej informacji, zobacz [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) (Otrzymywanie powiadomień o alertach).
> 
> 

## <a name="next-steps"></a>Następne kroki
Na powitania tooconfigure Twojego sposób alertów, można zauważyć bogaty zestaw narzędzi w hello **narzędzia** bloku. W tym miejscu można rozwiązywać problemy, monitorować wydajność testowania luk w zabezpieczeniach, zarządzać zasobami interakcję z konsolą maszyny Wirtualnej hello i dodawać przydatne rozszerzenia. Zapraszamy tooclick o każdym z tych narzędzi toodiscover hello proste, ale narzędzi na wyciągnięcie ręki.

Dowiedz się, jak toodo więcej z wdrożoną aplikacją. Oto lista wybranych funkcji:

* [Kupowanie i konfigurowanie niestandardowej nazwy domeny](custom-dns-web-site-buydomains-web-app.md) — kup atrakcyjną domenę dla aplikacji sieci Web i użyj jej zamiast domeny *.azurewebsites.net. Lub użyj domeny, która już istnieje.
* [Konfigurowanie środowisk przejściowych](web-sites-staged-publishing.md) — wdrażanie Twojego tooa aplikacji przemieszczania adres URL przed wprowadzeniem jej do środowiska produkcyjnego. Aktualizuj aplikację sieci Web bez obaw. Skonfiguruj złożone rozwiązanie związane z metodyką DevOps z wieloma miejscami wdrożenia.
* [Konfigurowanie wdrażania ciągłego](app-service-continuous-deployment.md) — zintegruj wdrażanie aplikacji z systemem kontroli źródła. Wdrażaj na platformie Azure z każdym zatwierdzeniem.
* [Dostęp do zasobów lokalnych](web-sites-hybrid-connection-get-started.md) — uzyskaj dostęp do istniejącej, lokalnej bazy danych lub systemu CRM.
* [Tworzenie kopii zapasowej aplikacji](web-sites-backup.md) — skonfiguruj tworzenie i przywracanie kopii zapasowych dla aplikacji sieci Web. Przygotuj się na nieoczekiwane awarie i odzyskaj po nich swoje dane.
* [Włączanie dzienników diagnostycznych](web-sites-enable-diagnostic-log.md) — rejestruje hello odczytu usług IIS z platformy Azure lub funkcji śledzenia aplikacji. Odczytaj dzienniki strumieniowo, pobierz je lub przekaż je do usługi [Application Insights](../application-insights/app-insights-overview.md), aby otrzymać kompleksową analizę.
* [Skanowanie aplikacji pod kątem luk w zabezpieczeniach](https://azure.microsoft.com/blog/web-vulnerability-scanning-for-azure-app-service-powered-by-tinfoil-security/) -
  Skanuj aplikację sieci web pod kątem współczesnych zagrożeń przy użyciu usługi zapewnianej przez [usługę Tinfoil Security](https://www.tinfoilsecurity.com/).
* [Uruchamianie zadań w tle](../azure-functions/functions-overview.md) — uruchamiaj zadania związane z przetwarzaniem danych, raportowaniem itp.
* [Dowiedz się, jak działa usługa App Service](../app-service/app-service-how-works-readme.md)

