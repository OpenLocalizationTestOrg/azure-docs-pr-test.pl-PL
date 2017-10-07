---
title: "aaaAutomated SaaS aplikacji Inicjowanie obsługi użytkowników w usłudze Azure AD | Dokumentacja firmy Microsoft"
description: "Toohow wprowadzenie przepisu tooautomatically usługi Azure AD, można użyć anulować aprowizację i aktualizowane na bieżąco kont użytkowników dla wielu aplikacji SaaS innych firm."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 58c5fa2d-bb33-4fba-8742-4441adf2cb62
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: curtand
ms.openlocfilehash: a1f3ecdd513e2b603f8ad9901e9f551b3b982b2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="automate-user-provisioning-and-deprovisioning-toosaas-applications-with-azure-active-directory"></a>Automatyzowanie użytkownika alokowania i anulowania alokowania tooSaaS aplikacji w usłudze Azure Active Directory
## <a name="what-is-automated-user-provisioning-for-saas-apps"></a>Co to jest automatyczne Inicjowanie obsługi użytkowników dla aplikacji SaaS?
Azure Active Directory (Azure AD) pozwala tooautomate hello tworzenia, obsługi i usuwania tożsamości użytkowników w chmurze ([SaaS](https://azure.microsoft.com/overview/what-is-saas/)) aplikacji, takich jak Dropbox, Salesforce, ServiceNow i inne.

**Poniżej przedstawiono kilka przykładów co ta funkcja pozwala toodo:**

* Automatycznie Utwórz nowych kont w hello prawo aplikacji SaaS dla nowych użytkowników w celu dołączenia zespołu.
* Automatycznie dezaktywuj konta z aplikacji SaaS w przypadku osób natychmiastową pozostawia hello zespołu.
* Upewnij się, że się toodate na podstawie zmian w katalogu hello są przechowywane tożsamości hello w aplikacji SaaS.
* Udostępnianie obiektów nienależących do użytkownika, takich jak grupy, tooSaaS aplikacje, które je obsługują.

**Inicjowanie obsługi użytkowników automatycznych zawiera również hello następujące funkcje:**

* Witaj możliwości toomatch istniejącej tożsamości między usługą Azure AD i aplikacji SaaS.
* Bieżące konfiguracje hello hello aplikacji SaaS, które organizacja korzysta obecnie mieści się toohelp opcje dostosowywania usługi Azure AD.
* Opcjonalne wiadomości e-mail dla alertów do inicjowania obsługi błędów.
* Raportowanie i działania toohelp dzienniki z monitorowania i rozwiązywania problemów.

## <a name="why-use-automated-provisioning"></a>Dlaczego warto używać automatyczne Inicjowanie obsługi?
Niektóre typowe motywacji dla tej funkcji obejmują:

* koszty hello tooavoid, wydajność i błędu ludzkiego związanego z ręcznego inicjowania obsługi procesów.
* toosecure organizacji przez natychmiastowe usunięcie tożsamości użytkowników z klucza aplikacji SaaS, gdy opuszczą hello organizacji.
* tooeasily importowania zbiorczego liczbę użytkowników do określonej aplikacji SaaS.
* tooenjoy hello wygodą dostępności rozwiązania inicjowania obsługi administracyjnej uruchomić wylogowuje hello tych samych zasad dostępu do aplikacji, zdefiniowane dla usługi Azure AD rejestracji jednokrotnej.

## <a name="frequently-asked-questions"></a>Często zadawane pytania
**Jak często usługi Azure AD pisanie aplikacji SaaS toohello zmiany katalogu?**

Usługi Azure AD sprawdza obecność zmian co pięć minut tooten. Jeśli aplikacja SaaS hello zwraca kilka błędów (np. wielkość liter hello poświadczeń administratora nieprawidłowy), następnie usługi Azure AD stopniowo spowolni jego częstotliwość tooonce tooup dziennie, dopóki błędy hello są stałe.

**Jak długo trwa tooprovision moich użytkowników?**

Ale jeśli próbujesz tooprovision niemal natychmiast wprowadzenia zmiany przyrostowe większości katalogu, a następnie zależy od hello liczbę użytkowników i grup, do których masz. Katalogi małych zająć tylko kilka minut, średnie katalogów może potrwać kilka minut i bardzo dużych katalogów może potrwać kilka godzin.

**Jak można śledzić postęp hello hello bieżące zadanie inicjowania obsługi administracyjnej**

Możesz przejrzeć hello raportu Inicjowanie obsługi konta w sekcji raportów hello katalogu. Inną opcją jest karty Pulpit nawigacyjny hello toovisit dla aplikacji SaaS, które w przypadku udostępniania hello i sprawdź w obszarze hello sekcji "Integracja stanu" dolnej hello hello strony.

**Jak wiedzą, jeśli użytkownicy nie tooget udostępniane poprawnie?**

Na końcu hello hello inicjowania obsługi administracyjnej Kreator konfiguracji jest opcja toosubscribe tooemail powiadomienia do inicjowania obsługi błędów. Możesz również sprawdzić hello toosee raportu błędów inicjowania obsługi użytkowników, którzy nie powiodło się toobe elastycznie i dlaczego.

**Można usługi Azure AD Zapisz zmiany z katalogu zapasowego toohello aplikacji SaaS hello**

Dla większości aplikacji SaaS Inicjowanie obsługi administracyjnej jest wychodzący tylko, które oznacza, że użytkownicy są zapisywane z hello katalogu toohello aplikacji, a zmiany z aplikacji hello nie można zapisać zwrotnie toohello katalogu. Aby uzyskać [produktu Workday](https://msdn.microsoft.com/library/azure/dn762434.aspx), jednak inicjowania obsługi administracyjnej jest ruchu przychodzącego — tylko, co oznacza, że aby użytkownicy byli zaimportowane do katalogu hello z produktu Workday i podobnie, zmiany w katalogu hello nie pobrać zapisywane do produktu Workday.

**Jak można przesłać zespołu inżynieryjnego toohello opinii?**

Skontaktuj się z nami za pośrednictwem hello [forum opinii w usłudze Azure Active Directory](https://feedback.azure.com/forums/169401-azure-active-directory/).

## <a name="how-does-automated-provisioning-work"></a>Jak działa automatycznego inicjowania obsługi administracyjnej?
Usługi Azure AD obsługuje aplikacje tooSaaS użytkowników łącząc punkty końcowe tooprovisioning dostarczanych przez dostawcę każdej aplikacji. Zezwalaj na te punkty końcowe usługi Azure AD tooprogrammatically tworzyć, aktualizować i usuwać użytkowników. Poniżej znajduje się krótki przegląd hello wykonania różnych kroków, że usługi Azure AD ma tooautomate inicjowania obsługi administracyjnej.

1. Po włączeniu udostępniania aplikacji dla powitania po raz pierwszy, wykonywane są następujące akcje hello:
   * Usługi Azure AD będzie podejmować toomatch istniejących użytkowników w aplikacji SaaS hello z ich odpowiednich tożsamościami w katalogu hello. Po dopasowaniu użytkownika, są one *nie* automatycznie włączone dla rejestracji jednokrotnej. Aby aplikację toohello użytkownika toohave dostępu ich musi mieć jawnie przypisanej toohello aplikacji w usłudze Azure AD, bezpośrednio lub za pośrednictwem członkostwa w grupie.
   * Jeśli został już określony użytkowników, którzy powinni należeć toohello aplikacji i usługi Azure AD nie powiedzie się toofind istniejących kont dla tych użytkowników, usługi Azure AD udostępnić nowe konta dla nich w aplikacji hello.
2. Po ukończeniu synchronizacji początkowej hello, jak opisano powyżej, usługi Azure AD będzie sprawdzać co 10 minut na powitania następujące zmiany:
   * Jeśli nowych użytkowników zostały przypisane toohello aplikacji (bezpośrednio lub za pośrednictwem członkostwa w grupie), a następnie zostaną one udostępnione nowe konto hello aplikacji SaaS.
   * Jeśli usunięto dostępu użytkownika, a następnie swojego konta w aplikacji SaaS hello zostaną oznaczone jako wyłączone (użytkownicy nigdy nie pełni usunięciu, która zabezpiecza przed utratą danych w przypadku hello błędnej konfiguracji).
   * Jeśli użytkownik niedawno został przypisany toohello aplikacji i ich już konto w hello aplikacji SaaS, konto zostanie oznaczony jako włączone, czy niektóre właściwości użytkownika mogą być aktualizowane, jeśli są nieaktualne w porównaniu toohello katalogu.
   * Jeśli informacje o użytkowniku (takie jak numer telefonu, oddział itp.) została zmieniona w katalogu hello, te informacje będzie można także zaktualizować w hello aplikacji SaaS.

Aby uzyskać więcej informacji o sposobie mapowania atrybutów między usługą Azure AD i aplikacji SaaS, zobacz artykuł hello na [Dostosowywanie mapowań atrybutów](active-directory-saas-customizing-attribute-mappings.md).

## <a name="list-of-apps-that-support-automated-user-provisioning"></a>Lista aplikacji, które obsługują automatyczne Inicjowanie obsługi użytkowników
Wszystkie aplikacje "Proponowanym" hello w galerii aplikacji usługi Azure AD hello obsługę automatycznych użytkownika. [w tym miejscu można wyświetlić listy Hello polecane aplikacje.](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps?page=1&subcategories=featured)

Aby aplikacja toosupport automatycznego przypisywania użytkowników należy najpierw ona hello niezbędne punkty końcowe, które umożliwiają tworzenie hello tooautomate programów zewnętrznych, obsługi i usuwania użytkowników. W związku z tym nie wszystkie aplikacje SaaS są zgodne z tą funkcją. Dla aplikacji, które obsługują to zespołu inżynieryjnego hello Azure AD zostanie następnie toobuild stanie inicjowania obsługi administracyjnej toothose łącznika aplikacji, i tej pracy jest priorytety według potrzeb hello aktualnych i potencjalnych klientów.

engineering hello Azure AD toocontact zespołu toorequest obsługę dodatkowych aplikacji do udostępniania, Prześlij komunikatu za pośrednictwem hello [forum opinii w usłudze Azure Active Directory](https://feedback.azure.com/forums/374982-azure-active-directory-application-requests/category/172035-user-provisioning).

## <a name="related-articles"></a>Pokrewne artykuły
* [Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory](active-directory-apps-index.md)
* [Dostosowywanie mapowań atrybutów do inicjowania obsługi użytkowników](active-directory-saas-customizing-attribute-mappings.md)
* [Tworzenie wyrażeń na potrzeby mapowań atrybutów](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [Filtry zakresu dla Inicjowanie obsługi użytkowników](active-directory-saas-scoping-filters.md)
* [Przy użyciu SCIM tooenable automatyczne Inicjowanie obsługi użytkowników i grup z usługi Azure Active Directory tooapplications](active-directory-scim-provisioning.md)
* [Powiadomienia aprowizacji kont](active-directory-saas-account-provisioning-notifications.md)
* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS](active-directory-saas-tutorial-list.md)

