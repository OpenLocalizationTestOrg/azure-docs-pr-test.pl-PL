---
title: "Wyświetlanie raportów dostępu i użycia | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, jak wyświetlanie raportów dostępu i użycia, aby uzyskać wgląd w integralności i bezpieczeństwa katalogu organizacji."
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
ms.openlocfilehash: 038ac79ebf61c6429fbf7ca21eefe9414bcfc03a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="view-your-access-and-usage-reports"></a>Wyświetlanie raportów dostępu i użycia
*Ta dokumentacja jest częścią [Przewodnika po raportach usługi Azure Active Directory](active-directory-reporting-guide.md).*

Dostęp do usługi Azure Active Directory i raporty użycia umożliwia wgląd we integralności i bezpieczeństwa katalogu organizacji. Dzięki tym informacjom administratora katalogu można lepiej określić, gdzie może znajdować się możliwe zagrożenia bezpieczeństwa, tak aby ich odpowiednio zaplanować ich eliminowania.

W portalu zarządzania Azure raporty są podzielone na następujące sposoby:

* Raporty anomalii — zawiera logowania zdarzenia znajdujące się nietypowych. Naszym celem jest uświadomić możesz takiego działania i umożliwiają mieć możliwość określenia, czy jest podejrzane zdarzenia.
* Zintegrowane raportów programu Application — zapewnia wgląd w sposób aplikacji w chmurze są używane w organizacji. Usługa Azure Active Directory oferuje integrację z tysiącami aplikacji w chmurze.
* Raporty o błędach — Wskazuj błędy, które mogą wystąpić podczas inicjowania obsługi administracyjnej kont do aplikacji zewnętrznych.
* Raporty dotyczące użytkownika — ekranu urządzenia/logowania dane o aktywności dla określonego użytkownika.
* Dzienniki aktywności — zawiera rekord wszystkich zdarzeń inspekcji w ostatnich 24 godzinach, ostatnich 7 dni lub ostatnich 30 dni, a także grupy działania zmiany i działanie resetowania i rejestracji hasła.

