---
title: "Witaj aaaTroubleshooting rozszerzenia Panelu dostępu platformy Azure dla programu Internet Explorer | Dokumentacja firmy Microsoft"
description: Jak toouse grupy zasad toodeploy hello programu Internet Explorer dodatek hello Moje aplikacje portalu.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: f56b3230-26fd-42ec-9e3d-2c12daf15479
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 23cbb6117f34759330206de3a26f1397486acedb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-access-panel-extension-for-internet-explorer"></a>Rozwiązywanie problemów z hello rozszerzenia Panel dostępu dla programu Internet Explorer
Ten artykuł pomoże w rozwiązaniu hello następujące problemy:

* Użytkownik jest aplikacji za pośrednictwem portalu Moje aplikacje hello tooaccess podczas korzystania z programu Internet Explorer.
* Zostanie wyświetlony komunikat "Zainstaluj oprogramowanie" nawet po zainstalowaniu oprogramowania hello hello.

Jeśli jesteś administratorem, zobacz też: [jak tooDeploy hello rozszerzenia Panel dostępu dla programu Internet Explorer przy użyciu zasad grupy](active-directory-saas-ie-group-policy.md)

## <a name="run-hello-diagnostic-tool"></a>Uruchom narzędzie diagnostyczne hello
Można diagnozować problemy instalacji z hello rozszerzenia Panel dostępu przez pobranie i uruchomienie narzędzia diagnostyczne hello panelu dostępu:

1. [Kliknij tutaj, narzędzie diagnostyczne hello toodownload.](https://account.activedirectory.windowsazure.com/applications/AccessPanelExtensionDiagnosticTool/AccessPanelExtensionDiagnosticTool.zip)
2. Witaj Otwórz plik, a następnie naciśnij klawisz **Wyodrębnij wszystkie** przycisku.
   
    ![Kliknij przycisk Wyodrębnij wszystkie](./media/active-directory-saas-ie-troubleshooting/extract1.png)
3. Następnie naciśnij klawisz hello **wyodrębnić** toocontinue przycisku.
   
    ![Naciśnij klawisz wyodrębniania](./media/active-directory-saas-ie-troubleshooting/extract2.png)
4. toorun hello narzędzia, kliknij prawym przyciskiem myszy hello plik o nazwie **AccessPanelExtensionDiagnosticTool**, a następnie wybierz pozycję **Otwórz za pomocą > na podstawie Host skryptów systemu Windows**.
   
    ![Otwórz za pomocą > hosta skryptów na podstawie systemu Microsoft Windows](./media/active-directory-saas-ie-troubleshooting/open_tool.png)
5. Zostanie wtedy wyświetlone powitania po diagnostycznych okna, które opisano, co może być problem z instalacją.
   
    ![Przykładowe okno diagnostycznych hello](./media/active-directory-saas-ie-troubleshooting/tool_preview.png)
6. Kliknij przycisk "**tak**" toolet hello program poprawka hello problemów, które zostały znalezione.
7. toosave te zmiany i zamknąć co okno programu Internet Explorer, a następnie otwórz go ponownie.<br />Jeśli nadal nie można uzyskać dostępu do aplikacji, spróbuj hello poniższe kroki.

## <a name="check-that-hello-access-panel-extension-is-enabled"></a>Sprawdź, że hello rozszerzenia Panel dostępu jest włączona
tooverify, który hello rozszerzenia Panel dostępu jest włączona w programie Internet Explorer:

1. W programie Internet Explorer kliknij hello **koło zębate ikonę** na powitania prawym górnym rogu okna hello. Następnie wybierz **Opcje internetowe**.<br />(W starszych wersjach programu Internet Explorer można go znaleźć, w obszarze **Narzędzia > Opcje internetowe**.
   
    ![Przejdź tooTools > Opcje internetowe](./media/active-directory-saas-ie-troubleshooting/internetoptions.png)
2. Kliknij przycisk hello **programy** , a następnie kliknij hello **Zarządzanie dodatkami** przycisku.
   
    ![Kliknij pozycję Zarządzanie dodatkami](./media/active-directory-saas-ie-troubleshooting/internetoptions_programs.png)
3. W tym oknie dialogowym wybierz **rozszerzenia Panel dostępu** , a następnie kliknij przycisk hello **włączyć** przycisku.
   
    ![Kliknij pozycję Włącz](./media/active-directory-saas-ie-troubleshooting/enableaddon.png)
4. toosave te zmiany i zamknąć co okno programu Internet Explorer, a następnie otwórz ponownie program Internet Explorer.

## <a name="enable-extensions-for-inprivate-browsing"></a>Włącz rozszerzenia do przeglądania InPrivate
Jeśli używasz trybu przeglądania InPrivate hello:

1. W programie Internet Explorer kliknij hello **koło zębate ikonę** na powitania prawym górnym rogu okna hello. Następnie wybierz **Opcje internetowe**.<br />(W starszych wersjach programu Internet Explorer można go znaleźć, w obszarze **Narzędzia > Opcje internetowe**.
   
    ![Przykładowe okno diagnostycznych hello](./media/active-directory-saas-ie-troubleshooting/inprivateoptions.png)
2. Przejdź toohello **prywatności** karcie następnie **Usuń zaznaczenie pola wyboru** hello pole wyboru **wyłącz paski narzędzi i rozszerzeń po uruchomieniu przeglądania InPrivate**</p>
   
    ![Usuń zaznaczenie pola wyboru Wyłącz paski narzędzi i rozszerzeń po uruchomieniu przeglądania InPrivate](./media/active-directory-saas-ie-troubleshooting/enabletoolbars.png)
3. toosave te zmiany i zamknąć co okno programu Internet Explorer, a następnie otwórz ponownie program Internet Explorer.

## <a name="uninstall-hello-access-panel-extension"></a>Odinstaluj hello rozszerzenia Panelu dostępu
Witaj toouninstall rozszerzenia Panelu dostępu z danego komputera:

1. Na klawiaturze naciśnij klawisz hello **klawisz systemu Windows** tooopen hello Start menu. Po otwarciu hello menu można wpisać niczego toodo wyszukiwania. Wpisz "Panel sterowania", a następnie otwórz hello **Panelu sterowania** po wyświetleniu w wynikach wyszukiwania hello.
   
    ![Wyszukaj Panelu sterowania](./media/active-directory-saas-ie-troubleshooting/search_sm.png)
2. W hello prawym górnym rogu hello Panelu sterowania, zmień hello **wyświetlić** opcję zbyt**duże ikony**. Następnie znajdź i kliknij hello **programy i funkcje** przycisku.
   
    ![Zmian hello widoku tooshow duże ikony](./media/active-directory-saas-ie-troubleshooting/control_panel.png)
3. Wybierz z listy hello **rozszerzenia Panel dostępu**i kliknij hello hello **Odinstaluj** przycisku.
   
    ![Kliknij przycisk Odinstaluj](./media/active-directory-saas-ie-troubleshooting/uninstall.png)
4. Rozszerzenie hello tooinstall może następnie spróbować ponownie toosee Jeśli hello problem został rozwiązany.

Jeśli wystąpią problemy dotyczące odinstalowywania rozszerzenia hello, można również usunąć go za pomocą hello [Microsoft Napraw go](https://go.microsoft.com/?linkid=9779673) narzędzia.

## <a name="related-articles"></a>Pokrewne artykuły
* [Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory](active-directory-apps-index.md)
* [Dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md)
* [Jak tooDeploy hello rozszerzenia Panel dostępu dla programu Internet Explorer przy użyciu zasad grupy](active-directory-saas-ie-group-policy.md)

