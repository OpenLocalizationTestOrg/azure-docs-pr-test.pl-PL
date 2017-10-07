---
title: aaaProblem tworzenia aplikacji serwera Proxy aplikacji | Dokumentacja firmy Microsoft
description: "Jak tootroubleshoot problemy tworzenia aplikacji serwera Proxy aplikacji w portalu usługi Azure AD administratora hello"
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
ms.openlocfilehash: 24fab83c38a49a9e5754854acf2f9711e374e559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="problem-creating-an-application-proxy-application"></a>Problem z tworzeniem aplikacji serwera Proxy aplikacji 

Poniżej przedstawiono niektóre typowe problemy hello krój osoby podczas tworzenia nowej aplikacji serwera proxy aplikacji.

## <a name="recommended-documents"></a>Zalecane dokumenty 

Zobacz toolearn więcej informacji na temat tworzenia aplikacji serwera Proxy aplikacji za pośrednictwem portalu administracyjnego hello [publikowanie aplikacji przy użyciu serwera Proxy aplikacji usługi Azure AD](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).

Jeśli są następujące kroki hello w tym dokumencie i uzyskiwania błąd podczas tworzenia aplikacji hello, zobacz szczegóły błędu hello informacji i sugestie dotyczące sposobu toofix hello aplikacji. Większość komunikaty o błędach obejmują sugerowanej poprawki. 

## <a name="specific-things-toocheck"></a>Określone informacje toocheck

Sprawdź tooavoid typowych błędów:

-   Administratorzy z toocreate uprawnienia aplikacji serwera Proxy aplikacji

-   wewnętrzny adres URL Hello jest unikatowa

-   zewnętrzny adres URL Hello jest unikatowa

-   Witaj adresy URL rozpoczyna się od http lub https i kończyć się "/"

-   adres URL Hello powinna być nazwą domeny, a nie adres IP

komunikat o błędzie Hello powinien być wyświetlany w prawym górnym rogu hello podczas tworzenia aplikacji hello. Można również wybrać hello powiadomień ikona toosee hello komunikaty o błędach.

   ![Wiersz powiadomień](./media/application-proxy-config-problem/error-message.png)

## <a name="next-steps"></a>Następne kroki
[Włącz serwer Proxy aplikacji w portalu Azure hello](active-directory-application-proxy-enable.md)
