---
title: "aaaAzure AD + wymagania usługi Active Directory dla usługi Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooset się toowork usługi Active Directory z usługą Azure RemoteApp."
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
ms.openlocfilehash: c1c4a7ad6fb96ec4d479fdc231f03d81b58b2b71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad--active-directory-requirements-for-azure-remoteapp"></a>Usługi Azure AD i wymagania usługi Active Directory dla usługi Azure RemoteApp
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.
> 
> 

Kolekcji hybrydowej usługi Azure RemoteApp lub kolekcji w chmurze, które mają toofederate za pomocą AD Connect należy toodo hello poniżej.

### <a name="connect-azure-ad-and-active-directory"></a>Łączenie usługi Azure AD i usługi Active Directory
Tooconnect dzierżawy usługi Azure AD i środowiska lokalnej usługi Active Directory, należy użyć AD Connect. Spowoduje przejście tylko [4 kliknięć](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) tooconnect hello dwa katalogi.

Uwaga — synchronizacja katalogów jest wymagana dla kolekcji hybrydowej.

### <a name="make-sure-your-domaincom-match"></a>Upewnij się, że Twoje "@domain.com" zgodny
Przed rozpoczęciem upewnij się, że hello nazwy UPN użytkownika lokalnego lasu dopasowań hello sufiksu domeny usługi Azure AD. 

Po skonfigurowaniu sufiks domeny hello nazwy UPN w usłudze Azure AD wszystkich użytkowników logujących się do usługi Azure RemoteApp będzie zalogować się jako "użytkownik @<hello suffix you set up>." Upewnij się, że użytkownicy mogą również Zaloguj się za pomocą hello takie same user@suffix w domenie lokalnej hello. W niektórych przypadkach skonfigurowaniem jedną nazwę domeny w usłudze Azure AD podczas określania sufiksu inną domenę dla hello użytkownika na — lokalnej W takim przypadku użytkowników nie będzie możliwe tooconnect tooany przyłączonych do domeny komputerów lub zasobów za pomocą usługi Azure RemoteApp.

Na przykład skonfigurować sufiks domeny Twojej nazwy UPN w usłudze AAD jako contoso.com, ale niektórzy użytkownicy korzystają z lokalnej usługi Active są toolog skonfigurowany przy użyciu @contoso.uk, a następnie te użytkownicy nie będą mogli toocorrectly Zaloguj się do hello ARA kolekcji. Użytkownicy muszą mieć nazwy UPN w usłudze AAD i AD hello takie same dla możliwości toobe logowania hello"

### <a name="create-objects-for-azure-remoteapp"></a>Tworzenie obiektów dla usługi Azure RemoteApp
Należy również hello toocreate po lokalnych obiektów usługi Active Directory:

* Usługa konta tooprovide dostępu toodomain zasobów dla programów RemoteApp przez dołączenie RDSH punktów końcowych toohello lokalnej domeny.
* Jednostki organizacyjnej (OU) toocontain RemoteApp obiekty komputera. Użycie hello jednostki Organizacyjnej jest konta hello tooisolate zalecane (ale nie są wymagane) i zasad, które będą używane z usługą RemoteApp.

Oba te obiekty potrzebne podczas tworzenia kolekcji usługi RemoteApp, więc najpierw należy toodo się, że te kroki.

