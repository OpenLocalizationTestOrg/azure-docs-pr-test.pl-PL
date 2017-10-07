---
title: "aaaView raportów dotyczących dostępu i użycia | Dokumentacja firmy Microsoft"
description: "W tym artykule wyjaśniono, jak tooview dostępu i użycia raporty toogain wgląd w hello integralności i bezpieczeństwa w katalogu organizacji."
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: a074bc4e-cf3f-4ad1-8cc6-4199d2e09ce4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 1c18fd2a327ae8b67f62ce2754f643bdb03514a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="view-your-access-and-usage-reports"></a>Wyświetlanie raportów dostępu i użycia
*Niniejsza dokumentacja jest częścią hello [Azure Active Directory Przewodnik po raportach](active-directory-reporting-guide.md).*

Umożliwia dostęp do usługi Azure Active Directory i użycia raporty toogain widoczność hello integralności i bezpieczeństwa w katalogu organizacji. Dzięki tym informacjom administratora katalogu można lepiej określić, gdzie może znajdować się możliwe zagrożenia bezpieczeństwa, tak aby ich odpowiednio zaplanować toomitigate te zagrożenia.

W portalu zarządzania Azure hello raporty są podzielone na powitania następujące sposoby:

* Raporty anomalii — zawiera rejestrowanie zdarzeń czy znaleziono toobe nietypowych. Naszym celem jest toomake należy pamiętać o tych działań oraz pozwalające użytkownikowi toobe toomake możliwe określenie, czy jest podejrzane zdarzenia.
* Zintegrowane raportów programu Application — zapewnia wgląd w sposób aplikacji w chmurze są używane w organizacji. Usługa Azure Active Directory oferuje integrację z tysiącami aplikacji w chmurze.
* Raporty o błędach — Wskazuj błędy, które mogą wystąpić podczas inicjowania obsługi administracyjnej kont tooexternal aplikacji.
* Raporty dotyczące użytkownika — ekranu urządzenia/logowania dane o aktywności dla określonego użytkownika.
* Dzienniki aktywności — zawiera rekord wszystkich zdarzeń inspekcji w ramach hello ostatnie 24 godziny, ostatnich 7 dni, lub ostatnich 30 dni, a także działania zmiany w grupie i działanie resetowania i rejestracji hasła.

