---
title: "Usługi Azure Active Directory B2C: Weryfikacja adresu E-mail, podczas tworzenia konta użytkownika wyłączyć | Dokumentacja firmy Microsoft"
description: "Temat prezentacja jak toodisable e-mail weryfikacji podczas tworzenia konta w usłudze Azure Active Directory B2C konsumenta"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 433f32b8-96d2-4113-aa82-efcf42fa9827
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/06/2017
ms.author: parakhj
ms.openlocfilehash: a8a42eddcb577725f04d70e1b1ebbebf10b5937c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-disable-email-verification-during-consumer-sign-up"></a>Usługa Azure Active Directory B2C: Weryfikacja adresu e-mail Wyłącz podczas tworzenia konta użytkownika
Po włączeniu usługi Azure Active Directory (Azure AD) B2C umożliwia a konsumenta hello toosign możliwości dla aplikacji, zapewniając adres e-mail i tworzenia konta lokalnego. Usługa Azure AD B2C zapewnia prawidłowe adresy e-mail, wymagając tooverify konsumentów ich podczas procesu tworzenia konta hello. Również uniemożliwia złośliwego zautomatyzowany proces generowania fałszywych kont dla aplikacji hello.

Niektórzy deweloperzy aplikacji preferowane jest Weryfikacja adresu e-mail tooskip podczas procesu tworzenia konta hello i zamiast tego ma użytkowników weryfikacji adresu e-mail hello później. toosupport to usługi Azure AD B2C może być skonfigurowany toodisable Weryfikacja adresu e-mail. Należy utworzyć płynniejszy procesu tworzenia konta i zapewnia deweloperom hello elastyczność toodifferentiate hello konsumentów, które sprawdzeniu swój adres e-mail z tych klientów, które nie mają.

Zasady rejestracji mają domyślnie włączona Weryfikacja adresu e-mail. Użyj hello następujące kroki tooturn go wyłączyć:

1. [Wykonaj te bloku funkcji toohello B2C toonavigate kroki na powitania portalu Azure](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).
2. Kliknij przycisk **zasady rejestracji** lub **zasad rejestracji i logowania** w zależności od konfiguracji dla rejestracji.
3. Kliknij przycisk tooopen Twojego zasady (na przykład "B2C_1_SiUp") go. Kliknij przycisk **Edytuj** u góry bloku hello hello.
4. Kliknij przycisk **dostosowywania interfejsu użytkownika strony**.
5. Kliknij przycisk **stronę tworzenia konta lokalnego konta**.
6. Kliknij przycisk **adres E-mail** w hello **nazwa** kolumnie hello **atrybuty rejestracji** sekcji.
7. Przełącz hello **Żądaj weryfikacji** opcję zbyt**nr**.
8. Kliknij przycisk **OK** u dołu hello aż hello **edytować zasady** bloku.
9. Kliknij przycisk **zapisać** u góry bloku hello hello. Gotowe!

> [!NOTE]
> Wyłączanie Weryfikacja adresu e-mail w procesie rejestracji hello może prowadzić toospam. Jeśli wyłączysz domyślny hello, zaleca się dodawania systemu weryfikacji.
> 
> 

Jesteśmy zawsze toofeedback otwarte i sugestie! Jeśli masz trudności w tym temacie lub mają zalecenia dotyczące poprawy tej zawartości, prosimy o wyrażenie opinii u dołu hello hello strony. Funkcja żądań, dodaj ich zbyt[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).
