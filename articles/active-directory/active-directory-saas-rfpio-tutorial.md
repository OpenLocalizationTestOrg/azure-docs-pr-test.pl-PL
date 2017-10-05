---
title: 'Samouczek: Integracji Azure Active Directory z RFPIO | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i RFPIO."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 87187076-7b50-4247-814f-f217b052703f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 26a8bb17dad5a01b401ce7f9b484f09822825cbf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rfpio"></a><span data-ttu-id="87a69-103">Samouczek: Integracji Azure Active Directory z RFPIO</span><span class="sxs-lookup"><span data-stu-id="87a69-103">Tutorial: Azure Active Directory integration with RFPIO</span></span>

<span data-ttu-id="87a69-104">Z tego samouczka dowiesz się integrowanie RFPIO z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="87a69-104">In this tutorial, you learn how to integrate RFPIO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="87a69-105">Integracja z usługą Azure AD RFPIO zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="87a69-105">Integrating RFPIO with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="87a69-106">Możesz kontrolować, kto w usłudze Azure AD, który ma dostęp do RFPIO.</span><span class="sxs-lookup"><span data-stu-id="87a69-106">You can control who in Azure AD who has access to RFPIO.</span></span>
- <span data-ttu-id="87a69-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do RFPIO (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="87a69-107">You can enable your users to automatically get signed-on to RFPIO (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="87a69-108">Możesz zarządzać kont w jednej centralnej lokalizacji--portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="87a69-108">You can manage your accounts in one central location--the Azure portal.</span></span>

<span data-ttu-id="87a69-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="87a69-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="87a69-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="87a69-110">Prerequisites</span></span>

<span data-ttu-id="87a69-111">Aby skonfigurować integrację usługi Azure AD z RFPIO, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="87a69-111">To configure Azure AD integration with RFPIO, you need the following items:</span></span>

- <span data-ttu-id="87a69-112">Subskrypcja usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="87a69-112">An Azure AD subscription.</span></span>
- <span data-ttu-id="87a69-113">RFPIO pojedynczy znak z włączoną subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="87a69-113">A RFPIO single sign-on-enabled subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="87a69-114">Firma Microsoft nie zaleca się używanie środowiska produkcyjnego do testowania czynności w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="87a69-114">We don't recommend that you use a production environment to test the steps in this tutorial.</span></span>

<span data-ttu-id="87a69-115">Aby przetestować kroki opisane w tym samouczku, wykonaj te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="87a69-115">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="87a69-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="87a69-116">Do not use your production environment unless it's necessary.</span></span>
- <span data-ttu-id="87a69-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać [miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="87a69-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="87a69-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="87a69-118">Scenario description</span></span>
<span data-ttu-id="87a69-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="87a69-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="87a69-120">Scenariusz, który jest opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="87a69-120">The scenario that's outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="87a69-121">Dodawanie RFPIO z galerii.</span><span class="sxs-lookup"><span data-stu-id="87a69-121">Adding RFPIO from the gallery.</span></span>
2. <span data-ttu-id="87a69-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="87a69-122">Configuring and testing Azure AD single sign-on.</span></span>

## <a name="add-rfpio-from-the-gallery"></a><span data-ttu-id="87a69-123">Dodaj RFPIO z galerii</span><span class="sxs-lookup"><span data-stu-id="87a69-123">Add RFPIO from the gallery</span></span>
<span data-ttu-id="87a69-124">Aby skonfigurować integrację usługi Azure AD RFPIO, należy dodać RFPIO z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="87a69-124">To configure the integration of RFPIO into Azure AD, you need to add RFPIO from the gallery to your list of managed SaaS apps.</span></span>

### <a name="to-add-rfpio-from-the-gallery"></a><span data-ttu-id="87a69-125">Aby dodać RFPIO z galerii</span><span class="sxs-lookup"><span data-stu-id="87a69-125">To add RFPIO from the gallery</span></span>

