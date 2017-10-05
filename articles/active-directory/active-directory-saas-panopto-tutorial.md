---
title: 'Samouczek: Integracji Azure Active Directory z Panopto | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Panopto."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 89c88e23-93ce-4970-9baa-1104c4e8fe4a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 725fba1227cfc9c4850f9e2d6fd0b13e88eafa20
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-panopto"></a><span data-ttu-id="03e7e-103">Samouczek: Integracji Azure Active Directory z Panopto</span><span class="sxs-lookup"><span data-stu-id="03e7e-103">Tutorial: Azure Active Directory integration with Panopto</span></span>

<span data-ttu-id="03e7e-104">Z tego samouczka dowiesz się integrowanie Panopto z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="03e7e-104">In this tutorial, you learn how to integrate Panopto with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="03e7e-105">Integracja z usługą Azure AD Panopto zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="03e7e-105">Integrating Panopto with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="03e7e-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Panopto</span><span class="sxs-lookup"><span data-stu-id="03e7e-106">You can control in Azure AD who has access to Panopto</span></span>
- <span data-ttu-id="03e7e-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Panopto (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="03e7e-107">You can enable your users to automatically get signed-on to Panopto (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="03e7e-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="03e7e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="03e7e-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="03e7e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="03e7e-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="03e7e-110">Prerequisites</span></span>

<span data-ttu-id="03e7e-111">Aby skonfigurować integrację usługi Azure AD z Panopto, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="03e7e-111">To configure Azure AD integration with Panopto, you need the following items:</span></span>

- <span data-ttu-id="03e7e-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="03e7e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="03e7e-113">Panopto logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="03e7e-113">A Panopto single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="03e7e-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="03e7e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="03e7e-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="03e7e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="03e7e-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="03e7e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="03e7e-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="03e7e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="03e7e-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="03e7e-118">Scenario description</span></span>
<span data-ttu-id="03e7e-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="03e7e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="03e7e-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="03e7e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="03e7e-121">Dodawanie Panopto z galerii</span><span class="sxs-lookup"><span data-stu-id="03e7e-121">Adding Panopto from the gallery</span></span>
2. <span data-ttu-id="03e7e-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="03e7e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-panopto-from-the-gallery"></a><span data-ttu-id="03e7e-123">Dodawanie Panopto z galerii</span><span class="sxs-lookup"><span data-stu-id="03e7e-123">Adding Panopto from the gallery</span></span>
<span data-ttu-id="03e7e-124">Aby skonfigurować integrację usługi Azure AD Panopto, należy dodać Panopto z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="03e7e-124">To configure the integration of Panopto into Azure AD, you need to add Panopto from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="03e7e-125">**Aby dodać Panopto z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="03e7e-125">**To add Panopto from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="03e7e-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="03e7e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="03e7e-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="03e7e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="03e7e-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="03e7e-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="03e7e-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="03e7e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="03e7e-133">W polu wyszukiwania wpisz **Panopto**.</span><span class="sxs-lookup"><span data-stu-id="03e7e-133">In the search box, type **Panopto**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_search.png)

5. <span data-ttu-id="03e7e-135">W panelu wyników wybierz **Panopto**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="03e7e-135">In the results panel, select **Panopto**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="03e7e-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="03e7e-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="03e7e-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Panopto na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="03e7e-138">In this section, you configure and test Azure AD single sign-on with Panopto based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="03e7e-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Panopto jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="03e7e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Panopto is to a user in Azure AD.</span></span> <span data-ttu-id="03e7e-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Panopto musi się.</span><span class="sxs-lookup"><span data-stu-id="03e7e-140">In other words, a link relationship between an Azure AD user and the related user in Panopto needs to be established.</span></span>

<span data-ttu-id="03e7e-141">W Panopto, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="03e7e-141">In Panopto, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="03e7e-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Panopto, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="03e7e-142">To configure and test Azure AD single sign-on with Panopto, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="03e7e-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="03e7e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="03e7e-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="03e7e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="03e7e-145">**[Tworzenie użytkownika testowego Panopto](#creating-a-panopto-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Panopto połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="03e7e-145">**[Creating a Panopto test user](#creating-a-panopto-test-user)** - to have a counterpart of Britta Simon in Panopto that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="03e7e-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="03e7e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="03e7e-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="03e7e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="03e7e-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="03e7e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="03e7e-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Panopto.</span><span class="sxs-lookup"><span data-stu-id="03e7e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Panopto application.</span></span>

<span data-ttu-id="03e7e-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Panopto, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="03e7e-150">**To configure Azure AD single sign-on with Panopto, perform the following steps:**</span></span>

1. <span data-ttu-id="03e7e-151">W portalu Azure na **Panopto** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="03e7e-151">In the Azure portal, on the **Panopto** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="03e7e-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="03e7e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_samlbase.png)

