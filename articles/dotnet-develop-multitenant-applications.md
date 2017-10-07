---
title: "Wzorzec aplikacji sieci Web dzierżawy aaaMulti | Dokumentacja firmy Microsoft"
description: "Znajdowanie omówienie architektury i wzorce projektowe, które opisują sposób tooimplement wielodostępnej sieci web aplikacji w systemie Azure."
services: 
documentationcenter: .net
author: wadepickett
manager: wpickett
editor: 
ms.assetid: 4f0281d2-1555-42b0-a99d-1222fade0b0f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/05/2015
ms.author: wpickett
ms.openlocfilehash: 3b7822c8ca4aa50d295a174973ae4746c230ba66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="multitenant-applications-in-azure"></a>Wielodostępna aplikacji na platformie Azure
Wielodostępna aplikacja jest zasób udostępniony, umożliwiający oddzielne aplikacji o hello tooview użytkowników lub "dzierżawcy," tak, jakby była własnych. Typowy scenariusz, który pozwala tooa wielodostępnych aplikacji jest jeden, w którym wszyscy użytkownicy hello aplikacja może ma środowisko użytkownika hello toocustomize, ale w przeciwnym razie ma takie same wymagania biznesowe podstawowe hello. Przykładem dużych aplikacji wielodostępnym są usługi Office 365, Outlook.com i visualstudio.com.

Z perspektywy dostawcę aplikacji hello zalet wielodostępności przede wszystkim odnoszą się toooperational i koszt wydajności. Jednej wersji aplikacji może zaspokoić potrzeby hello wielu dzierżawców/klientów, umożliwiając konsolidacji systemu zadań administracyjnych, takich jak monitorowanie, dostrajanie wydajności obsługi oprogramowania i kopie zapasowe danych.

Hello poniżej podano listę hello najważniejsze cele i wymagania względem dostawcy.

* **Inicjowanie obsługi administracyjnej**: musi być możliwe tooprovision nowi dzierżawcy dla aplikacji hello.  Dla wielodostępnych aplikacji z wieloma dzierżawcami, jest zazwyczaj konieczne tooautomate ten proces przez włączenie samoobsługowego inicjowania obsługi administracyjnej.
* **Możliwość utrzymania**: musi być możliwe tooupgrade aplikacji hello i wykonywać inne zadania konserwacji, gdy jest ona używana przez wielu dzierżawców.
* **Monitorowanie**: użytkownik musi być toomonitor stanie aplikacji hello tooidentify zawsze wszelkie problemy i tootroubleshoot je. Dotyczy to również monitorowanie jak każdego dzierżawcy jest przy użyciu aplikacji hello.

Właściwie zaimplementowana aplikacji wielodostępnym zawiera następujące hello przynosi korzyści toousers.

* **Izolacja**: hello działania poszczególnych dzierżaw nie wpływają na powitania stosowania aplikacji hello przez innych dzierżawców. Dzierżawcy nie może uzyskać dostępu w danych. Wygląda na to dzierżawy toohello tak, jakby mają wyłącznego użytku aplikacji hello.
* **Dostępność**: poszczególnych dzierżawcy chcą toobe aplikacji hello stale dostępny, prawdopodobnie z gwarancje określone w umowie SLA. Ponownie działania hello innych dzierżawców nie powinny mieć wpływ na dostępność hello aplikacji hello.
* **Skalowalność**: aplikacja hello skaluje Żądanie hello toomeet poszczególnych dzierżawców. Witaj obecności i akcje innych dzierżawców nie wpływają na wydajność hello aplikacji hello.
* **Koszty**: koszty są niższe niż uruchamianie aplikacji dedykowanym, pojedynczej dzierżawy, ponieważ umożliwia wielodostępność hello udostępnianie zasobów.
* **Dostosowywalności**. Witaj możliwości toocustomize hello aplikacji dla poszczególnych dzierżawców na różne sposoby, takie jak dodawanie lub usuwanie funkcji, zmienianie kolorów i logo lub nawet dodanie własnych kod lub skrypt.

Krótko mówiąc, gdy istnieją wiele kwestii, które należy wykonać w konta tooprovide wysoce skalowalna usługa są również liczbę hello cele i wymagania, które są typowe aplikacje wielodostępne toomany. Niektóre mogą nie być odpowiednie w określonych scenariuszach i hello znaczenie poszczególnych cele i wymagania będą się różnić w każdym ze scenariuszy. Jako dostawca wielodostępnych aplikacji hello również należy cele i wymagania, takich jak spotkania dzierżaw hello cele i wymagania, zyskowności, rozliczeń, wiele poziomów usług, inicjowania obsługi administracyjnej, łatwości monitorowania i automatyzacji.

Aby uzyskać więcej informacji na dodatkowe zagadnienia dotyczące projektu wielodostępnych aplikacji, zobacz [Hosting aplikacji wielodostępnym, w systemie Azure][Hosting a Multi-Tenant Application on Azure]. Aby uzyskać informacje na temat typowych wzorców architektury danych w aplikacjach baz danych typu oprogramowanie jako usługa (SaaS), zobacz artykuł [Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database](sql-database/sql-database-design-patterns-multi-tenancy-saas-applications.md) (Wzorce projektowe dla wielodostępnych aplikacji SaaS korzystających z usługi Azure SQL Database). 

Azure oferuje wiele funkcji umożliwiających tooaddress hello klucza problemy występujące podczas projektowania systemu wielodostępnym.

**Izolacji**

* Witryny sieci Web segmentu dzierżawcy przez nagłówkami hosta lub bez komunikacji SSL
* Segment dzierżaw witryny sieci Web na podstawie parametrów zapytania
* Usługi sieci Web, rolę procesu roboczego
  * Role proces roboczy. które zwykle przetwarzania danych hello wewnętrznej bazy danych aplikacji.
  * Role sieci Web, które zwykle pełnienie hello frontonu dla aplikacji.

