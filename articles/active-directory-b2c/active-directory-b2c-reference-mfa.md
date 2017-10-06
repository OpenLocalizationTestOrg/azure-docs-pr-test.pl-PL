---
title: "Azure Active Directory B2C: Uwierzytelnianie wieloskładnikowe | Dokumentacja firmy Microsoft"
description: "Jak tooenable uwierzytelniania wieloskładnikowego w aplikacjach użytkownika chronione przez usługę Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 53ef86c4-1586-45dc-9952-dbbd62f68afc
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 29beb1e6ab5d8ab5a65f9c5c068d9e71c60418dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-enable-multi-factor-authentication-in-your-consumer-facing-applications"></a>Usługa Azure Active Directory B2C: Włączanie uwierzytelniania wieloskładnikowego w aplikacjach dla użytkownika
Usługa Azure Active Directory (Azure AD) B2C integruje się bezpośrednio z [Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md) , aby mogli dodawać drugą warstwę zabezpieczeń środowiska toosign w górę i logowania w aplikacjach dla użytkownika. I można to zrobić bez pisania pojedynczy wiersz kodu. Obecnie firma Microsoft obsługuje połączenia telefonicznego i tekst komunikatu weryfikacji. Jeśli utworzono już zasad rejestracji i logowania, nadal można włączyć usługę Multi-Factor Authentication.

> [!NOTE]
> Uwierzytelnianie wieloskładnikowe można włączyć również podczas tworzenia zasad rejestracji i logowania, nie tylko przez edytowania istniejących zasad.
> 
> 

Funkcja ta ułatwia obsługę scenariuszy, takich jak hello następujące aplikacje:

* Nie wymaga uwierzytelniania wieloskładnikowego tooaccess jedną aplikację, ale wymagają tooaccess kolejnego. Na przykład można zalogować się do aplikacji ubezpieczenia automatycznie z kontem społecznościowych, ani w lokalnym powitania klienta, ale należy zweryfikować numer telefonu hello przed podczas uzyskiwania dostępu do macierzystego wypełniające hello zarejestrowane w hello sam katalogu.
* Uwierzytelnianie wieloskładnikowe tooaccess aplikacji nie wymagają ogólnie rzecz biorąc, ale wymagają tooaccess hello poufnych fragmentów w niej. Na przykład powitania klienta można zarejestrować się w aplikacji przy użyciu konta społecznościowych lub lokalnego i sprawdź stan konta bankowego tooa, ale należy zweryfikować numer telefonu hello przed podjęciem próby przeniesienia danych przesyłanych w sieci.

## <a name="modify-your-sign-up-policy-tooenable-multi-factor-authentication"></a>Modyfikowanie tooenable Twojego zasad rejestracji usługi Multi-Factor Authentication
1. [Wykonaj te bloku funkcji toohello B2C toonavigate kroki na powitania portalu Azure](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).
2. Kliknij przycisk **Zasady tworzenia konta**.
3. Kliknij przycisk tooopen Twojego zasad rejestracji (na przykład "B2C_1_SiUp") go.
4. Kliknij przycisk **uwierzytelnianie wieloskładnikowe** i włączyć hello **stanu** za**ON**. Kliknij przycisk **OK**.
5. Kliknij przycisk **zapisać** u góry bloku hello hello.

Można użyć funkcji "Uruchom teraz" hello na powitania zasad tooverify powitania klienta środowisko. Potwierdź hello następujące czynności:

Konto konsumenta pobiera tworzone w katalogu przed wystąpieniem hello kroku usługa Multi-Factor Authentication. Podczas kroku hello powitania klienta monitu tooprovide jego numeru telefonu i jego potwierdzenie. Jeśli weryfikacja zakończy się pomyślnie, numer telefonu hello jest dołączony toohello konta użytkownika do późniejszego użycia. Nawet jeśli powitania klienta anuluje lub porzuca, użytkownik można poprosić tooverify numeru telefonu ponownie podczas hello następnym logowaniu (przy użyciu uwierzytelniania wieloskładnikowego włączona).

## <a name="modify-your-sign-in-policy-tooenable-multi-factor-authentication"></a>Modyfikowanie tooenable Twojego zasad logowania usługi Multi-Factor Authentication
1. [Wykonaj te bloku funkcji toohello B2C toonavigate kroki na powitania portalu Azure](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).
2. Kliknij przycisk **zasad logowania**.
3. Kliknij przycisk tooopen Twojego zasad logowania (na przykład "B2C_1_SiIn") go. Kliknij przycisk **Edytuj** u góry bloku hello hello.
4. Kliknij przycisk **uwierzytelnianie wieloskładnikowe** i włączyć hello **stanu** za**ON**. Kliknij przycisk **OK**.
5. Kliknij przycisk **zapisać** u góry bloku hello hello.

Można użyć funkcji "Uruchom teraz" hello na powitania zasad tooverify powitania klienta środowisko. Potwierdź hello następujące czynności:

Gdy powitania klienta loguje się (przy użyciu konta społecznościowych lub lokalną), jeśli numer telefonu zweryfikowano jest dołączony toohello konto konsumenta dany użytkownik jest proszony tooverify go. Jeśli nie ma numeru telefonu nie jest podłączone, powitania klienta monitu tooprovide jedną i jego potwierdzenie. Pomyślnie weryfikację hello numer telefonu jest dołączony toohello konta użytkownika do późniejszego użycia.

## <a name="multi-factor-authentication-on-other-policies"></a>Uwierzytelnianie wieloskładnikowe na inne zasady
Zgodnie z opisem zasad rejestracji i logowania powyżej, jest również możliwe tooenable uwierzytelnianie wieloskładnikowe na rejestracji lub zasad logowania i hasło zresetowanie zasad. Będzie dostępna wkrótce w profilu edytowanie zasad.

