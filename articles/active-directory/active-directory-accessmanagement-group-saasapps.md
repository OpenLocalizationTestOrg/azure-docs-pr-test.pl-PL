---
title: "Zarządzanie dostępem do aplikacji SaaS przy użyciu grupy | Dokumentacja firmy Microsoft"
description: "Jak używać grup w usłudze Azure Active Directory — wersja Premium lub Basic udzielania dostępu do aplikacji SaaS, które są zintegrowane z usługą Azure Active Directory."
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
ms.openlocfilehash: d350011ee9fc5ced9ddb16993f68d3c840a645a5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="using-a-group-to-manage-access-to-saas-applications"></a>Używanie grupy do zarządzania dostępem do aplikacji SaaS
Za pomocą usługi Azure Active Directory (Azure AD) z licencją Azure AD Premium lub usługi Azure AD podstawowa, można użyć grupy do udzielania dostępu do aplikacji SaaS, który jest zintegrowany z usługą Azure AD. Na przykład, jeśli ma zostać przypisany dostęp dla działu marketingu do używania pięciu różnych aplikacji SaaS, można utworzyć grupę, która zawiera użytkowników w dziale marketingu i przypisz następujące pięć aplikacji SaaS, które są wymagane przez tę grupę Dział marketingu. W ten sposób można oszczędzić czas dzięki zarządzaniu członkostwa w dziale marketingu w jednym miejscu. Następnie przypisywania użytkowników do aplikacji podczas zostaną dodane jako członkowie grupy marketing, i ich przypisania usunięte z aplikacji w przypadku usunięcia ich z grupy marketing.

> [!IMPORTANT]
> Firma Microsoft zaleca zarządzanie usługą Azure AD przy użyciu [centrum administracyjnego usługi Azure AD](https://aad.portal.azure.com) w witrynie Azure Portal zamiast korzystania z klasycznej witryny Azure Portal przywołanej w niniejszym artykule. 

Ta możliwość może służyć z setkami aplikacji, które można dodać z w galerii aplikacji usługi Azure AD.

**Aby przypisać dostęp dla grupy do aplikacji SaaS**

1. W [klasycznego portalu Azure](https://manage.windowsazure.com), wybierz pozycję **usługi Active Directory** na pasku nawigacyjnym po lewej stronie.
2. Wybierz **katalogu** karcie, a następnie otwórz katalog, w której ma zostać przypisany dostęp dla grupy do aplikacji SaaS.
3. Wybierz **aplikacji** kartę. Wybierz aplikację, który został dodany w galerii aplikacji, a następnie kliknij przycisk **użytkowników i grup** kartę.
4. Na **użytkowników i grup** karcie **począwszy** pola, wprowadź nazwę grupy, do której ma zostać przypisany dostęp, a następnie wybierz znacznik wyboru w prawym górnym rogu. Należy wpisać pierwsza część nazwy grupy.
5. Wybierz grupę, a następnie wybierz **przypisywanie dostępu** przycisku. Wybierz **tak** gdy zostanie wyświetlony komunikat potwierdzenia. Aktualnie w ramach przypisywania do aplikacji na podstawie grup nie jest obsługiwane członkostwo w grupach zagnieżdżonych.
6. Można również sprawdzić, użytkowników, którzy są przypisane do aplikacji, bezpośrednio lub przez członkostwo w grupie. Aby to zrobić, należy zmienić **wyświetlenie listy rozwijanej z "Grupy"** do **"Wszyscy użytkownicy"**. Lista zawiera użytkowników w katalogu i czy każdy użytkownik jest przypisany do aplikacji. Lista zawiera również, czy przypisanych użytkowników przypisanych do aplikacji bezpośrednio (typ przydziału wyświetlane jako "Bezpośrednio") lub na podstawie członkostwa w grupie (typ przydziału wyświetlane jako "Dziedziczonych.")

> [!NOTE]
> Na karcie użytkowników i grup jest widoczny dopiero po włączeniu usługi Azure AD Premium lub usługi Azure AD podstawowa.
>
>

### <a name="next-steps"></a>Następne kroki
Te artykuły zawierają dodatkowe informacje o usłudze Azure Active Directory.

* [Zarządzanie dostępem do zasobów za pomocą grup usługi Azure Active Directory](active-directory-manage-groups.md)
* [Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory](active-directory-apps-index.md)
* [Polecenia cmdlet usługi Azure Active Directory służące do konfigurowania ustawień grupy](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [Co to jest usługa Azure Active Directory?](active-directory-whatis.md)
* [Integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md)
