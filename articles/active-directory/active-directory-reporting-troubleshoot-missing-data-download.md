---
title: "Rozwiązywanie problemów: Brak danych w hello pobrać Dzienniki aktywności w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Udostępnia rozpoznawanie danych toomissing w pobranych Dzienniki aktywności usługi Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ffce7eb1-99da-4ea7-9c4d-2322b755c8ce
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 027b70e6efc570f81d3c836f50ee52aaa89be71a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="i-cant-find-any-data-in-hello-azure-active-directory-activity-logs-i-have-downloaded"></a>Nie można znaleźć żadnych danych w dziennikach hello działania usługi Azure Active Directory, który został pobrany


## <a name="symptoms"></a>Objawy

Pobrany Dzienniki aktywności hello (inspekcji lub logowania) i wszystkie rekordy hello nie jest widoczny dla czasu hello, które zostało określone. Dlaczego? 

 ![Raportowanie](./media/active-directory-reporting-troubleshoot-missing-data-download/01.png)
 

## <a name="cause"></a>Przyczyna

Podczas pobierania dzienników aktywności w portalu Azure hello jest ograniczona rekordy too120K skali hello posortowane przez większość ostatnie. 

## <a name="resolution"></a>Rozwiązanie

Można wykorzystać [API Azure AD raportowania](active-directory-reporting-api-getting-started.md) toofetch tooa miliony rekordów na dowolnym etapie. Nasze podejście zalecane jest toorun skryptu zgodnie z harmonogramem wywołującą hello raportowania interfejsów API toofetch rejestruje w sposób przyrostowy w danym okresie czasu (np., codziennie lub co tydzień).

## <a name="next-steps"></a>Następne kroki
Zobacz hello [raportowania często zadawane pytania dotyczące usługi Azure Active Directory](active-directory-reporting-faq.md).

