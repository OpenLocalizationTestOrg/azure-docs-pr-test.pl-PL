---
title: "łączniki serwera Proxy aplikacji usługi Azure AD z portalu aaaClassic | Dokumentacja firmy Microsoft"
description: "Obejmuje jak toocreate grup łączników w serwera Proxy aplikacji usługi Azure AD i zarządzanie nimi."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: b283796a-9679-4c79-b703-802bb850f65d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 43559b0f4ffc3c7dbbf00901e89ac276d01796e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-on-separate-networks-and-locations-using-connector-groups"></a>Publikowanie aplikacji w odrębnych sieci i lokalizacje przy użyciu grup łącznika
> [!div class="op_single_selector"]
> * [Witryna Azure Portal](active-directory-application-proxy-connectors-azure-portal.md)
> * [Klasyczna witryna Azure Portal](active-directory-application-proxy-connectors.md)
>
>

Łącznik grupy są przydatne w przypadku różnych scenariuszy, w tym:

* Lokacje z wielu połączonych centrów danych. W takim przypadku ma tookeep tyle ruchu w ramach centrum danych hello możliwie ponieważ łącza między datacenter są kosztowne i bardzo wolno. Można wdrożyć łączników w każdym datacenter tooserve tylko hello aplikacje znajdujące się w obrębie centrum danych hello. Takie podejście minimalizuje łącza między datacenter i zapewnia całkowicie przezroczysty tooyour użytkowników.
* Zarządzanie aplikacji zainstalowanych w izolowanych sieciach, które nie są częścią sieci firmowej głównego hello. Łącznik grup tooinstall dedykowanego łączników można użyć w izolowanych sieciach tooalso odizolowanego aplikacji toohello sieci.
* Aplikacje zainstalowane na IaaS, aby uzyskać dostęp do chmury łącznik grupy zapewniają wspólnej toosecure hello dostępu tooall hello aplikacje usługi. Łącznik grup nie utworzyć dodatkowe zależności w sieci firmowej lub fragmentu środowisko aplikacji hello. Łączniki można zainstalować na każdym centrum danych w chmurze i służyć tylko te aplikacje, które znajdują się w tej sieci. Można zainstalować wiele łączników tooachieve wysokiej dostępności.
* Obsługa środowisk obejmującego wiele lasów, w których określonych łączników można wdrożone w każdym lesie i ustawić tooserve określonych aplikacji.
* Łącznik grupy mogą być używane w lokacjach odzyskiwania po awarii tooeither wykryć pracy awaryjnej lub jako kopia zapasowa hello główny witryny.
* Łącznik grup może również być używane tooserve wielu firm z pojedynczej dzierżawy.

## <a name="prerequisite-create-your-connectors"></a>Wymaganie wstępne: Tworzenie łączników
toogroup łączników, [zainstalować wiele łączników](active-directory-application-proxy-enable.md), nazwie i grupować. Na koniec masz tooassign ich toospecific aplikacji.

## <a name="step-1-create-connector-groups"></a>Krok 1: Tworzenie grup łącznika
Można utworzyć dowolną liczbę grup łącznika. Tworzenie grupy łącznika odbywa się w hello klasycznego portalu Azure.

1. Wybierz katalog, a następnie kliknij przycisk **Konfiguruj**.  
    ![Serwer proxy aplikacji, skonfiguruj zrzut ekranu — kliknij przycisk Zarządzaj grupami łącznika](./media/active-directory-application-proxy-connectors/app_proxy_connectors_creategroup.png)
2. W obszarze Serwer Proxy aplikacji, kliknij **grup zarządzania łącznika** i utworzyć grupę łącznika przez nadanie grupy hello nazwy.  
    ![Zrzut ekranu — Nazwa nowej grupy grup łącznika serwera proxy aplikacji](./media/active-directory-application-proxy-connectors/app_proxy_connectors_namegroup.png)

## <a name="step-2-assign-connectors-tooyour-groups"></a>Krok 2: Przypisywanie łączniki tooyour grup
Po utworzeniu grupy łącznika hello Przenieś hello łączniki toohello odpowiedniej grupy.

1. W obszarze **serwera Proxy aplikacji**, kliknij przycisk **Zarządzanie łączniki**.
2. W obszarze **grupy**, zaznacz grupę hello ma przez każdy łącznik. Łączniki hello się toobecome minut too10 może potrwać aktywne w hello nowej grupy.  
    ![Zrzut w ekranu łączniki serwera proxy aplikacji — wybierz grupę z menu rozwijanego](./media/active-directory-application-proxy-connectors/app_proxy_connectors_connectorlist.png)

## <a name="step-3-assign-applications-tooyour-connector-groups"></a>Krok 3: Przypisywanie aplikacji tooyour łącznika grup
ostatni krok Hello jest tooset każdej grupy łącznika toohello aplikacji, która dostarcza je.

1. W hello klasycznego portalu Azure w danym katalogu, wybierz hello aplikacji tooassign toohello grupy i kliknij **Konfiguruj**.
2. W obszarze **grupy łącznika**, wybierz grupy hello ma hello toouse aplikacji. Ta zmiana zostanie zastosowane natychmiast.  
    ![Zrzut ekranu z grupy łącznika serwera proxy aplikacji — wybierz grupę z menu rozwijanego](./media/active-directory-application-proxy-connectors/app_proxy_connectors_newgroup.png)

## <a name="see-also"></a>Zobacz też
* [Włączanie serwera Proxy aplikacji](active-directory-application-proxy-enable.md)
* [Włączanie logowania jednokrotnego](active-directory-application-proxy-sso-using-kcd.md)
* [Włączanie dostępu warunkowego](active-directory-application-proxy-conditional-access.md)
* [Rozwiązywanie problemów, które masz problem z serwerem Proxy aplikacji](active-directory-application-proxy-troubleshoot.md)

Najnowsze wiadomości powitania i aktualizacji, zapoznaj się z hello [Blog dotyczący serwera Proxy aplikacji](http://blogs.technet.com/b/applicationproxyblog/)
