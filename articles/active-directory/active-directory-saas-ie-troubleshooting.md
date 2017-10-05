---
title: "Rozwiązywanie problemów z rozszerzenia Panelu dostępu platformy Azure dla programu Internet Explorer | Dokumentacja firmy Microsoft"
description: "Jak wdrożyć dodatek programu Internet Explorer dla portalu Moje aplikacje przy użyciu zasad grupy."
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
ms.openlocfilehash: 938d0b4046afa8c80eabe542f4541d0554948f5d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshooting-the-access-panel-extension-for-internet-explorer"></a><span data-ttu-id="0c290-103">Rozwiązywanie problemów z rozszerzeniem Panel dostępu dla programu Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="0c290-103">Troubleshooting the Access Panel Extension for Internet Explorer</span></span>
<span data-ttu-id="0c290-104">Ten artykuł pomoże Ci rozwiązać następujące problemy:</span><span class="sxs-lookup"><span data-stu-id="0c290-104">This article helps you troubleshoot the following problems:</span></span>

* <span data-ttu-id="0c290-105">Nie możesz uzyskiwać dostęp do aplikacji za pośrednictwem portalu Moje aplikacje przy użyciu programu Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="0c290-105">You're unable to access your apps through the My Apps portal while using Internet Explorer.</span></span>
* <span data-ttu-id="0c290-106">Zostanie wyświetlony komunikat "Zainstaluj oprogramowanie" nawet po zainstalowaniu oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="0c290-106">You see the "Install Software" message even though you've already installed the software.</span></span>

<span data-ttu-id="0c290-107">Jeśli jesteś administratorem, zobacz też: [wdrażanie rozszerzenia Panel dostępu dla programu Internet Explorer przy użyciu zasad grupy](active-directory-saas-ie-group-policy.md)</span><span class="sxs-lookup"><span data-stu-id="0c290-107">If you are an admin, see also: [How to Deploy the Access Panel Extension for Internet Explorer using Group Policy](active-directory-saas-ie-group-policy.md)</span></span>

## <a name="run-the-diagnostic-tool"></a><span data-ttu-id="0c290-108">Uruchom narzędzie diagnostyczne</span><span class="sxs-lookup"><span data-stu-id="0c290-108">Run the Diagnostic Tool</span></span>
<span data-ttu-id="0c290-109">Można diagnozować problemy instalacji z rozszerzeniem panelu dostępu przez pobranie i uruchomienie narzędzia diagnostyczne panelu dostępu:</span><span class="sxs-lookup"><span data-stu-id="0c290-109">You can diagnose installation problems with the Access Panel Extension by downloading and running the Access Panel diagnostic tool:</span></span>

