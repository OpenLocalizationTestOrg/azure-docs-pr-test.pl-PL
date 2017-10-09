---
title: "aaaSecurity dla usługi Notification Hubs"
description: "W tym temacie wyjaśniono zabezpieczeń dla usługi Azure notification hubs."
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: 6506177c-e25c-4af7-8508-a3ddca9dc07c
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: multiple
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: f59ad4594c2c0a2e2b22ab0b6d6bad53825a4dc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="security"></a>Bezpieczeństwo
## <a name="overview"></a>Omówienie
W tym temacie opisano hello model zabezpieczeń usługi Azure Notification Hubs. Ponieważ usługi Notification Hubs jednostki magistrali usług, wdrażają hello tego samego modelu zabezpieczeń jako usługi Service Bus. Aby uzyskać więcej informacji, zobacz hello [uwierzytelniania magistrali usługi](https://msdn.microsoft.com/library/azure/dn155925.aspx) tematów.

## <a name="shared-access-signature-security-sas"></a>Zabezpieczenia sygnatury dostępu współdzielonego (SAS)
Notification Hubs implementuje schematu zabezpieczenia na poziomie jednostki nazywane SAS (Shared Access Signature). Ten program umożliwia komunikatów toodeclare jednostek reguły autoryzacji too12 w swoim opisie określającymi udzielenie uprawnienia na jednostkę.

Każda reguła zawiera nazwę, wartość klucza (wspólny klucz tajny) i zestaw praw, zgodnie z objaśnieniem w sekcji hello "Oświadczeń zabezpieczeń". Podczas tworzenia Centrum powiadomień, dwie reguły są tworzone automatycznie: jeden z nasłuchiwania uprawnień (hello zastosowań aplikacji klienta), a druga wszystkich uprawnień (hello używa wewnętrznej bazy danych aplikacji).

Podczas zarządzania rejestracji z aplikacji klienta, jeśli hello informacje wysyłane za pośrednictwem powiadomienia nie jest wielkość liter (na przykład aktualizacje pogody), typowe tooaccess sposób Centrum powiadomień jest toogive hello wartości klucza hello reguły dostęp tylko do nasłuchiwania toohello Aplikacja kliencka i toogive hello wartości klucza zaplecza aplikacji toohello hello reguły pełny dostęp.

Osadź hello wartości klucza w aplikacji ze Sklepu Windows klienta nie jest zalecane. Tooavoid sposób osadzenia hello wartości klucza jest toohave powitania klienta aplikacji pobrać go z zaplecza aplikacji hello podczas uruchamiania.

Ważne jest toounderstand, który hello klucza z dostępem do nasłuchiwania umożliwia klientowi tooregister aplikacji dla dowolnego tagu. Jeśli aplikacja musi ograniczyć rejestracje toospecific tagi toospecific klientów (na przykład gdy tagi reprezentują identyfikatory użytkowników), zapleczu swojej aplikacji należy wykonać hello rejestracji. Aby uzyskać więcej informacji zobacz Zarządzanie rejestracji. Należy pamiętać, że w ten sposób powitania klienta aplikacji nie mają tooNotification bezpośredni dostęp do koncentratorów.

## <a name="security-claims"></a>Oświadczeń zabezpieczeń
Podobne tooother jednostki Centrum powiadomień operacje są dozwolone dla trzech oświadczeń zabezpieczeń: nasłuchiwanie, wysyłania i zarządzanie nimi.

| Claim | Opis | Operacje dozwolone |
| --- | --- | --- |
| Nasłuchiwanie |Utworzyć lub zaktualizować przeczytać, a usunięcie pojedynczego rejestracji |Utwórz/Aktualizuj rejestracji<br><br>Przeczytaj rejestracji<br><br>Wszystkie rejestracji dla dojścia do odczytu<br><br>Usuwanie rejestracji |
| Send |Wyślij Centrum powiadomień toohello wiadomości |Wysyłanie wiadomości |
| Zarządzanie |CRUDs centra powiadomień (w tym aktualizacji poświadczeń systemu powiadomień platformy i kluczy zabezpieczeń) i odczytu rejestracje oparte na tagów |Centra powiadomień tworzenia/aktualizacji/odczytu/usuwania<br><br>Rejestracje odczytu według znaczników |

Centra powiadomień akceptuje oświadczenia przyznane przez tokeny kontroli dostępu usługi Microsoft Azure i tokeny sygnatury wygenerować za pomocą kluczy współużytkowanych skonfigurowane bezpośrednio na powitania Centrum powiadomień.

