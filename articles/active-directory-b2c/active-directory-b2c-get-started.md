---
title: "Usługa Azure Active Directory B2C: Tworzenie dzierżawy usługi Azure Active Directory B2C | Dokumentacja firmy Microsoft"
description: "Temat dotyczący sposobu dzierżawy usługi Azure Active Directory B2C toocreate"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: patricka
ms.assetid: eec4d418-453f-4755-8b30-5ed997841b56
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 06/07/2017
ms.author: swkrish
ms.openlocfilehash: e8b257d66c1f66ffb84f5d3d21b30b42eddcbac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-active-directory-b2c-tenant-in-hello-azure-portal"></a>Tworzenie dzierżawy usługi Azure Active Directory B2C w portalu Azure hello

Edytowany przez Sipi.

Ta opcja szybkiego startu ułatwia tworzenie dzierżawy usługi Microsoft Azure Active Directory (Azure AD) B2C w ciągu kilku minut. Po zakończeniu, masz toouse dzierżawy B2C do rejestrowania aplikacji B2C.

## <a name="prerequisites"></a>Wymagania wstępne

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

##  <a name="log-in-tooazure"></a>Zaloguj się za tooAzure

Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).

## <a name="create-an-azure-ad-b2c-tenant"></a>Tworzenie dzierżawy usługi Azure AD B2C

Nie można włączyć funkcji B2C w istniejących dzierżawców. Należy toocreate dzierżawy usługi Azure AD B2C.

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

Gratulacje, utworzono dzierżawy usługi Azure Active Directory B2C. Jesteś administratorem globalnym dzierżawcy hello. W razie potrzeby możesz dodawać innych administratorów globalnych. tooyour tooswitch nowej dzierżawy, kliknij przycisk hello *Zarządzanie nowe łącze dzierżawy*.

![Zarządzanie nowe łącze dzierżawy](./media/active-directory-b2c-get-started/manage-new-b2c-tenant-link.png)

> [!IMPORTANT]
> Jeśli planujesz toouse dzierżawy B2C do aplikacji produkcyjnej, przeczytaj artykuł hello na [skali produkcji a dzierżawcy usługi B2C w wersji zapoznawczej](active-directory-b2c-reference-tenant-type.md). Istnieją znane problemy podczas usuwania istniejących B2C dzierżawy i utwórz ją ponownie hello tą samą nazwą domeny. Należy toocreate dzierżawy B2C o nazwie innej domeny.
>
>

## <a name="link-your-tenant-tooyour-subscription"></a>Połączyć subskrypcję tooyour dzierżawy

Należy toolink programu Azure AD B2C dzierżawy wszystkie funkcje B2C tooyour tooenable subskrypcji platformy Azure i opłacać opłaty za użycie. toolearn, przeczytaj [w tym artykule](active-directory-b2c-how-to-enable-billing.md). Jeśli nie możesz połączyć Twoje tooyour dzierżawy usługi Azure AD B2C subskrypcji platformy Azure, niektóre funkcje jest zablokowany, a zostanie wyświetlony komunikat ostrzegawczy ("bez subskrypcji połączonego toothis B2C dzierżawy lub hello subskrypcji wymaga uwagi.") w ustawieniach hello B2C. Należy wykonać ten krok, przed wysłaniem aplikacji w środowisku produkcyjnym.

## <a name="easy-access-toosettings"></a>Toosettings łatwy dostęp

[!INCLUDE [active-directory-b2c-find-service-settings](../../includes/active-directory-b2c-find-service-settings.md)]

Można także przejść do bloku hello wprowadzając `Azure AD B2C` w **wyszukiwania zasobów** u góry hello hello portalu. Na liście wyników hello, wybierz **usługi Azure AD B2C** tooaccess hello bloku ustawienia B2C.

## <a name="next-steps"></a>Następne kroki

> [!div class="nextstepaction"]
> [Rejestrowanie aplikacji B2C w dzierżawcy usługi B2C](active-directory-b2c-app-registration.md)
