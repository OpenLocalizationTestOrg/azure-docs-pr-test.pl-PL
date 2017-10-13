---
title: "Używanie programu Azure AD Connect Health z usługami AD DS | Microsoft Docs"
description: "Jest to strona programu Azure AD Connect Health, na której omówiono monitorowanie usług AD DS."
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
ms.openlocfilehash: 9e5b45d71b978c383932409f0037a4f6f32d0cb3
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="using-azure-ad-connect-health-with-ad-ds"></a>Używanie programu Azure AD Connect Health z usługami AD DS
Poniższa dokumentacja dotyczy monitorowania Usług domenowych Active Directory przy użyciu programu Azure AD Connect Health. Obsługiwane wersje usługi AD DS: Windows Server 2008 R2, Windows Server 2012,Windows Server 2012 R2 i Windows Server 2016.

Aby uzyskać więcej informacji na temat monitorowania usług AD FS za pomocą programu Azure AD Connect Health, zobacz [Używanie programu Azure AD Connect Health z usługami AD FS](active-directory-aadconnect-health-adfs.md). Ponadto, aby uzyskać informacje na temat monitorowania programu Azure AD Connect (synchronizacja) za pomocą programu Azure AD Connect Health, zobacz [Używanie programu Azure AD Connect Health w celu synchronizacji](active-directory-aadconnect-health-sync.md).

![Program Azure AD Connect Health dla usług AD DS](./media/active-directory-aadconnect-health/aadconnect-health-adds-entry.png)

## <a name="alerts-for-azure-ad-connect-health-for-ad-ds"></a>Alerty programu Azure AD Connect Health dla usług AD DS
Sekcja Alerty w ramach programu Azure AD Connect Health dla usług AD DS zawiera listę aktywnych i rozwiązanych alertów związanych z kontrolerami domeny. Wybranie aktywnego lub rozwiązanego alertu spowoduje otworzenie nowego bloku zawierającego dodatkowe informacje, a także kroki rozwiązania i linki do dodatkowej dokumentacji. Każdy typ alertu może mieć jedno lub większą liczbę wystąpień odpowiadających każdemu kontrolerowi domeny, którego dotyczy dany alert. W dolnej części bloku alertu można kliknąć dwukrotnie kontroler domeny, którego dotyczy alert, aby otworzyć nowy blok z dodatkowymi szczegółami dotyczącymi tego wystąpienia alertu.

W ramach tego bloku można włączyć powiadomienia e-mail dla alertów i zmienić zakres czasu w widoku. Rozszerzenie zakresu czasu pozwoli zobaczyć wcześniejsze rozwiązane alerty.

![Błąd synchronizacji programu Azure AD Connect](./media/active-directory-aadconnect-health/aadconnect-health-adds-alerts.png)

## <a name="domain-controllers-dashboard"></a>Pulpit nawigacyjny kontrolerów domeny
Ten pulpit nawigacyjny udostępnia widok topologiczny środowiska wraz z kluczowymi metrykami operacyjnymi i stanem kondycji każdego z monitorowanych kontrolerów domeny. Prezentowane metryki ułatwiają szybkie identyfikowanie wszelkich kontrolerów domen, które mogą wymagać dalszych badań. Domyślnie jest wyświetlana tylko część kolumn. Jednak można wyświetlić wszystkie dostępne kolumny, klikając dwukrotnie polecenie Kolumny. Po wybraniu najbardziej interesujących kolumn ten pulpit nawigacyjny umożliwia łatwe sprawdzenie kondycji środowiska usług AD DS w jednym miejscu.

![Kontrolery domeny](./media/active-directory-aadconnect-health/aadconnect-health-adds-domainsandsites-dashboard.png)

Kontrolery domeny można grupować według ich odpowiedniej domeny lub lokacji, co pomaga w zrozumieniu topologii środowiska. Ponadto dwukrotne kliknięcie nagłówka bloku umożliwia zmaksymalizowanie pulpitu nawigacyjnego w celu wykorzystania całej dostępnej powierzchni ekranu. Ten większy widok jest przydatny, gdy jest wyświetlanych wiele kolumn.

## <a name="replication-status-dashboard"></a>Pulpit nawigacyjny stanu replikacji
Ten pulpit nawigacyjny zawiera widok stanu replikacji i topologii replikacji monitorowanych kontrolerów domeny. Wyświetlany jest stan ostatniej próby replikacji wraz z pomocną dokumentacją dotyczącą dowolnego znalezionego błędu. Możesz kliknąć dwukrotnie kontroler domeny z błędem, aby otworzyć nowy blok zawierający następujące informacje: szczegóły błędu, zalecane kroki rozwiązania oraz linki do dokumentacji dotyczącej rozwiązywania problemów.

![Stan replikacji](./media/active-directory-aadconnect-health/aadconnect-health-adds-replication.png)

## <a name="monitoring"></a>Monitorowanie
Ta funkcja udostępnia graficzne trendy różnych liczników wydajności, które są stale zbierane z każdego monitorowanego kontrolera domeny. Umożliwia to łatwe porównywanie wydajności kontrolera domeny ze wszystkimi innymi monitorowanymi kontrolerami domeny w lesie. Ponadto można wyświetlić obok siebie różne liczniki wydajności, co jest pomocne podczas rozwiązywania problemów w danym środowisku.

![Monitorowanie](./media/active-directory-aadconnect-health/aadconnect-health-adds-monitoring.png)

Domyślnie zostały wstępnie wybrane cztery liczniki wydajności. Można jednak dodać inne przez kliknięcie polecenia filtru i zaznaczenie lub usunięcie zaznaczenia odpowiednich liczników wydajności. Ponadto możesz kliknąć dwukrotnie wykres licznika wydajności, aby otworzyć nowy blok zawierający punkty danych dla każdego monitorowanego kontrolera domeny.

## <a name="related-links"></a>Powiązane linki
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Instalowanie agenta programu Azure AD Connect Health](active-directory-aadconnect-health-agent-install.md)
* [Operacje w programie Azure AD Connect Health](active-directory-aadconnect-health-operations.md)
* [Używanie programu Azure AD Connect Health z usługami AD FS](active-directory-aadconnect-health-adfs.md)
* [Używanie programu Azure AD Connect Health w celu synchronizacji](active-directory-aadconnect-health-sync.md)
* [Azure AD Connect Health — często zadawane pytania](active-directory-aadconnect-health-faq.md)
* [Historia wersji programu Azure AD Connect Health](active-directory-aadconnect-health-version-history.md)