1. <span data-ttu-id="87a69-126">W  **[portalu Azure](https://portal.azure.com)**, w okienku nawigacji po lewej stronie wybierz **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="87a69-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation pane, select the **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="87a69-128">Wybierz **aplikacje dla przedsiębiorstw**, a następnie wybierz **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="87a69-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="87a69-130">Aby dodać nową aplikację, zaznacz **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="87a69-130">To add a new application, select the **New application** button on the top of dialog box.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="87a69-132">W polu wyszukiwania wpisz **RFPIO**.</span><span class="sxs-lookup"><span data-stu-id="87a69-132">In the search box, type **RFPIO**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_search.png)

5. <span data-ttu-id="87a69-134">W panelu wyników wybierz **RFPIO**, a następnie wybierz **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="87a69-134">In the results panel, select **RFPIO**, and then select the **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="87a69-136">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="87a69-136">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="87a69-137">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z RFPIO w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="87a69-137">In this section, you configure and test Azure AD single sign-on with RFPIO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="87a69-138">Do rejestracji jednokrotnej do pracy usługi Azure AD musi ustalić relacji między użytkownikiem odpowiednika w RFPIO a użytkownikiem w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="87a69-138">For single sign-on to work, Azure AD needs to know what the relationship is between counterpart user in RFPIO and a user in Azure AD.</span></span> <span data-ttu-id="87a69-139">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w RFPIO musi się.</span><span class="sxs-lookup"><span data-stu-id="87a69-139">In other words, a link relationship between an Azure AD user and the related user in RFPIO needs to be established.</span></span>

<span data-ttu-id="87a69-140">W RFPIO, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="87a69-140">In RFPIO, assign the value of **user name** in Azure AD as the value of  **Username** to establish the link relationship.</span></span>

<span data-ttu-id="87a69-141">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z RFPIO, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="87a69-141">To configure and test Azure AD single sign-on with RFPIO, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="87a69-142">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**— aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="87a69-142">**[Configure Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**--to enable your users to use this feature.</span></span>
2. <span data-ttu-id="87a69-143">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**— do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="87a69-143">**[Create an Azure AD test user](#creating-an-azure-ad-test-user)**-- to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="87a69-144">**[Tworzenie użytkownika testowego RFPIO](#creating-a-rfpio-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta RFPIO połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="87a69-144">**[Create a RFPIO test user](#creating-a-rfpio-test-user)** --to have a counterpart of Britta Simon in RFPIO that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="87a69-145">**[Przypisz użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**— aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="87a69-145">**[Assign the Azure AD test user](#assigning-the-azure-ad-test-user)**--to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="87a69-146">**[Test rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="87a69-146">**[Test Single Sign-On](#testing-single-sign-on)** --to verify if the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="87a69-147">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="87a69-147">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="87a69-148">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji RFPIO.</span><span class="sxs-lookup"><span data-stu-id="87a69-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your RFPIO application.</span></span>

<span data-ttu-id="87a69-149">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z RFPIO, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="87a69-149">**To configure Azure AD single sign-on with RFPIO, perform the following steps:**</span></span>

1. <span data-ttu-id="87a69-150">W portalu Azure na **RFPIO** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="87a69-150">In the Azure portal, on the **RFPIO** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="87a69-152">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="87a69-152">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_samlbase.png)

3. <span data-ttu-id="87a69-154">Na **RFPIO domeny i adres URL** sekcji, jeśli chcesz skonfigurować aplikację w **IDP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="87a69-154">On the **RFPIO Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url.png)

    <span data-ttu-id="87a69-156">a.</span><span class="sxs-lookup"><span data-stu-id="87a69-156">a.</span></span> <span data-ttu-id="87a69-157">W **identyfikator** tekstowym, wpisz adres URL:`https://www.rfpio.com`</span><span class="sxs-lookup"><span data-stu-id="87a69-157">In the **Identifier** textbox, type the URL: `https://www.rfpio.com`</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url1.png)

    <span data-ttu-id="87a69-159">b.</span><span class="sxs-lookup"><span data-stu-id="87a69-159">b.</span></span> <span data-ttu-id="87a69-160">Sprawdź **Pokaż zaawansowane ustawienia adresu URL**.</span><span class="sxs-lookup"><span data-stu-id="87a69-160">Check **Show advanced URL settings**.</span></span>

    <span data-ttu-id="87a69-161">c.</span><span class="sxs-lookup"><span data-stu-id="87a69-161">c.</span></span> <span data-ttu-id="87a69-162">W **stan przekazywania** pole tekstowe Wprowadź wartość ciągu.</span><span class="sxs-lookup"><span data-stu-id="87a69-162">In the **Relay State** textbox enter a string value.</span></span> <span data-ttu-id="87a69-163">Skontaktuj się z [RFPIO obsługuje zespołu](https://www.rfpio.com/contact/) aby zyskać tę wartość.</span><span class="sxs-lookup"><span data-stu-id="87a69-163">Contact [RFPIO support team](https://www.rfpio.com/contact/) to get this value.</span></span> 

4. <span data-ttu-id="87a69-164">Sprawdź **Pokaż zaawansowane ustawienia adresu URL**.</span><span class="sxs-lookup"><span data-stu-id="87a69-164">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="87a69-165">Jeśli chcesz skonfigurować aplikację w **SP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="87a69-165">If you wish to configure the application in **SP** initiated mode:</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url2.png)

    <span data-ttu-id="87a69-167">W **Zaloguj się na adres URL** tekstowym, wpisz adres URL:`https://www.app.rfpio.com`</span><span class="sxs-lookup"><span data-stu-id="87a69-167">In the **Sign on URL** textbox, type the URL: `https://www.app.rfpio.com`</span></span>

