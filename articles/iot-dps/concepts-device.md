---
title: "Inicjowanie obsługi administracyjnej urządzeń Azure pojęcia dotyczące urządzenia | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano pojęcia specyficzne dla urządzeń z usługi udostępniania urządzenia i Centrum IoT aprowizacji urządzeń"
services: iot-dps
keywords: 
author: nberdy
ms.author: nberdy
ms.date: 09/05/2017
ms.topic: article
ms.service: iot-dps
documentationcenter: 
manager: timlt
ms.devlang: na
ms.custom: mvc
ms.openlocfilehash: 5297bc57729d9e983d63244c71eb21995cf73f0e
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="iot-hub-device-provisioning-service-device-concepts"></a>Pojęcia dotyczące urządzenia inicjowania obsługi usługi IoT Hub urządzeń

Usługa inicjowania obsługi urządzeń Centrum IoT to usługa pomocnika do Centrum IoT, które są używane do konfigurowania urządzenia bezobsługową alokacji dla określonego Centrum IoT. Przy użyciu usługi inicjowania obsługi urządzeń można udostępnić milionów urządzeń w sposób bezpieczny i skalowalności.

Ten artykuł zawiera omówienie *urządzenia* pojęcia związane z w Inicjowanie obsługi administracyjnej urządzeń. W tym artykule jest najodpowiedniejsze do osoby objętego [krok produkcyjnym](about-iot-dps.md#manufacturing-step) pobierania urządzenie jest gotowe do wdrożenia.

## <a name="attestation-mechanism"></a>Mechanizm zaświadczania

Mechanizm zaświadczania jest metoda stosowana do potwierdzenia tożsamości urządzenia. Mechanizm zaświadczania ma również zastosowanie do listy rejestracji, co informuje inicjowania obsługi usługi, którego metoda zaświadczania do użycia z danym urządzeniem.

> [!NOTE]
> Centrum IoT używa "schemat uwierzytelniania" podobne koncepcji w tej usłudze.

Usługa udostępniania urządzeń obsługuje dwa rodzaje poświadczenie:
* **Certyfikaty X.509** oparte na przepływie standardowe uwierzytelnianie certyfikatu X.509.
* **Tokeny sygnatury dostępu Współdzielonego** oparte na żądanie nonce kluczy przy użyciu standardowego modułu TPM. Ta sytuacja nie wymaga fizycznej modułu TPM na urządzeniu, ale usługa oczekuje, że poświadczenia przy użyciu klucza poręczenia na [specyfikacji modułu TPM](https://trustedcomputinggroup.org/work-groups/trusted-platform-module/).

## <a name="hardware-security-module"></a>Sprzętowy moduł zabezpieczeń

Sprzętowego modułu zabezpieczeń lub modułu HSM, służy do bezpieczny, sprzętowy magazyn kluczy tajnych urządzenia, a jest to najbezpieczniejsze formą tajny magazynu. Certyfikatów X.509 i tokeny sygnatury dostępu Współdzielonego mogą być przechowywane w module HSM. Moduły HSM mogą być używane z obu mechanizmów zaświadczania inicjowania obsługi administracyjnej obsługuje usługi.

> [!TIP]
> Zdecydowanie zaleca się użycie modułu HSM z urządzeniami bezpiecznie przechowywać kluczy tajnych na urządzeniach.

Klucze tajne urządzenia mogą być również przechowywane w oprogramowaniu (pamięci), ale jest mniej bezpieczne formularz magazynu niż modułu HSM.

## <a name="registration-id"></a>Identyfikator rejestracji

Identyfikator rejestracji jest używany do jednoznacznego identyfikowania urządzeń w usłudze udostępniania urządzeń. Identyfikator urządzenia muszą być unikatowe w usłudze udostępniania [identyfikator zakresu](#id-scope). Każde urządzenie musi mieć identyfikator rejestracji Identyfikator rejestracji jest alfanumeryczne, małe litery i może zawierać łączniki.

* W przypadku modułu TPM identyfikator rejestracji są udostępniane przez samego modułu TPM.
* W przypadku na podstawie X.509 zaświadczania identyfikator rejestracji podano jako nazwę podmiotu certyfikatu.

## <a name="device-id"></a>Identyfikator urządzenia

Identyfikator urządzenia jest Identyfikatorem, pojawiającą się w Centrum IoT. Identyfikator urządzenia odpowiednie może być ustawiona w wpisu rejestracji, ale nie jest to wymagane do ustawienia. Jeśli nie urządzeń określono Identyfikatora listy rejestracji, identyfikator rejestracji jest używany jako identyfikator urządzenia podczas rejestrowania urządzenia. Dowiedz się więcej o [urządzenia identyfikatorów w Centrum IoT](../iot-hub/iot-hub-devguide-identity-registry.md).

## <a name="id-scope"></a>Identyfikator zakresu

Identyfikator zakresu jest przypisany do usługi inicjowania obsługi urządzeń, gdy jest tworzony przez użytkownika i jest używany do jednoznacznego identyfikowania określonej usługi inicjowania obsługi, które urządzenia będą rejestrować się za pośrednictwem. Identyfikator zakresu jest generowany przez usługę i nie można modyfikować, które zapewnia unikatowość.

> [!NOTE]
> Unikatowość jest ważne w przypadku łączenia i przejęcia scenariusze i długotrwałe operacje wdrażania.
