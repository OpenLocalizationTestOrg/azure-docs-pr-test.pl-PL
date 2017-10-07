---
title: "łączniki serwera Proxy aplikacji usługi Azure AD aaaUnderstand | Dokumentacja firmy Microsoft"
description: "Obejmuje hello podstaw łączniki serwera Proxy aplikacji usługi Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 294cb26803ef7cf8be9f3af0678d6d2e64f6cc14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-ad-application-proxy-connectors"></a>Zrozumienie łączniki serwera Proxy aplikacji usługi Azure AD

Łączniki są co umożliwiają serwera Proxy aplikacji usługi Azure AD. Są toodeploy proste, łatwe i obsługa i super zaawansowanych. W tym artykule omówiono łączniki, jakie są, jak działają i sugestie dotyczące toooptimize wdrożenia. 

## <a name="what-is-an-application-proxy-connector"></a>Co to jest łącznik serwera Proxy aplikacji

Łączniki są lekkie agentów, które znajdują się lokalnie i umożliwiać hello wychodzące połączenie toohello serwera Proxy aplikacji usługi. Łączniki, musi być zainstalowany w systemie Windows Server, który ma dostęp toohello zaplecza aplikacji. Łączniki można organizować w grupy łącznika, z każdą grupą obsługi ruchu toospecific aplikacji. Równoważenie obciążenia łączniki automatycznie i może ułatwić toooptimize strukturę sieci. 

## <a name="requirements-and-deployment"></a>Wymagania i wdrożenia

Serwer Proxy aplikacji toodeploy pomyślnie, należy co najmniej jeden łącznik, ale zaleca się co najmniej dwóch dla większej odporności. Zainstaluj łącznik hello na maszynie 2016 lub Windows Server 2012 R2. Łącznik Hello musi toobe toocommunicate stanie powitania serwera Proxy aplikacji usługi, jak również hello lokalnymi aplikacjami, które opublikować. 

Aby uzyskać więcej informacji na temat wymagań sieciowych hello hello łącznika serwera, zobacz [Rozpoczynanie pracy z serwera Proxy aplikacji i zainstalować łącznik](active-directory-application-proxy-enable.md).

## <a name="maintenance"></a>Konserwacji
Hello łączników i usługi hello automatyzującą wszystkie zadania wysokiej dostępności hello. Można można dodać lub usunąć dynamicznie. Zawsze, gdy nowe żądanie dociera jest routingiem tooone hello łączników, która jest obecnie dostępna. Łącznik jest tymczasowo niedostępny, nie reagować toothis ruchu.

łączniki Hello są bezstanowych i nie mają konfiguracji danych na komputerze hello. Witaj tylko te dane, które przechowują to hello ustawienia do łączenia usługi hello i jego certyfikat uwierzytelniania. Łączą usługi toohello ściągnięcia wszystkie dane konfiguracyjne hello wymagane i go odświeżyć co kilka minut.

Łączniki wykonać sondowanie powitania serwera toofind się, czy istnieje nowsza wersja hello łącznika. Jeśli został znaleziony, łączników hello aktualizacji samodzielnie.

Łączniki z maszyny hello, w którym jest uruchomiona, można monitorować przy użyciu hello dziennika zdarzeń i liczniki wydajności. Lub można wyświetlić ich stan ze strony serwera Proxy aplikacji hello hello portalu Azure:

 ![Łączniki serwera Proxy aplikacji AzureAD](./media/application-proxy-understand-connectors/app-proxy-connectors.png)

Nie masz toomanually Usuń łączniki, które nie są używane. Łącznik jest uruchomiona, pozostaje aktywne jako łączy toohello usługi. Nieużywane łączników są oznaczone jako _nieaktywne_ i zostaną usunięte po upływie 10 dni nieaktywności. Jeśli chcesz toouninstall łącznika, jednak odinstalować zarówno hello usługi łącznika i Updater hello z serwera hello. Uruchom ponownie komputer toofully Usuń hello usługi.

## <a name="automatic-updates"></a>Automatyczne aktualizacje

