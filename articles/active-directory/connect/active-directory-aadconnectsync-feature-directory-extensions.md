---
title: "Synchronizacja programu Azure AD Connect: rozszerzenia katalogów | Dokumentacja firmy Microsoft"
description: "W tym temacie opisano funkcję rozszerzeń katalogu w programie Azure AD Connect."
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
ms.openlocfilehash: 8ab9944437443a6d796345782f4f798aec96a0f6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-directory-extensions"></a>Synchronizacja programu Azure AD Connect: rozszerzenia katalogów
Rozszerzenia katalogów umożliwia rozszerzanie schematu w usłudze Azure AD przy użyciu własnego atrybutów z lokalnej usługi Active Directory. Ta funkcja umożliwia tworzenie aplikacji biznesowych, korzystanie z atrybutów, można nadal zarządzać lokalnymi. Te atrybuty mogą być używane za pośrednictwem [rozszerzeń katalogu Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) lub [Microsoft Graph](https://graph.microsoft.io/). Widać atrybuty dostępne przy użyciu [explorer Azure AD Graph](https://graphexplorer.cloudapp.net) i [Eksplorator Microsoft Graph](https://graphexplorer2.azurewebsites.net/) odpowiednio.

Obecnie nie obciążenie usługi Office 365 wykorzystuje te atrybuty.

Możesz skonfigurować dodatkowych atrybutów, które chcesz synchronizować w ścieżce ustawienia niestandardowe w Kreatorze instalacji.
![Kreator rozszerzenia schematu](./media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)  
Instalacja zawiera następujące atrybuty, które są kandydatami prawidłowy:

* Typy obiektów użytkowników i grup
* Atrybuty jednowartościowe: String, Boolean, Integer, dane binarne
* Atrybuty wielowartościowe: ciąg, dane binarne

Lista atrybutów jest do odczytu z pamięci podręcznej schematu, utworzony podczas instalacji programu Azure AD Connect. Jeśli rozszerzono schemat usługi Active Directory przy użyciu dodatkowych atrybutów, a następnie [schematu musi zostać odświeżona](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema) przed te nowe atrybuty są widoczne.

Obiektu w usłudze Azure AD mogą mieć maksymalnie 100 atrybuty rozszerzenia katalogu. Maksymalna długość wynosi 250 znaków. Jeśli wartość atrybutu jest dłuższy, następnie zostanie obcięta przez aparat synchronizacji.

Podczas instalacji programu Azure AD Connect aplikacja jest zarejestrowany, których te atrybuty są dostępne. Można wyświetlić tę aplikację w portalu Azure.  
![Aplikacja rozszerzenia schematu](./media/active-directory-aadconnectsync-feature-directory-extensions/extension3new.png)

Te atrybuty są teraz dostępne za pośrednictwem wykresu:  
![Graph](./media/active-directory-aadconnectsync-feature-directory-extensions/extension4.png)

Atrybuty są poprzedzane prefiksem rozszerzenia\_{AppClientId}\_. AppClientId ma taką samą wartość dla wszystkich atrybutów w dzierżawie usługi Azure AD.

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o [synchronizacja programu Azure AD Connect](active-directory-aadconnectsync-whatis.md) konfiguracji.

Dowiedz się więcej na temat [integrowania tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).
