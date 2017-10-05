---
title: "Automatyczne inicjowanie obsługi użytkowników aplikacji SaaS w usłudze Azure AD | Dokumentacja firmy Microsoft"
description: "Wprowadzenie do wykorzystania usługi Azure AD można automatycznie udostępnić, usuwanie i aktualizowane na bieżąco kont użytkowników dla wielu aplikacji SaaS innych firm."
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
ms.openlocfilehash: 7cb780117d64d67449146b9757f8162e23e65d1e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="automate-user-provisioning-and-deprovisioning-to-saas-applications-with-azure-active-directory"></a>Automatyzowanie użytkownika alokowania i anulowania alokowania do aplikacji SaaS w usłudze Azure Active Directory
## <a name="what-is-automated-user-provisioning-for-saas-apps"></a>Co to jest automatyczne Inicjowanie obsługi użytkowników dla aplikacji SaaS?
Azure Active Directory (Azure AD) pozwala na automatyzację tworzenia, obsługi i usuwania tożsamości użytkowników w chmurze ([SaaS](https://azure.microsoft.com/overview/what-is-saas/)) aplikacji, takich jak Dropbox, Salesforce, ServiceNow i inne.

**Poniżej przedstawiono kilka przykładów co ta funkcja umożliwia:**

* Automatycznie Utwórz nowych kont w prawo aplikacji SaaS dla nowych użytkowników w celu dołączenia zespołu.
* Automatycznie dezaktywuj konta z aplikacji SaaS w przypadku osób natychmiastową pozostawia zespołu.
* Upewnij się, że tożsamości w aplikacji SaaS są aktualizowane na podstawie zmian w katalogu.
* Udostępnianie obiektów nienależących do użytkownika, takich jak grupy, do aplikacji SaaS, które je obsługują.

**Inicjowanie obsługi użytkowników automatycznych zawiera również następujące funkcje:**

* Możliwość odpowiada tożsamościom istniejących między usługą Azure AD i aplikacji SaaS.
* Bieżące konfiguracje aplikacji SaaS, które organizacja korzysta obecnie mieści się w opcji dostosowania do pomocy usługi Azure AD.
* Opcjonalne wiadomości e-mail dla alertów do inicjowania obsługi błędów.
* Dzienniki raportowania i działania do monitorowania i rozwiązywania problemów.

## <a name="why-use-automated-provisioning"></a>Dlaczego warto używać automatyczne Inicjowanie obsługi?
Niektóre typowe motywacji dla tej funkcji obejmują:

* Aby uniknąć kosztów, wydajność i błędu ludzkiego związanego z ręcznego inicjowania obsługi procesów.
* W celu zabezpieczenia organizacji natychmiastowe usunięcie tożsamości użytkowników z klucza aplikacji SaaS w przypadku opuszczenia organizacji.
* Aby łatwo importować zbiorczego liczbę użytkowników do określonej aplikacji SaaS.
* Aby korzystać z wygodą dostępności rozwiązania inicjowania obsługi administracyjnej uruchomić się te same zasady dostępu do aplikacji, zdefiniowane dla usługi Azure AD rejestracji jednokrotnej.

## <a name="frequently-asked-questions"></a>Często zadawane pytania
**Jak często usługi Azure AD Zapisz zmiany katalogu do aplikacji SaaS?**

Usługi Azure AD sprawdza obecność zmian co pięciu do dziesięciu minut. Jeśli aplikacja SaaS zwraca kilka błędów, (na przykład w przypadku poświadczeń administratora nieprawidłowy), w usłudze Azure AD spowoduje stopniowo spowolnienie jego częstotliwość maksymalnie raz dziennie, dopóki nie zostaną one usunięte.

**Jak długo trwa udostępnianie moich użytkowników?**

Zmiany przyrostowe zmienione niemal natychmiast, ale jeśli chcesz udostępnić większość katalogu, następnie zależy od liczby użytkowników i grup, do których masz. Katalogi małych zająć tylko kilka minut, średnie katalogów może potrwać kilka minut i bardzo dużych katalogów może potrwać kilka godzin.

**Jak można śledzić postęp bieżącego zadania inicjowania obsługi administracyjnej**

Możesz przejrzeć raportu Inicjowanie obsługi konta w sekcji raportów w katalogu. Inną możliwością jest wykonanie odwiedź karty Pulpit nawigacyjny dla aplikacji SaaS, które są inicjowania obsługi administracyjnej i poszukaj w sekcji "Integracja stan" w dolnej części strony.

**Jak wiedzą, jeśli użytkownicy nie mogą pobrać udostępniane poprawnie?**

Po zakończeniu inicjowania obsługi administracyjnej konfiguracji kreatora jest dostępna opcja subskrybować powiadomienia e-mail w celu obsługi błędów. Możesz również sprawdzić raportu błędów inicjowania obsługi administracyjnej, aby wyświetlić użytkowników, którzy nie można zainicjować obsługi administracyjnej i dlaczego.

**Można usługi Azure AD zapisywać zmiany z poziomu aplikacji SaaS do katalogu?**

Dla większości aplikacji SaaS Inicjowanie obsługi administracyjnej jest wychodzący tylko, co oznacza, że użytkownicy są zapisywane w katalogu aplikacji, a zmiany z aplikacji nie można zapisać zwrotnie katalogu. Aby uzyskać [produktu Workday](https://msdn.microsoft.com/library/azure/dn762434.aspx), jednak inicjowania obsługi administracyjnej jest ruchu przychodzącego — tylko, co oznacza, że aby użytkownicy byli zaimportowane do katalogu z produktu Workday i podobnie, zmiany w katalogu nie pobrać zapisywane do produktu Workday.

**Jak przesłać opinię do zespołu inżynieryjnego**

Skontaktuj się z nami za pośrednictwem [forum opinii w usłudze Azure Active Directory](https://feedback.azure.com/forums/169401-azure-active-directory/).

## <a name="how-does-automated-provisioning-work"></a>Jak działa automatycznego inicjowania obsługi administracyjnej?
Usługi Azure AD udostępnia użytkownikom aplikacji SaaS przez nawiązanie połączenia udostępniania punktów końcowych dostarczanych przez dostawcę każdej aplikacji. Te punkty końcowe umożliwiają usługi Azure AD, można programowo tworzyć, aktualizować i usuwać użytkowników. Poniżej znajduje się krótki przegląd różnych działań, które usługi Azure AD umożliwia automatyzację inicjowania obsługi.

1. Po włączeniu udostępniania dla aplikacji po raz pierwszy, są wykonywane następujące czynności:
   * Usługi Azure AD będzie podejmować próby odpowiada żadnych istniejących użytkowników w aplikacji SaaS, ich odpowiednich tożsamości w katalogu. Po dopasowaniu użytkownika, są one *nie* automatycznie włączone dla rejestracji jednokrotnej. Aby użytkownik miał dostęp do aplikacji ich musi mieć jawnie przypisanej do aplikacji w usłudze Azure AD, bezpośrednio lub za pośrednictwem członkostwa w grupie.
   * Jeśli został już określony użytkowników, którzy powinny zostać przypisane do aplikacji i nie może odnaleźć istniejących kont dla tych użytkowników usługi Azure AD, Azure AD udostępnić nowych kont dla nich w aplikacji.
2. Po ukończeniu synchronizacji początkowej, jak opisano powyżej, usługi Azure AD będzie sprawdzać co 10 minut dla następujących zmian:
   * Jeśli nowych użytkowników zostały przypisane do aplikacji (bezpośrednio lub za pośrednictwem członkostwa w grupie), następnie będzie można zainicjować obsługi administracyjnej nowych kont w aplikacji SaaS.
   * Jeśli usunięto dostępu użytkownika, a następnie swojego konta w aplikacji SaaS zostaną oznaczone jako wyłączone (użytkownicy nigdy nie pełni usunięciu, który chroni przed utratą danych w przypadku błędnej konfiguracji).
   * Jeśli użytkownik niedawno został przypisany do aplikacji i już swoje konto w aplikacji SaaS, tego konta zostanie oznaczony jako włączone, a niektóre właściwości użytkownika mogą być aktualizowane, jeśli są nieaktualne w porównaniu do katalogu.
   * Jeśli informacje o użytkowniku (takie jak numer telefonu, oddział itp.) została zmieniona w katalogu, a następnie te informacje będą aktualizowane również w aplikacji SaaS.

Aby uzyskać więcej informacji o sposobie mapowania atrybutów między usługą Azure AD i aplikacji SaaS, zapoznaj się z artykułem na [Dostosowywanie mapowań atrybutów](active-directory-saas-customizing-attribute-mappings.md).

## <a name="list-of-apps-that-support-automated-user-provisioning"></a>Lista aplikacji, które obsługują automatyczne Inicjowanie obsługi użytkowników
Wszystkie aplikacje "Proponowanym" w galerii aplikacji usługi Azure AD obsługuje użytkownika automatycznego inicjowania obsługi administracyjnej. [W tym miejscu można wyświetlić listę polecanych aplikacji.](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps?page=1&subcategories=featured)

Aby aplikacja do obsługi użytkowników automatycznego inicjowania obsługi administracyjnej on zawierał niezbędne punkty końcowe, które umożliwiają automatyzację tworzenia, obsługi i usuwania użytkowników zewnętrznych programy. W związku z tym nie wszystkie aplikacje SaaS są zgodne z tą funkcją. W przypadku aplikacji, które obsługują to zespołu inżynieryjnego usługi Azure AD będą w stanie Tworzenie łącznika inicjowania obsługi administracyjnej do tych aplikacji, a tej pracy jest priorytety zgodnie z potrzebami aktualnych i potencjalnych klientów.

Aby skontaktuj się z usługą Azure AD engineering team do żądania obsługi inicjowania obsługi administracyjnej dodatkowych aplikacji, Prześlij komunikatu za pośrednictwem [forum opinii w usłudze Azure Active Directory](https://feedback.azure.com/forums/374982-azure-active-directory-application-requests/category/172035-user-provisioning).

## <a name="related-articles"></a>Pokrewne artykuły
* [Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory](active-directory-apps-index.md)
* [Dostosowywanie mapowań atrybutów do inicjowania obsługi użytkowników](active-directory-saas-customizing-attribute-mappings.md)
* [Tworzenie wyrażeń na potrzeby mapowań atrybutów](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [Filtry zakresu dla Inicjowanie obsługi użytkowników](active-directory-saas-scoping-filters.md)
* [Włączanie automatycznej aprowizacji użytkowników i grup z usługi Azure Active Directory do aplikacji przy użyciu SCIM](active-directory-scim-provisioning.md)
* [Powiadomienia aprowizacji kont](active-directory-saas-account-provisioning-notifications.md)
* [Lista samouczków dotyczących sposobów integracji aplikacji SaaS](active-directory-saas-tutorial-list.md)

