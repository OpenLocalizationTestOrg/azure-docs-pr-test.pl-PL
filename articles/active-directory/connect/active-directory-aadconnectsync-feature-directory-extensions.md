---
title: "Synchronizacja programu Azure AD Connect: rozszerzenia katalogów | Dokumentacja firmy Microsoft"
description: "W tym temacie opisano funkcję rozszerzeń katalogu hello w programie Azure AD Connect."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 995ee876-4415-4bb0-a258-cca3cbb02193
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 31525ae914aa4d9e047ea1515b460a8311d5c815
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-directory-extensions"></a>Synchronizacja programu Azure AD Connect: rozszerzenia katalogów
Rozszerzenia katalogów pozwala tooextend hello schematu w usłudze Azure AD przy użyciu własnego atrybutów z lokalnej usługi Active Directory. Ta funkcja umożliwia aplikacji biznesowych toobuild korzystanie z atrybutów kontynuować toomanage lokalnymi. Te atrybuty mogą być używane za pośrednictwem [rozszerzeń katalogu Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) lub [Microsoft Graph](https://graph.microsoft.io/). Widać hello atrybuty dostępne przy użyciu [explorer Azure AD Graph](https://graphexplorer.cloudapp.net) i [Eksplorator Microsoft Graph](https://graphexplorer2.azurewebsites.net/) odpowiednio.

Obecnie nie obciążenie usługi Office 365 wykorzystuje te atrybuty.

Konfigurowanie dodatkowych atrybutów, które chcesz toosynchronize w ścieżce ustawienia niestandardowe powitania w Kreatorze instalacji hello.
![Kreator rozszerzenia schematu](./media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)  
Hello instalacji zawiera następujące atrybuty, które są prawidłowe kandydatów hello:

* Typy obiektów użytkowników i grup
* Atrybuty jednowartościowe: String, Boolean, Integer, dane binarne
* Atrybuty wielowartościowe: ciąg, dane binarne

Witaj listę atrybutów jest do odczytu z pamięci podręcznej schematu hello utworzony podczas instalacji programu Azure AD Connect. Jeśli rozszerzono schemat usługi Active Directory hello przy użyciu dodatkowych atrybutów, następnie hello [schematu musi zostać odświeżona](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema) przed te nowe atrybuty są widoczne.

Obiektu w usłudze Azure AD mogą mieć atrybutów rozszerzeń katalogu too100. Witaj maksymalna długość wynosi 250 znaków. Jeśli wartość atrybutu jest dłuższy, następnie zostanie obcięta przez hello aparatu synchronizacji.

Podczas instalacji programu Azure AD Connect aplikacja jest zarejestrowany, których te atrybuty są dostępne. Tę aplikację w portalu Azure hello jest widoczny.  
![Aplikacja rozszerzenia schematu](./media/active-directory-aadconnectsync-feature-directory-extensions/extension3new.png)

Te atrybuty są teraz dostępne za pośrednictwem wykresu:  
![Graph](./media/active-directory-aadconnectsync-feature-directory-extensions/extension4.png)

atrybuty Hello są poprzedzane prefiksem rozszerzenia\_{AppClientId}\_. Witaj AppClientId ma hello samą wartość dla wszystkich atrybutów w dzierżawie usługi Azure AD.

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o hello [synchronizacja programu Azure AD Connect](active-directory-aadconnectsync-whatis.md) konfiguracji.

Dowiedz się więcej na temat [integrowania tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).