Usługa Azure AD zapewnia aktualizacje automatyczne dla wszystkich łączników hello, które można wdrożyć. Tak długo, jak działa hello aktualizator łącznika serwera Proxy aplikacji usługi, łączników są aktualizowane automatycznie. Jeśli nie widzisz hello aktualizator łącznika usługi na serwerze, należy za[ponowne instalowanie łącznika programu](active-directory-application-proxy-enable.md) tooget żadnych aktualizacji. 

Jeśli nie chcesz toowait dla łącznika usługi aktualizacji automatycznych toocome tooyour można wykonywać ręcznego uaktualnienia. Przejdź toohello [stronę pobierania łącznika](https://download.msappproxy.net/subscription/d3c8b69d-6bf7-42be-a529-3fe9c2e70c90/connector/download) na serwerze hello gdzie Twojego łącznika jest zlokalizowany i wybierz pozycję **Pobierz**. Ten proces dotyczącego uaktualnienie hello łącznika lokalnego. 

W przypadku dzierżaw z wiele łączników aktualizacje automatyczne hello docelowego jeden łącznik w czasie w każdym przestoju tooprevent grupy w środowisku. 

Przestój mogą wystąpić podczas aktualizacji z łącznika, jeśli:  
- Masz tylko jeden łącznik. tooavoid to czas przestoju i ulepszania wysoką dostępność, zaleca się instalowania drugi łącznik i [Utwórz grupę łącznika](active-directory-application-proxy-connectors-azure-portal.md).  
- Łącznik został w środku hello transakcji podczas aktualizacji hello rozpoczęcia. Chociaż hello początkowej transakcji nie zostały utracone, przeglądarka automatycznie ponów operację hello lub można odświeżyć stronę. Podczas żądania hello jest ponowne wysłanie, hello jest kierowany tooa łącznika kopii zapasowej.

## <a name="creating-connector-groups"></a>Tworzenie grup łącznika

Łącznik grup Włącz tooassign określonych łączniki tooserve określonych aplikacji. Można zgrupować wiele łączników, a następnie przypisz każdej grupy tooa aplikacji. 

Łącznik grup umożliwiają łatwiejsze toomanage dużych wdrożeniach. Poprawiają opóźnienia również w przypadku dzierżaw mających aplikacji obsługiwanych w różnych regionach, ponieważ możesz tworzyć grupy na podstawie lokalizacji łącznika tooserve tylko lokalne aplikacje. 

toolearn więcej informacji na temat grup łącznika, zobacz [publikowania aplikacji w odrębnych sieci i lokalizacje przy użyciu łącznika grup](active-directory-application-proxy-connectors-azure-portal.md).

## <a name="security-and-networking"></a>Zabezpieczenia i sieci

Łączniki można zainstalować w dowolnym hello sieci, która umożliwia im toosend żądań toohello serwera Proxy aplikacji usługi. Co to jest ważne jest komputerze hello także uruchomiona hello łącznika ma dostęp tooyour aplikacji. Wewnątrz sieci firmowej lub z maszyny wirtualnej, która działa w chmurze hello można zainstalować łączniki. Łączniki mogą być uruchamiane w strefą zdemilitaryzowaną (DMZ), ale nie jest konieczne, ponieważ cały ruch jest wychodzący, dlatego sieci pozostają bezpieczne.

Łączniki tylko wysyłać żądania wychodzącego. ruch wychodzący Hello jest wysyłane toohello serwera Proxy aplikacji usługi i toohello opublikowane aplikacje. Nie masz tooopen porty wejściowe, ponieważ w obu kierunkach przepływa ruch po ustanowieniu sesji. Nie masz tooset się zrównoważenia obciążenia między łączniki hello lub skonfigurować dostęp przychodzących na zaporach. 

Aby uzyskać więcej informacji o konfigurowaniu wychodzących reguł zapory, zobacz [pracy przy użyciu istniejących lokalnych serwerów proxy](application-proxy-working-with-proxy-servers.md).

Użyj hello [Azure AD aplikacji serwera Proxy łącznika porty testu narzędzie](https://aadap-portcheck.connectorporttest.msappproxy.net/) tooverify, że Twoje łącznika może nawiązać połączenie powitania serwera Proxy aplikacji usługi. Co najmniej upewnij się, że hello środkowe stany USA regionu i tooyou najbliższy region hello jest wszystkich zaznaczeń zielony. Ponadto więcej zaznaczeń zielony oznacza większą elastyczność. 

## <a name="performance-and-scalability"></a>Wydajność i skalowalność

Skali powitania serwera Proxy aplikacji usługi jest niewidoczny, ale skala jest współczynnik dla łączników. Należy toohave wystarczającej ilości ruchu szczytu toohandle łączników. Jednak nie trzeba tooconfigure równoważenia obciążenia, ponieważ wszystkie łączniki w obrębie grupy łącznika automatycznie równoważyć obciążenie.

Ponieważ łączniki są bezstanowych, są one nie dotyczy hello liczby użytkowników lub sesji. Zamiast tego one odpowiadać toohello liczbę żądań i ich rozmiar ładunku. W przypadku ruchu standardowe sieci web średni maszyny może obsługiwać kilka tysięcy żądań na sekundę. określonej pojemności Hello zależy od hello dokładne maszyny właściwości. 

wydajność łącznika Hello jest związana z procesora CPU i sieci. Wydajność Procesora jest wymagany dla protokołu SSL szyfrowania i odszyfrowywania, gdy sieci jest ważne tooget szybkiego łączności toohello aplikacji i hello usługi online na platformie Azure.

Natomiast w pamięci jest mniejsza problemu dla łączników. usługi online Hello odpowiada on za dużo hello przetwarzania, a także cały ruch nieuwierzytelnione. Wszystko, co można zrobić w chmurze hello odbywa się w chmurze hello. 

Innym czynnikiem wpływającym na wydajność jest jakość hello hello sieci między łącznikami hello, w tym: 

* **Witaj usługi online**: toohello wolne lub dużymi opóźnieniami połączenia serwera Proxy aplikacji usługi Azure wpływ hello łącznika wydajności. Aby uzyskać najlepszą wydajność hello Uzyskuj dostęp do Twojej organizacji tooAzure Express Route. W przeciwnym razie ma zespołem sieci, upewnij się, że tooAzure połączeń są obsługiwane w najbardziej efektywny sposób. 
* **Witaj zaplecza aplikacji**: W niektórych przypadkach są dodatkowe serwery proxy między hello łącznika i hello wewnętrznej bazy danych aplikacji, które mogą spowalniać lub uniemożliwiać połączenia. tootroubleshoot tego scenariusza, otwórz przeglądarkę z hello łącznika serwera i spróbuj tooaccess hello aplikacji. Jeśli uruchamianie łączniki hello na platformie Azure, ale aplikacji hello są lokalne, środowisko hello może nie być spodziewać się użytkownicy.
* **Witaj kontrolerów domeny**: Jeśli łączniki hello wykonać logowanie Jednokrotne przy użyciu ograniczone delegowanie protokołu Kerberos, ich skontaktuj się z kontrolerów domeny hello przed wysłaniem hello żądania toohello wewnętrznej bazy danych. łączniki Hello mają pamięci podręcznej biletów Kerberos, ale w środowisku zajęty reakcji hello hello kontrolerów domeny może wpłynąć na wydajność. Ten problem nie zostanie częściej łączników, uruchom na platformie Azure, które komunikują się z kontrolerami domeny z lokalnymi. 

Aby uzyskać więcej informacji o optymalizacji sieci, zobacz [zagadnienia dotyczące topologii sieci, używając serwera Proxy usługi Azure Active Directory aplikacji](application-proxy-network-topology-considerations.md).

## <a name="domain-joining"></a>Sprzęganie domeny

Łączniki można uruchomić na komputerze, który nie jest przyłączony do domeny. Jeśli chcesz pojedynczego logowania jednokrotnego (SSO) tooapplications używanego zintegrowane uwierzytelnianie systemu Windows (IWA), jednak maszynie przyłączone do domeny. W takim przypadku hello łącznika maszyny musi być tooa przyłączone do domeny, która może przeprowadzać [Kerberos](https://web.mit.edu/kerberos) delegowania ograniczonego w imieniu użytkowników hello hello opublikowane aplikacje.

Łączniki mogą być również połączone toodomains lub częściowej relacji zaufania lub kontrolerów domeny tylko do tooread lasów.

## <a name="connector-deployments-on-hardened-environments"></a>Łącznik wdrożeń w środowiskach ze wzmocnionymi zabezpieczeniami

Zazwyczaj wdrażanie łącznika jest proste i nie wymaga specjalnej konfiguracji. Istnieją jednak niektóre unikatowe warunki, które należy wziąć pod uwagę:

* Organizacje, które ograniczyć ruch wychodzący hello musi [otworzyć porty wymagane](active-directory-application-proxy-enable.md#open-your-ports).
* Zgodne ze standardem FIPS maszyny może być wymagane toochange ich tooallow konfiguracji hello toogenerate procesów łącznika i przechowywania certyfikatu.
* Organizacje, które zablokowanie środowisku oparta na procesach hello hello tego problemu, żądania sieci mają toomake się, że obie te usługi łącznika są włączone tooaccess wszystkie wymagane porty i adresy IP.
* W niektórych przypadkach wychodzącego do przodu serwery proxy może przerwać hello dwukierunkowe certyfikatu uwierzytelniania i spowodować hello toofail komunikacji.

## <a name="connector-authentication"></a>Łącznik uwierzytelniania

tooprovide Usługa bezpiecznego łączników ma tooauthenticate kierunku hello usługi i usługa hello ma tooauthenticate kierunku hello łącznika. To uwierzytelnianie jest wykonywane przy użyciu certyfikatów klienta i serwera, gdy łączniki hello inicjują połączenia hello. Ten sposób administrator hello nazwy użytkownika i hasła nie są przechowywane na komputerze łącznika hello.

Certyfikaty Hello używane są toohello określonego serwera Proxy aplikacji usługi. Tworzone podczas rejestrowania początkowej hello i są automatycznie odnawiane przez łączniki hello co kilka miesięcy. 

Jeśli łącznik nie jest połączona usługa toohello dla kilku miesięcy, swoje certyfikaty mogą być nieaktualne. W takim przypadku odinstalowanie i ponowne zainstalowanie hello łącznika tootrigger rejestracji. Można uruchomić hello następujących poleceń programu PowerShell:

```
Import-module AppProxyPSModule
Register-AppProxyConnector
```

## <a name="under-hello-hood"></a>Pod maską hello

Łączniki są oparte na Windows serwer Proxy aplikacji sieci Web, więc większość hello same narzędzia do zarządzania tym dzienniki zdarzeń systemu Windows

 ![Zarządzanie dziennikami zdarzeń z hello Podgląd zdarzeń](./media/application-proxy-understand-connectors/event-view-window.png)

i liczników wydajności systemu Windows. 

 ![Dodaj liczniki toohello łącznika z hello monitora wydajności](./media/application-proxy-understand-connectors/performance-monitor.png)

łączniki Hello mają zarówno administratora, jak i sesji dzienników. dzienniki administracyjne Hello obejmują zdarzenia kluczy i ich błędy. Dzienniki sesji Hello obejmują wszystkie transakcje hello i ich szczegóły przetwarzania. 

toohello Podgląd zdarzeń, otwórz hello Przejdź dzienniki hello toosee, **widoku** menu, a następnie włączyć **wyświetlanie analityczne i debugowania dzienniki**. Następnie należy je włączyć toostart zbierania zdarzeń. Te dzienniki nie występują na liście serwera Proxy aplikacji sieci Web w systemie Windows Server 2012 R2, jak hello łączników są oparte na nowszą wersję.

Można sprawdzić stan hello usługi hello w oknie usługi hello. Łącznik Hello składa się z dwóch usług systemu Windows: hello rzeczywiste łącznika i hello aktualizacji. Obie z nich należy uruchomić wszystkie hello czasu.

 ![Lokalne usługi AzureAD](./media/application-proxy-understand-connectors/aad-connector-services.png)

## <a name="next-steps"></a>Następne kroki


* [Publikowanie aplikacji w odrębnych sieci i lokalizacje przy użyciu grup łącznika](active-directory-application-proxy-connectors-azure-portal.md)
* [Praca z istniejącym lokalnych serwerów proxy](application-proxy-working-with-proxy-servers.md)
* [Rozwiązywanie problemów z serwera Proxy aplikacji i łącznika](active-directory-application-proxy-troubleshoot.md)
* [Jak toosilently zainstalować hello łącznika serwera Proxy aplikacji w usłudze Azure AD](active-directory-application-proxy-silent-installation.md)

