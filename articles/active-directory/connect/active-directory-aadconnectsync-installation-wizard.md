---
title: "Ponowne uruchomienie Kreatora instalacji modułu hello Azure AD Connect | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, jak Kreator instalacji hello działa powitania po raz drugi uruchomienia."
keywords: "Kreator instalacji Hello Azure AD Connect umożliwia skonfigurowanie hello ustawienia konserwacji po raz drugi uruchomienia"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: d800214e-e591-4297-b9b5-d0b1581cc36a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 83cc74aca471ef9b4f65f7f3582e3e48d3d81cfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-running-hello-installation-wizard-a-second-time"></a>Synchronizacja programu Azure AD Connect: uruchamiania Kreatora instalacji powitania po raz drugi
Witaj Uruchom Kreatora instalacji hello Azure AD Connect, po raz pierwszy przeprowadzi Cię on przez jak tooconfigure instalacji. Jeśli ponownie uruchom Kreatora instalacji hello oferuje opcje konserwacji.

Kreator instalacji hello znajduje się w menu start hello o nazwie **Azure AD Connect**.

![Start menu](./media/active-directory-aadconnectsync-installation-wizard/startmenu.png)

Po uruchomieniu Kreatora instalacji hello pojawić się Strona z następującymi opcjami:

![Strona z listą dodatkowe zadania](./media/active-directory-aadconnectsync-installation-wizard/additionaltasks.png)

Po zainstalowaniu usług AD FS z programem Azure AD Connect, masz jeszcze więcej opcji. Witaj dodatkowe opcje masz dla usług AD FS są udokumentowane w artykule [zarządzania usług AD FS](active-directory-aadconnect-federation-management.md#manage-ad-fs).

Wybierz jedno z zadań hello i kliknij przycisk **dalej** toocontinue.

> [!IMPORTANT]
> Chociaż hello Kreatora instalacji, Otwórz, wszystkie operacje w aparacie synchronizacji hello są wstrzymane. Upewnij się, że zamknąć kreatora instalacji hello zaraz po zakończeniu zmiany w konfiguracji.
>
>

## <a name="view-current-configuration"></a>Wyświetl bieżącą konfigurację
Ta opcja umożliwia szybki przegląd aktualnie skonfigurowanych opcji.

![Strona z listą wszystkich opcji i ich stan](./media/active-directory-aadconnectsync-installation-wizard/viewconfig.png)

Kliknij przycisk **Wstecz** toogo Wstecz. W przypadku wybrania **zakończenia**, zamknąć kreatora instalacji hello.

## <a name="customize-synchronization-options"></a>Dostosuj opcje synchronizacji
Ta opcja jest używana toomake zmiany toohello synchronizacji konfiguracji. Zostanie wyświetlony podzbiór opcje ze ścieżki instalacji niestandardowej konfiguracji hello. Ta opcja jest widoczna, nawet jeśli początkowo użyć instalacji ekspresowej.

* [Dodaj więcej katalogów](active-directory-aadconnect-get-started-custom.md#connect-your-directories). Aby usunięcie katalogu, zobacz [usunąć łącznik](active-directory-aadconnectsync-service-manager-ui-connectors.md#delete).
* [Zmień domenę i jednostkę Organizacyjną filtrowania](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering).
* Usuń grupę filtrowania.
* [Zmień funkcje opcjonalne](active-directory-aadconnect-get-started-custom.md#optional-features).

Witaj innych opcji hello początkowej instalacji nie można zmienić i nie są dostępne. Dostępne są następujące opcje:

* Zmień hello toouse atrybut userPrincipalName i sourceAnchor.
* Zmień hello dołączenie metody dla obiektów z innego lasu.
* Włącz filtrowanie na podstawie grupy.

## <a name="refresh-directory-schema"></a>Odśwież schemat katalogu
Ta opcja jest używana, jeśli schemat hello zostały zmienione w jednym z lokalnymi lasami usługi AD DS. Na przykład może być zainstalowany program Exchange lub uaktualnić schematu tooa systemu Windows Server 2012 z obiektami urządzenia. W takim przypadku należy tooinstruct Azure AD Connect tooread hello schematu ponownie z usług AD DS i zaktualizować pamięci podręcznej. Ta akcja generuje również hello reguły synchronizacji. Jeśli dodasz hello schematu programu Exchange, na przykład hello reguły synchronizacji programu Exchange są dodawane toohello konfiguracji.

Po wybraniu tej opcji są wyświetlane wszystkie katalogi hello w konfiguracji. Możesz zachować hello domyślne ustawienie i Odśwież wszystkich lasach lub usuń zaznaczenie niektórych z nich.

![Strona z listą wszystkich katalogów w środowisku hello](./media/active-directory-aadconnectsync-installation-wizard/refreshschema.png)

## <a name="configure-staging-mode"></a>Konfigurowanie trybu przejściowego
Ta opcja pozwala tooenable i Wyłącz tryb przejściowy na powitania serwera. Więcej informacji o tymczasowych trybu i sposobie ich użycia można znaleźć w [operacji](active-directory-aadconnectsync-operations.md#staging-mode).

Opcja Hello pokazuje, czy przemieszczania jest obecnie włączona lub wyłączona:  
![Opcja, która również jest wyświetlany bieżący stan trybu przejściowego hello](./media/active-directory-aadconnectsync-installation-wizard/stagingmodecurrentstate.png)

toochange hello stanu, wybranie tej opcji i hello zaznacz lub usuń zaznaczenie pola wyboru.  
![Opcja, która również jest wyświetlany bieżący stan trybu przejściowego hello](./media/active-directory-aadconnectsync-installation-wizard/stagingmodeenable.png)

## <a name="change-user-sign-in"></a>Zmień logowanie użytkowników
Ta opcja umożliwia toochange toofederation synchronizacji haseł lub hello odwrotnie. Nie można zmienić za**nieskonfigurowane**.

Aby uzyskać więcej informacji na temat tej opcji, zobacz [logowania użytkownika](active-directory-aadconnect-user-signin.md#changing-the-user-sign-in-method).

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o hello model konfiguracji używane przez synchronizacja programu Azure AD Connect w [Aprowizacją deklaratywną opis](active-directory-aadconnectsync-understanding-declarative-provisioning.md).

**Tematy poglądowe**

* [Synchronizacja programu Azure AD Connect: zrozumienie i dostosowywanie synchronizacji](active-directory-aadconnectsync-whatis.md)
* [Integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md)
