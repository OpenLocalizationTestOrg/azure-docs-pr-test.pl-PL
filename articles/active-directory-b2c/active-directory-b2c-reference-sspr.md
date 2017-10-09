---
title: "Usługa Azure Active Directory B2C: Samoobsługowego resetowania hasła | Dokumentacja firmy Microsoft"
description: "Temat prezentacja sposób resetowania tooset samoobsługi hasła przez użytkowników w usłudze Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: curtand
ms.assetid: c87ed86e-1520-42b1-8c31-46cd44ed5310
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: ff87eea42259b610702da73af35d0a38eb7dd33d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-set-up-self-service-password-reset-for-your-consumers"></a>Usługa Azure Active Directory B2C: Konfigurowanie samoobsługowego resetowania haseł dla użytkowników
Z hello samoobsługowego resetowania hasła funkcji, użytkownikach (którzy utworzyli konto dla kont lokalnych), można zresetować hasła na ich własnych. Pozwala to znacznie ograniczyć hello obciążeń personelowi pomocy technicznej, zwłaszcza, jeśli aplikacja ma miliony użytkowników przy użyciu go na bieżąco. Aktualnie obsługiwany jest tylko metoda odzyskiwania przy użyciu ze zweryfikowanym adresem e-mail. W przyszłości hello dodamy metody dodatkowe odzyskiwania (numer telefonu zweryfikowane, pytań zabezpieczających, itp.).

> [!NOTE]
> Ten artykuł dotyczy hasło usługi tooself resetowania używane w kontekście hello zasad logowania. Jeśli potrzebujesz zasady resetowania hasła można swobodnie dostosowywać wywoływane z aplikacji, zobacz [w tym artykule](active-directory-b2c-reference-policies.md#create-a-password-reset-policy).
> 
> 

Domyślnie katalogu nie będzie miał hasła Samoobsługowe Resetowanie włączona. Użyj hello następujące kroki tooturn go na:

1. Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com/) jako hello administratorem subskrypcji. Jest to hello tej samej pracy lub konta służbowego lub hello tego samego konta Microsoft użyty toocreate katalogu.
2. Przejdź toohello rozszerzenie usługi Active Directory na powitania pasku nawigacyjnym po lewej stronie powitania.
3. Znajdź katalogu, w obszarze hello **katalogu** i kliknij ją.
4. Kliknij przycisk hello **Konfiguruj** kartę.
5. Przewiń w dół toohello **zasady resetowania hasła użytkownika** hello sekcji, a następnie **użytkownicy włączeni do resetowania hasła** opcję zbyt**tak**. Zwróć uwagę, że hello **alternatywny adres E-mail** zaznaczono opcję; pozostaw, ponieważ jest on.
   
    ![Samoobsługowe resetowanie haseł](./media/active-directory-b2c-reference-sspr/sspr.png)
6. Kliknij przycisk **zapisać** u dołu hello hello strony. Gotowe!

tootest, użyj hello "Uruchom teraz" funkcji na żadnych zasad logowania z kontami lokalnymi funkcję dostawcy tożsamości. Na logowanie lokalne konto hello strony (gdzie należy wprowadzić adres e-mail i hasło lub nazwę użytkownika i hasło), kliknij przycisk **nie może uzyskać dostępu do konta?** tooverify powitania klienta środowiska.

> [!NOTE]
> Witaj strony resetowania hasła samoobsługi można dostosować za pomocą hello [firmowe funkcji](../active-directory/active-directory-add-company-branding.md).
> 
> 

