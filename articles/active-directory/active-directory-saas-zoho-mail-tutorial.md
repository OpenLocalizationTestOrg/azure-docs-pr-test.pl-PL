---
title: 'Samouczek: Integracji Azure Active Directory z Zoho | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Zoho."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 9874e1f3-ade5-42e7-a700-e08b3731236a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jeedes
ms.openlocfilehash: f0688cb75584ada805b944d2ef5409d66ab37339
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zoho"></a><span data-ttu-id="29f81-103">Samouczek: Integracji Azure Active Directory z Zoho</span><span class="sxs-lookup"><span data-stu-id="29f81-103">Tutorial: Azure Active Directory integration with Zoho</span></span>

<span data-ttu-id="29f81-104">Z tego samouczka dowiesz się integrowanie Zoho z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="29f81-104">In this tutorial, you learn how to integrate Zoho with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="29f81-105">Integracja z usługą Azure AD Zoho zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="29f81-105">Integrating Zoho with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="29f81-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Zoho.</span><span class="sxs-lookup"><span data-stu-id="29f81-106">You can control in Azure AD who has access to Zoho.</span></span>
- <span data-ttu-id="29f81-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Zoho (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29f81-107">You can enable your users to automatically get signed-on to Zoho (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="29f81-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="29f81-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="29f81-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="29f81-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="29f81-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="29f81-110">Prerequisites</span></span>

<span data-ttu-id="29f81-111">Aby skonfigurować integrację usługi Azure AD z Zoho, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="29f81-111">To configure Azure AD integration with Zoho, you need the following items:</span></span>

- <span data-ttu-id="29f81-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="29f81-112">An Azure AD subscription</span></span>
- <span data-ttu-id="29f81-113">Zoho logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="29f81-113">A Zoho single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="29f81-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="29f81-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="29f81-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="29f81-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="29f81-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="29f81-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="29f81-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="29f81-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="29f81-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="29f81-118">Scenario description</span></span>
<span data-ttu-id="29f81-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="29f81-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="29f81-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="29f81-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="29f81-121">Dodawanie Zoho z galerii</span><span class="sxs-lookup"><span data-stu-id="29f81-121">Adding Zoho from the gallery</span></span>
2. <span data-ttu-id="29f81-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="29f81-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zoho-from-the-gallery"></a><span data-ttu-id="29f81-123">Dodawanie Zoho z galerii</span><span class="sxs-lookup"><span data-stu-id="29f81-123">Adding Zoho from the gallery</span></span>
<span data-ttu-id="29f81-124">Aby skonfigurować integrację usługi Azure AD Zoho, należy dodać Zoho z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="29f81-124">To configure the integration of Zoho into Azure AD, you need to add Zoho from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="29f81-125">**Aby dodać Zoho z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="29f81-125">**To add Zoho from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="29f81-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="29f81-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Przycisk usługi Azure Active Directory][1]

2. <span data-ttu-id="29f81-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="29f81-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="29f81-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="29f81-129">Then go to **All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa][2]
    
3. <span data-ttu-id="29f81-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="29f81-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Nowy przycisk aplikacji][3]

