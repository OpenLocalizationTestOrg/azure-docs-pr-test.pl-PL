---
title: aaaManage ustawienia weryfikacji dwuetapowej | Dokumentacja firmy Microsoft
description: "Zarządzanie, jak używasz usługi Azure Multi-Factor Authentication, włącznie ze zmianami swoje informacje kontaktowe i konfigurowanie urządzenia."
services: multi-factor-authentication
keywords: "Klient uwierzytelniania wieloskładnikowego, problem z uwierzytelnianiem, identyfikator korelacji"
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: d3372d9a-9ad1-4609-bdcf-2c4ca9679a3b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: 2c974b08c584943f3c5a6b9bf16497d1706e8329
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-settings-for-two-step-verification"></a>Zarządzanie ustawieniami na potrzeby weryfikacji dwuetapowej
Ten artykuł zawiera odpowiedzi na pytania dotyczące ustawień tooupdate uwierzytelnianie dwuetapowe weryfikacji lub Multi-Factor. Jeśli występują problemy dotyczące logowania konta tooyour, zapoznaj się zbyt[wystąpił problem w trakcie weryfikacji dwuetapowej](multi-factor-authentication-end-user-troubleshoot.md) dla pomocy w rozwiązywaniu problemów.

## <a name="where-toofind-hello-settings-page"></a>Gdzie toofind hello ustawienia strony
W zależności od tego, jak firma skonfigurowane uwierzytelnianie wieloskładnikowe Azure istnieje kilka miejsc, w którym można zmienić ustawienia, takie jak numer telefonu.

Jeśli administrator IT wysłane z określonym adresem URL lub weryfikacji dwuetapowej toomanage kroki, wykonaj te instrukcje. W przeciwnym razie hello instrukcjami powinny działać na każdy inny. Jeśli wykonaj następujące kroki, ale nie widzisz hello tych samych opcji, które oznacza, że konto służbowe dostosowanego własnych portalu. Poproś administratora portalu Azure Multi-Factor Authentication tooyour łącze hello.

1. Zaloguj się za[https://myapps.microsoft.com](https://myapps.microsoft.com)  
2. Wybierz nazwę konta w prawym górnym hello, a następnie wybierz **profilu**.  
3. Wybierz **dodatkowej weryfikacji zabezpieczeń**.  

    ![Myapps](./media/multi-factor-authentication-end-user-manage/myapps1.png)
4. ładuje Hello dodatkowe zabezpieczenia weryfikacji strony z ustawieniami.

    ![Biurowego](./media/multi-factor-authentication-end-user-manage/proofup.png)

## <a name="i-want-toochange-my-phone-number-or-add-a-secondary-number"></a>Mają toochange mój numer telefonu lub dodać dodatkowej numer
Jest ważne tooconfigure numer telefonu uwierzytelniania dodatkowego.  Ponieważ na serwerze podstawowym phone liczba i aplikacji mobilnej są prawdopodobnie na powitania sam telefonu, numeru telefonu dodatkowej hello jest jedynym sposobem hello, będzie możliwe tooget do swojego konta Jeśli telefon zostanie utracony lub skradziony.

> [!NOTE]
> Jeśli nie masz dostępu tooyour głównego numeru telefonu i potrzebujesz pomocy w tooyour konta, zobacz nasze tematy pomocy w [wystąpił problem w trakcie weryfikacji dwuetapowej](multi-factor-authentication-end-user-troubleshoot.md).  

**toochange Twojego podstawowy numer telefonu:**  

1. Na stronie weryfikacji dodatkowe zabezpieczenia hello zaznacz pole tekstowe hello bieżący numer telefonu i edytować za pomocą nowy numer telefonu.  
2. Wybierz pozycję **Zapisz**.  
3. Jeśli jest to numer hello używany dla Twojego preferowaną opcję weryfikacji, masz tooverify hello nowy numer, zanim będzie można go zapisać.  

**tooadd numeru telefonu dodatkowej:**  

1. Na stronie weryfikacji dodatkowe zabezpieczenia hello hello pole wyboru obok zbyt**numer telefonu uwierzytelniania alternatywny.**  
2. Wprowadź numer telefonu pomocniczy w polu tekstowym hello.  
3. Wybierz **zapisać** i zakończeniu zmiany.  

## <a name="require-two-step-verification-again-on-a-device-youve-marked-as-trusted"></a>Żądaj weryfikacji dwuetapowej ponownie na urządzeniu, które zostały oznaczone jako zaufany

W zależności od ustawienia organizacji może być stwierdzający, pole wyboru "nie pytaj ponownie o **X** dni" po wykonaniu weryfikacji dwuetapowej w przeglądarce. Jeśli to pole wyboru i utraty urządzenia lub podejrzenie, że Twoje konto jest zagrożone należy przywrócić tooall weryfikacji dwuetapowej urządzenia. 

1. Na stronie weryfikacji dodatkowe zabezpieczenia hello zaznacz **przywracania usługi Multi-Factor authentication na wcześniej zaufanych urządzeniach**.
2. Witaj następnym zalogowaniu się na dowolnym urządzeniu będzie tooperform zostanie wyświetlony monit o weryfikacji dwuetapowej. 

## <a name="how-do-i-clean-up-microsoft-authenticator-from-my-old-device-and-move-tooa-new-one"></a>Jak wyczyścić Authenticator firmy Microsoft z urządzeniem stary i Przenieś tooa nową?
Po odinstalowaniu aplikacji hello z urządzenia lub resetowania urządzenia hello aktywacji hello na zapleczu hello nie zostaną usunięte. Aby uzyskać więcej informacji, zobacz [Microsoft Authenticator](microsoft-authenticator-app-how-to.md).

## <a name="next-steps"></a>Następne kroki
* Uzyskać porady dotyczące rozwiązywania problemów i pomoc na temat [wystąpił problem w trakcie weryfikacji dwuetapowej](multi-factor-authentication-end-user-troubleshoot.md)
* Konfigurowanie [hasła aplikacji](multi-factor-authentication-end-user-app-passwords.md) dla wszystkich aplikacji, które nie obsługują weryfikacji dwuetapowej.
