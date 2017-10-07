---
title: "Wprowadzenie do raportów usługi Azure Active Directory | Microsoft Docs"
description: "Wyświetla hello raportów dostępnych w usłudze Azure Active Directory"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: 7ac99919-8df5-4424-9298-fc7c025ba949
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: f47875708398391dd7f3efdc56a741fdba273b76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-active-directory-reporting"></a>Wprowadzenie do raportów usługi Azure Active Directory
## <a name="what-it-is"></a>Co to jest
W usłudze Azure Active Directory (Azure AD) uwzględniono raporty dotyczące zabezpieczeń, działań i inspekcji dla katalogu. Poniżej przedstawiono listę raportów hello uwzględnionych:

### <a name="security-reports"></a>Raporty dotyczące zabezpieczeń
* Logowania z nieznanych źródeł
* Logowania po wielokrotnych niepowodzeniach
* Logowania z wielu lokalizacji geograficznych
* Logowania z adresów IP związanych z podejrzanymi działaniami
* Nieregularne działania związane z logowaniem
* Logowania z urządzeń, które mogą być zainfekowane
* Nietypowe działania użytkowników związane z logowaniem

### <a name="activity-reports"></a>Raporty dotyczące działań
* Podsumowanie użycia aplikacji
* Szczegóły użycia aplikacji
* Pulpit nawigacyjny aplikacji
* Błędy aprowizacji kont
* Urządzenia indywidualnych użytkowników
* Działania indywidualnych użytkowników
* Raport dotyczący działań grup
* Raport dotyczący działań związanych z rejestracją resetowania haseł
* Działania związane z resetowaniem haseł

### <a name="audit-reports"></a>Raporty dotyczące inspekcji
* Raport dotyczący inspekcji katalogu

> [!TIP]
> Więcej informacji dotyczących dokumentacji raportów usługi Azure AD zawiera temat [Wyświetlanie raportów dotyczących dostępu i użycia](active-directory-view-access-usage-reports.md).
> 
> 

## <a name="how-it-works"></a>Jak to działa
### <a name="reporting-pipeline"></a>Potok raportowania
Witaj potok raportowania składa się z trzech głównych kroków. Każdym zalogowaniu użytkownika lub uwierzytelnianie jest dokonywane, hello wykonywane są następujące czynności:

* Najpierw hello użytkownik jest uwierzytelniany (pomyślnie lub nie) i hello wynik jest zapisywany w bazach danych usługi Azure Active Directory hello.
* W regularnych odstępach czasu przetwarzane są wszystkie ostatnie logowania. W tym momencie nasze algorytmy analizy zabezpieczeń i nietypowych działań przeszukują wszystkie ostatnie logowania pod kątem podejrzanych działań.
* Po zakończeniu przetwarzania hello raporty są zapisywane, w pamięci podręcznej, a następnie w hello klasycznego portalu Azure.

### <a name="report-generation-times"></a>Czas trwania generowania raportów
Ze względu na dużą toohello liczbę uwierzytelnień i zaloguj się, że ins przetworzonych przez program hello platformy Azure AD hello najnowszych przetwarzane sesje logowania są, średnio o jedną godzinę. W rzadkich przypadkach może potrwać too8 godziny tooprocess hello ostatniego logowania.

Logowanie hello najnowsze przetworzone można znaleźć, sprawdzając tekst pomocy hello na powitania na początku każdego raportu.

![Tekst pomocy na powitania na początku każdego raportu](./media/active-directory-reporting-getting-started/reportingWatermark.PNG)

> [!TIP]
> Więcej informacji dotyczących dokumentacji raportów usługi Azure AD zawiera temat [Wyświetlanie raportów dotyczących dostępu i użycia](active-directory-view-access-usage-reports.md).
> 
> 

