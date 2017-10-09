---
title: "aaaMonitor lokalnej infrastruktury tożsamości w hello w chmurze."
description: "Jest to hello Azure AD Connect Health strony, która opisuje, co to jest i do czego służy."
services: active-directory
documentationcenter: 
author: karavar
manager: samueld
editor: curtand
ms.assetid: 82798ea6-5cd3-4f30-93ae-d56536f8d8e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 84d0b00ec800ba98094343731aa4e7317dfb0c61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-your-on-premises-identity-infrastructure-and-synchronization-services-in-hello-cloud"></a>Monitorowanie lokalnej tożsamości infrastruktury i synchronizacji usług w chmurze hello
Azure Active Directory (Azure AD) Connect Health pomaga monitorować i uzyskać wgląd w swoją tożsamość lokalnej infrastruktury i hello usług synchronizacji. Umożliwia toomaintain tooOffice niezawodnego połączenia 365 i Microsoft Online Services udostępniając funkcje monitorowania kluczowych składników tożsamości takich jak serwery usługi Active Directory Federation Services (AD FS), serwery Azure AD Connect (nazywanego także jako aparatem synchronizacji) kontrolery domeny usługi Active Directory, itp. Zapewnia także hello kluczowych punktów danych dotyczących tych składników łatwo dostępne, dzięki czemu można wyświetlić składnię i inne ważne insights toomake poinformowany decyzji.

Witaj informacje są prezentowane w hello [portalu Azure AD Connect Health](https://aka.ms/aadconnecthealth). W portalu Azure AD Connect Health hello można wyświetlić alerty, monitorowanie wydajności, analizy użycia i inne informacje. Azure AD Connect Health umożliwia hello pojedynczego pokazuje kondycję kluczowych składników tożsamości w jednym miejscu.

![Co to jest program Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnecthealth2.png)

Jak zwiększyć hello funkcji w programie Azure AD Connect Health, hello portal zawiera pojedynczy pulpit nawigacyjny za pośrednictwem obiektyw hello tożsamości. Możesz uzyskać jeszcze bardziej niezawodne, dobrej kondycji i zintegrowane środowisko tooincrease Twojego użytkowników wykonanie zadań tooget możliwości.

## <a name="why-use-azure-ad-connect-health"></a>Dlaczego warto korzystać z programu Azure AD Connect Health?
Po zintegrowaniu katalogów lokalnych z usługą Azure AD, użytkownicy są bardziej wydajni, ponieważ wspólną tożsamość tooaccess zarówno w chmurze i zasobów lokalnych. Integracja ta tworzy jednak wyzwaniem hello zapewnienie, że to środowisko jest w dobrej kondycji, aby użytkownicy niezawodny dostęp do zasobów zarówno lokalnie, jak i w hello w chmurze z dowolnego urządzenia. Azure AD Connect Health pomaga monitorować i uzyskać wgląd w infrastruktury tożsamości lokalnych, używane tooaccess usługi Office 365 lub innych aplikacji usługi Azure AD. Wymaga to jedynie zainstalowania agenta na każdym z lokalnych serwerów tożsamości.

## <a name="azure-ad-connect-health-for-ad-fsactive-directory-aadconnect-health-adfsmd"></a>[Program Azure AD Connect Health dla usług AD FS](active-directory-aadconnect-health-adfs.md)
Program Azure AD Connect Health dla usług AD FS obsługuje usługi AD FS 2.0 w systemach Windows Server 2008 R2, Windows Server 2012 i Windows Server 2012 R2. Obsługuje ona również monitorowania serwera proxy usług hello AD FS lub serwerów proxy aplikacji sieci web, które zapewniają uwierzytelnianie obsługuje dla dostępu z ekstranetu. Łatwe i ekonomicznych instalacji hello kondycji agenta Azure AD Connect Health dla usług AD FS zawiera powitania po zestaw kluczowych funkcji:

* Monitorowanie przy użyciu tooknow alerty, gdy serwery proxy FS usług AD FS i AD nie jest dobra
* Powiadomienia e-mail dotyczące alertów krytycznych
* Trendy w danych dotyczących wydajności przydatne do planowania wydajności usług AD FS
* Analiza użycia logowania usług AD FS z przestawień (aplikacje, użytkownicy, lokalizacja sieciowa itp.), które są przydatne toounderstand jak jest wprowadzenie wykorzystywany usług AD FS
* Raporty dotyczące usług AD FS, na przykład lista 50 użytkowników, którzy najczęściej nieprawidłowo podawali nazwę użytkownika/hasło, wraz z ostatnim adresem IP

Witaj poniższego klipu wideo zawiera omówienie programu Azure AD Connect Health dla usług AD FS.

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-AD-Connect-Health--Monitor-you-identity-bridge/player]
>
>

