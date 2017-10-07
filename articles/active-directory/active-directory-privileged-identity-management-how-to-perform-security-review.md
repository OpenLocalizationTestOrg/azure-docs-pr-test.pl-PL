---
title: "tooperform aaaHow Przegląd dostępu | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooperform przegląd z hello aplikacji Azure Privileged Identity Management."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 49ee2feb-7d2e-4acf-82c1-40ff23062862
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 301a5e9f97b68fedfbf4954e0bd7dadb7f0fc510
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-an-access-review-in-azure-ad-privileged-identity-management"></a>Jak tooperform dostępu Przejrzyj w usłudze Azure AD Privileged Identity Management
Azure Active Directory (AD) Privileged Identity Management upraszcza sposób przedsiębiorstw Zarządzanie tooresources uprzywilejowanego dostępu w usłudze Azure AD i innych usług online firmy Microsoft, takich jak usługi Office 365 lub Microsoft Intune.  

Jeśli przypisano rolę administracyjną tooan, administrator ról uprzywilejowanych w organizacji może poprosić tooregularly potwierdzić, że użytkownik nadal tej roli dla zadania. Może spowodować, że wiadomość e-mail zawierającą łącze lub przejść proste toohello [portalu Azure](https://portal.azure.com). Wykonaj kroki hello w tym tooperform artykułu własnym przeglądu przypisane role.

Jeśli administrator ról uprzywilejowanych zainteresowana przeglądami dostępu, Dowiedz się więcej na [jak toostart dostępu Przejrzyj](active-directory-privileged-identity-management-how-to-start-security-review.md).

## <a name="add-hello-privileged-identity-management-application"></a>Dodawanie aplikacji Privileged Identity Management hello
Można użyć hello Azure AD Privileged Identity zarządzania (PIM) aplikacji w hello [portalu Azure](https://portal.azure.com/) tooperform zapoznania się z nimi.  Jeśli nie masz hello aplikacji Azure AD Privileged Identity Management w portalu sieci należy wykonać te tooget kroki pracy.

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com/).
2. Wybierz swoją nazwę użytkownika w hello prawym górnym rogu hello portalu Azure i wybierz hello katalogu, której będzie można działać.
3. Wybierz **więcej usług** i użyj hello filtru pole tekstowe toosearch dla **Azure AD Privileged Identity Management**.
4. Sprawdź **toodashboard numeru Pin** , a następnie kliknij przycisk **Utwórz**. zostanie otwarta Hello aplikacji Privileged Identity Management.

## <a name="approve-or-deny-access"></a>Zatwierdzenia lub odmowy dostępu
Podczas zatwierdzania lub odmówić dostępu należy jest właśnie informuje recenzenta hello czy możesz nadal używać tej roli lub nie. Wybierz **Zatwierdź** Jeśli chcesz toostay w roli hello lub **Odmów** Jeśli użytkownik nie należy hello dostępu już. Stan użytkownika nie zostaną zmienione od razu, dopóki recenzenta hello stosuje hello wyników.
Wykonaj te kroki toofind i ukończyć powitalnych Przegląd dostępu:

1. W aplikacji PIM hello, wybierz **przeglądu uprzywilejowany dostęp**. Jeśli masz wszelkie oczekujące dostępu przeglądy pojawią się one w hello dostępu usługi Azure AD sprawdza bloku.
2. Wybierz przeglądu hello ma toocomplete.
3. Chyba że zostaną utworzone hello przeglądu, wyświetlane jako hello tylko użytkownik w przeglądzie hello. Wybierz następny nazwę tooyour hello znacznik wyboru.
4. Wybierz **zatwierdzić** lub **odmowy**. Może być konieczne tooinclude przyczynę decyzji w hello **przyczyny** pola tekstowego.  
5. Zamknij hello **ról Przegląd usługi Azure AD** bloku.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Następne kroki
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
