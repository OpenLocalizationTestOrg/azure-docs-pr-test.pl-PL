---
title: "Konfigurowanie samoobsługowego zarządzania dostępem do aplikacji w usłudze Azure Active Directory | Microsoft Docs"
description: "Tworzenie grup zabezpieczeń lub grup Office 365 w usłudze Azure Active Directory oraz zarządzanie nimi i żądanie członkostwa w grupach zabezpieczeń lub grupach usługi Office 365"
services: active-directory
documentationcenter: 
author: curtand
manager: mtillman
editor: 
ms.assetid: 904d5c70-c34a-46c4-a9a7-d1efecf4821c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 09/07/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 4798c9f9b289f8fa089498398079565c35ccdd2a
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/11/2017
---
# <a name="set-up-azure-active-directory-for-self-service-group-management"></a>Konfigurowanie usługi Azure Active Directory do samoobsługowego zarządzania grupami
W usłudze Azure Active Directory (Azure AD) użytkownicy mogą tworzyć swoje własne grupy zabezpieczeń lub grupy usługi Office 365 oraz zarządzać nimi. Użytkownicy mogą również żądać członkostwa w grupie zabezpieczeń lub grupie Office 365, a następnie właściciel grupy może zatwierdzić członkostwo lub odmówić jego przypisania. Codzienne zarządzanie członkostwem w grupach można przekazać osobom znającym kontekst biznesowy tego członkostwa. Funkcje samoobsługowego zarządzania grupami są dostępne wyłącznie w przypadku grup zabezpieczeń i grup Office 365, natomiast nie są dostępne w przypadku list dystrybucyjnych lub grup zabezpieczeń z włączoną obsługą poczty.

Samoobsługowe zarządzanie grupami aktualnie obsługuje dwa podstawowe scenariusze: delegowane zarządzanie grupami i samoobsługowe zarządzanie grupami.

* **Delegowane zarządzanie grupami** Przykładem może być administrator zarządzający dostępem do aplikacji SaaS używanej w firmie. Zarządzanie prawami dostępu jest coraz większym obciążeniem, więc administrator zwraca się do właściciela firmy o utworzenie nowej grupy. Administrator przypisuje nowej grupie dostęp do aplikacji i dodaje do grupy wszystkie osoby, które już uzyskują dostęp do aplikacji. Właściciel firmy może dodawać kolejnych użytkowników, dla których aplikacja jest automatycznie aprowizowana. Właściciel firmy nie musi czekać na administratora w celu zarządzania dostępem dla użytkowników. Jeśli administrator nada to samo uprawnienie menedżerowi w innej grupie biznesowej, może on następnie zarządzać dostępem swoich użytkowników. Właściciel firmy nie może wyświetlać użytkowników menedżera ani zarządzać nimi, a menedżer nie może wyświetlać użytkowników właściciela ani zarządzać nimi. Administrator nadal może wyświetlać wszystkich użytkowników mających dostęp do aplikacji i w razie potrzeby blokować prawa dostępu.
* **Samoobsługowe zarządzanie grupami** Przykładem tego scenariusza jest dwóch użytkowników mających niezależnie skonfigurowane witryny usługi SharePoint Online. Każdy z nich chce przydzielić dostęp do swojej witryny zespołowi drugiego użytkownika. W tym celu mogą utworzyć jedną grupę w usłudze Azure AD i wybrać tę grupę do przydzielenia dostępu do witryn w usłudze SharePoint Online. Gdy inna osoba będzie chciała uzyskać dostęp, wprowadzi żądanie w Panelu dostępu, a po zatwierdzeniu automatycznie uzyska dostęp do obu witryn usługi SharePoint Online. Jeden z użytkowników może stwierdzić później, że wszystkie osoby mające dostęp do witryny powinny również mieć dostęp do określonej aplikacji SaaS. Administrator aplikacji SaaS może dodać do witryny programu SharePoint Online prawa dostępu dla aplikacji. Od tego momentu zatwierdzenie żądania dostępu spowoduje przyznanie dostępu do obu witryn usługi SharePoint Online oraz do tej aplikacji SaaS.

## <a name="make-a-group-available-for-user-self-service"></a>Włączanie samoobsługi użytkowników w grupie
1. Zaloguj się w [centrum administracyjnym usługi Azure AD](https://aad.portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu.
2. Wybierz pozycję **Użytkownicy i grupy**, a następnie wybierz pozycję **Ustawienia grupy**.
3. Dla pozycji **Włączono samoobsługowe zarządzanie grupami** ustaw opcję **Tak**.
4. Dla pozycji **Użytkownicy mogą tworzyć grupy zabezpieczeń** lub **Użytkownicy mogą tworzyć grupy usługi Office 365** ustaw opcję **Tak**.
  * W przypadku włączenia tych ustawień wszyscy użytkownicy w katalogu mogą tworzyć nowe grupy zabezpieczeń i dodawać do nich członków. Te nowe grupy będą również wyświetlane na panelu dostępu dla innych użytkowników. Jeśli ustawienie zasad grupy to umożliwia, inni użytkownicy mogą tworzyć żądania, aby dołączyć do tych grup. 
  * Jeśli te ustawienia są wyłączone, użytkownicy nie mogą tworzyć grup ani zmieniać istniejących grup, których są właścicielami. Jednak nadal mogą zarządzać członkostwem w tych grupach i zatwierdzać żądania dołączenia do ich grup pochodzące od innych użytkowników.

Dodatkowo możesz użyć opcji **Użytkownicy, którzy mogą zarządzać grupami zabezpieczeń** i **Użytkownicy, którzy mogą zarządzać grupami usługi Office 365**, aby dokładniej sterować dostępem użytkowników do samoobsługowego zarządzania grupami. W przypadku włączenia opcji **Użytkownicy mogą tworzyć grupy** wszyscy użytkownicy w dzierżawie mogą tworzyć nowe grupy i dodawać do nich członków. Zmieniając ustawienie na **Niektóre**, możesz ograniczyć zarządzanie grupą do wybranych użytkowników. Gdy ten przełącznik ma wartość **Niektóre**, należy dodać użytkowników do grupy SSGMSecurityGroupsUsers, zanim będą oni mogli tworzyć nowe grupy i dodawać do nich członków. Wybranie ustawienia **Wszyscy** dla opcji **Użytkownicy, którzy mogą używać samoobsługi dla grup zabezpieczeń** i **Użytkownicy, którzy mogą zarządzać grupami usługi Office 365** umożliwi wszystkim użytkownikom w katalogu tworzenie nowych grup.

Możesz również użyć ustawienia **Grupa, która może zarządzać grupami zabezpieczeń** lub **Grupa, która może zarządzać grupami usługi Office 365**, aby określić jedną grupę, której członkowie mogą używać samoobsługi.

## <a name="next-steps"></a>Następne kroki
Te artykuły zawierają dodatkowe informacje o usłudze Azure Active Directory.

* [Zarządzanie dostępem do zasobów za pomocą grup usługi Azure Active Directory](active-directory-manage-groups.md)
* [Polecenia cmdlet usługi Azure Active Directory służące do konfigurowania ustawień grupy](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory](active-directory-apps-index.md)
* [Co to jest usługa Azure Active Directory?](active-directory-whatis.md)
* [Integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md)