## <a name="azure-ad-connect-health-for-syncactive-directory-aadconnect-health-syncmd"></a>[Program Azure AD Connect Health do celów synchronizacji](active-directory-aadconnect-health-sync.md)
Azure AD Connect Health do celów synchronizacji monitoruje i udostępnia informacje o synchronizacje hello, występujących między lokalnymi usługi Active Directory i Azure AD. Azure AD Connect Health do celów synchronizacji zawiera powitania po zestaw kluczowych funkcji:

* Monitorowanie za pomocą tooknow alerty, gdy serwera usługi Azure AD Connect, nazywane również hello aparatu synchronizacji, nie jest w dobrej kondycji
* Powiadomienia e-mail dotyczące alertów krytycznych
* Wgląd w dane operacyjne dotyczące synchronizacji, między innymi wykresy opóźnień operacji synchronizacji i trendy w innych operacjach, takich jak dodawanie, aktualizowanie i usuwanie
* Szybkiego dostępu informacje o właściwości synchronizacji i ostatniego pomyślnego eksportu tooAzure AD
* Raporty o błędach synchronizacji na poziomie obiektu \(nie wymagają usługi Azure AD w wersji Premium\)

Witaj poniższego klipu wideo zawiera omówienie programu Azure AD Connect Health do celów synchronizacji.

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-Health-Monitoring-the-sync-engine/player]
>
>

## <a name="azure-ad-connect-health-for-ad-dsactive-directory-aadconnect-health-addsmd"></a>[Program Azure AD Connect Health dla usług AD DS](active-directory-aadconnect-health-adds.md)
Program Azure AD Connect Health dla usług Active Directory Domain Services (AD DS) oferuje funkcje monitorowania kontrolerów domeny zainstalowanych w systemach Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 i Windows Server 2016. Hello instalacji agenta kondycji umożliwia możesz toomonitor lokalnej środowiska usług AD DS z hello chmury. Azure AD Connect Health dla usług AD DS zawiera powitania po zestaw kluczowych funkcji:

* Monitorowanie toodetect alerty, gdy kontrolery domeny są w złej kondycji i powiadomienia e-mail o alerty krytyczne
* pulpit nawigacyjny kontrolerów domeny Hello, która zapewnia szybki przegląd kondycji hello i stan operacyjny kontrolerów domeny
* pulpit nawigacyjny stan replikacji Hello, który ma hello najnowsze informacje o replikacji i łączy przewodniki tootroubleshooting w przypadku wykrycia błędów
* Szybkie bezpośredni dostęp do tooperformance wykresy danych liczników wydajności popularnych, które są niezbędne do monitorowania celów i rozwiązywanie problemów

Witaj poniższego klipu wideo zawiera omówienie programu Azure AD Connect Health dla usług AD DS.

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-AD-Connect-Health-monitors-on-premises-AD-Domain-Services/player]
>
>

## <a name="get-started-with-azure-ad-connect-health"></a>Wprowadzenie do programu Azure AD Connect Health
tooget wprowadzenie do usługi Azure AD Connect Health, użyj hello następujące kroki:

1. [Uzyskaj usługę Azure AD w wersji Premium](../active-directory-get-started-premium.md) lub [rozpocznij okres próbny](https://azure.microsoft.com/trial/get-started-active-directory/).
2. [Pobierz i zainstaluj agentów programu Azure AD Connect Health](#download-and-install-azure-ad-connect-health-agent) na serwerach tożsamości.
3. Widok hello Azure AD Connect Health w pulpicie nawigacyjnym w [https://aka.ms/aadconnecthealth](https://aka.ms/aadconnecthealth).

> [!NOTE]
> Należy pamiętać, że przed wyświetleniem danych na pulpicie nawigacyjnym usługi Azure AD Connect Health, należy tooinstall hello agentów programu Azure AD Connect Health na serwerach docelowych.
>
>

## <a name="download-and-install-azure-ad-connect-health-agent"></a>Pobieranie i instalowanie agenta programu Azure AD Connect Health
* Upewnij się, że możesz [spełniają wymagania hello](active-directory-aadconnect-health-agent-install.md#requirements) dla usługi Azure AD Connect Health.
* Wprowadzenie do korzystania z programu Azure AD Connect Health dla usług AD FS
    * [Pobierz agenta programu Azure AD Connect Health dla usług AD FS.](http://go.microsoft.com/fwlink/?LinkID=518973)
    * [Zobacz instrukcje dotyczące instalacji hello](active-directory-aadconnect-health-agent-install.md#installing-the-azure-ad-connect-health-agent-for-ad-fs).
* Wprowadzenie do korzystania z programu Azure AD Connect Health do celów synchronizacji
    * [Pobierz i zainstaluj najnowszą wersję programu Azure AD Connect, hello](http://go.microsoft.com/fwlink/?linkid=615771). Witaj agenta programu Health do celów synchronizacji zostanie zainstalowana jako część hello Azure AD Connect instalacji (w wersji 1.0.9125.0 lub nowszej).
* Wprowadzenie do korzystania z programu Azure AD Connect Health dla usług AD DS
    * [Pobierz agenta programu Azure AD Connect Health dla usług AD DS](http://go.microsoft.com/fwlink/?LinkID=820540).
    * [Zobacz instrukcje dotyczące instalacji hello](active-directory-aadconnect-health-agent-install.md#installing-the-azure-ad-connect-health-agent-for-ad-ds).

## <a name="azure-ad-connect-health-portal"></a>Portal programu Azure AD Connect Health
portal Azure AD Connect Health Hello zawiera widoki alertów, monitorowania wydajności i analizy użycia. Witaj https://aka.ms/aadconnecthealth adres URL przejście toohello głównego bloku programu Azure AD Connect Health. Blok możesz traktować jak okno. W głównym bloku hello, zobacz **Szybki Start**, usługi Azure AD Connect Health i dodatkowe opcje konfiguracji. Zobacz hello zrzut ekranu i krótki wyjaśnienia, które należy wykonać zrzut ekranu hello. Po wdrożeniu agentów hello usługi kondycji hello automatycznie rozpoznaje hello usługi Azure AD Connect Health jest monitorowanie.

> [!NOTE]
> Informacje o licencji zbiorczej, zobacz hello [Azure AD Connect — często zadawane pytania](active-directory-aadconnect-health-faq.md) lub hello [strony cennik usługi Azure AD](https://aka.ms/aadpricing).
    
![Portal programu Azure AD Connect Health](./media/active-directory-aadconnect-health/portal4.png)

* **Szybki Start**: po wybraniu tej opcji hello **Szybki Start** zostanie otwarty blok. Możesz pobrać hello Azure AD Connect Health Agent, wybierając **Pobierz narzędzia**. Można również uzyskać dostęp do dokumentacji i przekazać swoją opinię.
* **Usługi federacyjne Active Directory**: Ta opcja powoduje wyświetlenie wszystkich hello usług AD FS usługi Azure AD Connect Health są aktualnie monitorowane. Po wybraniu wystąpienia bloku hello, którego kliknięcie spowoduje otwarcie zawiera informacje dotyczące tego wystąpienia usługi. Informacje te obejmują przegląd, właściwości, alerty, wyniki monitorowania i analizy użycia. Dowiedz się więcej o możliwości hello na [przy użyciu usługi Azure AD Connect Health z usługami AD FS](active-directory-aadconnect-health-adfs.md).
* **Azure Active Directory Connect (synchronizacja)**: ta opcja umożliwia pokazanie serwerów programu Azure AD Connect, które są aktualnie monitorowane przez program Azure AD Connect Health. Po wybraniu wpis hello bloku hello, którego kliknięcie spowoduje otwarcie zawiera informacje na temat serwerów programu Azure AD Connect. Dowiedz się więcej o możliwości hello na [przy użyciu usługi Azure AD Connect Health dla synchronizacji](active-directory-aadconnect-health-sync.md).
* **Usługi domenowe Active Directory**: Ta opcja powoduje wyświetlenie wszystkich lasów usług AD DS hello Azure AD Connect Health są aktualnie monitorowane. Po wybraniu lesie bloku hello, którego kliknięcie spowoduje otwarcie zawiera informacje o tym lesie. Informacje te obejmują przegląd istotnymi informacjami, hello kontrolerów domeny z pulpitu nawigacyjnego, pulpit nawigacyjny stan replikacji hello, alerty i monitorowania. Dowiedz się więcej o możliwości hello na [przy użyciu usługi Azure AD Connect Health z usługami AD DS](active-directory-aadconnect-health-adds.md).
* **Skonfiguruj**: Ta sekcja zawiera następujące opcje tooturn hello lub wyłącz:

  - Automatyczna aktualizacja tooautomatically aktualizacji hello Azure AD Connect Health agent toohello najnowszą wersję: udostępnianych będą automatycznie aktualizowane toohello najnowsze wersje hello Azure AD Connect Health Agent. Ta opcja jest domyślnie włączona.
  - Zezwalaj na dane kondycji katalogu programu Microsoft access tooyour usługi Azure AD w celu rozwiązywania problemów tylko: Jeśli ta opcja jest włączona, można zobaczyć Microsoft hello tych samych danych, które pojawi się. Te informacje mogą ułatwić rozwiązywanie problemów i uzyskiwanie pomocy. Ta opcja jest domyślnie wyłączona.

## <a name="related-links"></a>Powiązane linki
* [Instalowanie agenta programu Azure AD Connect Health](active-directory-aadconnect-health-agent-install.md)
* [Operacje w programie Azure AD Connect Health](active-directory-aadconnect-health-operations.md)
* [Używanie programu Azure AD Connect Health z usługami AD FS](active-directory-aadconnect-health-adfs.md)
* [Używanie programu Azure AD Connect Health w celu synchronizacji](active-directory-aadconnect-health-sync.md)
* [Używanie programu Azure AD Connect Health z usługami AD DS](active-directory-aadconnect-health-adds.md)
* [Azure AD Connect Health — często zadawane pytania](active-directory-aadconnect-health-faq.md)
* [Historia wersji programu Azure AD Connect Health](active-directory-aadconnect-health-version-history.md)