5. <span data-ttu-id="87a69-168">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="87a69-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_certificate.png) 

6. <span data-ttu-id="87a69-170">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="87a69-170">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="87a69-172">W oknie przeglądarki innej witryny sieci web, zaloguj się do **RFPIO** witryny sieci Web jako administrator.</span><span class="sxs-lookup"><span data-stu-id="87a69-172">In a different web browser window, login to the **RFPIO** website as an administrator.</span></span>

8. <span data-ttu-id="87a69-173">Kliknij menu rozwijanego lewym rogu dolnej.</span><span class="sxs-lookup"><span data-stu-id="87a69-173">Click on the bottom left corner dropdown.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/app1.png)

9. <span data-ttu-id="87a69-175">Polecenie **ustawienia organizacji**.</span><span class="sxs-lookup"><span data-stu-id="87a69-175">Click on the **Organization Settings**.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/app2.png)

10. <span data-ttu-id="87a69-177">Polecenie **funkcje & integracji**.</span><span class="sxs-lookup"><span data-stu-id="87a69-177">Click on the **FEATURES & INTEGRATION**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/app4.png)

11. <span data-ttu-id="87a69-179">W **konfiguracji logowania jednokrotnego SAML** kliknij **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="87a69-179">In the **SAML SSO Configuration** Click **Edit**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/app3.png)