3. <span data-ttu-id="03e7e-155">Na **Panopto domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="03e7e-155">On the **Panopto Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_url.png)

    <span data-ttu-id="03e7e-157">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<tenant-name>.panopto.com`</span><span class="sxs-lookup"><span data-stu-id="03e7e-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.panopto.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="03e7e-158">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="03e7e-158">This value is not real.</span></span> <span data-ttu-id="03e7e-159">Zaktualizuj tę wartość przy rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="03e7e-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="03e7e-160">Skontaktuj się z [zespołem pomocy technicznej klienta Panopto](mailto:support@panopto.com‎) aby zyskać tę wartość.</span><span class="sxs-lookup"><span data-stu-id="03e7e-160">Contact [Panopto Client support team](mailto:support@panopto.com‎) to get this value.</span></span> 
 
4. <span data-ttu-id="03e7e-161">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="03e7e-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_certificate.png) 

5. <span data-ttu-id="03e7e-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="03e7e-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-panopto-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="03e7e-165">Na **konfiguracji Panopto** , kliknij przycisk **skonfigurować Panopto** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="03e7e-165">On the **Panopto Configuration** section, click **Configure Panopto** to open **Configure sign-on** window.</span></span> <span data-ttu-id="03e7e-166">Kopiuj **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="03e7e-166">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_configure.png) 

7. <span data-ttu-id="03e7e-168">W oknie przeglądarki innej witryny sieci web należy zalogować się jako administrator do witryny firmy Panopto.</span><span class="sxs-lookup"><span data-stu-id="03e7e-168">In a different web browser window, log in to your Panopto company site as an administrator.</span></span>

8. <span data-ttu-id="03e7e-169">Na pasku narzędzi po lewej stronie kliknij **systemu**, a następnie kliknij przycisk **dostawców tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="03e7e-169">In the toolbar on the left, click **System**, and then click **Identity Providers**.</span></span>
   
   <span data-ttu-id="03e7e-170">![System](./media/active-directory-saas-panopto-tutorial/ic777670.png "systemu")</span><span class="sxs-lookup"><span data-stu-id="03e7e-170">![System](./media/active-directory-saas-panopto-tutorial/ic777670.png "System")</span></span>
9. <span data-ttu-id="03e7e-171">Kliknij przycisk **dodać dostawcę**.</span><span class="sxs-lookup"><span data-stu-id="03e7e-171">Click **Add Provider**.</span></span>
   
   <span data-ttu-id="03e7e-172">![Dostawców tożsamości](./media/active-directory-saas-panopto-tutorial/ic777671.png "dostawców tożsamości")</span><span class="sxs-lookup"><span data-stu-id="03e7e-172">![Identity Providers](./media/active-directory-saas-panopto-tutorial/ic777671.png "Identity Providers")</span></span>
   
10. <span data-ttu-id="03e7e-173">W sekcji dostawcy SAML wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="03e7e-173">In the SAML provider section, perform the following steps:</span></span>
   
    <span data-ttu-id="03e7e-174">![Konfiguracja SaaS](./media/active-directory-saas-panopto-tutorial/ic777672.png "SaaS konfiguracji")</span><span class="sxs-lookup"><span data-stu-id="03e7e-174">![SaaS configuration](./media/active-directory-saas-panopto-tutorial/ic777672.png "SaaS configuration")</span></span>
    
    <span data-ttu-id="03e7e-175">a.</span><span class="sxs-lookup"><span data-stu-id="03e7e-175">a.</span></span> <span data-ttu-id="03e7e-176">Z **typ dostawcy** listy, wybierz **SAML20**.</span><span class="sxs-lookup"><span data-stu-id="03e7e-176">From the **Provider Type** list, select **SAML20**.</span></span>    
    
    <span data-ttu-id="03e7e-177">b.</span><span class="sxs-lookup"><span data-stu-id="03e7e-177">b.</span></span> <span data-ttu-id="03e7e-178">W **nazwa wystąpienia** tekstowym, wpisz nazwę wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="03e7e-178">In the **Instance Name** textbox, type a name for the instance.</span></span>

    <span data-ttu-id="03e7e-179">c.</span><span class="sxs-lookup"><span data-stu-id="03e7e-179">c.</span></span> <span data-ttu-id="03e7e-180">W **przyjazny opis** tekstowym, wpisz przyjazny opis.</span><span class="sxs-lookup"><span data-stu-id="03e7e-180">In the **Friendly Description** textbox, type a friendly description.</span></span>
    
    <span data-ttu-id="03e7e-181">d.</span><span class="sxs-lookup"><span data-stu-id="03e7e-181">d.</span></span> <span data-ttu-id="03e7e-182">W **Odbijanie adres Url strony** pole tekstowe, Wklej wartość **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="03e7e-182">In **Bounce Page Url** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="03e7e-183">e.</span><span class="sxs-lookup"><span data-stu-id="03e7e-183">e.</span></span> <span data-ttu-id="03e7e-184">W **wystawcy** pole tekstowe, Wklej wartość **identyfikator jednostki SAML**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="03e7e-184">In the **Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="03e7e-185">f.</span><span class="sxs-lookup"><span data-stu-id="03e7e-185">f.</span></span> <span data-ttu-id="03e7e-186">Otwórz base-64 zakodowanego certyfikatu, który został już pobrany z portalu Azure, skopiuj zawartość go do Schowka, a następnie wklej go do **klucz publiczny** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="03e7e-186">Open your base-64 encoded certificate, which you have downloaded from Azure portal, copy the content of it in to your clipboard, and then paste it to the **Public Key**  textbox.</span></span>

11. <span data-ttu-id="03e7e-187">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="03e7e-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="03e7e-188">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="03e7e-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="03e7e-189">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="03e7e-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="03e7e-190">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="03e7e-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="03e7e-191">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="03e7e-191">Creating an Azure AD test user</span></span>

<span data-ttu-id="03e7e-192">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="03e7e-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="03e7e-194">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="03e7e-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="03e7e-195">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="03e7e-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-panopto-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="03e7e-197">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="03e7e-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-panopto-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="03e7e-199">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="03e7e-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-panopto-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="03e7e-201">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="03e7e-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-panopto-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="03e7e-203">a.</span><span class="sxs-lookup"><span data-stu-id="03e7e-203">a.</span></span> <span data-ttu-id="03e7e-204">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="03e7e-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="03e7e-205">b.</span><span class="sxs-lookup"><span data-stu-id="03e7e-205">b.</span></span> <span data-ttu-id="03e7e-206">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="03e7e-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="03e7e-207">c.</span><span class="sxs-lookup"><span data-stu-id="03e7e-207">c.</span></span> <span data-ttu-id="03e7e-208">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="03e7e-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="03e7e-209">d.</span><span class="sxs-lookup"><span data-stu-id="03e7e-209">d.</span></span> <span data-ttu-id="03e7e-210">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="03e7e-210">Click **Create**.</span></span>
 
### <a name="creating-a-panopto-test-user"></a><span data-ttu-id="03e7e-211">Tworzenie użytkownika testowego Panopto</span><span class="sxs-lookup"><span data-stu-id="03e7e-211">Creating a Panopto test user</span></span>

<span data-ttu-id="03e7e-212">Nie ma elementu akcji do skonfigurowania inicjowania obsługi administracyjnej Panopto użytkownika.</span><span class="sxs-lookup"><span data-stu-id="03e7e-212">There is no action item for you to configure user provisioning to Panopto.</span></span>  
<span data-ttu-id="03e7e-213">Gdy przypisany użytkownik próbuje zalogować się do Panopto za pomocą panelu dostępu, Panopto sprawdza, czy użytkownik istnieje.</span><span class="sxs-lookup"><span data-stu-id="03e7e-213">When an assigned user tries to log in to Panopto using the access panel, Panopto checks whether the user exists.</span></span>  

<span data-ttu-id="03e7e-214">Jeśli nie jest Brak konta użytkownika dostępny jeszcze, są tworzone przez Panopto.</span><span class="sxs-lookup"><span data-stu-id="03e7e-214">If there is no user account available yet, it is automatically created by Panopto.</span></span>

>[!NOTE]
><span data-ttu-id="03e7e-215">Możesz użyć innych Panopto użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Panopto do udostępnienia konta użytkownika usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="03e7e-215">You can use any other Panopto user account creation tools or APIs provided by Panopto to provision Azure AD user accounts.</span></span>
>
>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="03e7e-216">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="03e7e-216">Assigning the Azure AD test user</span></span>

<span data-ttu-id="03e7e-217">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Panopto.</span><span class="sxs-lookup"><span data-stu-id="03e7e-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Panopto.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="03e7e-219">**Aby przypisać Simona Britta Panopto, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="03e7e-219">**To assign Britta Simon to Panopto, perform the following steps:**</span></span>

1. <span data-ttu-id="03e7e-220">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="03e7e-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="03e7e-222">Na liście aplikacji zaznacz **Panopto**.</span><span class="sxs-lookup"><span data-stu-id="03e7e-222">In the applications list, select **Panopto**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_app.png) 

3. <span data-ttu-id="03e7e-224">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="03e7e-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="03e7e-226">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="03e7e-226">Click **Add** button.</span></span> <span data-ttu-id="03e7e-227">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="03e7e-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="03e7e-229">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="03e7e-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="03e7e-230">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="03e7e-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="03e7e-231">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="03e7e-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="03e7e-232">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="03e7e-232">Testing single sign-on</span></span>

<span data-ttu-id="03e7e-233">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="03e7e-233">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="03e7e-234">Po kliknięciu kafelka Panopto w panelu dostępu, należy uzyskać automatycznie strony logowania Panopto aplikacji.</span><span class="sxs-lookup"><span data-stu-id="03e7e-234">When you click the Panopto tile in the Access Panel, you should get automatically login page of Panopto application.</span></span>
<span data-ttu-id="03e7e-235">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="03e7e-235">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="03e7e-236">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="03e7e-236">Additional resources</span></span>

* [<span data-ttu-id="03e7e-237">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="03e7e-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="03e7e-238">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="03e7e-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_203.png

