---
title: "Samouczek: Azure Active Directory integracji z oprogramowaniem chlorowców | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między oprogramowaniem halogenowe i Azure Active Directory."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2ca2298d-9a0c-4f14-925c-fa23f2659d28
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: e09fa93038965e4880a23002bac6917ad2a077f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halogen-software"></a><span data-ttu-id="75033-103">Samouczek: Azure Active Directory integracji z oprogramowaniem chlorowców</span><span class="sxs-lookup"><span data-stu-id="75033-103">Tutorial: Azure Active Directory integration with Halogen Software</span></span>

<span data-ttu-id="75033-104">Z tego samouczka dowiesz się integrowanie chlorowców oprogramowania z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="75033-104">In this tutorial, you learn how to integrate Halogen Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="75033-105">Integrowanie chlorowców oprogramowania z usługi Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="75033-105">Integrating Halogen Software with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="75033-106">Można kontrolować w usłudze Azure AD, który ma dostęp do oprogramowania chlorowców</span><span class="sxs-lookup"><span data-stu-id="75033-106">You can control in Azure AD who has access to Halogen Software</span></span>
- <span data-ttu-id="75033-107">Umożliwia użytkownikom automatycznie pobrać zalogowane oprogramowania chlorowców (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="75033-107">You can enable your users to automatically get signed-on to Halogen Software (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="75033-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="75033-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="75033-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="75033-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="75033-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="75033-110">Prerequisites</span></span>

<span data-ttu-id="75033-111">Aby skonfigurować integrację usługi Azure AD z oprogramowaniem halogenowe, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="75033-111">To configure Azure AD integration with Halogen Software, you need the following items:</span></span>

- <span data-ttu-id="75033-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="75033-112">An Azure AD subscription</span></span>
- <span data-ttu-id="75033-113">Oprogramowanie chlorowców logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="75033-113">A Halogen Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="75033-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="75033-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="75033-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="75033-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="75033-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="75033-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="75033-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="75033-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="75033-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="75033-118">Scenario description</span></span>

<span data-ttu-id="75033-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="75033-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="75033-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="75033-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="75033-121">Dodawanie oprogramowania chlorowców z galerii</span><span class="sxs-lookup"><span data-stu-id="75033-121">Adding Halogen Software from the gallery</span></span>
2. <span data-ttu-id="75033-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="75033-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-halogen-software-from-the-gallery"></a><span data-ttu-id="75033-123">Dodawanie oprogramowania chlorowców z galerii</span><span class="sxs-lookup"><span data-stu-id="75033-123">Adding Halogen Software from the gallery</span></span>

<span data-ttu-id="75033-124">Aby skonfigurować integrację usługi Azure AD chlorowców oprogramowania, należy dodać chlorowców oprogramowania z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="75033-124">To configure the integration of Halogen Software into Azure AD, you need to add Halogen Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="75033-125">**Aby dodać chlorowców oprogramowanie z poziomu galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="75033-125">**To add Halogen Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="75033-126">W ** [portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="75033-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="75033-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="75033-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="75033-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="75033-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="75033-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="75033-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="75033-133">W polu wyszukiwania wpisz **oprogramowania chlorowców**.</span><span class="sxs-lookup"><span data-stu-id="75033-133">In the search box, type **Halogen Software**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_search.png)

5. <span data-ttu-id="75033-135">W panelu wyników wybierz **oprogramowania chlorowców**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="75033-135">In the results panel, select **Halogen Software**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="75033-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="75033-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="75033-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z oprogramowaniem chlorowców w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="75033-138">In this section, you configure and test Azure AD single sign-on with Halogen Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="75033-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w oprogramowaniu halogenowe jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="75033-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Halogen Software is to a user in Azure AD.</span></span> <span data-ttu-id="75033-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i danemu użytkownikowi w oprogramowaniu chlorowców musi określone.</span><span class="sxs-lookup"><span data-stu-id="75033-140">In other words, a link relationship between an Azure AD user and the related user in Halogen Software needs to be established.</span></span>

<span data-ttu-id="75033-141">W oprogramowaniu chlorowców przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="75033-141">In Halogen Software, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="75033-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z oprogramowaniem chlorowców, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="75033-142">To configure and test Azure AD single sign-on with Halogen Software, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="75033-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on) ** — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="75033-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="75033-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user) ** — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="75033-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="75033-145">**[Tworzenie użytkownika testowego oprogramowania chlorowców](#creating-a-halogen-software-test-user) ** — w celu zapewnienia odpowiednikiem Simona Britta chlorowców oprogramowania, które jest połączone z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="75033-145">**[Creating a Halogen Software test user](#creating-a-halogen-software-test-user)** - to have a counterpart of Britta Simon in Halogen Software that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="75033-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user) ** — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="75033-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="75033-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on) ** — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="75033-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="75033-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="75033-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="75033-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w używanej aplikacji halogenowe.</span><span class="sxs-lookup"><span data-stu-id="75033-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Halogen Software application.</span></span>