1. [<span data-ttu-id="0c290-110">Kliknij tutaj, aby pobrać narzędzie diagnostyczne.</span><span class="sxs-lookup"><span data-stu-id="0c290-110">Click here to download the diagnostic tool.</span></span>](https://account.activedirectory.windowsazure.com/applications/AccessPanelExtensionDiagnosticTool/AccessPanelExtensionDiagnosticTool.zip)
2. <span data-ttu-id="0c290-111">Otwórz plik i naciśnij klawisz **Wyodrębnij wszystkie** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0c290-111">Open the file, and press **Extract all** button.</span></span>
   
    ![Kliknij przycisk Wyodrębnij wszystkie](./media/active-directory-saas-ie-troubleshooting/extract1.png)
3. <span data-ttu-id="0c290-113">Następnie naciśnij klawisz **wyodrębnić** przycisk, aby kontynuować.</span><span class="sxs-lookup"><span data-stu-id="0c290-113">Then press the **Extract** button to continue.</span></span>
   
    ![Naciśnij klawisz wyodrębniania](./media/active-directory-saas-ie-troubleshooting/extract2.png)
4. <span data-ttu-id="0c290-115">Aby uruchomić narzędzie, kliknij prawym przyciskiem myszy plik o nazwie **AccessPanelExtensionDiagnosticTool**, a następnie wybierz pozycję **Otwórz za pomocą > na podstawie Host skryptów systemu Windows**.</span><span class="sxs-lookup"><span data-stu-id="0c290-115">To run the tool, right-click the file named **AccessPanelExtensionDiagnosticTool**, then select **Open with > Microsoft Windows Based Script Host**.</span></span>
   
    ![Otwórz za pomocą > hosta skryptów na podstawie systemu Microsoft Windows](./media/active-directory-saas-ie-troubleshooting/open_tool.png)
5. <span data-ttu-id="0c290-117">Zostanie wtedy wyświetlone następujące okno diagnostyczne w tym artykule opisano, co może być problem z instalacją.</span><span class="sxs-lookup"><span data-stu-id="0c290-117">You will then see the following diagnostic window, which describes what might be wrong with your installation.</span></span>
   
    ![Przykładowe okno diagnostycznych](./media/active-directory-saas-ie-troubleshooting/tool_preview.png)
6. <span data-ttu-id="0c290-119">Kliknij przycisk "**tak**" Aby pozwolić, aby rozwiązać problemy, które zostały znalezione program.</span><span class="sxs-lookup"><span data-stu-id="0c290-119">Click "**YES**" to let the program fix the issues that have been found.</span></span>
7. <span data-ttu-id="0c290-120">Aby zapisać te zmiany, Zamknij co okno programu Internet Explorer, a następnie otwórz go ponownie.</span><span class="sxs-lookup"><span data-stu-id="0c290-120">To save these changes, close every Internet Explorer window, and then open Internet Explorer again.</span></span><br /><span data-ttu-id="0c290-121">Jeśli nadal nie można uzyskać dostępu do aplikacji, spróbuj wykonać poniższe czynności.</span><span class="sxs-lookup"><span data-stu-id="0c290-121">If you still can't access your apps, try the steps below.</span></span>

## <a name="check-that-the-access-panel-extension-is-enabled"></a><span data-ttu-id="0c290-122">Sprawdź, czy włączono rozszerzenie panelu dostępu</span><span class="sxs-lookup"><span data-stu-id="0c290-122">Check that the Access Panel Extension is enabled</span></span>
<span data-ttu-id="0c290-123">Aby sprawdzić, czy rozszerzenie panelu dostępu jest włączona w programie Internet Explorer:</span><span class="sxs-lookup"><span data-stu-id="0c290-123">To verify that the Access Panel Extension is enabled in Internet Explorer:</span></span>

1. <span data-ttu-id="0c290-124">W programie Internet Explorer, kliknij przycisk **koło zębate ikonę** w prawym górnym rogu okna.</span><span class="sxs-lookup"><span data-stu-id="0c290-124">In Internet Explorer, click the **Gear icon** on the top right corner of the window.</span></span> <span data-ttu-id="0c290-125">Następnie wybierz **Opcje internetowe**.</span><span class="sxs-lookup"><span data-stu-id="0c290-125">Then select **Internet options**.</span></span><br /><span data-ttu-id="0c290-126">(W starszych wersjach programu Internet Explorer można go znaleźć, w obszarze **Narzędzia > Opcje internetowe**.</span><span class="sxs-lookup"><span data-stu-id="0c290-126">(In older versions of Internet Explorer you can find this under **Tools > Internet options**.</span></span>
   
    ![Przejdź do pozycji Narzędzia > Opcje internetowe](./media/active-directory-saas-ie-troubleshooting/internetoptions.png)
2. <span data-ttu-id="0c290-128">Kliknij przycisk **programy** , a następnie kliknij **Zarządzanie dodatkami** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0c290-128">Click the **Programs** tab, then click the **Manage add-ons** button.</span></span>
   
    ![Kliknij pozycję Zarządzanie dodatkami](./media/active-directory-saas-ie-troubleshooting/internetoptions_programs.png)
3. <span data-ttu-id="0c290-130">W tym oknie dialogowym wybierz **rozszerzenia Panel dostępu** , a następnie kliknij przycisk **włączyć** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0c290-130">In this dialog, select **Access Panel Extension** and then click the **Enable** button.</span></span>
   
    ![Kliknij pozycję Włącz](./media/active-directory-saas-ie-troubleshooting/enableaddon.png)
4. <span data-ttu-id="0c290-132">Aby zapisać te zmiany, zamknij okno programu Internet Explorer, co, a następnie otwórz go ponownie.</span><span class="sxs-lookup"><span data-stu-id="0c290-132">To save these changes, close every Internet Explorer window and then open Internet Explorer again.</span></span>

## <a name="enable-extensions-for-inprivate-browsing"></a><span data-ttu-id="0c290-133">Włącz rozszerzenia do przeglądania InPrivate</span><span class="sxs-lookup"><span data-stu-id="0c290-133">Enable Extensions for InPrivate Browsing</span></span>
<span data-ttu-id="0c290-134">Jeśli używasz trybu przeglądania InPrivate:</span><span class="sxs-lookup"><span data-stu-id="0c290-134">If you are using the InPrivate Browsing mode:</span></span>

1. <span data-ttu-id="0c290-135">W programie Internet Explorer, kliknij przycisk **koło zębate ikonę** w prawym górnym rogu okna.</span><span class="sxs-lookup"><span data-stu-id="0c290-135">In Internet Explorer, click the **Gear icon** on the top right corner of the window.</span></span> <span data-ttu-id="0c290-136">Następnie wybierz **Opcje internetowe**.</span><span class="sxs-lookup"><span data-stu-id="0c290-136">Then select **Internet options**.</span></span><br /><span data-ttu-id="0c290-137">(W starszych wersjach programu Internet Explorer można go znaleźć, w obszarze **Narzędzia > Opcje internetowe**.</span><span class="sxs-lookup"><span data-stu-id="0c290-137">(In older versions of Internet Explorer you can find this under **Tools > Internet options**.</span></span>
   
    ![Przykładowe okno diagnostycznych](./media/active-directory-saas-ie-troubleshooting/inprivateoptions.png)
2. <span data-ttu-id="0c290-139">Przejdź do **prywatności** karcie następnie **Usuń zaznaczenie pola wyboru** pola wyboru **wyłącz paski narzędzi i rozszerzeń po uruchomieniu przeglądania InPrivate**</span><span class="sxs-lookup"><span data-stu-id="0c290-139">Go to the **Privacy** tab, then **uncheck** the checkbox labeled **Disable toolbars and extensions when InPrivate Browsing starts**</span></span></p>
   
    ![Usuń zaznaczenie pola wyboru Wyłącz paski narzędzi i rozszerzeń po uruchomieniu przeglądania InPrivate](./media/active-directory-saas-ie-troubleshooting/enabletoolbars.png)
3. <span data-ttu-id="0c290-141">Aby zapisać te zmiany, zamknij okno programu Internet Explorer, co, a następnie otwórz go ponownie.</span><span class="sxs-lookup"><span data-stu-id="0c290-141">To save these changes, close every Internet Explorer window and then open Internet Explorer again.</span></span>

## <a name="uninstall-the-access-panel-extension"></a><span data-ttu-id="0c290-142">Odinstaluj rozszerzenie panelu dostępu</span><span class="sxs-lookup"><span data-stu-id="0c290-142">Uninstall the Access Panel Extension</span></span>
<span data-ttu-id="0c290-143">Aby odinstalować rozszerzenia Panelu dostępu z tego komputera:</span><span class="sxs-lookup"><span data-stu-id="0c290-143">To uninstall the Access Panel extension from your computer:</span></span>

1. <span data-ttu-id="0c290-144">Na klawiaturze naciśnij klawisz **klawisz systemu Windows** aby otworzyć Start menu.</span><span class="sxs-lookup"><span data-stu-id="0c290-144">On your keyboard, press the **Windows key** to open the Start menu.</span></span> <span data-ttu-id="0c290-145">Po otwarciu menu można wpisać niczego do wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="0c290-145">When the menu is open, you can type anything to do a search.</span></span> <span data-ttu-id="0c290-146">Wpisz "Panel sterowania", a następnie otwórz **Panelu sterowania** po wyświetleniu w wynikach wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="0c290-146">Type "Control Panel" and then open the **Control Panel** when it appears in the search results.</span></span>
   
    ![Wyszukaj Panelu sterowania](./media/active-directory-saas-ie-troubleshooting/search_sm.png)
2. <span data-ttu-id="0c290-148">W prawym górnym rogu panelu sterowania Zmień **wyświetlić** opcji w celu **duże ikony**.</span><span class="sxs-lookup"><span data-stu-id="0c290-148">In the top right corner of the Control Panel, change the **View by** option to **Large icons**.</span></span> <span data-ttu-id="0c290-149">Następnie znajdź i kliknij **programy i funkcje** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0c290-149">Then find and click the **Programs and Features** button.</span></span>
   
    ![Zmian widok do pokazania duże ikony](./media/active-directory-saas-ie-troubleshooting/control_panel.png)
3. <span data-ttu-id="0c290-151">Wybierz z listy, **rozszerzenia Panel dostępu**, a następnie kliknij **Odinstaluj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0c290-151">From the list, select **Access Panel Extension**, and the click the **Uninstall** button.</span></span>
   
    ![Kliknij przycisk Odinstaluj](./media/active-directory-saas-ie-troubleshooting/uninstall.png)
4. <span data-ttu-id="0c290-153">Następnie spróbujesz zainstalować rozszerzenie ponownie, aby sprawdzić, czy problem został rozwiązany.</span><span class="sxs-lookup"><span data-stu-id="0c290-153">You can then try to install the extension again to see if the problem has been resolved.</span></span>

<span data-ttu-id="0c290-154">Jeśli wystąpią problemy dotyczące odinstalowywania rozszerzenia, można również usunąć go za pomocą [Microsoft Napraw go](https://go.microsoft.com/?linkid=9779673) narzędzia.</span><span class="sxs-lookup"><span data-stu-id="0c290-154">If you encounter issues uninstalling the extension, you can also remove it using the [Microsoft Fix It](https://go.microsoft.com/?linkid=9779673) tool.</span></span>

## <a name="related-articles"></a><span data-ttu-id="0c290-155">Pokrewne artykuły</span><span class="sxs-lookup"><span data-stu-id="0c290-155">Related Articles</span></span>
* [<span data-ttu-id="0c290-156">Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0c290-156">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="0c290-157">Dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0c290-157">Application access and single sign-on with Azure Active Directory</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="0c290-158">Wdrażanie rozszerzenia Panel dostępu dla programu Internet Explorer przy użyciu zasad grupy</span><span class="sxs-lookup"><span data-stu-id="0c290-158">How to Deploy the Access Panel Extension for Internet Explorer using Group Policy</span></span>](active-directory-saas-ie-group-policy.md)