4. <span data-ttu-id="29f81-133">W polu wyszukiwania wpisz **Zoho**, wybierz pozycję **Zoho** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="29f81-133">In the search box, type **Zoho**, select **Zoho** from result panel then click **Add** button to add the application.</span></span>

    ![Zoho na liście wyników](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="29f81-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="29f81-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="29f81-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Zoho w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="29f81-136">In this section, you configure and test Azure AD single sign-on with Zoho based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="29f81-137">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Zoho jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29f81-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Zoho is to a user in Azure AD.</span></span> <span data-ttu-id="29f81-138">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Zoho musi się.</span><span class="sxs-lookup"><span data-stu-id="29f81-138">In other words, a link relationship between an Azure AD user and the related user in Zoho needs to be established.</span></span>

<span data-ttu-id="29f81-139">W Zoho, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="29f81-139">In Zoho, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="29f81-140">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Zoho, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="29f81-140">To configure and test Azure AD single sign-on with Zoho, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="29f81-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="29f81-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="29f81-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="29f81-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="29f81-143">**[Tworzenie użytkownika testowego Zoho](#create-a-zoho-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Zoho połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="29f81-143">**[Create a Zoho test user](#create-a-zoho-test-user)** - to have a counterpart of Britta Simon in Zoho that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="29f81-144">**[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="29f81-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="29f81-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="29f81-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="29f81-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="29f81-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="29f81-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Zoho.</span><span class="sxs-lookup"><span data-stu-id="29f81-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zoho application.</span></span>

<span data-ttu-id="29f81-148">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Zoho, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="29f81-148">**To configure Azure AD single sign-on with Zoho, perform the following steps:**</span></span>

1. <span data-ttu-id="29f81-149">W portalu Azure na **Zoho** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="29f81-149">In the Azure portal, on the **Zoho** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="29f81-151">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="29f81-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_samlbase.png)

3. <span data-ttu-id="29f81-153">Na **Zoho domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="29f81-153">On the **Zoho Domain and URLs** section, perform the following steps:</span></span>

    ![Adresy URL i domeny Zoho pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_url.png)

    <span data-ttu-id="29f81-155">a.</span><span class="sxs-lookup"><span data-stu-id="29f81-155">a.</span></span> <span data-ttu-id="29f81-156">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<company name>.zohomail.com`</span><span class="sxs-lookup"><span data-stu-id="29f81-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.zohomail.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="29f81-157">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="29f81-157">This value is not real.</span></span> <span data-ttu-id="29f81-158">Zaktualizuj tę wartość przy rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="29f81-158">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="29f81-159">Skontaktuj się z [zespołem pomocy technicznej klienta Zoho](https://www.zoho.com/mail/contact.html) aby zyskać tę wartość.</span><span class="sxs-lookup"><span data-stu-id="29f81-159">Contact [Zoho Client support team](https://www.zoho.com/mail/contact.html) to get this value.</span></span> 
 
4. <span data-ttu-id="29f81-160">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="29f81-160">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Łącze pobierania certyfikatu](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_certificate.png) 

5. <span data-ttu-id="29f81-162">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="29f81-162">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="29f81-164">Na **konfiguracji Zoho** , kliknij przycisk **skonfigurować Zoho** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="29f81-164">On the **Zoho Configuration** section, click **Configure Zoho** to open **Configure sign-on** window.</span></span> <span data-ttu-id="29f81-165">Kopiuj **Sign-Out adres URL, Zmień adres URL hasła i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="29f81-165">Copy the **Sign-Out URL, Change Password URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfiguracja Zoho](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_configure.png) 

7. <span data-ttu-id="29f81-167">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy poczty Zoho jako administrator.</span><span class="sxs-lookup"><span data-stu-id="29f81-167">In a different web browser window, log into your Zoho Mail company site as an administrator.</span></span>

8. <span data-ttu-id="29f81-168">Przejdź do **Panelu sterowania**.</span><span class="sxs-lookup"><span data-stu-id="29f81-168">Go to the **Control panel**.</span></span>
   
    <span data-ttu-id="29f81-169">![Panel sterowania](./media/active-directory-saas-zoho-mail-tutorial/ic789607.png "Panel sterowania")</span><span class="sxs-lookup"><span data-stu-id="29f81-169">![Control Panel](./media/active-directory-saas-zoho-mail-tutorial/ic789607.png "Control Panel")</span></span>

9. <span data-ttu-id="29f81-170">Kliknij przycisk **uwierzytelnianie SAML** kartę.</span><span class="sxs-lookup"><span data-stu-id="29f81-170">Click the **SAML Authentication** tab.</span></span>
   
    <span data-ttu-id="29f81-171">![Uwierzytelnianie SAML](./media/active-directory-saas-zoho-mail-tutorial/ic789608.png "uwierzytelnianie SAML")</span><span class="sxs-lookup"><span data-stu-id="29f81-171">![SAML Authentication](./media/active-directory-saas-zoho-mail-tutorial/ic789608.png "SAML Authentication")</span></span>

10. <span data-ttu-id="29f81-172">W **Szczegóły okna uwierzytelnianie SAML** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="29f81-172">In the **SAML Authentication Details** section, perform the following steps:</span></span>
   
    <span data-ttu-id="29f81-173">![Szczegóły okna uwierzytelnianie SAML](./media/active-directory-saas-zoho-mail-tutorial/ic789609.png "Szczegóły okna uwierzytelnianie SAML")</span><span class="sxs-lookup"><span data-stu-id="29f81-173">![SAML Authentication Details](./media/active-directory-saas-zoho-mail-tutorial/ic789609.png "SAML Authentication Details")</span></span>
   
    <span data-ttu-id="29f81-174">a.</span><span class="sxs-lookup"><span data-stu-id="29f81-174">a.</span></span> <span data-ttu-id="29f81-175">W **adres URL logowania** pole tekstowe, Wklej **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="29f81-175">In the **Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="29f81-176">b.</span><span class="sxs-lookup"><span data-stu-id="29f81-176">b.</span></span> <span data-ttu-id="29f81-177">W **adresu URL wylogowania** pole tekstowe, Wklej **Sign-Out URL** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="29f81-177">In the **Logout URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="29f81-178">c.</span><span class="sxs-lookup"><span data-stu-id="29f81-178">c.</span></span> <span data-ttu-id="29f81-179">W **Zmień adres URL hasła** pole tekstowe, Wklej **Zmień adres URL hasła** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="29f81-179">In the **Change Password URL** textbox, paste **Change Password URL** which you have copied from Azure portal.</span></span>
       
    <span data-ttu-id="29f81-180">d.</span><span class="sxs-lookup"><span data-stu-id="29f81-180">d.</span></span> <span data-ttu-id="29f81-181">Otwórz base-64 zakodowany certyfikat pobrany z portalu Azure w programie Notatnik, skopiuj zawartość go do Schowka, a następnie wklej go do **PublicKey** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="29f81-181">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **PublicKey** textbox.</span></span>
   
    <span data-ttu-id="29f81-182">e.</span><span class="sxs-lookup"><span data-stu-id="29f81-182">e.</span></span> <span data-ttu-id="29f81-183">Jako **algorytm**, wybierz pozycję **RSA**.</span><span class="sxs-lookup"><span data-stu-id="29f81-183">As **Algorithm**, select **RSA**.</span></span>
   
    <span data-ttu-id="29f81-184">f.</span><span class="sxs-lookup"><span data-stu-id="29f81-184">f.</span></span> <span data-ttu-id="29f81-185">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="29f81-185">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="29f81-186">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="29f81-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="29f81-187">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="29f81-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="29f81-188">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="29f81-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="29f81-189">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="29f81-189">Create an Azure AD test user</span></span>

<span data-ttu-id="29f81-190">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="29f81-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="29f81-192">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="29f81-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="29f81-193">W portalu Azure, w okienku po lewej stronie kliknij **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="29f81-193">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Przycisk usługi Azure Active Directory](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="29f81-195">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="29f81-195">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="29f81-197">Aby otworzyć **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** w górnej części **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="29f81-197">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Przycisk Dodaj](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="29f81-199">W **użytkownika** okna dialogowego wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="29f81-199">In the **User** dialog box, perform the following steps:</span></span>

    ![Okno dialogowe użytkownika](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_04.png)

    <span data-ttu-id="29f81-201">a.</span><span class="sxs-lookup"><span data-stu-id="29f81-201">a.</span></span> <span data-ttu-id="29f81-202">W **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="29f81-202">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="29f81-203">b.</span><span class="sxs-lookup"><span data-stu-id="29f81-203">b.</span></span> <span data-ttu-id="29f81-204">W **nazwy użytkownika** wpisz adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="29f81-204">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="29f81-205">c.</span><span class="sxs-lookup"><span data-stu-id="29f81-205">c.</span></span> <span data-ttu-id="29f81-206">Wybierz **Pokaż hasło** pole wyboru, a następnie zanotuj wartość, która jest wyświetlana w **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="29f81-206">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="29f81-207">d.</span><span class="sxs-lookup"><span data-stu-id="29f81-207">d.</span></span> <span data-ttu-id="29f81-208">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="29f81-208">Click **Create**.</span></span>
 
### <a name="create-a-zoho-test-user"></a><span data-ttu-id="29f81-209">Tworzenie użytkownika testowego Zoho</span><span class="sxs-lookup"><span data-stu-id="29f81-209">Create a Zoho test user</span></span>

<span data-ttu-id="29f81-210">Aby włączyć użytkowników usługi Azure AD zalogować się do Zoho poczty, muszą mieć przydzielone do Zoho poczty.</span><span class="sxs-lookup"><span data-stu-id="29f81-210">In order to enable Azure AD users to log into Zoho Mail, they must be provisioned into Zoho Mail.</span></span> <span data-ttu-id="29f81-211">W przypadku poczty Zoho Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="29f81-211">In the case of Zoho Mail, provisioning is a manual task.</span></span>

> [!NOTE]
> <span data-ttu-id="29f81-212">Możesz użyć innych Zoho poczty użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Zoho poczty do kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="29f81-212">You can use any other Zoho Mail user account creation tools or APIs provided by Zoho Mail to provision AAD user accounts.</span></span>

### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="29f81-213">Aby udostępnić konta użytkownika, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="29f81-213">To provision a user account, perform the following steps:</span></span>

1. <span data-ttu-id="29f81-214">Zaloguj się do Twojego **poczty Zoho** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="29f81-214">Log in to your **Zoho Mail** company site as an administrator.</span></span>

2. <span data-ttu-id="29f81-215">Przejdź do **Panel sterowania \> poczty & Docs**.</span><span class="sxs-lookup"><span data-stu-id="29f81-215">Go to **Control Panel \> Mail & Docs**.</span></span>

3. <span data-ttu-id="29f81-216">Przejdź do **szczegóły użytkownika \> dodać użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="29f81-216">Go to **User Details \> Add User**.</span></span>
   
    <span data-ttu-id="29f81-217">![Dodaj użytkownika](./media/active-directory-saas-zoho-mail-tutorial/ic789611.png "Dodaj użytkownika")</span><span class="sxs-lookup"><span data-stu-id="29f81-217">![Add User](./media/active-directory-saas-zoho-mail-tutorial/ic789611.png "Add User")</span></span>

4. <span data-ttu-id="29f81-218">Na **dodawania użytkowników** okna dialogowego, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="29f81-218">On the **Add users** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="29f81-219">![Dodaj użytkownika](./media/active-directory-saas-zoho-mail-tutorial/ic789612.png "Dodaj użytkownika")</span><span class="sxs-lookup"><span data-stu-id="29f81-219">![Add User](./media/active-directory-saas-zoho-mail-tutorial/ic789612.png "Add User")</span></span>
   
    <span data-ttu-id="29f81-220">a.</span><span class="sxs-lookup"><span data-stu-id="29f81-220">a.</span></span> <span data-ttu-id="29f81-221">W **imię** tekstowym, wpisz imię użytkownika, takich jak **Britta**.</span><span class="sxs-lookup"><span data-stu-id="29f81-221">In the **First Name** textbox, type the first name of user like **Britta**.</span></span>

    <span data-ttu-id="29f81-222">b.</span><span class="sxs-lookup"><span data-stu-id="29f81-222">b.</span></span> <span data-ttu-id="29f81-223">W **nazwisko** tekstowym, wpisz nazwisko użytkownika, takich jak **Simona**.</span><span class="sxs-lookup"><span data-stu-id="29f81-223">In the **Last Name** textbox, type the last name of user like **Simon**.</span></span>

    <span data-ttu-id="29f81-224">c.</span><span class="sxs-lookup"><span data-stu-id="29f81-224">c.</span></span> <span data-ttu-id="29f81-225">W **identyfikator wiadomości E-mail** pole tekstowe, typ identyfikatora e-mail użytkownika, takich jak  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="29f81-225">In the **Email ID** textbox, type the email id of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="29f81-226">d.</span><span class="sxs-lookup"><span data-stu-id="29f81-226">d.</span></span> <span data-ttu-id="29f81-227">W **hasło** pole tekstowe, wprowadź hasło użytkownika.</span><span class="sxs-lookup"><span data-stu-id="29f81-227">In the **Password** textbox, enter password of user.</span></span>
   
    <span data-ttu-id="29f81-228">e.</span><span class="sxs-lookup"><span data-stu-id="29f81-228">e.</span></span> <span data-ttu-id="29f81-229">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="29f81-229">Click **OK**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="29f81-230">Właściciel konta usługi Azure Active Directory zostanie wysłana wiadomość e-mail z łączem do potwierdzenia konta, zanim staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="29f81-230">The Azure Active Directory account holder will receive an email with a link to confirm the account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="29f81-231">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="29f81-231">Assign the Azure AD test user</span></span>

<span data-ttu-id="29f81-232">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Zoho.</span><span class="sxs-lookup"><span data-stu-id="29f81-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zoho.</span></span>

![Przypisanie roli użytkownika][200] 

<span data-ttu-id="29f81-234">**Aby przypisać Simona Britta Zoho, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="29f81-234">**To assign Britta Simon to Zoho, perform the following steps:**</span></span>

1. <span data-ttu-id="29f81-235">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="29f81-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="29f81-237">Na liście aplikacji zaznacz **Zoho**.</span><span class="sxs-lookup"><span data-stu-id="29f81-237">In the applications list, select **Zoho**.</span></span>

    ![Łącze Zoho na liście aplikacji](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_app.png)  

3. <span data-ttu-id="29f81-239">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="29f81-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Łącze "Użytkownicy i grupy"][202]

4. <span data-ttu-id="29f81-241">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="29f81-241">Click **Add** button.</span></span> <span data-ttu-id="29f81-242">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="29f81-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![W okienku Dodaj przydziału][203]

5. <span data-ttu-id="29f81-244">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="29f81-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="29f81-245">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="29f81-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="29f81-246">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="29f81-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="29f81-247">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="29f81-247">Test single sign-on</span></span>

<span data-ttu-id="29f81-248">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="29f81-248">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="29f81-249">Po kliknięciu kafelka Zoho w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Zoho.</span><span class="sxs-lookup"><span data-stu-id="29f81-249">When you click the Zoho tile in the Access Panel, you should get automatically signed-on to your Zoho application.</span></span>
<span data-ttu-id="29f81-250">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="29f81-250">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="29f81-251">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="29f81-251">Additional resources</span></span>

* [<span data-ttu-id="29f81-252">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="29f81-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="29f81-253">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="29f81-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_203.png

