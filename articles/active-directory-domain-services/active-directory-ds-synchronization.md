---
title: "Usługi Azure Active Directory Domain Services: Synchronizacja w domenach zarządzanych | Dokumentacja firmy Microsoft"
description: "Zrozumienie synchronizacji w domenie zarządzanej usług domenowych Azure Active Directory"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 57cbf436-fc1d-4bab-b991-7d25b6e987ef
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 9be25b61823a6b031906f3576395782e73831fc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="synchronization-in-an-azure-ad-domain-services-managed-domain"></a>Synchronizacja w domenie zarządzanej usług domenowych Azure AD
Hello poniższym diagramie przedstawiono sposób działania synchronizacji w w usługach domenowych Azure AD domen zarządzanych.

![Topologia synchronizacji w usługach domenowych Azure AD](./media/active-directory-domain-services-design-guide/sync-topology.png)

## <a name="synchronization-from-your-on-premises-directory-tooyour-azure-ad-tenant"></a>Synchronizacja z dzierżawą lokalnego katalogu tooyour usługi Azure AD
Synchronizacja programu Azure AD Connect jest używane toosynchronize kont użytkowników, członkostwa w grupach i dzierżawy tooyour usługi Azure AD skrótów poświadczeń. Atrybuty użytkownika konta, takich jak hello UPN i lokalnymi identyfikatora SID (identyfikator zabezpieczeń) są synchronizowane. Jeśli używasz usług domenowych Azure AD skrótów starszych poświadczeń wymaganych do uwierzytelniania NTLM i Kerberos są również tooyour zsynchronizowanej dzierżawy usługi Azure AD.

Jeśli skonfigurujesz zapisu zmiany zachodzące w katalogu usługi Azure AD są synchronizowane wstecz tooyour lokalnej usługi Active Directory. Na przykład w przypadku zmiany hasła przy użyciu funkcji zmiany hasła samoobsługi usługi Azure AD, zmiany hasła hello jest aktualizowany w lokalnej domeny usługi AD.

> [!NOTE]
> Zawsze używaj hello najnowszą wersję programu Azure AD Connect tooensure masz poprawek dla wszystkich znanych błędów.
>
>

## <a name="synchronization-from-your-azure-ad-tenant-tooyour-managed-domain"></a>Domeny zarządzane synchronizacji z Twojej tooyour dzierżawy usługi Azure AD
Konta użytkowników, członkostwa w grupach i skrótów poświadczeń są synchronizowane z Twojej tooyour dzierżawy usługi Azure AD domeny zarządzanej usług domenowych Azure AD. Ten proces synchronizacji odbywa się automatycznie. Nie trzeba tooconfigure, monitorowanie i zarządzanie ten proces synchronizacji. Po zakończeniu hello jednorazowego wstępnej synchronizacji katalogu on zwykle trwa około 20 minut, aby zmiany wprowadzone w usłudze Azure AD toobe odzwierciedlone w domeny zarządzanej. Ten interwał synchronizacji stosuje zmiany toopassword lub zmienia tooattributes wprowadzone w usłudze Azure AD.

proces synchronizacji Hello jest również jednorazowe-way/jednokierunkowe charakter. Domeny zarządzanej jest przede wszystkim tylko do odczytu z wyjątkiem wszystkich niestandardowych jednostkach organizacyjnych, należy utworzyć. W związku z tym nie można wprowadzić zmiany atrybutów toouser, hasła lub członkostwa w grupach w ramach domeny zarządzanej hello. W związku z tym jest nie odwrotnej synchronizacja zmian z Twojej domeny zarządzanej tooyour wstecz dzierżawy usługi Azure AD.

## <a name="synchronization-from-a-multi-forest-on-premises-environment"></a>Synchronizacja w środowisku wielu lasów lokalnych
Organizacje często mają dość złożone lokalnymi infrastruktury tożsamości, składające się z wielu lasów kont. Azure AD Connect obsługuje synchronizacji użytkowników, grup i skrótów poświadczeń z dzierżawy tooyour usługi Azure AD w środowisku wielu lasów.

Z kolei dzierżawy usługi Azure AD jest znacznie prostsza i płaskiej przestrzeni nazw. tooenable użytkowników tooreliably uzyskiwać dostęp do aplikacji zabezpieczonej przez usługi Azure AD, rozwiązywanie konfliktów UPN między kontami użytkowników w różnych lasach. Twoje posiada domeny zarządzanej usług domenowych Azure AD Zamknij dzierżawy usługi Azure AD tooyour wynik. W związku z tym Zobacz płaska struktura jednostek organizacyjnych w domenie zarządzanej. Wszyscy użytkownicy i grupy są przechowywane w kontenerze "AADDC użytkownicy" hello, niezależnie od hello lokalnej domeny i lasu, z której zostały zsynchronizowane w. Skonfigurowane hierarchiczna jednostki Organizacyjnej struktury lokalnymi. Jednak domeny zarządzanej nadal ma prosty płaska struktura jednostki Organizacyjnej.

