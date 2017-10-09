---
title: "aaaAzure RemoteApp — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Informacje o odpowiedzi toohello najczęściej zadawane pytania dotyczące usługi Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: swadhwa
editor: 
ms.assetid: bad66603-91f9-437f-8a70-236405d2a27f
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: da981fea9e38b4e74694aeaba5f97c8ed897ccd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-remoteapp-faq"></a>Często zadawane pytania dotyczące usługi Azure RemoteApp
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.
> 
> 

Otrzymujemy następujące pytania dotyczące usługi Azure RemoteApp hello. Masz więcej pytań? Odwiedź hello [fora usługi RemoteApp](https://social.msdn.microsoft.com/Forums/azure/home?forum=AzureRemoteApp) i Daj nam znać, co należy tooknow, lub Dodaj komentarz poniżej.

## <a name="cant-find-what-youre-looking-for-have-a-question-we-didnt-answer"></a>Nie możesz znaleźć, czego szukasz? Masz pytanie, na które nie odpowiedzieliśmy?
Jeśli nie możesz znaleźć informacje hello należy lub mają dodatkowe pytania, na które firma Microsoft nie jest tutaj obejmujące, przejdź toohello [forum usługi Azure RemoteApp](http://aka.ms/araforum) i Zadaj pytanie. Zawsze możemy dodać więcej odpowiedzi tutaj.

## <a name="what-is-azure-remoteapp"></a>Co to jest usługa Azure RemoteApp?
* **Co to jest usługa Azure RemoteApp?** Usługi RemoteApp jest usługą platformy Azure pomaga zapewnić bezpieczny zdalny dostęp tooapplications z wielu różnych urządzeń użytkowników. Dowiedz się więcej na temat usługi [Azure RemoteApp](remoteapp-whatis.md).
* **Jakie są opcje wdrażania hello?** Istnieją dwa rodzaje kolekcji usługi RemoteApp: w chmurze i hybrydowa. Wybór odpowiedniej opcji zależy od wielu czynników, takich jak potrzeba przyłączania do domeny. Wszystkie te aspekty zostały omówione [w tym miejscu](remoteapp-collections.md).

## <a name="quick-tips-on-using-azure-remoteapp"></a>Szybkie porady dotyczące korzystania z usługi Azure RemoteApp
* **Kiedy nastąpi odłączenie? Jak długo można pozostawać w stanie bezczynności przed przekazaniem mnie hello rozruchu?** 4 godziny. W przypadku pozostawania w stanie bezczynności przez Ciebie lub jednego z Twoich użytkowników przez 4 godziny nastąpi automatyczne wylogowanie z usługi Azure RemoteApp. Wyewidencjonowanie hello innymi ustawieniami domyślnymi w [subskrypcji platformy Azure i ograniczenia usługi, przydziały i ograniczenia](../azure-subscription-service-limits.md).
* **Czy można wypróbować tę usługę bezpłatnie?** Tak. Jest dostępna bezpłatna wersja próbna ważna przez 30 dni. Po zakończeniu hello wersji próbnej, może przejść tooa konto (możesz użyć w środowisku produkcyjnym) lub przy użyciu usługi hello stop. Uruchom bezpłatną wersję próbną, przechodząc zbyt[portal.azure.com](http://portal.azure.com) — Utwórz nowe wystąpienie usługi RemoteApp. Z bezpłatnej wersji próbnej hello można utworzyć 2 wystąpienia usługi RemoteApp z 10 użytkownikami dla każdego wystąpienia. Należy pamiętać, że ta wersja próbna działa tylko przez 30 dni.
  
  ## <a name="azure-remoteapp-subscription-details"></a>Szczegółowe informacje o subskrypcji usługi Azure RemoteApp
* **Jakie są ograniczenia usługi hello?** Możesz więcej informacji na temat ustawień domyślnych hello i usługi limity usługi Azure RemoteApp w [subskrypcji platformy Azure i ograniczenia usługi, przydziały i ograniczenia](../azure-subscription-service-limits.md). Poinformuj nas, jeśli masz więcej pytań.
* **Ilu użytkowników czy mam toohave?** Minimalna liczba użytkowników wynosi 20. Powtórzmy tego toobe pełnej jasności — Witaj minimalna wynosi 20. Opłaty będą naliczane za 20 użytkowników. 
* **Jaki jest koszt usługi RemoteApp?** Zapoznaj się z tematem [Szczegółowe informacje o cenach usługi Azure RemoteApp](https://azure.microsoft.com/pricing/details/remoteapp/).
* **Czy kolekcje różnych typów różnią się ceną?** Tak, w zależności od wymagań kolekcji. Kolekcja hybrydowa wymaga połączenia z siecią lokalną tooyour usługi Azure RemoteApp. Jeśli używana jest sieć wirtualna lub usługa Express Route, nie ma żadnych dodatkowych kosztów. Ale jeśli używasz nowej sieci Wirtualnej platformy Azure oraz bramy lub usługi Express Route zostanie naliczona dla hello [bramy sieci VPN](https://azure.microsoft.com/pricing/details/vpn-gateway) lub [Express Route](https://azure.microsoft.com/pricing/details/expressroute/). Ten koszt (szczegóły w łączach hello) jest na Twoje miesięczne usługi Azure RemoteApp kosztów.

## <a name="collections---whats-supported-which-should-you-use-and-others"></a>Kolekcje — co jest obsługiwane, czego należy używać i inne informacje
* **Czy są obsługiwane niestandardowe aplikacje LOB (biznesowe)?** Tak. Tworzenie niestandardowych aplikacji w usłudze Azure RemoteApp toouse [obrazu niestandardowego szablonu](remoteapp-create-custom-image.md), a następnie przekaż toohello kolekcji usługi RemoteApp.
* **Moje niestandardowych aplikacji biznesowych będzie działać w usłudze Azure RemoteApp?**  hello najlepsze toofigure sposób, który limit jest tootest go. Zapoznaj się z hello [Centrum zgodności pulpitu zdalnego](http://www.rdcompatibility.com/compatibility/default.aspx).
* **Która metoda wdrażania (w chmurze czy hybrydowa) jest najlepsza dla mojej organizacji?** Kolekcje hybrydowe zawierają najbardziej kompleksowe środowisko hello, jeśli chcesz pełnej integracji z logowaniem jednokrotnym (SSO) i bezpieczną lokalną połączeń sieciowych. Kolekcje w chmurze umożliwiają elastyczne i łatwe tooisolate wdrożenia przy użyciu wielu metod uwierzytelniania. Dowiedz się więcej o hello [opcje wdrażania](remoteapp-whatis.md).
* **Korzystamy z bazy danych SQL lub innej bazy danych lokalnie lub na platformie Azure. Jaki typ wdrożenia powinniśmy zastosować?** To zależy od lokalizacji bazy danych SQL lub bazy danych zaplecza. Jeśli hello baza danych znajduje się w sieciach prywatnych, należy użyć kolekcji hybrydowej hello. Jeśli baza danych hello jest narażonych toohello Internet i umożliwia klientowi tooit tooconnect połączenia, można użyć kolekcji w chmurze hello.
* **Jak wygląda sytuacja w przypadku mapowania dysku, portów USB i szeregowych, udostępniania schowka i przekierowywania drukarki?** Wszystkie te funkcje są obsługiwane przez usługę Azure RemoteApp. Udostępnianie schowka i przekierowywanie drukarki jest domyślnie włączone. Dowiedz się więcej o przekierowywaniu [tutaj](remoteapp-redirection.md). 

## <a name="template-images"></a>Obrazy szablonów
* **Czy można użyć chmury lub istniejącej maszyny wirtualnej jako hello szablonu mojej kolekcji usługi RemoteApp?** Tak! Można utworzyć obraz oparty na maszynie Wirtualnej platformy Azure, użyj jednego z obrazów hello uwzględnionych w subskrypcji lub utworzyć obraz niestandardowy. Zapoznaj się z hello [opcje obrazu usługi RemoteApp](remoteapp-imageoptions.md).

## <a name="network-options"></a>Opcje sieciowe
* **Witaj kolekcja hybrydowa wymaga sieci Wirtualnej. Czy można użyć istniejącej sieci wirtualnej?** Możesz Jeśli hello istniejącej sieci Wirtualnej jest sieć Wirtualną platformy Azure. Zobacz "krok 1: Konfigurowanie sieci wirtualnej" w hello [instrukcjach dotyczących kolekcji hybrydowej](remoteapp-create-hybrid-deployment.md) Aby uzyskać więcej informacji.
* **Czy w przypadku kolekcji w chmurze można użyć sieci wirtualnej?** Tak, można. Aby uzyskać więcej informacji, zobacz temat [Tworzenie kolekcji w chmurze](remoteapp-create-cloud-deployment.md), w szczególności krok 1.

## <a name="authentication-options"></a>Opcje uwierzytelniania
* **Jak rozwiązano kwestię uwierzytelniania? Które metody są obsługiwane?**  hello kolekcji w chmurze obsługuje konta Microsoft i konta usługi Azure Active Directory, które są również kontami usługi Office 365. Kolekcja hybrydowa Hello obsługuje tylko konta usługi Azure Active Directory, które zostały zsynchronizowane (przy użyciu narzędzia, takiego jak [synchronizacji Azure Active Directory](http://blogs.technet.com/b/ad/archive/2014/09/16/azure-active-directory-sync-is-now-ga.aspx)) od wdrożenia programu Windows Server Active Directory; ściślej mówiąc, albo zsynchronizowane z hello Opcja synchronizacji haseł lub zsynchronizowane ze skonfigurowaną Federacją usług federacyjnych Active Directory (AD FS). Można również skonfigurować uwierzytelnianie [Multi-Factor Authentication (MFA)](https://azure.microsoft.com/services/multi-factor-authentication/).

> [!NOTE]
> Hello użytkowników usługi Azure Active Directory muszą pochodzić z dzierżawy hello, który został skojarzony z subskrypcją. (Można wyświetlać i modyfikować subskrypcji na powitania **ustawienia** kartę w portalu hello. Zobacz [dzierżawy usługi Azure Active Directory hello zmiany używanej przez usługę RemoteApp](remoteapp-changetenant.md) Aby uzyskać więcej informacji.)
> 
> 

* **Dlaczego nie można przekazać mój dostępu do konta usługi Azure Active Directory?**  hello użytkowników usługi Azure Active Directory muszą pochodzić z katalogu hello, który został skojarzony z subskrypcją. Można wyświetlać lub modyfikować tego katalogu, w portalu hello hello na karcie Ustawienia. Zobacz [dzierżawy usługi Azure Active Directory hello zmiany używanej przez usługę RemoteApp](remoteapp-changetenant.md) Aby uzyskać więcej informacji.

## <a name="clients---what-device-can-i-use-tooaccess-azure-remoteapp"></a>Klienci — jakiego urządzenia można używać tooaccess usługi Azure RemoteApp?
Można znaleźć informacje o klientach, w tym kroki instalacji różnych klientów hello na [podczas uzyskiwania dostępu do aplikacji w usłudze Azure RemoteApp](remoteapp-clients.md).

* **Urządzenia i systemy operacyjne są obsługiwane aplikacje klienckie hello?**
  Pierwszy hello komputery i tablety: 
  
  * Windows 10 (wersja zapoznawcza klienta)
  * Windows 8.1 i Windows 8
  * Windows 7 z dodatkiem Service Pack 1
  * Mac OS X
  * Windows RT
  * Tablety z systemem Android
  * Tablety iPad

    I telefony hello:
  * iPhone
  * Android
  * Windows Phone
    
    [Pobierz](https://www.remoteapp.windowsazure.com/ClientDownload/AllClients.aspx) teraz klienta usługi RemoteApp.
* **Czy usługa Azure RemoteApp obsługuje zubożonych klientów?** Tak, hello następujących klientów zubożonych Windows Embedded są obsługiwane:
  
  * Windows Embedded Standard 7
  * Windows Embedded 8 Standard
  * Windows Embedded 8.1 Industry Pro
  * Windows 10 IoT Enterprise
* **Która wersja systemu Windows Server jest obsługiwana dla hello hosta sesji zdalnego pulpitu (RDSH)?** Windows Server 2012 R2.

## <a name="support-and-feedback"></a>Pomoc techniczna i opinie
* **Co to jest plan pomocy technicznej hello usługi RemoteApp?** Obsługa zarządzania rozliczeniami i subskrypcjami jest bezpłatna. Pomoc techniczna jest dostępna za pośrednictwem hello [planów usług platformy Azure](https://azure.microsoft.com/support/plans/). Można również uzyskać bezpłatne wsparcie społeczności za pośrednictwem [forum dyskusyjnego platformy Azure](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=AzureRemoteApp). 
* **Jak przesłać opinię?** Odwiedź hello [forum opinii](https://feedback.azure.com/forums/247748-azure-remoteapp/).
* **Który może komunikować toolearn więcej informacji na temat usługi Azure RemoteApp?** W dodatku tooour [forum dyskusyjne](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=AzureRemoteApp), która jest doskonałym miejscem toopost pytania, możesz także dołączyć do hello co tydzień [poprosić internetowych z udziałem ekspertów hello](https://azureinfo.microsoft.com/US-Azure-WBNR-FY15-11Nov-AzureRemoteAppAskTheExperts-Registration-Page.html), gdzie są omawiane wszystkie tematy związane z usługi RemoteApp.
* **Co z dokumentacją usługi RemoteApp?** Cieszymy się z tego pytania. Ponadto zawartość w szufladzie pomocy portalu hello pomocy toohello (wystarczy kliknąć hello **?** na każdej stronie w portalu hello) hello następujące artykuły są dostępne tooteach możesz wszystkie aspekty usługi RemoteApp:
  
  * **Wprowadzenie:**
    * [Co to jest RemoteApp?](remoteapp-whatis.md)
    * [Co to jest hello zawierają obrazy szablonów usługi RemoteApp?](remoteapp-images.md)
    * [Jak działa licencjonowanie?](remoteapp-licensing.md)
    * [Jak programy pakietu Office współpracują z usługą RemoteApp?](remoteapp-o365.md)
    * [Jak działa przekierowanie w usłudze RemoteApp](remoteapp-redirection.md)?
  * **Wdrażanie:**
    * [Tworzenie niestandardowego obrazu szablonu](remoteapp-create-custom-image.md)
    * [Tworzenie kolekcji hybrydowej](remoteapp-create-hybrid-deployment.md)
    * [Tworzenie kolekcji w chmurze](remoteapp-create-cloud-deployment.md)
    * [Konfigurowanie usługi Azure Active Directory dla usługi RemoteApp](remoteapp-ad.md)
    * [Publikowanie aplikacji w usłudze RemoteApp](remoteapp-publish.md)
  * **Zarządzanie:**
    
    * [Dodawanie użytkowników](remoteapp-user.md)
    * [Najlepsze rozwiązania dotyczące konfigurowania i używania usługi RemoteApp](remoteapp-bestpractices.md)    
    
    Filmy. Mamy także szereg filmów dotyczących usługi RemoteApp. Niektóre zapewniają wprowadzenie ([tooAzure wprowadzenie RemoteApp](https://azure.microsoft.com/documentation/videos/cloud-cover-ep-150-azure-remote-app-with-thomas-willingham-and-nihar-namjoshi/)), podczas gdy inne dotyczą wdrożenia ([wdrożenie w chmurze](https://www.youtube.com/watch?v=3NAv2iwZtGc&feature=youtu.be) i [wdrożenia hybrydowego](https://www.youtube.com/watch?v=GCIMxPUvg0c&feature=youtu.be)). Warto się z nimi zapoznać.

### <a name="help-us-help-you"></a>Pomóż nam sobie pomóc
Czy wiesz, że w toorating dodanie ten artykuł i dodać komentarze poniżej, możesz wprowadzić samym artykule toohello zmiany? Brakuje informacji? Coś jest nie tak? Treść artykułu jest niejasna? Przewiń w górę i kliknij przycisk **Edytuj w serwisie GitHub** zmiany toomake - te modyfikacje zostaną toous do przeglądu, a następnie, zatwierdzeniu na nich, zostanie wyświetlone Twoje zmiany i udoskonalenia tutaj.

