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
# <a name="troubleshooting-hello-access-panel-extension-for-internet-explorer"></a><span data-ttu-id="d0cd3-103">Rozwiązywanie problemów z hello rozszerzenia Panel dostępu dla programu Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="d0cd3-103">Troubleshooting hello Access Panel Extension for Internet Explorer</span></span>
<span data-ttu-id="d0cd3-104">Ten artykuł pomoże w rozwiązaniu hello następujące problemy:</span><span class="sxs-lookup"><span data-stu-id="d0cd3-104">This article helps you troubleshoot hello following problems:</span></span>

* <span data-ttu-id="d0cd3-105">Użytkownik jest aplikacji za pośrednictwem portalu Moje aplikacje hello tooaccess podczas korzystania z programu Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="d0cd3-105">You're unable tooaccess your apps through hello My Apps portal while using Internet Explorer.</span></span>
* <span data-ttu-id="d0cd3-106">Zostanie wyświetlony komunikat "Zainstaluj oprogramowanie" nawet po zainstalowaniu oprogramowania hello hello.</span><span class="sxs-lookup"><span data-stu-id="d0cd3-106">You see hello "Install Software" message even though you've already installed hello software.</span></span>

<span data-ttu-id="d0cd3-107">Jeśli jesteś administratorem, zobacz też: [jak tooDeploy hello rozszerzenia Panel dostępu dla programu Internet Explorer przy użyciu zasad grupy](active-directory-saas-ie-group-policy.md)</span><span class="sxs-lookup"><span data-stu-id="d0cd3-107">If you are an admin, see also: [How tooDeploy hello Access Panel Extension for Internet Explorer using Group Policy](active-directory-saas-ie-group-policy.md)</span></span>

## <a name="run-hello-diagnostic-tool"></a><span data-ttu-id="d0cd3-108">Uruchom narzędzie diagnostyczne hello</span><span class="sxs-lookup"><span data-stu-id="d0cd3-108">Run hello Diagnostic Tool</span></span>
<span data-ttu-id="d0cd3-109">Można diagnozować problemy instalacji z hello rozszerzenia Panel dostępu przez pobranie i uruchomienie narzędzia diagnostyczne hello panelu dostępu:</span><span class="sxs-lookup"><span data-stu-id="d0cd3-109">You can diagnose installation problems with hello Access Panel Extension by downloading and running hello Access Panel diagnostic tool:</span></span>