## <a name="exclusions---what-isnt-synchronized-tooyour-managed-domain"></a>Wykluczenia — co nie jest zsynchronizowany tooyour domeny zarządzanej
Hello następujących obiektów i atrybutów nie są zsynchronizowane tooyour dzierżawy usługi Azure AD lub domeny zarządzanej tooyour:

* **Wykluczone atrybutów:** można wybrać tooexclude niektóre atrybuty synchronizowanie dzierżawy usługi Azure AD tooyour z domeny lokalnej za pomocą usługi Azure AD Connect. Te atrybuty wykluczone nie są dostępne w Twojej domeny zarządzanej.
* **Zasady grupy:** skonfigurowane w domenie lokalnych zasad grupy nie są zsynchronizowane tooyour domeny zarządzanej.
* **Udział SYSVOL:** podobnie hello hello udziału SYSVOL w domenie lokalnej nie są zsynchronizowane tooyour domeny zarządzanej.
* **Obiekty komputerów:** obiektów komputera dla komputerów tooyour dołączonego do lokalnej domeny nie są zsynchronizowane tooyour domeny zarządzanej. Te komputery nie relacji zaufania z domeną zarządzanych i należeć tylko tooyour lokalnej domeny. W domenie zarządzanej możesz znaleźć obiekty komputerów tylko przez komputery mają jawnie przyłączonych do domeny toohello zarządzane domeny.
* **Atrybuty SidHistory dla użytkowników i grup:** hello głównego użytkownika i identyfikatory SID z domeny lokalnej grupy podstawowej są zsynchronizowane tooyour domeny zarządzanej. Istniejące atrybuty SidHistory dla użytkowników i grup nie są synchronizowane z lokalnej domeny zarządzanej tooyour domeny.
* **Struktury jednostek (OU) w organizacji:** jednostek organizacyjnych zdefiniowanych w domenie lokalnej nie Synchronizuj tooyour domeny zarządzanej. Istnieją dwa wbudowane jednostek organizacyjnych w domenie zarządzanej. Domyślnie domeny zarządzanej ma prosty struktury jednostek organizacyjnych. Można jednak wybrać zbyt[Tworzenie niestandardowej jednostki Organizacyjnej w domenie zarządzanej](active-directory-ds-admin-guide-create-ou.md).

## <a name="how-specific-attributes-are-synchronized-tooyour-managed-domain"></a>Jak określone atrybuty są synchronizowane tooyour domeny zarządzanej
Witaj w poniższej tabeli przedstawiono niektóre typowe atrybuty i w tym artykule opisano, jak są one zsynchronizowane tooyour domeny zarządzanej.

| Atrybut w domeny zarządzanej | Element źródłowy | Uwagi |
|:--- |:--- |:--- |
| NAZWY UPN |Atrybut nazwy UPN użytkownika w dzierżawie usługi Azure AD |Atrybut nazwy głównej użytkownika Hello z dzierżawy usługi Azure AD są synchronizowane zgodnie z domeny tooyour zarządzane. W związku z tym hello najbardziej niezawodnym sposobem toosign w domenie zarządzanej tooyour korzysta z nazwy UPN. |
| sAMAccountName |MailNickname użytkownika atrybut w dzierżawie usługi Azure AD lub generowane automatycznie |Atrybut SAMAccountName Hello są uzyskiwane z atrybutu mailNickname hello w dzierżawie usługi Azure AD. Jeśli wiele kont użytkowników powitalne tego samego atrybutu mailNickname, hello SAMAccountName jest generowane automatycznie. Jeśli hello mailNickname lub prefiks nazwy UPN użytkownika jest dłuższa niż 20 znaków, hello SAMAccountName jest generowane automatycznie toosatisfy hello 20 limit znaków na atrybuty SAMAccountName. |
| Hasła |Hasło użytkownika z dzierżawy usługi Azure AD |Skrótów poświadczeń wymaganych do uwierzytelniania NTLM lub Kerberos (nazywanych również dodatkowe poświadczenia) są synchronizowane z dzierżawy usługi Azure AD. Jeśli dzierżawy usługi Azure AD jest zsynchronizowanej dzierżawy, te poświadczenia pochodzą z domeny lokalnej. |
| Podstawowy użytkownik/identyfikator SID grupy |Wygenerowany automatycznie |Hello podstawowy identyfikator SID dla konta użytkownika/grupy jest generowany automatycznie domeny zarządzanej. Ten atrybut nie pasuje do hello podstawowego użytkownika/grupy identyfikator SID obiektu hello w lokalnej domeny usługi AD. Ta niezgodność jest ponieważ domeny zarządzanej hello ma inną przestrzeń nazw identyfikatora SID niż domeny lokalnej. |
| Historii identyfikatora SID dla użytkowników i grup |Podstawowy użytkownik lokalny i identyfikator SID grupy |Witaj SidHistory dla użytkowników i grup w domenie zarządzanej ustawiono atrybut toomatch hello odpowiedniego użytkownika podstawowego lub identyfikator SID grupy w domenie lokalnej. Ta funkcja pomaga upewnij przyrostu i shift z lokalnej aplikacji toohello domeny zarządzanej łatwiejsze, ponieważ nie ma potrzeby listy ACL toore zasobów. |