12. <span data-ttu-id="87a69-181">W tej sekcji należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="87a69-181">In this Section perform following actions:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/app5.png)
    
    <span data-ttu-id="87a69-183">a.</span><span class="sxs-lookup"><span data-stu-id="87a69-183">a.</span></span> <span data-ttu-id="87a69-184">Skopiuj zawartość **pobierane metadane XML** i wklej ją do **konfiguracji tożsamości** pola.</span><span class="sxs-lookup"><span data-stu-id="87a69-184">Copy the content of the **Downloaded Metadata XML** and paste it into the **identity configuration** field.</span></span>

    > [!NOTE]
    ><span data-ttu-id="87a69-185">Aby skopiować zawartość pobrana **XML metadanych** użyj **Notatnik ++** lub właściwe **edytora XML**.</span><span class="sxs-lookup"><span data-stu-id="87a69-185">To copy the content of downloaded **Metadata XML** Use **Notepad++** or proper **XML Editor**.</span></span> 

    <span data-ttu-id="87a69-186">b.</span><span class="sxs-lookup"><span data-stu-id="87a69-186">b.</span></span> <span data-ttu-id="87a69-187">Kliknij przycisk **zweryfikować**.</span><span class="sxs-lookup"><span data-stu-id="87a69-187">Click **Validate**.</span></span>

    <span data-ttu-id="87a69-188">c.</span><span class="sxs-lookup"><span data-stu-id="87a69-188">c.</span></span> <span data-ttu-id="87a69-189">Po kliknięciu przycisku **zweryfikować**, przerzucania **SAML(Enabled)** do włączenia.</span><span class="sxs-lookup"><span data-stu-id="87a69-189">After Clicking **Validate**, Flip **SAML(Enabled)** to on.</span></span>

    <span data-ttu-id="87a69-190">d.</span><span class="sxs-lookup"><span data-stu-id="87a69-190">d.</span></span> <span data-ttu-id="87a69-191">Kliknij przycisk **przesłać**.</span><span class="sxs-lookup"><span data-stu-id="87a69-191">Click **Submit**.</span></span>

> [!TIP]
> <span data-ttu-id="87a69-192">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="87a69-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="87a69-193">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="87a69-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="87a69-194">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="87a69-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="87a69-195">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="87a69-195">Create an Azure AD test user</span></span>
<span data-ttu-id="87a69-196">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="87a69-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="87a69-198">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="87a69-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="87a69-199">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="87a69-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="87a69-201">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="87a69-201">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="87a69-203">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="87a69-203">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="87a69-205">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="87a69-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="87a69-207">a.</span><span class="sxs-lookup"><span data-stu-id="87a69-207">a.</span></span> <span data-ttu-id="87a69-208">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="87a69-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="87a69-209">b.</span><span class="sxs-lookup"><span data-stu-id="87a69-209">b.</span></span> <span data-ttu-id="87a69-210">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="87a69-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="87a69-211">c.</span><span class="sxs-lookup"><span data-stu-id="87a69-211">c.</span></span> <span data-ttu-id="87a69-212">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="87a69-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="87a69-213">d.</span><span class="sxs-lookup"><span data-stu-id="87a69-213">d.</span></span> <span data-ttu-id="87a69-214">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="87a69-214">Click **Create**.</span></span>
 
### <a name="create-a-rfpio-test-user"></a><span data-ttu-id="87a69-215">Tworzenie użytkownika testowego RFPIO</span><span class="sxs-lookup"><span data-stu-id="87a69-215">Create a RFPIO test user</span></span>

<span data-ttu-id="87a69-216">Aby umożliwić użytkownikom usługi Azure AD zalogować się do RFPIO, musi być przygotowana do RFPIO.</span><span class="sxs-lookup"><span data-stu-id="87a69-216">To enable Azure AD users to log in to RFPIO, they must be provisioned into RFPIO.</span></span>  
<span data-ttu-id="87a69-217">W przypadku RFPIO Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="87a69-217">In the case of RFPIO, provisioning is a manual task.</span></span>

<span data-ttu-id="87a69-218">**Aby udostępnić konta użytkownika, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="87a69-218">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="87a69-219">Zaloguj się do witryny firmy RFPIO jako administrator.</span><span class="sxs-lookup"><span data-stu-id="87a69-219">Log in to your RFPIO company site as an administrator.</span></span>

2. <span data-ttu-id="87a69-220">Kliknij menu rozwijanego lewym rogu dolnej.</span><span class="sxs-lookup"><span data-stu-id="87a69-220">Click on the bottom left corner dropdown.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/app1.png)

3. <span data-ttu-id="87a69-222">Polecenie **ustawienia organizacji**.</span><span class="sxs-lookup"><span data-stu-id="87a69-222">Click on the **Organization Settings**.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/app2.png)

