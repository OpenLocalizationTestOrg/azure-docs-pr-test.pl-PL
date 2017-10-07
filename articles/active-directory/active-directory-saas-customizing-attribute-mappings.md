---
title: "aaaCustomizing mapowań atrybutów AD Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jakie mapowań atrybutów dla aplikacji SaaS w usłudze Azure Active Directory są, jak można je zmodyfikować tooaddress firmy wymaga."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 549e0b8c-87ce-4c9b-b487-b7bf0155dc77
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: markvi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 14db5303f06fc8df3b07a0a8b75713312e71bbfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="customizing-user-provisioning-attribute-mappings-for-saas-applications-in-azure-active-directory"></a>Dostosowywanie użytkownika udostępniania mapowań atrybutów dla aplikacji SaaS w usłudze Azure Active Directory
Microsoft Azure AD zapewnia obsługę aprowizacji aplikacji SaaS toothird firm, takie jak Salesforce, Google Apps i innych użytkowników. Jeśli masz użytkownika Inicjowanie obsługi administracyjnej dla aplikacji SaaS innych firm włączone hello portalu zarządzania Azure określa jego wartości atrybutów w postaci konfiguracji o nazwie "mapowanie atrybutu".

Brak zestawu wstępnie skonfigurowanych atrybutu mapowania między obiektami użytkownika usługi Azure AD i każda aplikacja SaaS użytkownika. Niektóre aplikacje zarządzania innych typów obiektów, takich jak grup ani kontaktów. <br> 
 Mapowanie atrybutów domyślne hello zgodnie z potrzebami biznesowymi tooyour można dostosować. Oznacza to, że możesz zmienić lub usunąć istniejące mapowania atrybutu lub utworzyć nowe mapowanie atrybutów.

W portalu hello Azure AD, możesz korzystać z tej funkcji, klikając **mapowania** Konfiguracja **inicjowania obsługi administracyjnej** w hello **Zarządzaj** części  **Aplikacja całościowa**.


![SalesForce][5] 

Kliknięcie przycisku **mapowania** konfiguracji, otwiera hello powiązane **mapowanie atrybutu** bloku.  
Brak mapowań atrybutów, które są wymagane przez toofunction aplikacji SaaS poprawnie. Dla wymaganych atrybutów hello **usunąć** funkcja jest niedostępna.


![SalesForce][6]  

W powyższym przykładzie hello, widać, że hello **Username** atrybutu zarządzanego obiektu w usłudze Salesforce jest wypełniana hello **userPrincipalName** wartość hello połączonego obiektu usługi Azure Active Directory.

Można dostosować istniejący **mapowań atrybutów** klikając mapowania. Spowoduje to otwarcie hello **atrybutu Edytuj** bloku.

![SalesForce][7]  


  

## <a name="understanding-attribute-mapping-types"></a>Opis atrybutu mapowania typów
Z mapowań atrybutów możesz kontrolować sposób atrybuty są wypełnione w aplikacji SaaS innych firm. Istnieją cztery typy innego mapowania obsługiwane:

* **Bezpośrednie** — atrybut target hello jest wypełniana hello wartości atrybutu hello połączonego obiektu w usłudze Azure AD.
* **Stała** — atrybut target hello jest wypełniana określony ciąg został określony.
* **Wyrażenie** — atrybut target hello jest wypełniana na podstawie wyniku hello wyrażenia przypominającej skryptu. 
  Aby uzyskać więcej informacji, zobacz [pisać wyrażenia potrzeby mapowań atrybutów w usłudze Azure Active Directory](active-directory-saas-writing-expressions-for-attribute-mappings.md).
* **Brak** — atrybut target hello zostanie pozostawiony bez modyfikacji. Jednak jeśli atrybut target hello jest kiedykolwiek puste, zostanie wprowadzony z wartością domyślną hello, który określisz.