> [!NOTE]
> **Zaloguj się toohello domeny zarządzanej przy użyciu formatu UPN hello:** atrybut SAMAccountName hello mogą być generowane automatycznie dla niektórych kont użytkowników w domenie zarządzanej. Jeśli wielu użytkowników ma hello tego samego atrybutu mailNickname lub użytkownicy mają zbyt długo UPN prefiksy, hello SAMAccountName dla tych użytkowników może zostać wygenerowany automatycznie. W związku z tym hello SAMAccountName format (na przykład "CONTOSO100\joeuser") nie jest zawsze toosign niezawodnym sposobem, w domenie toohello. SAMAccountName automatycznie generowanej użytkowników może różnić się od prefiksu ich nazwy UPN. Użyj formatu nazwy UPN hello (na przykład "joeuser@contoso100.com") toosign w toohello zarządzane niezawodnie domeny.
>
>

### <a name="attribute-mapping-for-user-accounts"></a>Mapowanie atrybutu dla kont użytkowników
Hello w poniższej tabeli przedstawiono sposób określonych atrybutów dla obiektów użytkowników w dzierżawie usługi Azure AD są zsynchronizowane toocorresponding atrybutów w domeny zarządzanej.

| Atrybut użytkownika w dzierżawie usługi Azure AD | Atrybut użytkownika w domenie zarządzanej |
|:--- |:--- |
| AccountEnabled |kontroli konta użytkownika (zestawów lub czyści hello ACCOUNT_DISABLED-bitowy) |
| city |l |
| Kraju |co |
| Dział |Dział |
| Nazwa wyświetlana |Nazwa wyświetlana |
| facsimileTelephoneNumber |facsimileTelephoneNumber |
| Imię |Imię |
| Stanowisko |Tytuł |
| Poczty |Poczty |
| mailNickname |atrybut msDS-AzureADMailNickname |
| mailNickname |SAMAccountName (czasami może się generowane automatycznie) |
| Telefon komórkowy |Telefon komórkowy |
| Identyfikator obiektu |atrybut msDS-AzureADObjectId |
| onPremiseSecurityIdentifier |historii SID |
| passwordPolicies |kontroli konta użytkownika (zestawów lub czyści hello DONT_EXPIRE_PASSWORD-bitowy) |
| physicalDeliveryOfficeName |physicalDeliveryOfficeName |
| KodPocztowy |KodPocztowy |
| preferredLanguage |preferredLanguage |
| state |St |
| Adres |Adres |
| nazwisko |SN |
| TelephoneNumber |TelephoneNumber |
| userPrincipalName |userPrincipalName |

### <a name="attribute-mapping-for-groups"></a>Mapowanie atrybutu dla grup
Hello w poniższej tabeli przedstawiono atrybutów określonych dla grupy obiektów w dzierżawie usługi Azure AD są zsynchronizowane toocorresponding atrybutów w domeny zarządzanej.

| Grupa atrybutów w dzierżawie usługi Azure AD | Atrybut grupy w domenie zarządzanej |
|:--- |:--- |
| Nazwa wyświetlana |Nazwa wyświetlana |
| Nazwa wyświetlana |SAMAccountName (czasami może się generowane automatycznie) |
| Poczty |Poczty |
| mailNickname |atrybut msDS-AzureADMailNickname |
| Identyfikator obiektu |atrybut msDS-AzureADObjectId |
| onPremiseSecurityIdentifier |historii SID |
| Securityenabled musi |GroupType |

## <a name="objects-that-are-not-synchronized-tooyour-azure-ad-tenant-from-your-managed-domain"></a>Obiekty, które nie są zsynchronizowane dzierżawy usługi Azure AD tooyour z domeny zarządzanej
Zgodnie z opisem w poprzedniej sekcji tego artykułu, nie istnieje żadne synchronizacji z Twojej domeny zarządzanej tooyour wstecz dzierżawy usługi Azure AD. Można wybrać zbyt[Tworzenie niestandardowej jednostki organizacyjnej (OU)](active-directory-ds-admin-guide-create-ou.md) w domenie zarządzanej. Ponadto można utworzyć jednostek organizacyjnych, użytkownicy, grupy lub konta usług w ramach tych niestandardowych jednostek organizacyjnych. Brak utworzonych w ramach jednostkami organizacyjnymi niestandardowych obiektów hello są synchronizowane wstecz tooyour dzierżawy usługi Azure AD. Te obiekty są dostępne do użycia tylko w obrębie domeny zarządzanej. W związku z tym te obiekty nie są widoczne, przy użyciu poleceń cmdlet programu PowerShell usługi Azure AD, Azure AD Graph API lub interfejs użytkownika zarządzania hello Azure AD.

## <a name="related-content"></a>Powiązana zawartość
* [Funkcje — usługi domenowe Azure AD](active-directory-ds-features.md)
* [Scenariusze wdrażania - usługi domenowe Azure AD](active-directory-ds-scenarios.md)
* [Zagadnienia dotyczące sieci dla usług domenowych Azure AD](active-directory-ds-networking.md)
* [Wprowadzenie do usług domenowych Azure AD](active-directory-ds-getting-started.md)