1. [<span data-ttu-id="d0cd3-110">Kliknij tutaj, narzędzie diagnostyczne hello toodownload.</span><span class="sxs-lookup"><span data-stu-id="d0cd3-110">Click here toodownload hello diagnostic tool.</span></span>](https://account.activedirectory.windowsazure.com/applications/AccessPanelExtensionDiagnosticTool/AccessPanelExtensionDiagnosticTool.zip)
2. <span data-ttu-id="d0cd3-111">Witaj Otwórz plik, a następnie naciśnij klawisz **Wyodrębnij wszystkie** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d0cd3-111">Open hello file, and press **Extract all** button.</span></span>
   
    ![Kliknij przycisk Wyodrębnij wszystkie](./media/active-directory-saas-ie-troubleshooting/extract1.png)
3. <span data-ttu-id="d0cd3-113">Następnie naciśnij klawisz hello **wyodrębnić** toocontinue przycisku.</span><span class="sxs-lookup"><span data-stu-id="d0cd3-113">Then press hello **Extract** button toocontinue.</span></span>
   
    ![Naciśnij klawisz wyodrębniania](./media/active-directory-saas-ie-troubleshooting/extract2.png)
4. <span data-ttu-id="d0cd3-115">toorun hello narzędzia, kliknij prawym przyciskiem myszy hello plik o nazwie **AccessPanelExtensionDiagnosticTool**, a następnie wybierz pozycję **Otwórz za pomocą > na podstawie Host skryptów systemu Windows**.</span><span class="sxs-lookup"><span data-stu-id="d0cd3-115">toorun hello tool, right-click hello file named **AccessPanelExtensionDiagnosticTool**, then select **Open with > Microsoft Windows Based Script Host**.</span></span>
   
    ![Otwórz za pomocą > hosta skryptów na podstawie systemu Microsoft Windows](./media/active-directory-saas-ie-troubleshooting/open_tool.png)
5. <span data-ttu-id="d0cd3-117">Zostanie wtedy wyświetlone powitania po diagnostycznych okna, które opisano, co może być problem z instalacją.</span><span class="sxs-lookup"><span data-stu-id="d0cd3-117">You will then see hello following diagnostic window, which describes what might be wrong with your installation.</span></span>
   
    ![Przykładowe okno diagnostycznych hello](./media/active-directory-saas-ie-troubleshooting/tool_preview.png)
6. <span data-ttu-id="d0cd3-119">Kliknij przycisk "**tak**" toolet hello program poprawka hello problemów, które zostały znalezione.</span><span class="sxs-lookup"><span data-stu-id="d0cd3-119">Click "**YES**" toolet hello program fix hello issues that have been found.</span></span>
7. <span data-ttu-id="d0cd3-120">toosave te zmiany i zamknąć co okno programu Internet Explorer, a następnie otwórz go ponownie.</span><span class="sxs-lookup"><span data-stu-id="d0cd3-120">toosave these changes, close every Internet Explorer window, and then open Internet Explorer again.</span></span><br /><span data-ttu-id="d0cd3-121">Jeśli nadal nie można uzyskać dostępu do aplikacji, spróbuj hello poniższe kroki.</span><span class="sxs-lookup"><span data-stu-id="d0cd3-121">If you still can't access your apps, try hello steps below.</span></span>

## <a name="check-that-hello-access-panel-extension-is-enabled"></a><span data-ttu-id="d0cd3-122">Sprawdź, że hello rozszerzenia Panel dostępu jest włączona</span><span class="sxs-lookup"><span data-stu-id="d0cd3-122">Check that hello Access Panel Extension is enabled</span></span>
<span data-ttu-id="d0cd3-123">tooverify, który hello rozszerzenia Panel dostępu jest włączona w programie Internet Explorer:</span><span class="sxs-lookup"><span data-stu-id="d0cd3-123">tooverify that hello Access Panel Extension is enabled in Internet Explorer:</span></span>

1. <span data-ttu-id="d0cd3-124">W programie Internet Explorer kliknij hello **koło zębate ikonę** na powitania prawym górnym rogu okna hello.</span><span class="sxs-lookup"><span data-stu-id="d0cd3-124">In Internet Explorer, click hello **Gear icon** on hello top right corner of hello window.</span></span> <span data-ttu-id="d0cd3-125">Następnie wybierz **Opcje internetowe**.</span><span class="sxs-lookup"><span data-stu-id="d0cd3-125">Then select **Internet options**.</span></span><br /><span data-ttu-id="d0cd3-126">(W starszych wersjach programu Internet Explorer można go znaleźć, w obszarze **Narzędzia > Opcje internetowe**.</span><span class="sxs-lookup"><span data-stu-id="d0cd3-126">(In older versions of Internet Explorer you can find this under **Tools > Internet options**.</span></span>
   
    ![Przejdź tooTools > Opcje internetowe](./media/active-directory-saas-ie-troubleshooting/internetoptions.png)
2. <span data-ttu-id="d0cd3-128">Kliknij przycisk hello **programy** , a następnie kliknij hello **Zarządzanie dodatkami** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d0cd3-128">Click hello **Programs** tab, then click hello **Manage add-ons** button.</span></span>
   
    ![Kliknij pozycję Zarządzanie dodatkami](./media/active-directory-saas-ie-troubleshooting/internetoptions_programs.png)
3. <span data-ttu-id="d0cd3-130">W tym oknie dialogowym wybierz **rozszerzenia Panel dostępu** , a następnie kliknij przycisk hello **włączyć** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d0cd3-130">In this dialog, select **Access Panel Extension** and then click hello **Enable** button.</span></span>
   
    ![Kliknij pozycję Włącz](./media/active-directory-saas-ie-troubleshooting/enableaddon.png)
4. <span data-ttu-id="d0cd3-132">toosave te zmiany i zamknąć co okno programu Internet Explorer, a następnie otwórz ponownie program Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="d0cd3-132">toosave these changes, close every Internet Explorer window and then open Internet Explorer again.</span></span>

## <a name="enable-extensions-for-inprivate-browsing"></a><span data-ttu-id="d0cd3-133">Włącz rozszerzenia do przeglądania InPrivate</span><span class="sxs-lookup"><span data-stu-id="d0cd3-133">Enable Extensions for InPrivate Browsing</span></span>
<span data-ttu-id="d0cd3-134">Jeśli używasz trybu przeglądania InPrivate hello:</span><span class="sxs-lookup"><span data-stu-id="d0cd3-134">If you are using hello InPrivate Browsing mode:</span></span>

1. <span data-ttu-id="d0cd3-135">W programie Internet Explorer kliknij hello **koło zębate ikonę** na powitania prawym górnym rogu okna hello.</span><span class="sxs-lookup"><span data-stu-id="d0cd3-135">In Internet Explorer, click hello **Gear icon** on hello top right corner of hello window.</span></span> <span data-ttu-id="d0cd3-136">Następnie wybierz **Opcje internetowe**.</span><span class="sxs-lookup"><span data-stu-id="d0cd3-136">Then select **Internet options**.</span></span><br /><span data-ttu-id="d0cd3-137">(W starszych wersjach programu Internet Explorer można go znaleźć, w obszarze **Narzędzia > Opcje internetowe**.</span><span class="sxs-lookup"><span data-stu-id="d0cd3-137">(In older versions of Internet Explorer you can find this under **Tools > Internet options**.</span></span>
   
    ![Przykładowe okno diagnostycznych hello](./media/active-directory-saas-ie-troubleshooting/inprivateoptions.png)
2. <span data-ttu-id="d0cd3-139">Przejdź toohello **prywatności** karcie następnie **Usuń zaznaczenie pola wyboru** hello pole wyboru **wyłącz paski narzędzi i rozszerzeń po uruchomieniu przeglądania InPrivate**</span><span class="sxs-lookup"><span data-stu-id="d0cd3-139">Go toohello **Privacy** tab, then **uncheck** hello checkbox labeled **Disable toolbars and extensions when InPrivate Browsing starts**</span></span></p>
   
    ![Usuń zaznaczenie pola wyboru Wyłącz paski narzędzi i rozszerzeń po uruchomieniu przeglądania InPrivate](./media/active-directory-saas-ie-troubleshooting/enabletoolbars.png)
3. <span data-ttu-id="d0cd3-141">toosave te zmiany i zamknąć co okno programu Internet Explorer, a następnie otwórz ponownie program Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="d0cd3-141">toosave these changes, close every Internet Explorer window and then open Internet Explorer again.</span></span>

## <a name="uninstall-hello-access-panel-extension"></a><span data-ttu-id="d0cd3-142">Odinstaluj hello rozszerzenia Panelu dostępu</span><span class="sxs-lookup"><span data-stu-id="d0cd3-142">Uninstall hello Access Panel Extension</span></span>
<span data-ttu-id="d0cd3-143">Witaj toouninstall rozszerzenia Panelu dostępu z danego komputera:</span><span class="sxs-lookup"><span data-stu-id="d0cd3-143">toouninstall hello Access Panel extension from your computer:</span></span>

1. <span data-ttu-id="d0cd3-144">Na klawiaturze naciśnij klawisz hello **klawisz systemu Windows** tooopen hello Start menu.</span><span class="sxs-lookup"><span data-stu-id="d0cd3-144">On your keyboard, press hello **Windows key** tooopen hello Start menu.</span></span> <span data-ttu-id="d0cd3-145">Po otwarciu hello menu można wpisać niczego toodo wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="d0cd3-145">When hello menu is open, you can type anything toodo a search.</span></span> <span data-ttu-id="d0cd3-146">Wpisz "Panel sterowania", a następnie otwórz hello **Panelu sterowania** po wyświetleniu w wynikach wyszukiwania hello.</span><span class="sxs-lookup"><span data-stu-id="d0cd3-146">Type "Control Panel" and then open hello **Control Panel** when it appears in hello search results.</span></span>
   
    ![Wyszukaj Panelu sterowania](./media/active-directory-saas-ie-troubleshooting/search_sm.png)
2. <span data-ttu-id="d0cd3-148">W hello prawym górnym rogu hello Panelu sterowania, zmień hello **wyświetlić** opcję zbyt**duże ikony**.</span><span class="sxs-lookup"><span data-stu-id="d0cd3-148">In hello top right corner of hello Control Panel, change hello **View by** option too**Large icons**.</span></span> <span data-ttu-id="d0cd3-149">Następnie znajdź i kliknij hello **programy i funkcje** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d0cd3-149">Then find and click hello **Programs and Features** button.</span></span>
   
    ![Zmian hello widoku tooshow duże ikony](./media/active-directory-saas-ie-troubleshooting/control_panel.png)
3. <span data-ttu-id="d0cd3-151">Wybierz z listy hello **rozszerzenia Panel dostępu**i kliknij hello hello **Odinstaluj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d0cd3-151">From hello list, select **Access Panel Extension**, and hello click hello **Uninstall** button.</span></span>
   
    ![Kliknij przycisk Odinstaluj](./media/active-directory-saas-ie-troubleshooting/uninstall.png)
4. <span data-ttu-id="d0cd3-153">Rozszerzenie hello tooinstall może następnie spróbować ponownie toosee Jeśli hello problem został rozwiązany.</span><span class="sxs-lookup"><span data-stu-id="d0cd3-153">You can then try tooinstall hello extension again toosee if hello problem has been resolved.</span></span>

<span data-ttu-id="d0cd3-154">Jeśli wystąpią problemy dotyczące odinstalowywania rozszerzenia hello, można również usunąć go za pomocą hello [Microsoft Napraw go](https://go.microsoft.com/?linkid=9779673) narzędzia.</span><span class="sxs-lookup"><span data-stu-id="d0cd3-154">If you encounter issues uninstalling hello extension, you can also remove it using hello [Microsoft Fix It](https://go.microsoft.com/?linkid=9779673) tool.</span></span>

## <a name="related-articles"></a><span data-ttu-id="d0cd3-155">Pokrewne artykuły</span><span class="sxs-lookup"><span data-stu-id="d0cd3-155">Related Articles</span></span>
* [<span data-ttu-id="d0cd3-156">Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d0cd3-156">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="d0cd3-157">Dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d0cd3-157">Application access and single sign-on with Azure Active Directory</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="d0cd3-158">Jak tooDeploy hello rozszerzenia Panel dostępu dla programu Internet Explorer przy użyciu zasad grupy</span><span class="sxs-lookup"><span data-stu-id="d0cd3-158">How tooDeploy hello Access Panel Extension for Internet Explorer using Group Policy</span></span>](active-directory-saas-ie-group-policy.md)