Dodanie toothese cztery podstawowe atrybutu mapowania typów mapowania atrybutu niestandardowego obsługuje pojęcie hello opcjonalny **domyślne** przypisanie wartości. Przypisanie wartości domyślne Hello gwarantuje, że atrybut docelowy jest wypełniana wartości, które nie istnieje żadna wartość w usłudze Azure AD, ani na obiekcie docelowym hello. najbardziej typowe konfiguracje Hello jest tooleave tym puste.


## <a name="understanding-attribute-mapping-properties"></a>Opis właściwości Mapowanie atrybutów

W poprzedniej sekcji hello zostały już wprowadzone toohello atrybutu mapowania typu właściwości.
We właściwości toothis dodanie mapowań atrybutów obsługują hello następujące atrybuty:

- **Atrybut źródłowy** -hello atrybut użytkownika z systemu źródłowego hello (np.: Azure Active Directory).
- **Atrybut TARGET** — Witaj atrybut użytkownika w systemie docelowym hello (np.: ServiceNow).
- **Zgodne obiektów przy użyciu tego atrybutu** — czy stosuje się to mapowanie toouniquely zidentyfikować użytkowników między systemami hello źródłowym i docelowym. To jest zwykle ustawiana na powitania userPrincipalName lub atrybut poczty w usłudze Azure AD, która jest zwykle mapowane tooa pole nazwy użytkownika w aplikacji docelowej.
- **Dopasowywanie pierwszeństwo** — wiele pasujących atrybuty można ustawić. Jeśli dostępnych jest wiele, są oceniane pod w kolejności hello wynika z tego pola. Jak dopasowania zostanie znaleziony, żadne dodatkowe dopasowania atrybuty są oceniane.
- **Zastosuj to mapowanie**
    - **Zawsze** — Zastosuj to mapowanie na obu Tworzenie użytkownika i aktualizowanie akcji
    - **Tylko podczas tworzenia** -Zastosuj to mapowanie tylko akcje creation użytkownika


## <a name="what-you-should-know"></a>Co należy wiedzieć

Microsoft Azure AD zapewnia wydajne wykonania procesu synchronizacji. W środowisku zainicjowana tylko obiekty wymagające aktualizacji są przetwarzane podczas cyklu synchronizacji. Aktualizowanie mapowań atrybutów ma wpływ na wydajność hello cyklu synchronizacji. Konfiguracja mapowania atrybutu toohello aktualizacji wymaga wszystkich toobe zarządzanych obiektów ponownie oceniane. Jest zalecane najlepsze praktyki tookeep hello wiele mapowań atrybutów tooyour kolejne zmiany w co najmniej.

## <a name="next-steps"></a>Następne kroki

* [Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory](active-directory-apps-index.md)
* [Automatyzowanie inicjowania obsługi administracyjnej użytkowników/anulowania zastrzeżenia tooSaaS aplikacji](active-directory-saas-app-provisioning.md)
* [Tworzenie wyrażeń na potrzeby mapowań atrybutów](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [Filtry zakresu dla Inicjowanie obsługi użytkowników](active-directory-saas-scoping-filters.md)
* [Przy użyciu SCIM tooenable automatyczne Inicjowanie obsługi użytkowników i grup z usługi Azure Active Directory tooapplications](active-directory-scim-provisioning.md)
* [Powiadomienia aprowizacji kont](active-directory-saas-account-provisioning-notifications.md)
* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-customizing-attribute-mappings/ic765497.png
[2]: ./media/active-directory-saas-customizing-attribute-mappings/ic775419.png
[3]: ./media/active-directory-saas-customizing-attribute-mappings/ic775420.png
[4]: ./media/active-directory-saas-customizing-attribute-mappings/ic775421.png
[5]: ./media/active-directory-saas-customizing-attribute-mappings/21.png
[6]: ./media/active-directory-saas-customizing-attribute-mappings/22.png
[7]: ./media/active-directory-saas-customizing-attribute-mappings/23.png

