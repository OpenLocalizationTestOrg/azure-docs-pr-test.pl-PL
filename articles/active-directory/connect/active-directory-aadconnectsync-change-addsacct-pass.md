---
title: "Synchronizacja programu Azure AD Connect: zmiany hasła konta DS hello AD | Dokumentacja firmy Microsoft"
description: "W tym dokumencie temacie opisano, jak Azure AD Connect po hello hasło do konta usług AD DS hello tooupdate zostanie zmieniona."
services: active-directory
keywords: "Usługi AD DS konta, konto usługi Active Directory, hasło"
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 76b19162-8b16-4960-9e22-bd64e6675ecc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2707c9246446612f8d083ecde876b3b4fb2435ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="changing-hello-ad-ds-account-password"></a>Zmiana hasła konta hello AD DS
Witaj AD DS konto odnosi się toohello konto użytkownika używane przez toocommunicate Azure AD Connect z lokalną usługą Active Directory. Jeśli zmienisz hasło hello hello konta usług AD DS, należy zaktualizować Azure AD Connect usługi synchronizacji z hello nowe hasło. W przeciwnym razie powitalne synchronizacji nie będzie można poprawnie synchronizowane z hello lokalnej usługi Active Directory i wystąpi hello następujące błędy:

* W hello Menedżera usługi synchronizacji, importu lub eksportu operację z lokalnymi AD kończy się niepowodzeniem z **logowanie bez poświadczeń na początku** błędu.

* W Podglądzie zdarzeń systemu Windows, w dzienniku zdarzeń aplikacji hello zawiera błąd **6000 identyfikator zdarzenia** i komunikat **"hello zarządzania agenta"contoso.com"nie powiodło się toorun ponieważ hello poświadczenia były nieprawidłowe"** .


## <a name="how-tooupdate-hello-synchronization-service-with-new-password-for-ad-ds-account"></a>Jak tooupdate hello usługi synchronizacji z nowe hasło dla konta usług AD DS
Witaj tooupdate usługi synchronizacji z hello nowe hasło:

1. Uruchom hello Synchronization Service Manager (START → usługa synchronizacji).
</br>![Menedżera usługi synchronizacji](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)  

2. Przejdź toohello **łączniki** kartę.

3. Wybierz hello **łącznika AD** , który odpowiada toohello AD DS konto, dla którego jego hasło zostało zmienione.

4. W obszarze **akcje**, wybierz pozycję **właściwości**.

5. W wyskakującym oknie dialogowym hello, wybierz **Connect lesie katalogu tooActive**:

6. Wprowadź nowe hasło hello konta hello usług AD DS w hello **hasło** pola tekstowego.

7. Kliknij przycisk **OK** toosave hello nowe hasło i zamknij hello podręczne okno dialogowe.

8. Ponowne uruchomienie hello Azure AD Connect usługi synchronizacji w obszarze Menedżer sterowania usługami systemu Windows. Jest to tooensure który wszelkie odwołania toohello stare hasło jest usuwany z hello pamięci podręcznej.

## <a name="next-steps"></a>Następne kroki
**Tematy poglądowe**

* [Synchronizacja programu Azure AD Connect: zrozumienie i dostosowywanie synchronizacji](active-directory-aadconnectsync-whatis.md)

* [Integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md)
