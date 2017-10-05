---
title: "Znajdź raporty dotyczące działań w portalu Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak znaleźć raporty działania usługi Azure Active Directory w portalu Azure."
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
ms.openlocfilehash: f1875582476c3817b9eb0082b6548cc15043cb98
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="find-activity-reports-in-the-azure-portal"></a>Znajdź raporty dotyczące działań w portalu Azure

Jeśli przenosisz z klasycznego portalu Azure w portalu Azure, możesz uzyskać wygląda na dzienniki aktywności w usłudze Azure Active Directory (Azure AD). W ostatnie [wpis w blogu](https://blogs.technet.microsoft.com/enterprisemobility/2016/11/08/azuread-weve-just-turned-on-detailed-auditing-and-sign-in-logs-in-the-new-azure-portal/), możemy wyjaśniają, jak widać, dzienniki aktywności w kontekście zasobów pracuje w portalu Azure. W tym artykule opisano firma Microsoft, jak można znaleźć raporty, które były używane w klasycznym portalu Azure w portalu Azure.

## <a name="whats-new"></a>Co nowego

Raporty w klasycznym portalu Azure są podzielone na kategorie:

1.  Raporty dotyczące zabezpieczeń
2.  Raporty dotyczące działań
3.  Raporty zintegrowanych aplikacji

### <a name="activity-and-integrated-app-reports"></a>Działanie i raporty zintegrowanych aplikacji

Kontekstowa raportowanie w portalu Azure, istniejących raportów są scalane w ramach jednego widoku. Jeden podstawowy interfejs API udostępnia dane do widoku.

Do wyświetlenia tego widoku na **usługi Azure Active Directory** bloku, w obszarze **działania**, wybierz pozycję **dzienniki inspekcji**.

![Dzienniki inspekcji](./media/active-directory-reporting-migration/482.png "Dzienniki inspekcji")

Następujące raporty są konsolidowane w tym widoku:

-   Raport dotyczący inspekcji
-   Działania związane z resetowaniem haseł
-   Aktywność rejestracji resetowania haseł
-   Raport aktywności grup samoobsługi
-   Zmiany nazwy grupy usługi Office 365
-   Działanie aprowizacji kont
-   Stan przerzucania hasła
-   Błędy aprowizacji kont


Raport użycia aplikacji zostały rozszerzone i znajduje się w **logowania** widoku. Aby wyświetlić ten widok na **usługi Azure Active Directory** bloku, w obszarze **działania**, wybierz pozycję **logowania**.

![Widok logowania](./media/active-directory-reporting-migration/483.png "wyświetlić logowania")

**Logowania** widok zawiera sesje logowania użytkownika. Aby uzyskać informacje na temat wykorzystania aplikacji, można użyć tych informacji. Możesz również przeglądać informacje użycia aplikacji w **aplikacje dla przedsiębiorstw** omówienie w **ZARZĄDZAJ** sekcji.

![Aplikacje dla przedsiębiorstw](./media/active-directory-reporting-migration/484.png "aplikacje dla przedsiębiorstw")

## <a name="access-a-specific-report"></a>Dostęp do określonego raportu

Mimo że portalu Azure oferuje pojedynczego widoku, także zapoznanie się z określonych raportów.

### <a name="audit-logs"></a>Dzienniki inspekcji

W odpowiedzi na opinie klientów, w portalu Azure możesz użyć filtrowania zaawansowanego dostępu do danych, które mają. Jest jeden filtr, można użyć *kategorii działań*, który zawiera różne typy aktywności logowania w usłudze Azure AD. Aby ograniczyć wyniki do czego szukasz, możesz wybrać kategorię.

Na przykład, jeśli interesuje Cię tylko działania związane z resetowanie haseł samoobsługi, można wybierać **Samoobsługowe zarządzanie hasłami** kategorii. Kategorie dostępne są oparte na zasób, do którego użytkownik pracuje w.  

![Na stronie dzienniki inspekcji filtr kategorii opcje](./media/active-directory-reporting-migration/06.png "opcje kategorii na stronie dzienniki inspekcji filtru")

Kategorie działań:

- Katalog podstawowy
- Samoobsługowe zarządzanie hasłami
- Samoobsługowe zarządzanie grupami
- Aprowizacja kont

### <a name="application-usage"></a>Użycie aplikacji

Aby wyświetlić szczegóły dotyczące użycia aplikacji dla wszystkich aplikacji lub tylko jednej aplikacji w obszarze **działania**, wybierz pozycję **logowania**. Aby zawęzić wyniki, można filtrować według nazwy użytkownika lub aplikacji.

![Filtr zdarzeń logowania strony](./media/active-directory-reporting-migration/07.png "strony filtr rejestrowania zdarzeń")

### <a name="security-reports"></a>Raporty dotyczące zabezpieczeń

#### <a name="azure-ad-anomalous-activity-reports"></a>Raporty nietypowe działanie usługi Azure AD

Azure AD nietypowego działania zabezpieczeń raportów z klasycznego portalu Azure zostały skonsolidowane dostarczają jeden, widok centralnej. Ten widok przedstawia wszystkie zdarzenia związane z zabezpieczeniami ryzyka może wykrywać i raport dotyczący usługi Azure AD.

Następujące tabeli list programu Azure AD nietypowego działania zabezpieczeń raportów i odpowiednie typy zdarzeń ryzyko w portalu Azure.

| Raport nietypowych działań w usłudze Azure AD |  Typ zdarzenia ryzyka ochrony tożsamości|
| :--- | :--- |
| Użytkownicy z ujawnionymi poświadczeniami | Ujawnione poświadczenia |
| Nieregularne działania związane z logowaniem | Niemożliwa podróż do nietypowych lokalizacji |
| Logowania z urządzeń, które mogą być zainfekowane | Logowania z zainfekowanych urządzeń|
| Logowania z nieznanych źródeł | Logowania z anonimowych adresów IP |
| Logowania z adresów IP związanych z podejrzanymi działaniami | Logowania z adresów IP związanych z podejrzanymi działaniami |
| - | Logowania z nieznanych lokalizacji |

Następujące zabezpieczeń usługi Azure AD w nietypowych działań raporty nie są uwzględniane jako zdarzenia ryzyka w portalu Azure:

* Logowania po wielokrotnych niepowodzeniach
* Logowania z wielu lokalizacji geograficznych

Te raporty są nadal dostępne w klasycznym portalu Azure, ale zostaną wycofane w czasie w przyszłości.

Aby uzyskać więcej informacji, zobacz [Zdarzenia o podwyższonym ryzyku w usłudze Azure Active Directory](active-directory-identity-protection-risk-events.md).  


#### <a name="detected-risk-events"></a>Zdarzenia wykrytego ryzyka

W portalu Azure, możesz mogą uzyskiwać dostęp do raportów o zdarzeniach wykryte zagrożenie **usługi Azure Active Directory** bloku, w obszarze **zabezpieczeń**. Zdarzenia wykrytego ryzyka są śledzone w następujące raporty:   

- Zagrożonych użytkowników
- Ryzykowne logowania

![Raporty dotyczące zabezpieczeń](./media/active-directory-reporting-migration/04.png "raporty dotyczące zabezpieczeń")

Aby uzyskać więcej informacji o raportach zabezpieczeń zobacz:

- [Użytkownicy ryzyka raport zabezpieczeń w portalu usługi Azure Active Directory](active-directory-reporting-security-user-at-risk.md)
- [Ryzykowne raportu logowania w portalu usługi Azure Active Directory](active-directory-reporting-security-risky-sign-ins.md)


## <a name="activity-reports-in-the-azure-classic-portal-vs-the-azure-portal"></a>Raporty dotyczące działań w klasycznym portalu Azure, a portalu Azure

W tej sekcji tabela zawiera listę istniejących raportów w klasycznym portalu Azure. Opisuje również, jak te same informacje można uzyskać w portalu Azure.

Aby wyświetlić wszystkich danych inspekcji, na **usługi Azure Active Directory** bloku, w obszarze **działania**, przejdź do **dzienniki inspekcji**.

![Dzienniki inspekcji](./media/active-directory-reporting-migration/61.png "Dzienniki inspekcji")

| klasyczny portal Azure                 | Aby znaleźć w portalu Azure                                                         |
| ---                                  | ---                                                                        |
| Dzienniki inspekcji                           | Dla **kategorii działań**, wybierz pozycję **katalogu Core**.                       |
| Działania związane z resetowaniem haseł              | Aby uzyskać **kategorii działań**, wybierz pozycję **Samoobsługowe zarządzanie hasłami**. |
| Aktywność rejestracji resetowania haseł | Aby uzyskać **kategorii działań**, wybierz pozycję **Samoobsługowe zarządzanie hasłami**.     |
| Raport aktywności grup samoobsługi         | Aby uzyskać **kategorii działań**, wybierz pozycję **Samoobsługowe zarządzanie grupami**.        |
| Działanie aprowizacji kont        | Aby uzyskać **kategorii działań**, wybierz pozycję **Inicjowanie obsługi konta użytkownika**.         |
| Stan przerzucania hasła             | Aby uzyskać **kategorii działań**, wybierz pozycję **automatycznego przerzucania hasła aplikacji**.      |
| Błędy aprowizacji kont          | Aby uzyskać **kategorii działań**, wybierz pozycję **Inicjowanie obsługi konta użytkownika**.        |
| Zmiany nazwy grupy usługi Office 365         | Aby uzyskać **kategorii działań**, wybierz pozycję **Samoobsługowe zarządzanie hasłami**. Dla **typu zasobu działania**, wybierz pozycję **grupy**. Aby uzyskać **źródło działania**, wybierz pozycję **grup usługi Office 365**.|

Aby wyświetlić **użycia aplikacji** raportu na **usługi Azure Active Directory** bloku, w obszarze **ZARZĄDZAJ**, wybierz pozycję **aplikacje dla przedsiębiorstw**, a następnie wybierz **logowania**.


![Raport logowania aplikacji przedsiębiorstwa](./media/active-directory-reporting-migration/199.png "raport logowania aplikacji przedsiębiorstwa")

## <a name="next-steps"></a>Następne kroki

Omówienie funkcji raportowania można znaleźć w temacie [Raporty w usłudze Azure Active Directory](active-directory-reporting-azure-portal.md).
