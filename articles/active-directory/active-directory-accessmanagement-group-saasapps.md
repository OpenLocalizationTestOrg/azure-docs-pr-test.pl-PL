---
title: "aaaUsing grupy tooSaaS dostępu toomanage aplikacji | Dokumentacja firmy Microsoft"
description: "Jak toouse grup w usłudze Azure Active Directory — wersja Premium lub podstawowa tooassign dostęp do aplikacji tooSaaS, które są zintegrowane z usługą Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: ab8dee63-bedc-46ca-8852-234f5c16ae98
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: it-pro;oldportal
ms.openlocfilehash: f45ea4472b3d88e8ea514af3db31b4cc9ea68d58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-a-group-toomanage-access-toosaas-applications"></a>Przy użyciu aplikacji tooSaaS grupy toomanage dostępu
Za pomocą usługi Azure Active Directory (Azure AD) z licencją Azure AD Premium lub usługi Azure AD podstawowa, można użyć grup tooassign dostępu tooa SaaS aplikacji, która jest zintegrowany z usługą Azure AD. Na przykład jeśli chcesz tooassign dostępu dla hello marketing działu toouse pięciu różnych aplikacji SaaS, można utworzyć grupę, która zawiera użytkowników hello w dziale marketingu hello i przypisz tej grupy toothese pięć SaaS aplikacje, które są wymagane przez dział marketingu hello. W ten sposób można oszczędzić czas dzięki zarządzaniu hello członkostwa hello marketingu dział w jednym miejscu. Następnie przypisywania użytkowników aplikacji toohello podczas zostaną dodane jako członkowie grupy marketing hello, i ich przypisania usunięte z aplikacji hello usunięcie z hello marketingu.

> [!IMPORTANT]
> Firma Microsoft zaleca się, że zarządzania usługi Azure AD przy użyciu hello [Centrum administracyjnego usługi Azure AD](https://aad.portal.azure.com) w hello portalu Azure zamiast hello klasycznego portalu Azure, do którego odwołuje się w tym artykule. 

Ta możliwość może służyć z setkami aplikacji, które można dodać z wewnątrz hello galerii aplikacji usługi Azure AD.

**dostęp tooassign tooa grupy aplikacji SaaS**

1. W hello [klasycznego portalu Azure](https://manage.windowsazure.com), wybierz pozycję **usługi Active Directory** na pasku nawigacyjnym hello na powitania lewą stronę.
2. Wybierz hello **katalogu** kartę, a następnie otwórz hello katalogu, w której ma dostęp tooassign tooa grupy aplikacji SaaS.
3. Wybierz hello **aplikacji** kartę. Wybierz aplikację, która dodaje z hello galerii aplikacji, a następnie kliknij przycisk hello **użytkowników i grup** kartę.
4. Na powitania **użytkowników i grup** na karcie hello **począwszy** wprowadź nazwę hello hello grupy toowhich ma tooassign dostępu, a następnie wybierz hello znacznik wyboru w prawym górnym rogu hello. Wystarczy tootype hello pierwsza część nazwy grupy.
5. Wybierz grupę hello, a następnie wybierz opcję hello **przypisywanie dostępu** przycisku. Wybierz **tak** po wyświetleniu komunikatu potwierdzenia hello. Członkostwo grup zagnieżdżonych nie są obsługiwane dla tooapplications przypisywania na podstawie grupy w tej chwili.
6. Można również sprawdzić, użytkowników, którzy są przypisane aplikacji toohello, bezpośrednio lub przez członkostwo w grupie. toodo tego hello zmiany **wyświetlenie listy rozwijanej z "Grupy"** za**"Wszyscy użytkownicy"**. Lista Hello zawiera użytkowników w katalogu hello i czy każdy użytkownik jest przypisany toohello aplikacji. Lista Hello zawiera również hello przypisane użytkownikami przypisanymi bezpośrednio aplikacji toohello (typ przydziału wyświetlane jako "Bezpośrednio"), czy na podstawie członkostwa w grupie (typ przydziału wyświetlane jako "Dziedziczonych.")

> [!NOTE]
> Widać hello użytkownicy i grupy dopiero po włączeniu usługi Azure AD Premium lub usługi Azure AD podstawowa.
>
>

### <a name="next-steps"></a>Następne kroki
Te artykuły zawierają dodatkowe informacje o usłudze Azure Active Directory.

* [Zarządzanie tooresources dostępu za pomocą grup usługi Azure Active Directory](active-directory-manage-groups.md)
* [Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory](active-directory-apps-index.md)
* [Polecenia cmdlet usługi Azure Active Directory służące do konfigurowania ustawień grupy](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [Co to jest usługa Azure Active Directory?](active-directory-whatis.md)
* [Integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md)
