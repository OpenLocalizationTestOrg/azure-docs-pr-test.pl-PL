---
title: "Usług domenowych Azure Active Directory: Funkcje | Dokumentacja firmy Microsoft"
description: "Funkcje usług domenowych w usłudze Azure Active Directory"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 8d1c3eb3-1022-4add-a919-c98cc6584af1
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 1a9417bafa35959d280eabf3db6ad8530db4ea45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-domain-services"></a>Azure AD Domain Services
## <a name="features"></a>Funkcje
Witaj, następujące funkcje są dostępne w domenach zarządzanych usług domenowych Azure AD.

* **Środowisko proste wdrożenie:** można włączyć usługi domenowe Azure AD dla dzierżawy usługi Azure AD za pomocą kilku kliknięć. Niezależnie od tego, czy dzierżawy usługi Azure AD jest dzierżawą chmury lub synchronizacji z katalogiem lokalnym można szybko za domeny zarządzanej.
* **Obsługa przyłączenie do domeny:** możesz z łatwością przyłączenie do domeny komputerów w hello domeny zarządzanej, jest dostępny w sieci wirtualnej platformy Azure. środowisko przyłączenie do domeny Hello na kliencie systemu Windows i działa systemy operacyjne serwera bezproblemowo względem domeny obsługiwanych przez usługi domenowe Azure AD. Można również użyć zautomatyzowane sprzężenie narzędzi względem tych domen.
* **Wystąpienia jednej domeny na katalog usługi Azure AD:** można utworzyć pojedynczej domeny usługi Active Directory dla każdego katalogu usługi Azure AD.
* **Tworzenia domen z niestandardowych nazw:** można utworzyć domeny niestandardowej nazwy (na przykład "contoso100.com") przy użyciu usług domenowych Azure AD. Można używać nazw albo zweryfikowane i niezweryfikowane domeny. Opcjonalnie można również utworzyć domenę z sufiksem domeny wbudowanej hello (to znaczy "*. onmicrosoft.com") oferowane przez katalog usługi Azure AD.
* **Zintegrowane z usługą Azure AD:** nie wymagają tooconfigure lub zarządzać replikacją usług domenowych w usłudze tooAzure AD. Konta użytkowników, członkostwa w grupach i poświadczeń użytkownika (hasła) z katalogiem Azure AD są automatycznie dostępne w usługach domenowych Azure AD. Nowi użytkownicy, grupy lub tooattributes zmiany z dzierżawy usługi Azure AD lub katalogu lokalnego są automatycznie synchronizowane tooAzure AD usług domenowych w usłudze.
* **Uwierzytelnianie NTLM i Kerberos:** o obsługę uwierzytelniania NTLM i Kerberos, można wdrożyć aplikacji wykorzystujących zintegrowane uwierzytelnianie systemu Windows.
* **Użyj poświadczeń firmowych/hasła:** haseł dla użytkowników usługi Azure AD dzierżawcy korzystają z usług domenowych Azure AD. Użytkownicy mogą Użyj swoich poświadczeń firmowych sprzężenia toodomain maszyn, logowania interakcyjnego lub za pośrednictwem pulpitu zdalnego i uwierzytelniania względem domeny zarządzanej hello.
* **Wiązanie LDAP & LDAP odczytu pomocy technicznej:** mogą używać aplikacji, które opierają się na wiązania LDAP tooauthenticate użytkowników w domenach obsługiwanych przez usługi domenowe Azure AD. Ponadto aplikacje, które używają protokołu LDAP operacje odczytu dla którego tooquery atrybuty użytkownika i komputera z katalogu hello może również współpracować z usługami domenowymi Azure AD.
* **Bezpieczny protokół LDAP (LDAPS):** można włączyć dostęp do katalogu toohello za pośrednictwem bezpiecznego protokołu LDAP (LDAPS). Bezpieczny dostęp LDAP jest dostępna w ramach sieci wirtualnej hello domyślnie. Jednak również opcjonalnie można włączyć bezpieczny dostęp LDAP poprzez hello internet.
* **Zasady grupy:** można użyć jednego wbudowanych GPO hello użytkownicy i komputery kontenery tooenforce zgodności z zasadami zabezpieczeń wymaganych dla kont użytkowników i komputerów przyłączonych do domeny. Możesz również utworzyć własne niestandardowe obiekty zasad grupy i przypisać je jednostek organizacyjnych toocustom zbyt[Zarządzanie zasadami grupy](active-directory-ds-admin-guide-administer-group-policy.md).
* **Zarządzanie DNS:** członków grupy "Administratorzy kontrolera domeny usługi AAD" hello, można zarządzać DNS dla domeny zarządzanej przy użyciu znanych administracji DNS narzędzi, takich jak hello przystawki MMC administracyjnych DNS.
* **Tworzenie niestandardowych jednostek organizacyjnych (OU):** członków grupy "Administratorzy kontrolera domeny usługi AAD" hello można tworzyć niestandardowe jednostek organizacyjnych w domenie zarządzanej hello. Te użytkownicy mają prawo pełne uprawnienia administracyjne za pośrednictwem niestandardowych jednostek organizacyjnych, więc ich można usunąć konta usług, komputerów, grup itp. w ramach tych niestandardowych jednostek organizacyjnych.
* **Dostępne w wielu regionach platformy Azure:** hello zobacz [usług Azure według regionu](https://azure.microsoft.com/regions/#services/) tooknow strony hello regiony platformy Azure, w których są dostępne usługi domenowe Azure AD.
* **Wysoka dostępność:** usługi domenowe Azure AD oferują wysoką dostępność domeny. Ta funkcja oferuje hello gwarancji wyższej toofailures dostępności i odporności usługi. Wbudowane monitorowania oferty automatyczne rozwiązywanie problemów z błędami przez Obracająca się nowych wystąpień wystąpień tooreplace nie powiodło się i tooprovide kondycji nadal usługi dla tej domeny.
* **Użyj narzędzi zarządzania znanych:** za pomocą znanych narzędzi zarządzania usługi Active Directory systemu Windows Server takich jak domen tooadminister zarządzane hello Centrum administracyjne usługi Active Directory lub środowiska PowerShell usługi Active Directory.
