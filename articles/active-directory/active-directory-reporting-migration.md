---
title: "działanie aaaFind raporty w programie hello portalu Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toofind działania usługi Azure Active Directory raporty w programie hello portalu Azure."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: d93521f8-dc21-4feb-aaff-4bb300f04812
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: f8d7a968403e10ccc5319f27fedad38b1553ded0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="find-activity-reports-in-hello-azure-portal"></a>Znajdź raporty aktywności w hello portalu Azure

Jeśli przenosisz z hello Azure toohello portalu klasycznego portalu Azure, możesz uzyskać nowy przeglądać dzienniki aktywności w usłudze Azure Active Directory (Azure AD). W ostatnie [wpis w blogu](https://blogs.technet.microsoft.com/enterprisemobility/2016/11/08/azuread-weve-just-turned-on-detailed-auditing-and-sign-in-logs-in-the-new-azure-portal/), możemy wyjaśniają, jak widać, dzienniki aktywności w kontekście hello zasobu hello pracuje w hello portalu Azure. W tym artykule opisano sposób toofind zgłasza, że używane w hello klasycznego portalu Azure w hello portalu Azure.

## <a name="whats-new"></a>Co nowego

Raporty w hello klasycznego portalu Azure są podzielone na kategorie:

1.  Raporty dotyczące zabezpieczeń
2.  Raporty dotyczące działań
3.  Raporty zintegrowanych aplikacji

### <a name="activity-and-integrated-app-reports"></a>Działanie i raporty zintegrowanych aplikacji

Kontekstowa raportowania w programie hello portalu Azure, istniejących raportów są scalane w ramach jednego widoku. Jednej podstawowej interfejsu API zawiera hello danych toohello widok.

Ten widok na powitania toosee **usługi Azure Active Directory** bloku, w obszarze **działania**, wybierz pozycję **dzienniki inspekcji**.

![Dzienniki inspekcji](./media/active-directory-reporting-migration/482.png "Dzienniki inspekcji")

następujące raporty Hello są konsolidowane w tym widoku:

-   Raport dotyczący inspekcji
-   Działania związane z resetowaniem haseł
-   Aktywność rejestracji resetowania haseł
-   Raport aktywności grup samoobsługi
-   Zmiany nazwy grupy usługi Office 365
-   Działanie aprowizacji kont
-   Stan przerzucania hasła
-   Błędy aprowizacji kont


Raport użycia aplikacji Hello został ulepszony, znajduje się w hello **logowania** widoku. Ten widok na powitania toosee **usługi Azure Active Directory** bloku, w obszarze **działania**, wybierz pozycję **logowania**.

![Widok logowania](./media/active-directory-reporting-migration/483.png "wyświetlić logowania")

Witaj **logowania** widok zawiera sesje logowania użytkownika. Można użyć tych informacji tooget aplikacji użycia informacji. Również można wyświetlić informacje na temat wykorzystania aplikacji w hello **aplikacje dla przedsiębiorstw** omówienie w hello **ZARZĄDZAJ** sekcji.

![Aplikacje dla przedsiębiorstw](./media/active-directory-reporting-migration/484.png "aplikacje dla przedsiębiorstw")

## <a name="access-a-specific-report"></a>Dostęp do określonego raportu

Mimo że hello portalu Azure oferuje pojedynczego widoku, także zapoznanie się z określonych raportów.

### <a name="audit-logs"></a>Dzienniki inspekcji

W odpowiedzi toocustomer opinii w hello portalu Azure, można użyć zaawansowanych filtrowania tooaccess hello żądane dane. Jest jeden filtr, można użyć *kategorii działań*, który wyświetla listę różnych typów hello działania logowania w usłudze Azure AD. toonarrow powoduje toowhat, którego szukasz, możesz wybrać kategorię.

Na przykład jeśli interesuje Cię tylko resetuje powiązane hasło usługi tooself działań, możesz wybrać hello **Samoobsługowe zarządzanie hasłami** kategorii. kategorie Hello, dostępne są oparte na powitania zasób, który użytkownik pracuje w.  

![Opcje kategorii na stronie dzienniki inspekcji filtru hello](./media/active-directory-reporting-migration/06.png "opcje kategorii na stronie dzienniki inspekcji filtru hello")

Kategorie działań:

- Katalog podstawowy
- Samoobsługowe zarządzanie hasłami
- Samoobsługowe zarządzanie grupami
- Aprowizacja kont

### <a name="application-usage"></a>Użycie aplikacji

tooview szczegółowe informacje dotyczące użycia aplikacji dla wszystkich aplikacji lub tylko jednej aplikacji w obszarze **działania**, wybierz pozycję **logowania**. wyniki hello toonarrow, można filtrować według nazwy użytkownika lub aplikacji.

![Filtr zdarzeń logowania strony](./media/active-directory-reporting-migration/07.png "strony filtr rejestrowania zdarzeń")

### <a name="security-reports"></a>Raporty dotyczące zabezpieczeń

#### <a name="azure-ad-anomalous-activity-reports"></a>Raporty nietypowe działanie usługi Azure AD

Zabezpieczeń nietypowe działania usługi Azure AD raportów z klasycznego portalu Azure hello zostać skonsolidowane tooprovide można z nich, widokiem centralnej. Ten widok przedstawia wszystkie zdarzenia związane z zabezpieczeniami ryzyka może wykrywać i raport dotyczący usługi Azure AD.

Witaj w poniższej tabeli wymieniono raporty dotyczące zabezpieczeń nietypowych działań hello Azure AD i odpowiednie typy zdarzeń ryzyko w hello portalu Azure.

| Raport nietypowych działań w usłudze Azure AD |  Typ zdarzenia ryzyka ochrony tożsamości|
| :--- | :--- |
| Użytkownicy z ujawnionymi poświadczeniami | Ujawnione poświadczenia |
| Nieregularne działania związane z logowaniem | Niemożliwa podróż tooatypical lokalizacji |
| Logowania z urządzeń, które mogą być zainfekowane | Logowania z zainfekowanych urządzeń|
| Logowania z nieznanych źródeł | Logowania z anonimowych adresów IP |
| Logowania z adresów IP związanych z podejrzanymi działaniami | Logowania z adresów IP związanych z podejrzanymi działaniami |
| - | Logowania z nieznanych lokalizacji |

Raporty powitania po zabezpieczeń nietypowe działania usługi Azure AD nie są uwzględniane jako zdarzenia ryzyka w hello portalu Azure:

* Logowania po wielokrotnych niepowodzeniach
* Logowania z wielu lokalizacji geograficznych

Te raporty są nadal dostępne w hello klasycznego portalu Azure, ale zostaną wycofane w czasie w przyszłości hello.

Aby uzyskać więcej informacji, zobacz [Zdarzenia o podwyższonym ryzyku w usłudze Azure Active Directory](active-directory-identity-protection-risk-events.md).  


#### <a name="detected-risk-events"></a>Zdarzenia wykrytego ryzyka

W portalu Azure hello, można dostęp do raportów o zdarzeniach wykryte zagrożenie na powitania **usługi Azure Active Directory** bloku, w obszarze **zabezpieczeń**. Zdarzenia wykrytego ryzyka są śledzone w hello następujące raporty:   

- Zagrożonych użytkowników
- Ryzykowne logowania

![Raporty dotyczące zabezpieczeń](./media/active-directory-reporting-migration/04.png "raporty dotyczące zabezpieczeń")

Aby uzyskać więcej informacji o raportach zabezpieczeń zobacz:

- [Użytkownicy ryzyka raport zabezpieczeń w portalu usługi Azure Active Directory hello](active-directory-reporting-security-user-at-risk.md)
- [Ryzykowne raportu logowania w portalu usługi Azure Active Directory hello](active-directory-reporting-security-risky-sign-ins.md)


## <a name="activity-reports-in-hello-azure-classic-portal-vs-hello-azure-portal"></a>Raporty dotyczące działań w hello klasycznego portalu Azure a hello portalu Azure

w tej sekcji tabela Hello zawiera listę istniejących raportów w hello klasycznego portalu Azure. Ponadto opisano, jak wprowadzasz hello tych samych informacji w hello portalu Azure.

tooview wszystkie inspekcja danych na powitania **usługi Azure Active Directory** bloku, w obszarze **działania**, przejdź zbyt**dzienniki inspekcji**.

![Dzienniki inspekcji](./media/active-directory-reporting-migration/61.png "Dzienniki inspekcji")

| klasyczny portal Azure                 | toofind w hello portalu Azure                                                         |
| ---                                  | ---                                                                        |
| Dzienniki inspekcji                           | Dla **kategorii działań**, wybierz pozycję **katalogu Core**.                       |
| Działania związane z resetowaniem haseł              | Aby uzyskać **kategorii działań**, wybierz pozycję **Samoobsługowe zarządzanie hasłami**. |
| Aktywność rejestracji resetowania haseł | Aby uzyskać **kategorii działań**, wybierz pozycję **Samoobsługowe zarządzanie hasłami**.     |
| Raport aktywności grup samoobsługi         | Aby uzyskać **kategorii działań**, wybierz pozycję **Samoobsługowe zarządzanie grupami**.        |
| Działanie aprowizacji kont        | Aby uzyskać **kategorii działań**, wybierz pozycję **Inicjowanie obsługi konta użytkownika**.         |
| Stan przerzucania hasła             | Aby uzyskać **kategorii działań**, wybierz pozycję **automatycznego przerzucania hasła aplikacji**.      |
| Błędy aprowizacji kont          | Aby uzyskać **kategorii działań**, wybierz pozycję **Inicjowanie obsługi konta użytkownika**.        |
| Zmiany nazwy grupy usługi Office 365         | Aby uzyskać **kategorii działań**, wybierz pozycję **Samoobsługowe zarządzanie hasłami**. Dla **typu zasobu działania**, wybierz pozycję **grupy**. Aby uzyskać **źródło działania**, wybierz pozycję **grup usługi Office 365**.|

tooview hello **użycia aplikacji** raportu na powitania **usługi Azure Active Directory** bloku, w obszarze **ZARZĄDZAJ**, wybierz pozycję **aplikacje dla przedsiębiorstw**, a następnie wybierz **logowania**.


![Raport logowania aplikacji przedsiębiorstwa](./media/active-directory-reporting-migration/199.png "raport logowania aplikacji przedsiębiorstwa")

## <a name="next-steps"></a>Następne kroki

Omówienie raportowania patrz hello [raportowania usługi Azure Active Directory](active-directory-reporting-azure-portal.md).
