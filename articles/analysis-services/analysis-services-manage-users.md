---
title: "aaaAuthentication i uprawnień użytkowników w usłudze Azure Analysis Services | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat uwierzytelniania i uprawnień użytkowników w usłudze Azure Analysis Services."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: dd49fd59eec1f68dfe8a0fe373fa612ac46de4e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-user-permissions"></a>Uprawnienia do uwierzytelniania i użytkownika
Azure Analysis Services używa usługi Azure Active Directory (Azure AD) do uwierzytelniania użytkowników i zarządzania tożsamościami. Dowolny użytkownik, tworzenia, zarządzania, lub łącząc tooan Azure Analysis Services serwer musi mieć tożsamość prawidłowego użytkownika w [dzierżawy usługi Azure AD](../active-directory/active-directory-administer.md) w hello tej samej subskrypcji.

Azure Analysis Services obsługuje [współpracy B2B usługi Azure AD](../active-directory/active-directory-b2b-what-is-azure-ad-b2b.md). Z B2B użytkowników spoza organizacji mogą być zapraszani jako goście w katalogu usługi Azure AD. Goście mogą pochodzić z innego katalogu dzierżawy usługi Azure AD lub dowolnego adresu e-mail. Zaproszenie raz i hello użytkownik akceptuje zaproszenie hello wysyłane pocztą e-mail z platformy Azure, hello że tożsamość użytkownika została dodana toohello katalog dzierżawy. Tych tożsamości można dodawać grup toosecurity lub jako członkowie roli administratora lub bazy danych serwera.

![Architektura uwierzytelniania w usłudze Azure Analysis Services](./media/analysis-services-manage-users/aas-manage-users-arch.png)

## <a name="authentication"></a>Authentication
Wszystkie aplikacje klienckie i narzędzia używać co najmniej jeden hello usług Analysis Services [bibliotek klienckich](analysis-services-data-providers.md) (AMO, MSOLAP, ADOMD) tooconnect tooa serwera. 

Wszystkie trzy klienta biblioteki obsługują usługi Azure AD interaktywnego przepływu i metody nieinterakcyjnej uwierzytelniania. Witaj dwie metody nieinterakcyjnej, metody hasła usługi Active Directory i zintegrowane uwierzytelnianie usługi Active Directory mogą być używane w aplikacji przy użyciu AMOMD i MSOLAP. Te dwie metody nigdy nie powoduje podręcznych oknach dialogowych.