4. <span data-ttu-id="87a69-224">Kliknij przycisk **członków zespołu**.</span><span class="sxs-lookup"><span data-stu-id="87a69-224">Click **TEAM MEMBERS**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/app6.png)

5. <span data-ttu-id="87a69-226">Polecenie **Dodaj członków**.</span><span class="sxs-lookup"><span data-stu-id="87a69-226">Click on **ADD MEMBERS**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/app7.png)

6. <span data-ttu-id="87a69-228">W **Dodawanie nowych elementów członkowskich** sekcji.</span><span class="sxs-lookup"><span data-stu-id="87a69-228">In the **Add New Members** section.</span></span> <span data-ttu-id="87a69-229">Wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="87a69-229">Perform following actions:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/app8.png)

    <span data-ttu-id="87a69-231">a.</span><span class="sxs-lookup"><span data-stu-id="87a69-231">a.</span></span> <span data-ttu-id="87a69-232">Wprowadź **adres E-mail** w **Podaj jeden adres e-mail w jednym wierszu** pola.</span><span class="sxs-lookup"><span data-stu-id="87a69-232">Enter **Email address** in the **Enter one email per line** field.</span></span>

    <span data-ttu-id="87a69-233">b.</span><span class="sxs-lookup"><span data-stu-id="87a69-233">b.</span></span> <span data-ttu-id="87a69-234">Wybierz Plese **roli** zgodnie z wymaganiami.</span><span class="sxs-lookup"><span data-stu-id="87a69-234">Plese select **Role** according your requirements.</span></span>

    <span data-ttu-id="87a69-235">c.</span><span class="sxs-lookup"><span data-stu-id="87a69-235">c.</span></span> <span data-ttu-id="87a69-236">Kliknij przycisk **Dodaj członków**.</span><span class="sxs-lookup"><span data-stu-id="87a69-236">Click **ADD MEMBERS**.</span></span>
        
    > [!NOTE]
    > <span data-ttu-id="87a69-237">Właściciel konta usługi Azure Active Directory otrzymuje wiadomość e-mail i następuje łącze, aby potwierdzić swoje konto, zanim staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="87a69-237">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="87a69-238">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="87a69-238">Assign the Azure AD test user</span></span>

<span data-ttu-id="87a69-239">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu RFPIO.</span><span class="sxs-lookup"><span data-stu-id="87a69-239">In this section, you enable Britta Simon to use Azure single sign-on by granting access to RFPIO.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="87a69-241">**Aby przypisać Simona Britta RFPIO, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="87a69-241">**To assign Britta Simon to RFPIO, perform the following steps:**</span></span>

1. <span data-ttu-id="87a69-242">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="87a69-242">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="87a69-244">Na liście aplikacji zaznacz **RFPIO**.</span><span class="sxs-lookup"><span data-stu-id="87a69-244">In the applications list, select **RFPIO**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_app.png) 

3. <span data-ttu-id="87a69-246">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="87a69-246">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="87a69-248">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="87a69-248">Click **Add** button.</span></span> <span data-ttu-id="87a69-249">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="87a69-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="87a69-251">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="87a69-251">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="87a69-252">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="87a69-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="87a69-253">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="87a69-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="87a69-254">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="87a69-254">Test single sign-on</span></span>

<span data-ttu-id="87a69-255">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="87a69-255">In this section, you test your Azure AD single sign-on configuration by using the Access Panel.</span></span>

<span data-ttu-id="87a69-256">Po kliknięciu kafelka RFPIO w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji RFPIO.</span><span class="sxs-lookup"><span data-stu-id="87a69-256">When you click the RFPIO tile in the Access Panel, you should get automatically signed-on to your RFPIO application.</span></span>
<span data-ttu-id="87a69-257">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="87a69-257">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="87a69-258">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="87a69-258">Additional resources</span></span>

* [<span data-ttu-id="87a69-259">Lista samouczków dotyczących sposobu integracji aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="87a69-259">List of tutorials about how to integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="87a69-260">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="87a69-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_203.png