> [!NOTE]
> * Niektóre zaawansowane raporty użycia anomalii i zasoby są dostępne tylko po włączeniu [Azure Active Directory Premium](active-directory-get-started-premium.md). Zaawansowanych raportów pomagają poprawić zabezpieczenia dostępu odpowiadać toopotential zagrożeń i uzyskiwanie dostępu tooanalytics na użycie urządzeń dostępu i aplikacji.
> * Azure Active Directory Premium i podstawowa wydań są dostępne dla klientów w Chinach przy użyciu hello na całym świecie wystąpienia usługi Azure Active Directory. Azure Active Directory Premium i podstawowa wersje nie są obecnie obsługiwane w hello Microsoft Azure świadczonej przez 21Vianet w Chinach. Aby uzyskać więcej informacji, skontaktuj się z nami na powitania [Azure Active Directory Forum](https://feedback.azure.com/forums/169401-azure-active-directory/).
> 
> 

## <a name="reports"></a>Raporty
| Raport | Opis |
| --- | --- |
| **Raporty dotyczące nietypowych działań** | |
| [Logowania z nieznanych źródeł](active-directory-reporting-sign-ins-from-unknown-sources.md) |Może sygnalizować toosign próba w bez śledzone. |
| [Logowania po wielokrotnych niepowodzeniach](active-directory-reporting-sign-ins-after-multiple-failures.md) |Może sygnalizować atak siłowy powiodło się. |
| [Logowania z wielu lokalizacji geograficznych](active-directory-reporting-sign-ins-from-multiple-geographies.md) |Może sygnalizować, że wielu użytkowników są zalogować hello same konta. |
| [Logowania z adresów IP związanych z podejrzanymi działaniami](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md) |Może sygnalizować pomyślnego logowania po próbie przez nieautoryzowanego dostępu. |
| [Logowania z potencjalnie zainfekowanych urządzeń](active-directory-reporting-sign-ins-from-possibly-infected-devices.md) |Może sygnalizować toosign próba w z potencjalnie zainfekowanych urządzeń. |
| [Nieprawidłowe logowanie działania](active-directory-reporting-irregular-sign-in-activity.md) |Może sygnalizować toousers zdarzenia nietypowe logowania wzorce. |
| [Użytkownicy z nietypowe logowania działania](active-directory-reporting-users-with-anomalous-sign-in-activity.md) |Wskazuje użytkowników, których konta zostały naruszone. |
| Użytkownicy z ujawnionymi poświadczeniami |Użytkownicy z ujawnionymi poświadczeniami |
| **Dzienniki aktywności** | |
| Raport dotyczący inspekcji |Zdarzenia inspekcji w katalogu |
| Działania związane z resetowaniem haseł |Udostępnia szczegółowy widok resetowanie haseł, które występują w Twojej organizacji. |
| Aktywność rejestracji resetowania haseł |Zawiera szczegółowy widok hasła resetowania rejestracji, które występują w Twojej organizacji. |
| Raport aktywności grup samoobsługi |Udostępnia tooall dziennika aktywności grupy samoobsługi działania w katalogu |
| **Zintegrowane aplikacje** | |
| Użycie aplikacji |Zawiera podsumowanie użycia dla wszystkich aplikacji SaaS zintegrowanych z katalogiem. |
| Działanie aprowizacji kont |Zawiera historię prób tooprovision kont tooexternal aplikacji. |
| Stan przerzucania hasła |Szczegółowe omówienie hasła automatycznego przerzucania stan aplikacji SaaS. |
| Błędy aprowizacji kont |Wskazuje toousers wpływu dostępu tooexternal aplikacji. |
| **Usługi rights management** | |
| Użycie usługi RMS |Zawiera podsumowanie użycia usługi Rights Management |
| Najbardziej aktywni użytkownicy usługi RMS |Wyświetla listę top 1000 aktywnych użytkowników, którzy uzyskać dostępu do plików chronionych przez usługi RMS |
| Użycie urządzeń usługi RMS |Wyświetla listę urządzeń używanych podczas uzyskiwania dostępu do plików chronionych przez usługi RMS |
| Użycie aplikacji z obsługą usług RMS |Zapewnia możliwość aplikacjami obsługującymi użycia usług RMS |

## <a name="report-editions"></a>Wersje raportu
| Raport | Bezpłatna | Podstawowa | Premium |
| --- | --- | --- | --- |
| **Raporty dotyczące nietypowych działań** | | | |
| Logowania z nieznanych źródeł |✓ |✓ |✓ |
| Logowania po wielokrotnych niepowodzeniach |✓ |✓ |✓ |
| Logowania z wielu lokalizacji geograficznych |✓ |✓ |✓ |
| Logowania z adresów IP związanych z podejrzanymi działaniami | | |✓ |
| Logowania z potencjalnie zainfekowanych urządzeń | | |✓ |
| Nieprawidłowe logowanie działania | | |✓ |
| Użytkownicy z nietypowe logowania działania | | |✓ |
| Użytkownicy z ujawnionymi poświadczeniami | | |✓ |
| **Dzienniki aktywności** | | | |
| Raport dotyczący inspekcji |✓ |✓ |✓ |
| Działania związane z resetowaniem haseł | | |✓ |
| Aktywność rejestracji resetowania haseł | | |✓ |
| Raport aktywności grup samoobsługi | | |✓ |
| **Zintegrowane aplikacje** | | | |
| Użycie aplikacji | | |✓ |
| Działanie aprowizacji kont |✓ |✓ |✓ |
| Stan przerzucania hasła | | |✓ |
| Błędy aprowizacji kont |✓ |✓ |✓ |
| **Usługi rights management** | | | |
| Użycie usługi RMS | | |Tylko usługi RMS |
| Najbardziej aktywni użytkownicy usługi RMS | | |Tylko usługi RMS |
| Użycie urządzeń usługi RMS | | |Tylko usługi RMS |
| Użycie aplikacji z obsługą usług RMS | | |Tylko usługi RMS |

## <a name="anomalous-activity-reports"></a>Raporty dotyczące nietypowych działań
<p>nietypowe Hello Zaloguj raporty aktywności logowania podejrzane flagi tooOffice365 działania, portalu zarządzania Azure, Panel dostępu usługi Azure AD, Sharepoint Online, Dynamics CRM Online i innych usług online firmy Microsoft.</p>

<p>Wszystkie te raporty, z wyjątkiem Witaj "Logowania po wielokrotnych niepowodzeniach" raport również Flaga podejrzane <i>federacyjnych</i> zarejestrować ins toohello wyżej wymienione usługi, niezależnie od dostawcy federacyjnego hello. </p>

<p>dostępne są Hello następujące raporty: </p><ul>

<li>[Logowania z nieznanych źródeł](active-directory-reporting-sign-ins-from-unknown-sources.md).</li>

<li>[Logowania po wielokrotnych niepowodzeniach](active-directory-reporting-sign-ins-after-multiple-failures.md).</li>

<li>[Logowania z wielu lokalizacji geograficznych](active-directory-reporting-sign-ins-from-multiple-geographies.md).</li>

<li>[Logowania z adresów IP z podejrzaną aktywność](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md).</li>

<li>[Nieprawidłowe logowanie działania](active-directory-reporting-irregular-sign-in-activity.md).</li>

<li>[Logowania z potencjalnie zainfekowanych urządzeń](active-directory-reporting-sign-ins-from-possibly-infected-devices.md).</li>

<li>[Z nietypowe logowania działania](active-directory-reporting-users-with-anomalous-sign-in-activity.md).</li>

<li>Użytkownicy z ujawnionymi poświadczeniami</li></ul>

## <a name="activity-logs"></a>Dzienniki aktywności
### <a name="audit-report"></a>Raport dotyczący inspekcji
| Opis | Lokalizacja raportu |
|:--- |:--- |
| Przedstawia rekord wszystkich zdarzeń inspekcji w ramach hello w ostatnich 24 godzinach, ostatnich 7 dni i ostatnich 30 dni. <br /> Aby uzyskać więcej informacji, zobacz [Azure Active Directory zdarzenia raportowania inspekcji usługi](active-directory-reporting-audit-events.md) |Katalog > karta raporty |

![Raport dotyczący inspekcji](./media/active-directory-view-access-usage-reports/auditReport.PNG)

### <a name="password-reset-activity"></a>Działania związane z resetowaniem haseł
| Opis | Lokalizacja raportu |
|:--- |:--- |
| Pokazuje resetowania hasła wszystkich prób, które wystąpiły w Twojej organizacji. |Katalog > karta raporty |

![Działania związane z resetowaniem haseł](./media/active-directory-view-access-usage-reports/passwordResetActivity.PNG)

### <a name="password-reset-registration-activity"></a>Aktywność rejestracji resetowania haseł
| Opis | Lokalizacja raportu |
|:--- |:--- |
| Zawiera informacje o rejestracji, które wystąpiły w Twojej organizacji resetowania hasła wszystkich |Katalog > karta raporty |

![Aktywność rejestracji resetowania haseł](./media/active-directory-view-access-usage-reports/passwordResetRegistrationActivity.PNG)

### <a name="self-service-groups-activity"></a>Raport aktywności grup samoobsługi
| Opis | Lokalizacja raportu |
|:--- |:--- |
| Przedstawia wszystkie działania dla grup zarządzanych samoobsługi hello w katalogu. |Katalog > Użytkownicy > <i>użytkownika</i> > kartę urządzenia |

![Raport aktywności grup samoobsługi](./media/active-directory-view-access-usage-reports/selfServiceGroupsActivity.PNG)

## <a name="integrated-applications-reports"></a>Raporty zintegrowanych aplikacji
### <a name="application-usage-summary"></a>Podsumowanie użycia aplikacji
| Opis | Lokalizacja raportu |
|:--- |:--- |
| Ten raport ma toosee użycia dla wszystkich aplikacji SaaS hello w katalogu. Ten raport jest oparty na powitania liczba użytkowników kliknęli aplikacji hello w hello panelu dostępu. |Katalog > karta raporty |

Ten raport zawiera logowania za*wszystkie* aplikacji, które katalogu ma dostęp do, tym wstępnie zintegrowanych aplikacji firmy Microsoft.

Wstępnie zintegrowanych aplikacji Microsoft obejmują usługi Office 365, Sharepoint, hello portalu zarządzania Azure i inne.

![Podsumowanie użycia aplikacji](./media/active-directory-view-access-usage-reports/applicationUsage.PNG)

### <a name="application-usage-detailed"></a>Szczegóły użycia aplikacji
| Opis | Lokalizacja raportu |
|:--- |:--- |
| Ten raport ma toosee ile określonej aplikacji SaaS jest używany. Ten raport jest oparty na powitania liczba użytkowników kliknęli aplikacji hello w hello panelu dostępu. |Katalog > karta raporty |

### <a name="application-dashboard"></a>Pulpit nawigacyjny aplikacji
| Opis | Lokalizacja raportu |
|:--- |:--- |
| Ten raport wskazuje rejestracji zbiorczej ins toohello aplikacji przez użytkowników w organizacji przez wybrany okres. Wykres Hello na stronie pulpitu nawigacyjnego hello ułatwia identyfikację trendów użycia wszystkie tej aplikacji. |Katalog > aplikacji > karty Pulpit nawigacyjny |

## <a name="error-reports"></a>Raporty o błędach
### <a name="account-provisioning-errors"></a>Błędy aprowizacji kont
| Opis | Lokalizacja raportu |
|:--- |:--- |
| Użyj tego toomonitor o błędach podczas synchronizacji hello kont z tooAzure aplikacji SaaS usługi Active Directory. |Katalog > karta raporty |

![Błędy aprowizacji kont](./media/active-directory-view-access-usage-reports/accountProvisioningErrors.PNG)

## <a name="user-specific-reports"></a>Raporty dotyczące użytkownika
### <a name="devices"></a>Urządzenia
| Opis | Lokalizacja raportu |
|:--- |:--- |
| Ten raport ma adres IP hello toosee i lokalizację geograficzną urządzenia, czy określony użytkownik został użyty tooaccess usługi Azure Active Directory. |Katalog > Użytkownicy > <i>użytkownika</i> > kartę urządzenia |

### <a name="activity"></a>Działanie
| Opis | Lokalizacja raportu |
|:--- |:--- |
| Zawiera znak hello działania dla użytkownika. Witaj raport zawiera informacje, takie jak zalogowaniem się do aplikacji hello, urządzenie używane adresu IP i lokalizacji. Nie gromadzimy hello Historia dla użytkowników, którzy Zaloguj się przy użyciu konta Microsoft. |Katalog > Użytkownicy > <i>użytkownika</i> > karta działanie |

#### <a name="sign-in-events-included-in-hello-user-activity-report"></a>Zaloguj się zdarzeń zawartych w hello raport aktywność użytkownika
Niektóre rodzaje logowania zdarzenia będą wyświetlane w hello raport aktywności użytkownika.

| Typ zdarzenia | Włączone? |
| --- | --- |
| Zaloguj się ins toohello [panelu dostępu](http://myapps.microsoft.com/) |Tak |
| Zaloguj się ins toohello [portalu zarządzania Azure](https://manage.windowsazure.com/) |Tak |
| Zaloguj się ins toohello [portalu Microsoft Azure](https://portal.azure.com/) |Tak |
| Zaloguj się ins toohello [portalu usługi Office 365](http://portal.office.com/) |Tak |
| Zaloguj się ins tooa natywnych aplikacji, takich jak program Outlook (zobacz wyjątek poniżej) |Tak |
| Podpisać ins tooa federacyjnych udostępniane za pośrednictwem hello Panel dostępu, takie jak Salesforce |Tak |
| Podpisywanie ins tooa opartego na hasłach aplikacji za pośrednictwem hello Panel dostępu, takich jak usługi Twitter |Tak |
| Podpisywania aplikacji biznesowych niestandardowych tooa dodatków, dodanym toohello katalogu |Nie (wkrótce) |
| Podpisywanie aplikacji serwera Proxy aplikacji usługi Azure AD tooan dodatków, dodanym toohello katalogu |Nie (wkrótce) |

> Uwaga: tooreduce hello ilość szumu w tym raporcie logowania przez hello [Microsoft Online Services Asystenta logowania](http://community.office365.com/en-us/w/sso/534.aspx) nie są pokazywane.
> 
> 

## <a name="things-tooconsider-if-you-suspect-security-breach"></a>Tooconsider rzeczy, jeśli zachodzi podejrzenie złamania zabezpieczeń
Jeśli zachodzi podejrzenie, że konto użytkownika może być naruszona lub dowolny rodzaj użytkownika podejrzane działanie, które może spowodować naruszenie zabezpieczeń tooa dane katalogu w chmurze hello można tooconsider co najmniej jednego hello następujące akcje:

* Skontaktuj się z hello użytkownika tooverify hello działania
* Resetowanie hasła użytkownika hello
* [Włączanie uwierzytelniania wieloskładnikowego](../multi-factor-authentication/multi-factor-authentication-get-started.md) celu zapewnienia dodatkowych zabezpieczeń

## <a name="view-or-download-a-report"></a>Wyświetl lub pobranie raportu
1. W hello klasycznego portalu Azure, kliknij przycisk **usługi Active Directory**, kliknij nazwę hello katalogu organizacji, a następnie kliknij przycisk **raporty**.
2. Na stronie powitania, raporty, kliknij przycisk Raport hello ma tooview i/lub pobrania.
   
   > [!NOTE]
   > Jeśli hello jest po raz pierwszy używasz hello raportowania funkcji usługi Azure Active Directory, zostanie wyświetlony tooOpt wiadomości w. Jeśli akceptujesz, kliknij przycisk toocontinue Ikona znacznika wyboru hello.
   > 
   > 
3. Kliknij przycisk Dalej tooInterval menu rozwijanego hello, a następnie wybierz jedną z powitania po przedziałów czasu, które powinny być używane podczas generowania tego raportu:
   
   * Ostatnie 24 godziny
   * Ostatnie 7 dni
   * Ostatnie 30 dni
4. Kliknij przycisk hello znacznik wyboru Ikona toorun hello raport.
   * Zapasowej too1000 zdarzenia będą wyświetlane w hello klasycznego portalu Azure.
5. Jeśli to konieczne, kliknij przycisk **Pobierz** toodownload hello tooa skompresowany plik raportu w formacie wartości rozdzielanych przecinkami (CSV) do wyświetlania w trybie offline lub archiwizacji.
   * Zapasowej too75 000 zdarzenia zostaną uwzględnione w pliku hello pobrane.
   * Dla większej ilości danych, zapoznaj się z hello [Azure AD interfejsu API raportowania](active-directory-reporting-api-getting-started.md).

## <a name="ignore-an-event"></a>Ignoruj zdarzenia
Jeśli wyświetlasz wszystkie raporty, anomalii, mogą pojawić się zignorować różnych zdarzeń, które są widoczne w powiązanych raportów. tooignore zdarzenie, po prostu zaznacz zdarzeń hello hello raportu, a następnie kliknij przycisk **Ignoruj**. Witaj **Ignoruj** przycisku spowoduje trwałe usunięcie zaznaczonego zdarzenia hello z raportu hello i mogą być używane tylko przez licencjonowane administratorów globalnych.

## <a name="automatic-email-notifications"></a>Powiadomienia e-mail automatyczne
Dla więcej informacji na temat usługi Azure AD do raportowania powiadomień, zapoznaj się z [Azure Active Directory powiadomienia o raportach](active-directory-reporting-notifications.md).

## <a name="whats-next"></a>Co dalej
* [Wprowadzenie do usługi Azure Active Directory — wersja Premium](active-directory-get-started-premium.md)
* [Dodawanie znakowania firmowego tooyour logowania i panelu dostępu do stron](active-directory-add-company-branding.md)

