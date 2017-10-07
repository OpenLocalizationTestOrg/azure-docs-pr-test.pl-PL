---
title: "Azure AD Connect: Następne kroki i w jaki sposób toomanage Azure AD Connect | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooextend hello domyślnej konfiguracji i zadania operacyjne programu Azure AD Connect."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: c18bee36-aebf-4281-b8fc-3fe14116f1a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 4404aaff24d54d76b83baca3b331a6a250ba4c03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="next-steps-and-how-toomanage-azure-ad-connect"></a>Następne kroki i w jaki sposób toomanage Azure AD Connect
Użyj procedur operacyjnych hello w programie toomeet Połącz usługi Azure Active Directory (Azure AD) toocustomize tego artykułu, wymagań i potrzeb organizacji.  

## <a name="add-additional-sync-admins"></a>Dodaj administratorów dodatkowe synchronizacji
Domyślnie tylko użytkownik hello, który hello instalacji i Administratorzy lokalni są aparatu synchronizacji hello zainstalowany toomanage stanie. Dla tooaccess stanie toobe dodatkowe osoby i zarządzać aparatem synchronizacji hello, Znajdź hello grupy o nazwie ADSyncAdmins na serwerze lokalnym hello je i Dodaj toothis grupy.

## <a name="assign-licenses-tooazure-ad-premium-and-enterprise-mobility-suite-users"></a>Przypisywanie licencji tooAzure użytkowników AD — wersja Premium i Enterprise Mobility Suite
Teraz, gdy użytkownicy zostały zsynchronizowane toohello chmury, należy tooassign je licencji, można rozpocząć korzystanie z aplikacji w chmurze takich jak Office 365.

### <a name="tooassign-an-azure-ad-premium-or-enterprise-mobility-suite-license"></a>tooassign Azure AD Premium lub Enterprise Mobility Suite licencji

1. Zaloguj się toohello portalu Azure jako administrator.
2. Po lewej stronie powitania, wybierz **usługi Active Directory**.
3. Na powitania **usługi Active Directory** kliknij dwukrotnie hello katalogu, który ma hello użytkownicy mają tooset w górę.
4. U góry strony katalogu hello hello, wybierz **licencji**.
5. Na powitania **licencji** wybierz pozycję **Active Directory Premium** lub **Enterprise Mobility Suite**, a następnie kliknij przycisk **przypisać**.
6. Okno dialogowe hello wybierz opcję użytkownicy hello mają tooassign licencji, a następnie kliknij hello znacznik wyboru Ikona toosave hello zmiany.

## <a name="verify-hello-scheduled-synchronization-task"></a>Sprawdź hello zaplanowanej synchronizacji zadań
Użyj hello Azure toocheck portalu hello stan synchronizacji.

### <a name="tooverify-hello-scheduled-synchronization-task"></a>tooverify hello zaplanowanej synchronizacji zadań
1. Zaloguj się toohello portalu Azure jako administrator.
2. Po lewej stronie powitania, wybierz **usługi Active Directory**.
3. Na powitania **usługi Active Directory** kliknij dwukrotnie hello katalogu, który ma hello użytkownicy mają tooset w górę.
4. U góry strony katalogu hello hello, wybierz **integracji katalogów**.
5. W obszarze **Integracja z lokalną usługą active directory**, Uwaga hello czas ostatniej synchronizacji.

<center>![Czas synchronizacji katalogu](./media/active-directory-aadconnect-whats-next/verify.png)</center>

## <a name="start-a-scheduled-synchronization-task"></a>Uruchom zadanie synchronizacji według harmonogramu
Jeśli potrzebujesz toorun zadania synchronizacji, można w tym, uruchamiając ponownie kreatora hello Azure AD Connect.  Należy tooprovide poświadczeń usługi Azure AD.  W Kreatorze hello wybierz hello **Dostosuj opcje synchronizacji** zadań, a następnie kliknij przycisk **dalej** toomove za pomocą Kreatora hello. Na koniec hello, upewnij się, że hello **Uruchom proces synchronizacji hello zaraz po zakończeniu początkowej konfiguracji hello** zaznaczone pole.

<center>![Uruchom synchronizację](./media/active-directory-aadconnect-whats-next/startsynch.png)</center>

Aby uzyskać więcej informacji na powitania usługi Azure AD Connect synchronizacji harmonogramu, zobacz [Azure AD Connect harmonogramu](active-directory-aadconnectsync-feature-scheduler.md).

## <a name="additional-tasks-available-in-azure-ad-connect"></a>Dodatkowe zadania dostępne w programie Azure AD Connect
Po początkowej instalacji programu Azure AD Connect można zawsze uruchomić Kreator hello ponownie z hello Azure AD Connect start strony lub pulpitu skrótów.  Można zauważyć, że ponownie przejść za pomocą Kreatora hello zawiera niektóre nowe opcje w formie hello dodatkowe zadania.  

Witaj Poniższa tabela zawiera podsumowanie tych zadań i krótki opis każdego zadania.

![Lista dodatkowych zadań](./media/active-directory-aadconnect-whats-next/addtasks.png)

| Dodatkowe zadania | Opis |
| --- | --- |
| **Wybrany scenariusz hello widoku** |Umożliwia wyświetlenie bieżącego rozwiązania Azure AD Connect.  Obejmuje to ustawienia ogólne synchronizacji katalogów i ustawień synchronizacji. |
| **Dostosuj opcje synchronizacji** |Zmień hello bieżącej konfiguracji, takie jak dodanie dodatkowej konfiguracji toohello lasy usługi Active Directory lub włączanie opcji synchronizacji, takie jak użytkownika, grupy, urządzenia lub zapisywania zwrotnego haseł. |
| **Włącz tryb przejściowy** |Etap informacje, które nie są natychmiast zsynchronizowane i nie jest eksportowane tooAzure AD lub lokalnej usługi Active Directory.  Ta funkcja umożliwia podgląd synchronizacje hello przed ich wystąpieniem. |

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o [integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).
