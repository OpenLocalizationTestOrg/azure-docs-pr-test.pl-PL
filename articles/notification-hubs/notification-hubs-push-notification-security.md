---
title: "Zabezpieczenia usługi Notification Hubs"
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
ms.openlocfilehash: 7c3283799806135060bb8ca57ea398c93d1106bb
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="security"></a>Bezpieczeństwo
## <a name="overview"></a>Omówienie
W tym temacie opisano model zabezpieczeń usługi Azure Notification Hubs. Ponieważ usługi Notification Hubs jednostki magistrali usług, ich implementować ten sam model zabezpieczeń jako usługi Service Bus. Aby uzyskać więcej informacji, zobacz [uwierzytelniania magistrali usługi](https://msdn.microsoft.com/library/azure/dn155925.aspx) tematów.

## <a name="shared-access-signature-security-sas"></a>Zabezpieczenia sygnatury dostępu współdzielonego (SAS)
Notification Hubs implementuje schematu zabezpieczenia na poziomie jednostki nazywane SAS (Shared Access Signature). Ten program umożliwia jednostek obsługi komunikatów zadeklarować maksymalnie 12 reguły autoryzacji w swoim opisie, które prawa w tej jednostce.

Każda reguła zawiera nazwę, wartość klucza (wspólny klucz tajny) i zestaw praw, jak opisano w sekcji "Oświadczeń zabezpieczeń". Podczas tworzenia Centrum powiadomień, dwie reguły są tworzone automatycznie: jeden z nasłuchiwania uprawnień (korzysta z aplikacji klienckiej) i jeden z dowolnymi prawami (używane zaplecza aplikacji).

Podczas zarządzania rejestracji z aplikacji klienta, jeśli informacje wysyłane za pośrednictwem powiadomienia nie jest wielkość liter (na przykład pogody aktualizacji), jest typowym sposobem dostęp do Centrum powiadomień, aby nadać wartość klucza reguły dostęp tylko do nasłuchiwania aplikacji klienckiej i umożliwić wartość klucza reguły pełny dostęp do zaplecza aplikacji.

Osadź wartości klucza w aplikacji ze Sklepu Windows klienta nie jest zalecane. Sposobem uniknięcia osadzania wartość klucza ma pobrać zaplecza aplikacji przy uruchamianiu aplikacji klienckiej.

Należy zrozumieć, że klucz z dostępem do nasłuchiwania umożliwia aplikacji klienta zarejestrować dla dowolnego tagu. Jeśli aplikacja ograniczyć rejestracji w znacznikach na określonych klientach (na przykład gdy tagi reprezentują identyfikatory użytkowników), zapleczu swojej aplikacji należy wykonać rejestracji. Aby uzyskać więcej informacji zobacz Zarządzanie rejestracji. Należy pamiętać, że w ten sposób aplikacji klienckiej nie mają bezpośredniego dostępu do usługi Notification Hubs.

## <a name="security-claims"></a>Oświadczeń zabezpieczeń
Podobnie jak inne jednostki, operacje Centrum powiadomień są dozwolone dla trzech oświadczeń zabezpieczeń: nasłuchiwanie, wysyłania i zarządzanie nimi.

| Claim | Opis | Operacje dozwolone |
| --- | --- | --- |
| Nasłuchiwanie |Utworzyć lub zaktualizować przeczytać, a usunięcie pojedynczego rejestracji |Utwórz/Aktualizuj rejestracji<br><br>Przeczytaj rejestracji<br><br>Wszystkie rejestracji dla dojścia do odczytu<br><br>Usuwanie rejestracji |
| Send |Wysyłanie komunikatów do Centrum powiadomień |Wysyłanie wiadomości |
| Zarządzanie |CRUDs centra powiadomień (w tym aktualizacji poświadczeń systemu powiadomień platformy i kluczy zabezpieczeń) i odczytu rejestracje oparte na tagów |Centra powiadomień tworzenia/aktualizacji/odczytu/usuwania<br><br>Rejestracje odczytu według znaczników |

Centra powiadomień akceptuje oświadczenia przyznane przez tokeny kontroli dostępu usługi Microsoft Azure i tokeny sygnatury wygenerować za pomocą kluczy współużytkowanych skonfigurowane bezpośrednio w Centrum powiadomień.