<span data-ttu-id="75033-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z oprogramowaniem halogenowe, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="75033-150">**To configure Azure AD single sign-on with Halogen Software, perform the following steps:**</span></span>

1. <span data-ttu-id="75033-151">W portalu Azure na **oprogramowania chlorowców** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="75033-151">In the Azure portal, on the **Halogen Software** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="75033-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="75033-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_samlbase.png)

3. <span data-ttu-id="75033-155">Na **chlorowców oprogramowania domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="75033-155">On the **Halogen Software Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_url.png)

    <span data-ttu-id="75033-157">a.</span><span class="sxs-lookup"><span data-stu-id="75033-157">a.</span></span> <span data-ttu-id="75033-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://global.hgncloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="75033-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://global.hgncloud.com/<companyname>`</span></span>

    <span data-ttu-id="75033-159">b.</span><span class="sxs-lookup"><span data-stu-id="75033-159">b.</span></span> <span data-ttu-id="75033-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca: `https://global.halogensoftware.com/<companyname>`,`https://global.hgncloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="75033-160">In the **Identifier** textbox, type a URL using the following pattern: `https://global.halogensoftware.com/<companyname>`, `https://global.hgncloud.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="75033-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="75033-161">These values are not real.</span></span> <span data-ttu-id="75033-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="75033-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="75033-163">Skontaktuj się z [zespołem pomocy technicznej klienta oprogramowania chlorowców](https://support.halogensoftware.com/) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="75033-163">Contact [Halogen Software Client support team](https://support.halogensoftware.com/) to get these values.</span></span> 
 


4. <span data-ttu-id="75033-164">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="75033-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_certificate.png) 

5. <span data-ttu-id="75033-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="75033-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-halogen-software-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="75033-168">W oknie innej przeglądarki, logowanie do Twojej **oprogramowania chlorowców** aplikacji jako administrator.</span><span class="sxs-lookup"><span data-stu-id="75033-168">In a different browser window, sign-on to your **Halogen Software** application as an administrator.</span></span>

7. <span data-ttu-id="75033-169">Kliknij przycisk **opcje** kartę.</span><span class="sxs-lookup"><span data-stu-id="75033-169">Click the **Options** tab.</span></span> 
   
    ![Co to jest program Azure AD Connect][12]

8. <span data-ttu-id="75033-171">W okienku nawigacji po lewej stronie kliknij **Konfiguracja SAML**.</span><span class="sxs-lookup"><span data-stu-id="75033-171">In the left navigation pane, click **SAML Configuration**.</span></span> 
   
    ![Co to jest program Azure AD Connect][13]

9. <span data-ttu-id="75033-173">Na **Konfiguracja SAML** wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="75033-173">On the **SAML Configuration** page, perform the following steps:</span></span> 

    ![Co to jest program Azure AD Connect][14]

     <span data-ttu-id="75033-175">a.</span><span class="sxs-lookup"><span data-stu-id="75033-175">a.</span></span> <span data-ttu-id="75033-176">Jako **Unikatowy identyfikator**, wybierz pozycję **NameID**.</span><span class="sxs-lookup"><span data-stu-id="75033-176">As **Unique Identifier**, select **NameID**.</span></span>

     <span data-ttu-id="75033-177">b.</span><span class="sxs-lookup"><span data-stu-id="75033-177">b.</span></span> <span data-ttu-id="75033-178">Jako **mapy Unikatowy identyfikator do**, wybierz pozycję **Username**.</span><span class="sxs-lookup"><span data-stu-id="75033-178">As **Unique Identifier Maps To**, select **Username**.</span></span>
  
     <span data-ttu-id="75033-179">c.</span><span class="sxs-lookup"><span data-stu-id="75033-179">c.</span></span> <span data-ttu-id="75033-180">Aby przekazać plik metadanych pobranych, kliknij przycisk **Przeglądaj** i wybierz plik, a następnie **Przekaż plik**.</span><span class="sxs-lookup"><span data-stu-id="75033-180">To upload your downloaded metadata file, click **Browse** to select the file, and then **Upload File**.</span></span>
 
     <span data-ttu-id="75033-181">d.</span><span class="sxs-lookup"><span data-stu-id="75033-181">d.</span></span> <span data-ttu-id="75033-182">Aby przetestować konfigurację, kliknij przycisk **Uruchom Test**.</span><span class="sxs-lookup"><span data-stu-id="75033-182">To test the configuration, click **Run Test**.</span></span> 
    
    >[!NOTE]
    ><span data-ttu-id="75033-183">Należy oczekiwać na komunikat "*zakończeniu testu SAML. Zamknij to okno*".</span><span class="sxs-lookup"><span data-stu-id="75033-183">You need to wait for the message "*The SAML test is complete. Please close this window*".</span></span> <span data-ttu-id="75033-184">Zamknięcie okna przeglądarki otwarty.</span><span class="sxs-lookup"><span data-stu-id="75033-184">Then, close the opened browser window.</span></span> <span data-ttu-id="75033-185">**Włącz SAML** pole wyboru jest włączone, tylko jeśli test została ukończona.</span><span class="sxs-lookup"><span data-stu-id="75033-185">The **Enable SAML** checkbox is only enabled if the test has been completed.</span></span> 
     
     <span data-ttu-id="75033-186">e.</span><span class="sxs-lookup"><span data-stu-id="75033-186">e.</span></span> <span data-ttu-id="75033-187">Wybierz **Włącz SAML**.</span><span class="sxs-lookup"><span data-stu-id="75033-187">Select **Enable SAML**.</span></span>
    
     <span data-ttu-id="75033-188">f.</span><span class="sxs-lookup"><span data-stu-id="75033-188">f.</span></span> <span data-ttu-id="75033-189">Kliknij przycisk **zapisać zmiany**.</span><span class="sxs-lookup"><span data-stu-id="75033-189">Click **Save Changes**.</span></span> 

> [!TIP]
> <span data-ttu-id="75033-190">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="75033-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="75033-191">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="75033-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="75033-192">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="75033-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="75033-193">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="75033-193">Creating an Azure AD test user</span></span>

<span data-ttu-id="75033-194">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="75033-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="75033-196">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="75033-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="75033-197">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="75033-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="75033-199">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="75033-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="75033-201">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="75033-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="75033-203">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="75033-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="75033-205">a.</span><span class="sxs-lookup"><span data-stu-id="75033-205">a.</span></span> <span data-ttu-id="75033-206">W **nazwa** pole tekstowe, nazwa typu jako **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="75033-206">In the **Name** textbox, type name as **BrittaSimon**.</span></span>

    <span data-ttu-id="75033-207">b.</span><span class="sxs-lookup"><span data-stu-id="75033-207">b.</span></span> <span data-ttu-id="75033-208">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="75033-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="75033-209">c.</span><span class="sxs-lookup"><span data-stu-id="75033-209">c.</span></span> <span data-ttu-id="75033-210">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="75033-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="75033-211">d.</span><span class="sxs-lookup"><span data-stu-id="75033-211">d.</span></span> <span data-ttu-id="75033-212">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="75033-212">Click **Create**.</span></span>
 
### <a name="creating-a-halogen-software-test-user"></a><span data-ttu-id="75033-213">Tworzenie użytkownika testowego chlorowców oprogramowania</span><span class="sxs-lookup"><span data-stu-id="75033-213">Creating a Halogen Software test user</span></span>

<span data-ttu-id="75033-214">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta chlorowców oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="75033-214">The objective of this section is to create a user called Britta Simon in Halogen Software.</span></span>

<span data-ttu-id="75033-215">**Aby utworzyć użytkownika o nazwie Simona Britta chlorowców oprogramowania, wykonaj następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="75033-215">**To create a user called Britta Simon in Halogen Software, perform the following steps:**</span></span>

1. <span data-ttu-id="75033-216">Zaloguj się na Twojej **oprogramowania chlorowców** aplikacji jako administrator.</span><span class="sxs-lookup"><span data-stu-id="75033-216">Sign on to your **Halogen Software** application as an administrator.</span></span>

2. <span data-ttu-id="75033-217">Kliknij przycisk **użytkownika Centrum** , a następnie kliknij pozycję **Tworzenie użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="75033-217">Click the **User Center** tab, and then click **Create User**.</span></span>
   
    ![Co to jest program Azure AD Connect][300]  

3. <span data-ttu-id="75033-219">Na **nowego użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="75033-219">On the **New User** dialog page, perform the following steps:</span></span>
   
    ![Co to jest program Azure AD Connect][301]

    <span data-ttu-id="75033-221">a.</span><span class="sxs-lookup"><span data-stu-id="75033-221">a.</span></span> <span data-ttu-id="75033-222">W **imię** tekstowym, wpisz imię użytkownika, takich jak **Britta**.</span><span class="sxs-lookup"><span data-stu-id="75033-222">In the **First Name** textbox, type first name of the user like **Britta**.</span></span>
    
    <span data-ttu-id="75033-223">b.</span><span class="sxs-lookup"><span data-stu-id="75033-223">b.</span></span> <span data-ttu-id="75033-224">W **nazwisko** tekstowym, wpisz nazwisko użytkownika, takich jak **Simona**.</span><span class="sxs-lookup"><span data-stu-id="75033-224">In the **Last Name** textbox, type last name of the user like **Simon**.</span></span> 

    <span data-ttu-id="75033-225">c.</span><span class="sxs-lookup"><span data-stu-id="75033-225">c.</span></span> <span data-ttu-id="75033-226">W **Username** pole tekstowe, typ **Simona Britta**, nazwę użytkownika w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="75033-226">In the **Username** textbox, type **Britta Simon**, the user name as in the Azure portal.</span></span>

    <span data-ttu-id="75033-227">d.</span><span class="sxs-lookup"><span data-stu-id="75033-227">d.</span></span> <span data-ttu-id="75033-228">W **hasło** tekstowym, wpisz hasło dla Britta.</span><span class="sxs-lookup"><span data-stu-id="75033-228">In the **Password** textbox, type a password for Britta.</span></span>
    
    <span data-ttu-id="75033-229">e.</span><span class="sxs-lookup"><span data-stu-id="75033-229">e.</span></span> <span data-ttu-id="75033-230">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="75033-230">Click **Save**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="75033-231">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="75033-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="75033-232">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do oprogramowania halogenowe.</span><span class="sxs-lookup"><span data-stu-id="75033-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Halogen Software.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="75033-234">**Aby przypisać Simona Britta chlorowców oprogramowania, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="75033-234">**To assign Britta Simon to Halogen Software, perform the following steps:**</span></span>

1. <span data-ttu-id="75033-235">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="75033-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="75033-237">Na liście aplikacji zaznacz **oprogramowania chlorowców**.</span><span class="sxs-lookup"><span data-stu-id="75033-237">In the applications list, select **Halogen Software**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_app.png) 

3. <span data-ttu-id="75033-239">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="75033-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="75033-241">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="75033-241">Click **Add** button.</span></span> <span data-ttu-id="75033-242">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="75033-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="75033-244">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="75033-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="75033-245">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="75033-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="75033-246">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="75033-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="75033-247">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="75033-247">Testing single sign-on</span></span>

<span data-ttu-id="75033-248">Celem tej sekcji służy do testowania konfigurację usługi Azure AD z logowania jednokrotnego za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="75033-248">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="75033-249">Po kliknięciu kafelka oprogramowania chlorowców w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji oprogramowania halogenowe.</span><span class="sxs-lookup"><span data-stu-id="75033-249">When you click the Halogen Software tile in the Access Panel, you should get automatically signed-on to your Halogen Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="75033-250">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="75033-250">Additional resources</span></span>

* [<span data-ttu-id="75033-251">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="75033-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="75033-252">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="75033-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_04.png

[12]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_12.png

[13]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_13.png

[14]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_14.png

[100]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_203.png

[300]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_300.png

[301]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_301.png
