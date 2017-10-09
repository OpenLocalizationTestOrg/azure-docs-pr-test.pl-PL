---
title: "aaaUser inicjowania obsługi usługi Azure AD tooan galerii aplikacji jest lub więcej godzin z argumentami | Dokumentacja firmy Microsoft"
description: "Jak toofind się, dlaczego Inicjowanie obsługi administracyjnej tooyour aplikacji może trwać dłużej niż oczekiwano"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 0658f041724c91ddd1997cc7759393b46680f13a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="user-provisioning-tooan-azure-ad-gallery-application-is-taking-hours-or-more"></a>Inicjowanie obsługi administracyjnej tooan usługi Azure AD galerii aplikacji użytkownika jest lub więcej godzin z argumentami

Podczas włączania najpierw automatyczne Inicjowanie obsługi administracyjnej dla aplikacji, hello początkowej synchronizacji może potrwać od godziny tooseveral 20 minut, w zależności od wielkości hello hello katalog usługi Azure AD i hello liczbę użytkowników w zakresie obsługi. 

Kolejne synchronizacje po początkowej synchronizacji hello przebiegać szybciej, jak znaki wodne, przedstawiające stan hello obu systemów po początkowej synchronizacji hello, poprawa wydajności kolejne synchronizacje magazyny hello inicjowania obsługi usługi.

## <a name="how-tooimprove-provisioning-performance"></a>Jak tooimprove inicjowania obsługi administracyjnej wydajności

Jeśli hello początkowej synchronizacji trwa dłużej niż kilka godzin, należy co możesz zrobić tooimprove wydajności:

-   **Filtry zakresu użytkownika.** Filtry zakresu pozwalają toofine strojenia hello dane, które hello inicjowania obsługi administracyjnej wyodrębnia usługi z usługi Azure AD przez filtrowanie na podstawie wartości atrybutu określonych użytkowników. Aby uzyskać więcej informacji na filtrami zakresów, zobacz [udostępniania aplikacji na podstawie atrybutów z filtrami zakresów](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters).

## <a name="next-steps"></a>Następne kroki
[Automatyzowanie Inicjowanie obsługi użytkowników i anulowania zastrzeżenia tooSaaS aplikacji za pomocą usługi Azure Active Directory](active-directory-saas-app-provisioning.md)