**Storage**

Zarządzanie danymi, takie jak usługi baza danych SQL Azure lub usługi Azure Storage, takich jak hello usługa, która zapewnia usługi do przechowywania dużych ilości danych bez struktury tabel i hello usługa Blob, która zapewnia usługi toostore dużych ilości nieustrukturyzowanych tekstu lub dane binarne, takie jak wideo, audio i obrazów.

* Zabezpieczanie danych wielodostępnej w bazie danych SQL odpowiednie logowania do programu SQL Server dla dzierżawy.
* Za pomocą tabel Azure dla aplikacji zasobów za pośrednictwem zasad dostępu na poziomie kontenera, można hello uprawnienia tooadjust możliwości bez konieczności tooissue nowego adresu URL dla zasobów hello chronione przy użyciu sygnatury dostępu współdzielonego.
* Kolejek platformy Azure dla kolejek Azure zasoby aplikacji są często używane toodrive przetwarzania imieniu dzierżawcy, ale może być również używane toodistribute pracy wymagane do inicjowania obsługi administracyjnej lub zarządzania.
* Kolejek usługi Service Bus dla zasobów aplikacji tego tooa pracy wypchnięć udostępnione usługi, gdzie każdego nadawcy dzierżawy ma tylko uprawnienia (jak określony na podstawie oświadczeń wystawione przez usługi ACS) toopush toothat kolejki podczas tylko odbiorcy hello z hello usługi można użyć pojedynczej kolejki ma uprawnienie toopull z hello kolejki hello danych z wieloma dzierżawcami.

**Połączenie i usług zabezpieczeń**

* Usługa Azure Service Bus, infrastruktury obsługi wiadomości, która znajduje się między aplikacjami, dzięki czemu komunikaty tooexchange luźno powiązanych sposób uzyskać lepsze skalowanie i odporność.

**Usługi sieciowe**

Platforma Azure udostępnia kilka usług sieciowych, które obsługuje uwierzytelnianie i zwiększyć możliwości zarządzania hostowanej aplikacji. Te usługi obejmują następujące hello:

* Azure umożliwia sieci wirtualnej, należy udostępnić i zarządzanie wirtualnych sieci prywatnych (VPN) na platformie Azure jak bezpiecznie połączyć je z lokalnej infrastruktury IT.
* Menedżer ruchu sieci wirtualnej umożliwia równoważenie tooload przychodzącego ruchu sieciowego między wiele Azure hostowanej usługi, czy jest na nich uruchomione w hello tym samym centrum danych lub w różnych centrach danych wokół hello world.
* Azure Active Directory (Azure AD) jest usługą nowoczesny, opartego na interfejsie REST, która udostępnia możliwości kontroli dostępu i zarządzania tożsamościami dla aplikacji w chmurze. Używanie programu Azure AD dla zasobów aplikacji usługi Azure AD tooprovides łatwy sposób uwierzytelniania i autoryzacji użytkowników toogain dostępu tooyour aplikacji i usług zezwalając hello funkcji uwierzytelniania i autoryzacji toobe wzięciu pod uwagę z sieci Kod.
* Usługa Azure Service Bus zapewnia bezpiecznej wymiany komunikatów i możliwość przepływu danych dla rozproszonej i hybrydowych aplikacji, takie jak komunikacja między Azure hostowanej aplikacji i lokalnych aplikacji i usług, bez konieczności złożonych zapory i zabezpieczeń infrastruktura. Przekaźnik magistrali usług przy użyciu toohello zasoby aplikacji usługi, które są dostępne jako punkty końcowe może należeć toohello dzierżawy (na przykład hostowane poza hello systemu, takie jak lokalnie) lub mogą być udostępniane specjalnie z myślą o hello dzierżawy (usług ponieważ dane poufne, specyficznego dla dzierżawy są przesyłane w nich).

**Inicjowanie obsługi zasobów**

Platforma Azure udostępnia kilka różnych sposobów udostępniania nowi dzierżawcy dla aplikacji hello. Dla wielodostępnych aplikacji z wieloma dzierżawcami, jest zazwyczaj konieczne tooautomate ten proces przez włączenie samoobsługowego inicjowania obsługi administracyjnej.

* Proces roboczy ról pozwala tooprovision i dezaktywowanie dostarczanie na zasoby dzierżawcy (na przykład gdy nowej dzierżawy znaki w górę lub anuluje), zbierać metryki pomiaru użycia oraz zarządzania nimi skali od niektórych harmonogramu lub w odpowiedzi toohello przekroczenia progów klucza wskaźniki wydajności. Tej samej roli może być również używane toopush limit rozwiązania toohello aktualizacji i uaktualnień.
* Obiekty BLOB platformy Azure może być używane tooprovision obliczeń lub zasobów wstępnie zainicjowana magazynu dla nowego dzierżawcy zapewniając kontenera dostępu na poziomie zasady tooprotect hello obliczeń pakietów usług, obrazy VHD i inne zasoby.
* Opcje inicjowania obsługi administracyjnej zasobów bazy danych SQL dla dzierżawy obejmują:
  
  * DDL w skryptach lub osadzony jako zasoby w obrębie zestawów
  * SQL Server 2008 R2 pakiety DAC wdrożyć programowo.
  * Kopiowanie z bazy danych master odwołania
  * Przy użyciu bazy danych importu i eksportu tooprovision nowych baz danych z pliku.

<!--links-->

[Hosting a Multi-Tenant Application on Azure]: http://msdn.microsoft.com/library/hh534480.aspx
[Designing Multitenant Applications on Azure]: http://msdn.microsoft.com/library/windowsazure/hh689716