Aplikacje klienckie, takie jak program Excel i Power BI Desktop i narzędzi, takich jak SSMS i narzędzi SSDT zainstalować najnowsze wersje bibliotek powitania po zaktualizowaniu hello toohello najnowszej wersji. Power BI Desktop, SSMS i narzędzi SSDT są aktualizowane co miesiąc. Program Excel jest [aktualizacji z usługi Office 365](https://support.office.com/en-us/article/When-do-I-get-the-newest-features-in-Office-2016-for-Office-365-da36192c-58b9-4bc9-8d51-bb6eed468516). Aktualizacje usługi Office 365 są dłuższe interwały i niektóre organizacje użyć hello odroczonego kanału, znaczenie aktualizacje są odroczone toothree miesięcy.

 W zależności od aplikacji klienckiej hello lub narzędzia, których używasz hello typ uwierzytelniania i jak możesz się zalogować może się różnić. Każda aplikacja może obsługiwać różne funkcje podłączania toocloud usług takich jak Azure Analysis Services.


### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)
Serwery usług Analysis Services Azure obsługuje połączenia z [SSMS V17.1](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) i wyższych przy użyciu uwierzytelniania systemu Windows, uwierzytelniania hasła w usłudze Active Directory i uniwersalnych uwierzytelnianie usługi Active Directory. Ogólnie rzecz biorąc zalecane jest, że używasz uniwersalnych uwierzytelnianie usługi Active Directory, ponieważ:

*  Obsługuje metod uwierzytelniania interakcyjnym i nieinterakcyjnym.

*  Obsługuje zaproszenie do dzierżawy Azure AS hello gości B2B usługi Azure. Podczas łączenia z serwerem tooa, gości, musisz wybrać uniwersalnych uwierzytelnianie usługi Active Directory podczas łączenia z serwerem toohello.

*  Obsługuje uwierzytelnianie wieloskładnikowe (MFA). Usługa Azure MFA ułatwia zabezpieczenie dostępu toodata i aplikacji z szeroką gamę opcji weryfikacji: połączenie telefoniczne, wiadomość tekstowa, karty inteligentne z numeru pin lub powiadomienie aplikacji mobilnej. Interakcyjne MFA z usługą Azure AD może spowodować wyskakujące okno dialogowe do weryfikacji.

### <a name="sql-server-data-tools-ssdt"></a>SQL Server Data Tools (SSDT)
Program SSDT łączy tooAzure Analysis Services za pomocą uwierzytelniania uniwersalnego usługi Active Directory z obsługą uwierzytelniania Wieloskładnikowego. Użytkownicy są zostanie wyświetlony monit o toosign w tooAzure przy pierwszym wdrożeniu hello przy użyciu swojego Identyfikatora organizacyjnego (poczta e-mail). Użytkownicy muszą się zalogować w tooAzure przy użyciu konta z uprawnieniami administratora serwera na powitania serwera wdrażania do. Podczas rejestrowania się w tooAzure powitania po raz pierwszy, token jest przypisany. Program SSDT buforuje hello tokenu w pamięci dla przyszłych Ponowne podłączenia.

### <a name="power-bi-desktop"></a>Power BI Desktop
Power BI Desktop łączy tooAzure usług Analysis Services za pomocą uwierzytelniania uniwersalnego usługi Active Directory z obsługą uwierzytelniania Wieloskładnikowego. Użytkownicy są zostanie wyświetlony monit o toosign w tooAzure na powitania pierwszego połączenia przy użyciu swojego Identyfikatora organizacyjnego (poczta e-mail). Użytkownicy muszą się zalogować w tooAzure przy użyciu konta, który znajduje się w administrator serwera lub roli bazy danych.

### <a name="excel"></a>Excel
Excel użytkownicy mogą łączyć tooa serwera przy użyciu konta systemu Windows, identyfikator organizacji (adres e-mail) lub adres e-mail zewnętrznych. Tożsamość zewnętrzna wiadomość e-mail, musi istnieć w hello Azure AD jako Gość.

## <a name="user-permissions"></a>Uprawnienia użytkowników

**Administratorzy serwera** są wystąpienie serwera usług Azure Analysis Services tooan określone. Połączenie jest nawiązywane z narzędzi, takich jak portalu Azure, programu SSMS i narzędzi SSDT tooperform zadania, takie jak dodawanie baz danych i zarządzanie rolami użytkowników. Domyślnie program hello użytkownika, który tworzy serwer hello jest automatycznie dodawany jako administrator serwera usług Analysis Services. Za pomocą portalu Azure lub SSMS można dodawać innych administratorów. Administratorzy serwera musi mieć konto w dzierżawie powitalnych usługi Azure AD w hello tej samej subskrypcji. toolearn więcej, zobacz [administratorom serwerów zarządzania](analysis-services-server-admins.md). 


**Bazy danych użytkowników** połączyć toomodel baz danych przy użyciu aplikacji klienckich, takich jak Excel lub Power BI. Użytkownicy muszą zostać dodane toodatabase ról. Role bazy danych definiuje administratora, proces ani uprawnienia do odczytu bazy danych. Koniecznie toounderstand bazy danych użytkowników w roli z uprawnieniami administratora różni się od administratorów serwera. Jednak domyślnie administratorom serwerów są również administratorami baz danych. toolearn więcej, zobacz [Zarządzanie ról bazy danych i użytkowników](analysis-services-database-users.md).

**Właściciele zasobów platformy Azure**. Właścicieli zasobów, zarządzanie zasobami subskrypcji platformy Azure. Właścicieli zasobów można dodać tooOwner tożsamości użytkownika usługi Azure AD lub współautora ról w ramach subskrypcji przy użyciu **kontrola dostępu** w portalu Azure lub za pomocą szablonów usługi Azure Resource Manager. 

![Kontrola dostępu w portalu Azure](./media/analysis-services-manage-users/aas-manage-users-rbac.png)

Role na tym poziomie zastosować toousers lub konta, które wymagają tooperform zadania, które można wykonać w portalu hello lub przy użyciu szablonów usługi Azure Resource Manager. toolearn więcej, zobacz [kontroli dostępu opartej na rolach](../active-directory/role-based-access-control-what-is.md). 


## <a name="database-roles"></a>Role bazy danych

 Role zdefiniowane dla modelu tabelarycznego są role bazy danych. Oznacza to hello role zawierają elementy Członkowskie składające się z usługi Azure AD użytkownicy i grupy zabezpieczeń, które mają określone uprawnienia definiujące akcji hello tych członków, może przyjmować bazy danych modelu. Rola bazy danych zostanie utworzona jako oddzielny obiekt w bazie danych hello i stosuje toohello tylko bazy danych, w której jest tworzona tej roli.   
  
 Domyślnie podczas tworzenia nowego projektu modelu tabelarycznego, projekt z modelem hello nie ma żadnych ról. Role można zdefiniować przy użyciu powitalne okno dialogowe menedżera ról programu SSDT. Po zdefiniowaniu ról podczas tworzenia projektu modelu są zastosowane tylko toohello modelu obszaru roboczego z bazy danych. Po wdrożeniu modelu hello hello ról są zastosowane toohello wdrożone modelu. Po wdrożeniu modelu serwera i bazy danych Administratorzy mogą zarządzać rolami i elementów członkowskich za pomocą narzędzia SSMS. toolearn więcej, zobacz [Zarządzanie ról bazy danych i użytkowników](analysis-services-database-users.md).
  


## <a name="next-steps"></a>Następne kroki

[Zarządzanie tooresources dostępu za pomocą grup usługi Azure Active Directory](../active-directory/active-directory-manage-groups.md)   
[Zarządzanie ról bazy danych i użytkowników](analysis-services-database-users.md)  
[Zarządzanie administratorami serwerów](analysis-services-server-admins.md)  
[Kontrola dostępu oparta na rolach](../active-directory/role-based-access-control-what-is.md)  