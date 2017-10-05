---
title: "Usługi Azure AD i wymagania usługi Active Directory dla usługi Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skonfigurować usługi Active Directory do pracy z usługą Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 66366b25-6012-45fa-a4f6-da0ddfe0b486
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 78008a032faa93795cc02b720d68a0c6f5f16e9a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad--active-directory-requirements-for-azure-remoteapp"></a>Usługi Azure AD i wymagania usługi Active Directory dla usługi Azure RemoteApp
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Szczegółowe informacje zawiera [powiadomienie](https://go.microsoft.com/fwlink/?linkid=821148).
> 
> 

Kolekcji hybrydowej usługi Azure RemoteApp lub kolekcji w chmurze, która ma zostać utworzona Federacja za pomocą AD Connect należy wykonać następujące czynności.

### <a name="connect-azure-ad-and-active-directory"></a>Łączenie usługi Azure AD i usługi Active Directory
Jeśli chcesz połączyć z dzierżawy usługi Azure AD i środowiska lokalnej usługi Active Directory, należy użyć AD Connect. Spowoduje przejście tylko [4 kliknięć](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) nawiązać dwa katalogi.

Uwaga — synchronizacja katalogów jest wymagana dla kolekcji hybrydowej.

### <a name="make-sure-your-domaincom-match"></a>Upewnij się, że Twoje "@domain.com" zgodny
Przed rozpoczęciem pracy upewnij się, że nazwa UPN lasu lokalnego zgodny z sufiksem domeny domenę usługi Azure AD. 

Po skonfigurowaniu sufiks nazwy UPN domeny w usłudze Azure AD wszystkich użytkowników logujących się do usługi Azure RemoteApp będzie zalogować się jako "użytkownik @<the suffix you set up>." Upewnij się, że użytkownicy mogą również Zaloguj się za pomocą takie same user@suffix w domenie lokalnej. W niektórych przypadkach skonfigurowaniem jedną nazwę domeny w usłudze Azure AD podczas określania sufiksu inną domenę dla użytkownika na — lokalnej W takim przypadku użytkowników nie będzie można połączyć się z dowolnym komputerów przyłączonych do domeny lub zasobów za pomocą usługi Azure RemoteApp.

Na przykład skonfigurować sufiks domeny Twojej nazwy UPN w usłudze AAD jako contoso.com, ale niektórzy użytkownicy korzystają z lokalnej usługi Active są skonfigurowane do logowania się przy użyciu @contoso.uk, nie będzie mógł poprawnie Zaloguj się do kolekcji ARA tych użytkowników. Użytkownicy nazwy UPN w usłudze AAD i AD muszą być takie same, dla nazwy logowania w celu umożliwienia"

### <a name="create-objects-for-azure-remoteapp"></a>Tworzenie obiektów dla usługi Azure RemoteApp
Należy także utworzyć następujące lokalną obiektów usługi Active Directory:

* Konto usługi, aby zapewnić dostęp do zasobów domeny dla programów RemoteApp przez dołączenie do domeny lokalnej RDSH punktów końcowych.
* Jednostki organizacyjnej (OU) zawierają obiekty komputera usługi RemoteApp. Użyj jednostki organizacyjnej, jest zalecane (lecz nie wymagane) izolowanie kont i zasad, które będą używane z usługi RemoteApp.

Oba te obiekty potrzebne podczas tworzenia kolekcji usługi RemoteApp, dlatego należy najpierw wykonać następujące kroki.