> [!NOTE]
> * Niektóre zaawansowane raporty użycia anomalii i zasoby są dostępne tylko po włączeniu [Azure Active Directory Premium](active-directory-get-started-premium.md). Zaawansowane raporty ułatwiające poprawić zabezpieczenia dostępu, odpowiadanie na potencjalne zagrożenia i uzyskać dostęp do analityka na użycie urządzeń dostępu i aplikacji.
> * Klienci w Chinach mogą używać wersji Premium i Podstawowa usługi Azure Active Directory za pomocą wystąpienia usługi Azure Active Directory dostępnego na całym świecie. Wersje Premium i Podstawowa usługi Azure Active Directory nie są obecnie obsługiwane w usłudze Microsoft Azure świadczonej przez 21Vianet w Chinach. Aby uzyskać więcej informacji, skontaktuj się z nami na [forum usługi Azure Active Directory](https://feedback.azure.com/forums/169401-azure-active-directory/).
> 
> 

## <a name="reports"></a>Raporty
| Raport | Opis |
| --- | --- |
| **Raporty dotyczące nietypowych działań** | |
| [Logowania z nieznanych źródeł](active-directory-reporting-sign-ins-from-unknown-sources.md) |Mogą oznaczać próbę logowania się bez śledzone. |
| [Logowania po wielokrotnych niepowodzeniach](active-directory-reporting-sign-ins-after-multiple-failures.md) |Może sygnalizować atak siłowy powiodło się. |
| [Logowania z wielu lokalizacji geograficznych](active-directory-reporting-sign-ins-from-multiple-geographies.md) |Może sygnalizować, że logujesz się przy użyciu tego samego konta wielu użytkowników. |
| [Logowania z adresów IP związanych z podejrzanymi działaniami](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md) |Może sygnalizować pomyślnego logowania po próbie przez nieautoryzowanego dostępu. |
| [Logowania z potencjalnie zainfekowanych urządzeń](active-directory-reporting-sign-ins-from-possibly-infected-devices.md) |Mogą oznaczać próbę zalogować z potencjalnie zainfekowanych urządzeń. |
| [Nieprawidłowe logowanie działania](active-directory-reporting-irregular-sign-in-activity.md) |Może sygnalizować nietypowe logowania użytkowników wzorce zdarzenia. |
| [Użytkownicy z nietypowe logowania działania](active-directory-reporting-users-with-anomalous-sign-in-activity.md) |Wskazuje użytkowników, których konta zostały naruszone. |
| Użytkownicy z ujawnionymi poświadczeniami |Użytkownicy z ujawnionymi poświadczeniami |
| **Dzienniki aktywności** | |
| Raport dotyczący inspekcji |Zdarzenia inspekcji w katalogu |
| Działania związane z resetowaniem haseł |Udostępnia szczegółowy widok resetowanie haseł, które występują w Twojej organizacji. |
| Aktywność rejestracji resetowania haseł |Zawiera szczegółowy widok hasła resetowania rejestracji, które występują w Twojej organizacji. |
| Raport aktywności grup samoobsługi |Zawiera dziennik aktywności, aby wszystkie grupy samoobsługi działania w katalogu |
| **Zintegrowane aplikacje** | |
| Użycie aplikacji |Zawiera podsumowanie użycia dla wszystkich aplikacji SaaS zintegrowanych z katalogiem. |
| Działanie aprowizacji kont |Zawiera historię prób do obsługi administracyjnej kont do aplikacji zewnętrznych. |
| Stan przerzucania hasła |Szczegółowe omówienie hasła automatycznego przerzucania stan aplikacji SaaS. |
| Błędy aprowizacji kont |Wskazuje wpływu na dostęp użytkowników do aplikacji zewnętrznych. |
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
<p>Nietypowe logowania raporty aktywności Flaga podejrzane znak w działaniu usługi Office 365 portalu zarządzania Azure, Panel dostępu usługi Azure AD, Sharepoint Online, Dynamics CRM Online i innych usług online firmy Microsoft.</p>

<p>Wszystkie te raporty, z wyjątkiem raport "Logowania po wielokrotnych niepowodzeniach" również Flaga podejrzane <i>federacyjnych</i> logowania do usług wyżej wymienione, niezależnie od dostawcy federacyjnego. </p>

<p>Dostępne są następujące raporty: </p><ul>

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
| Przedstawia rekord wszystkich zdarzeń inspekcji w ciągu ostatnich 24 godzin, ostatnich 7 dni i ostatnich 30 dni. <br /> Aby uzyskać więcej informacji, zobacz [Azure Active Directory zdarzenia raportowania inspekcji usługi](active-directory-reporting-audit-events.md) |Katalog > karta raporty |

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
| Przedstawia wszystkie działania w grupach zarządzanych samoobsługi w katalogu. |Katalog > Użytkownicy > <i>użytkownika</i> > kartę urządzenia |

![Raport aktywności grup samoobsługi](./media/active-directory-view-access-usage-reports/selfServiceGroupsActivity.PNG)

## <a name="integrated-applications-reports"></a>Raporty zintegrowanych aplikacji
### <a name="application-usage-summary"></a>Podsumowanie użycia aplikacji
| Opis | Lokalizacja raportu |
|:--- |:--- |
| Ten raport ma być wyświetlone użycia dla wszystkich aplikacji SaaS w katalogu. Ten raport jest oparty na liczbę powtórzeń klikać użytkowników aplikacji, w panelu dostępu. |Katalog > karta raporty |

Ten raport zawiera logowania do aplikacji *wszystkie* aplikacji, które katalogu ma dostęp do, tym wstępnie zintegrowanych aplikacji firmy Microsoft.

Wstępnie zintegrowanych aplikacji Microsoft obejmują usługi Office 365, Sharepoint, portalu zarządzania Azure i inne.

![Podsumowanie użycia aplikacji](./media/active-directory-view-access-usage-reports/applicationUsage.PNG)

### <a name="application-usage-detailed"></a>Szczegóły użycia aplikacji
| Opis | Lokalizacja raportu |
|:--- |:--- |
| Ten raport chcesz sprawdzić, ile określonej aplikacji SaaS jest używany. Ten raport jest oparty na liczbę powtórzeń klikać użytkowników aplikacji, w panelu dostępu. |Katalog > karta raporty |

### <a name="application-dashboard"></a>Pulpit nawigacyjny aplikacji
| Opis | Lokalizacja raportu |
|:--- |:--- |
| Ten raport wskazuje rejestracji zbiorczej dodatki do aplikacji przez użytkowników w organizacji przez wybrany okres. Wykres na stronie pulpitu nawigacyjnego pomoże zidentyfikować trendy użycia wszystkie tej aplikacji. |Katalog > aplikacji > karty Pulpit nawigacyjny |

## <a name="error-reports"></a>Raporty o błędach
### <a name="account-provisioning-errors"></a>Błędy aprowizacji kont
| Opis | Lokalizacja raportu |
|:--- |:--- |
| Umożliwia monitorowanie błędów występujących podczas synchronizacji kont z aplikacji SaaS w usłudze Azure Active Directory. |Katalog > karta raporty |

![Błędy aprowizacji kont](./media/active-directory-view-access-usage-reports/accountProvisioningErrors.PNG)

## <a name="user-specific-reports"></a>Raporty dotyczące użytkownika
### <a name="devices"></a>Urządzenia
| Opis | Lokalizacja raportu |
|:--- |:--- |
| Ten raport umożliwia zapoznaj się z adresu IP i lokalizację geograficzną urządzenia używane przez określonego użytkownika można uzyskać dostępu do usługi Azure Active Directory. |Katalog > Użytkownicy > <i>użytkownika</i> > kartę urządzenia |

### <a name="activity"></a>Działanie
| Opis | Lokalizacja raportu |
|:--- |:--- |
| Pokazuje konta działania dla użytkownika. Raport zawiera informacje, takie jak zalogowaniem się do aplikacji, urządzenie, adres IP i lokalizacji. Nie gromadzimy Historia dla użytkowników, którzy Zaloguj się przy użyciu konta Microsoft. |Katalog > Użytkownicy > <i>użytkownika</i> > karta działanie |

#### <a name="sign-in-events-included-in-the-user-activity-report"></a>Zaloguj się zdarzenia uwzględnionych w raporcie aktywności użytkownika
Niektóre rodzaje logowania zdarzenia będą wyświetlane w raport aktywności użytkownika.

| Typ zdarzenia | Włączone? |
| --- | --- |
| Logowania się do [panelu dostępu](http://myapps.microsoft.com/) |Tak |
| Logowania się do [portalu zarządzania Azure](https://manage.windowsazure.com/) |Tak |
| Logowania się do [portalu Microsoft Azure](https://portal.azure.com/) |Tak |
| Logowania się do [portalu usługi Office 365](http://portal.office.com/) |Tak |
| Logowania do aplikacji natywnej, takich jak program Outlook (zobacz wyjątek poniżej) |Tak |
| Logowania do aplikacji federacyjnych udostępniane za pośrednictwem panelu dostępu, takie jak Salesforce |Tak |
| Logowania do aplikacji opartych na hasłach za pomocą panelu dostępu, takich jak usługi Twitter |Tak |
| Logowania do aplikacji firm niestandardowych, który został dodany do katalogu |Nie (wkrótce) |
| Logowania dla aplikacji serwera Proxy aplikacji usługi Azure AD, który został dodany do katalogu |Nie (wkrótce) |

> Uwaga: Aby zmniejszyć ilość szumu w tym raporcie, logowania przez [Microsoft Online Services Asystenta logowania](http://community.office365.com/en-us/w/sso/534.aspx) nie są pokazywane.
> 
> 

## <a name="things-to-consider-if-you-suspect-security-breach"></a>Co należy wziąć pod uwagę, jeśli podejrzewasz naruszenia zabezpieczeń
Jeśli zachodzi podejrzenie, że konto użytkownika może być naruszona lub dowolnego rodzaju użytkownika podejrzane działanie, które mogą prowadzić do naruszenia zabezpieczeń danych katalogu w chmurze, warto wziąć pod uwagę jedną lub więcej z następujących czynności:

* Skontaktuj się z użytkownika, aby sprawdzić działanie
* Resetowanie hasła użytkownika.
* [Włączanie uwierzytelniania wieloskładnikowego](../multi-factor-authentication/multi-factor-authentication-get-started.md) celu zapewnienia dodatkowych zabezpieczeń

## <a name="view-or-download-a-report"></a>Wyświetl lub pobranie raportu
1. W klasycznym portalu Azure, kliknij przycisk **usługi Active Directory**, kliknij nazwę katalogu organizacji, a następnie kliknij przycisk **raporty**.
2. Na stronie Raporty kliknij raport, który chcesz wyświetlić i/lub pobrania.
   
   > [!NOTE]
   > Jeśli jest to funkcja raportowania usługi Azure Active Directory jest używany po raz pierwszy, zobaczysz komunikat do uczestnictwa w. Jeśli akceptujesz, kliknij ikonę znacznika wyboru, aby kontynuować.
   > 
   > 
3. Kliknij menu rozwijanym obok interwał, a następnie wybierz jedną z następujących przedziałów czasu, które powinny być używane podczas generowania tego raportu:
   
   * Ostatnie 24 godziny
   * Ostatnie 7 dni
   * Ostatnie 30 dni
4. Kliknij ikonę znacznika wyboru, aby uruchomić raport.
   * Maksymalnie 1000 zdarzenia będą wyświetlane w klasycznym portalu Azure.
5. Jeśli to konieczne, kliknij przycisk **Pobierz** pobierania raportu do skompresowanego pliku w formacie wartości rozdzielanych przecinkami (CSV) do wyświetlania w trybie offline lub archiwizacji.
   * Maksymalnie 75,000 zdarzenia będą uwzględniane w pobranym pliku.
   * Dla większej ilości danych, zapoznaj się z [Azure AD interfejsu API raportowania](active-directory-reporting-api-getting-started.md).

## <a name="ignore-an-event"></a>Ignoruj zdarzenia
Jeśli wyświetlasz wszystkie raporty, anomalii, mogą pojawić się zignorować różnych zdarzeń, które są widoczne w powiązanych raportów. Aby zignorować zdarzenia, po prostu zaznacz zdarzenie w raporcie, a następnie kliknij przycisk **Ignoruj**. **Ignoruj** przycisku spowoduje trwałe usunięcie zaznaczonego zdarzenia z raportu i mogą być używane tylko przez licencjonowane administratorów globalnych.

## <a name="automatic-email-notifications"></a>Powiadomienia e-mail automatyczne
Dla więcej informacji na temat usługi Azure AD do raportowania powiadomień, zapoznaj się z [Azure Active Directory powiadomienia o raportach](active-directory-reporting-notifications.md).

## <a name="whats-next"></a>Co dalej
* [Wprowadzenie do usługi Azure Active Directory — wersja Premium](active-directory-get-started-premium.md)
* [Dodawanie znakowania firmowego do stron logowania i panelu dostępu](active-directory-add-company-branding.md)

