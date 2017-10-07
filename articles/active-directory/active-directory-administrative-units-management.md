---
title: "Podgląd zarządzania jednostki aaaAdministrative w usłudze Azure Active Directory"
description: "Przy użyciu jednostek administracyjnych do zapewnienia jeszcze bardziej precyzyjnej delegowania uprawnień w usłudze Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 8464cd6b-1d1a-470d-a4fb-ee29b8eab4c4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/17/2017
ms.author: curtand
ms.reviewer: elkuzmen
ms.custom: oldportal;it-pro;
ms.openlocfilehash: ee2c7beb6f9f6292bbf3cdeab00801ac066ae0e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="administrative-units-management-in-azure-ad---public-preview"></a>Zarządzanie jednostkami administracyjnymi w usłudze Azure AD - publicznej wersji zapoznawczej
W tym artykule opisano jednostkami administracyjnymi — nowy kontener usługi Azure Active Directory zasobów, które mogą służyć do delegowania uprawnień administracyjnych za pośrednictwem podzbiór użytkowników i stosowania zasad tooa podzbioru użytkowników. W usłudze Azure Active Directory jednostki administracyjne włączyć centralnej Administratorzy toodelegate uprawnienia tooregional Administratorzy lub tooset zasad na poziomie szczegółowym.

Jest to przydatne w przypadku organizacji z działów niezależne, na przykład, który składa się z wielu szkoły autonomicznego (służbowe biznesowych, szkoły inżynierii itd.), niezależne od siebie uniwersytetu duże. Takie podziałów ma własnych administratorów IT, którzy kontroli dostępu, zarządzania użytkownikami i ustawić zasady specjalnie z myślą o ich dzielenia. Administratorzy centralnej mają toobe stanie Udziel tych uprawnień administratorom działów przez użytkowników hello w ich określonego działów. Dokładniej za pomocą tego przykładu, głównym administratorem można, na przykład utworzyć jednostkę administracyjne dla konkretnego szkole (służbowe Business) i wypełnić ją tylko hello służbowe biznesowych. Następnie centralnej administrator może dodać hello firm służbowe roli tooa zakres personelu IT, innymi słowy, grant hello personel działu informatycznego uprawnień administracyjnych służbowe firm tylko za pośrednictwem jednostki administracyjne hello biznesowej służbowe.

> [!IMPORTANT]
> Role administratora o zakresie jednostki administracyjne można przypisać tylko w przypadku włączenia usługi Azure Active Directory — wersja Premium. Aby uzyskać więcej informacji, zobacz [wprowadzenie do korzystania z usługi Azure AD Premium](active-directory-get-started-premium.md).
>


Z punktu widzenia administratora centralnego hello jednostki administracyjne jest obiektu katalogu, które mogą być tworzone i wypełniane przy użyciu zasobów. **W tej wersji zapoznawczej te zasoby może być tylko użytkownicy.** Po utworzeniu i wypełniane, jednostki administracyjne hello może służyć jako uprawnienie tylko za pośrednictwem zasoby zawarte w jednostce administracyjnej hello hello toorestrict zakresu.

## <a name="managing-administrative-units"></a>Zarządzanie jednostkami administracyjnymi
W tej wersji zapoznawczej można tworzyć i zarządzać przy użyciu poleceń cmdlet usługi Azure Active Directory modułu dla środowiska Windows PowerShell hello jednostkami administracyjnymi. więcej informacji na temat toolearn toodo, który zobacz [Praca z jednostkami administracyjnymi](https://docs.microsoft.com/powershell/azure/active-directory/working-with-administrative-units?view=azureadps-2.0)

Aby uzyskać więcej informacji na temat instalowania modułu hello Azure AD i wymagania dotyczące oprogramowania oraz informacje dotyczące hello polecenia cmdlet usługi Azure AD modułu Zarządzanie jednostkami administracyjnymi, wraz ze składnią, opisy parametrów i przykłady, zobacz [usługi Azure Active PowerShell katalogu](https://docs.microsoft.com/powershell/azure/active-directory/overview?view=azureadps-2.0).

## <a name="next-steps"></a>Następne kroki
[Wersje usługi Azure Active Directory](active-directory-editions.md)