## <a name="getting-started"></a>Wprowadzenie
### <a name="sign-into-hello-azure-classic-portal"></a>Zaloguj się do hello klasycznego portalu Azure
Najpierw należy toosign do hello [klasycznego portalu Azure](https://manage.windowsazure.com) jako administrator globalny lub zgodności. Możesz również musi być administratorem usługi subskrypcji platformy Azure lub współadministratorem lub używać hello "dostępu tooAzure AD" subskrypcji platformy Azure.

### <a name="navigate-tooreports"></a>Przejdź tooReports
tooview raporty, przejdź na karcie raporty toohello u góry hello katalogu.

Jeśli jest to pierwsza wyświetlania raportów hello, musisz okno dialogowe tooa tooagree Aby móc wyświetlać raporty hello. To jest możliwa do administratorów w Twojej organizacji tooview tooensure te dane, które mogą być uznawane za informacje osobiste w niektórych krajach.

![Okno dialogowe](./media/active-directory-reporting-getting-started/dialogBox.png)

### <a name="explore-each-report"></a>Eksplorowanie każdego raportu
Przejdź do każdego raportu toosee hello zbieranych danych i przetwarzane sesje logowania hello. Można znaleźć [listę wszystkich raportów tutaj hello](active-directory-reporting-guide.md).

![Wszystkie raporty](./media/active-directory-reporting-getting-started/reportsMain.png)

### <a name="download-hello-reports-as-csv"></a>Pobierz raporty hello jako woluminu CSV
Każdy raport można pobrać jako plik CSV (wartości rozdzielane przecinkami). Można używać tych plików w programie Excel, usługa Power bi lub programy toofurther analizowania danych analitycznych innych firm.

toodownload żadnego raportu jako woluminu CSV, przejdź toohello raportu i kliknij przycisk "Pobierz" u dołu hello.

![Przycisk Pobierz](./media/active-directory-reporting-getting-started/downloadButton.png)

> [!TIP]
> Więcej informacji dotyczących dokumentacji raportów usługi Azure AD zawiera temat [Wyświetlanie raportów dotyczących dostępu i użycia](active-directory-view-access-usage-reports.md).
> 
> 

## <a name="next-steps"></a>Następne kroki
### <a name="customize-alerts-for-anomalous-sign-in-activity"></a>Dostosowywanie alertów dotyczących nietypowych działań związanych z logowaniem
Przejdź toohello karty "Konfiguruj" katalogu.

Przewiń w sekcji "Powiadomienia" toohello.

Włącz lub wyłącz sekcji "Powiadomienia E-mail o nietypowych logowania" hello.

![Witaj sekcja powiadomienia](./media/active-directory-reporting-getting-started/notificationsSection.png)

### <a name="integrate-with-hello-azure-ad-reporting-api"></a>Integracja z hello Azure AD interfejsu API raportowania
Zobacz [wprowadzenie hello interfejsu API raportowania](active-directory-reporting-api-getting-started.md).

### <a name="engage-multi-factor-authentication-on-users"></a>Włączanie usługi Multi-Factor Authentication dla użytkowników
Wybierz użytkownika w raporcie.

Kliknij przycisk "Włącz usługę MFA" hello u dołu hello hello ekranu.

![przycisk usługi Multi-Factor Authentication Hello u dołu hello hello ekranu](./media/active-directory-reporting-getting-started/mfaButton.png)

> [!TIP]
> Więcej informacji dotyczących dokumentacji raportów usługi Azure AD zawiera temat [Wyświetlanie raportów dotyczących dostępu i użycia](active-directory-view-access-usage-reports.md).
> 
> 

## <a name="learn-more"></a>Dowiedz się więcej
### <a name="audit-events"></a>Inspekcja zdarzeń
Dowiedz się, jakie zdarzenia są poddawane inspekcji w katalogu hello [Azure Active Directory zdarzenia inspekcji raportowania](active-directory-reporting-audit-events.md).

### <a name="api-integration"></a>Integracja z interfejsem API
Zobacz [wprowadzenie hello interfejsu API raportowania](active-directory-reporting-api-getting-started.md) i hello [dokumentacji interfejsu API](https://msdn.microsoft.com/library/azure/mt126081.aspx).

### <a name="get-in-touch"></a>Kontakt
Jeśli chcesz przesłać opinię, potrzebujesz pomocy lub masz pytania, wyślij wiadomość e-mail na adres [aadreportinghelp@microsoft.com](mailto:aadreportinghelp@microsoft.com).

> [!TIP]
> Więcej informacji dotyczących dokumentacji raportów usługi Azure AD zawiera temat [Wyświetlanie raportów dotyczących dostępu i użycia](active-directory-view-access-usage-reports.md).
> 
> 

