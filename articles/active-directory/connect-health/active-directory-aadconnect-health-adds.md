---
title: "Program Azure AD Connect Health z usługami AD DS aaaUsing | Dokumentacja firmy Microsoft"
description: "Jest to strona hello Azure AD Connect Health, która będzie omawiać jak toomonitor usług AD DS."
services: active-directory
documentationcenter: 
author: arluca
manager: femila
editor: curtand
ms.assetid: 19e3cf15-f150-46a3-a10c-2990702cd700
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: e2fb6be65407d02c214dcab385b85d6cb54f48de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-ad-connect-health-with-ad-ds"></a>Używanie programu Azure AD Connect Health z usługami AD DS
po dokumentacji Hello jest toomonitoring określonych Active Directory usług domenowych w usłudze Azure AD Connect Health. Witaj obsługiwane wersje usług AD DS są: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 i Windows Server 2016.

Aby uzyskać więcej informacji na temat monitorowania usług AD FS za pomocą programu Azure AD Connect Health, zobacz [Używanie programu Azure AD Connect Health z usługami AD FS](active-directory-aadconnect-health-adfs.md). Ponadto, aby uzyskać informacje na temat monitorowania programu Azure AD Connect (synchronizacja) za pomocą programu Azure AD Connect Health, zobacz [Używanie programu Azure AD Connect Health w celu synchronizacji](active-directory-aadconnect-health-sync.md).

![Program Azure AD Connect Health dla usług AD DS](./media/active-directory-aadconnect-health/aadconnect-health-adds-entry.png)

## <a name="alerts-for-azure-ad-connect-health-for-ad-ds"></a>Alerty programu Azure AD Connect Health dla usług AD DS
Hello sekcja alerty w ramach usługi Azure AD Connect Health dla usług AD DS, udostępnia listę aktywne i rozwiązane alerty, powiązane tooyour kontrolerów domeny. Wybór aktywnego lub rozwiązanego alertu zostanie otwarty nowy blok z dodatkowymi informacjami, wraz z kroki rozwiązania i łączy toosupporting dokumentacji. Każdy typ alertu może mieć co najmniej jedno wystąpienie, które odpowiada tooeach kontrolerów domeny hello objętych tym alertem określonego. Dolnej hello hello bloku alertu kliknij dwukrotnie tooopen kontrolera domeny dodatkowe blok zawierający więcej szczegółów dotyczących tego wystąpienia alertu.

W ramach tego bloku można włączyć powiadomienia e-mail dla alertów i zmień zakres czasu hello w widoku. Rozszerzanie zakresu czasu hello umożliwia toosee wcześniejsze rozstrzygnięte alerty.

![Błąd synchronizacji programu Azure AD Connect](./media/active-directory-aadconnect-health/aadconnect-health-adds-alerts.png)

## <a name="domain-controllers-dashboard"></a>Pulpit nawigacyjny kontrolerów domeny
Ten pulpit nawigacyjny udostępnia widok topologiczny środowiska wraz z kluczowymi metrykami operacyjnymi i stanem kondycji każdego z monitorowanych kontrolerów domeny. metryki Hello przedstawione pomocy tooquickly zidentyfikować, wszystkie kontrolery domeny, które mogą wymagać dalszego postępowania. Domyślnie jest wyświetlany tylko podzestaw hello kolumn. Jednak możesz znaleźć hello cały zestaw dostępnych kolumn, klikając polecenie kolumny hello. Wybieranie kolumn hello, które najbardziej interesujących Cię, włącza ten pulpit nawigacyjny w pojedynczy i łatwe umieścić tooview hello kondycji środowiska usług AD DS.

![Kontrolery domeny](./media/active-directory-aadconnect-health/aadconnect-health-adds-domainsandsites-dashboard.png)

Kontrolery domeny można grupować według ich odpowiedniej domeny lub lokacji, co jest przydatne dla zrozumienia hello środowiska topologii. Ponadto po dwukrotnym kliknięciu nagłówka bloku hello pulpitu nawigacyjnego hello maksymalizuje tooutilize hello dostępne ekranu nieruchomości. Ten większy widok jest przydatny, gdy jest wyświetlanych wiele kolumn.

## <a name="replication-status-dashboard"></a>Pulpit nawigacyjny stanu replikacji
Ten pulpit nawigacyjny zawiera widok hello topologii replikacji w stan i replikacji z monitorowanych kontrolerów domeny. Stan Hello hello ostatniej próby replikacji znajduje się wraz z jakiegokolwiek błędu, który można znaleźć w dokumentacji przydatne. Dwukrotne kliknięcie kontrolera domeny z powodu błędu tooopen nowy blok informacji takich jak: szczegółowe informacje o błędzie hello, zalecane kroki rozwiązania i łączy tootroubleshooting dokumentacji.

![Stan replikacji](./media/active-directory-aadconnect-health/aadconnect-health-adds-replication.png)

## <a name="monitoring"></a>Monitorowanie
Ta funkcja zapewnia graficznego trendów liczników wydajności różnych, które są stale pobierane z każdej hello monitorowanych kontrolerów domeny. Umożliwia to łatwe porównywanie wydajności kontrolera domeny ze wszystkimi innymi monitorowanymi kontrolerami domeny w lesie. Ponadto można wyświetlić obok siebie różne liczniki wydajności, co jest pomocne podczas rozwiązywania problemów w danym środowisku.

![Monitorowanie](./media/active-directory-aadconnect-health/aadconnect-health-adds-monitoring.png)

Domyślnie możemy wstępnie zostały wybrane cztery liczniki wydajności; Możesz jednak zawierać inne polecenie filtru hello i zaznaczając lub usunięcie zaznaczenia wszystkie liczniki wydajności żądany. Ponadto można kliknąć dwukrotnie tooopen wykres licznika wydajności nowy blok, w tym punktów danych dla poszczególnych kontrolerów domeny hello monitorowane.

## <a name="related-links"></a>Powiązane linki
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Instalowanie agenta programu Azure AD Connect Health](active-directory-aadconnect-health-agent-install.md)
* [Operacje w programie Azure AD Connect Health](active-directory-aadconnect-health-operations.md)
* [Używanie programu Azure AD Connect Health z usługami AD FS](active-directory-aadconnect-health-adfs.md)
* [Używanie programu Azure AD Connect Health w celu synchronizacji](active-directory-aadconnect-health-sync.md)
* [Azure AD Connect Health — często zadawane pytania](active-directory-aadconnect-health-faq.md)
* [Historia wersji programu Azure AD Connect Health](active-directory-aadconnect-health-version-history.md)

