---
title: 'Samouczek: Integracji Azure Active Directory z Citrix ShareFile | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Citrix ShareFile."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: e14fc310-bac4-4f09-99ef-87e5c77288b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2017
ms.author: jeedes
ms.openlocfilehash: b85680104fe4f33638c559b2a12483a2312a4476
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-sharefile"></a><span data-ttu-id="f765e-103">Samouczek: Integracji Azure Active Directory z Citrix ShareFile</span><span class="sxs-lookup"><span data-stu-id="f765e-103">Tutorial: Azure Active Directory integration with Citrix ShareFile</span></span>

<span data-ttu-id="f765e-104">Z tego samouczka dowiesz się sposobu integracji z usługą Azure Active Directory (Azure AD) Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="f765e-104">In this tutorial, you learn how to integrate Citrix ShareFile with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f765e-105">Integracja z usługą Azure AD Citrix ShareFile zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="f765e-105">Integrating Citrix ShareFile with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f765e-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="f765e-106">You can control in Azure AD who has access to Citrix ShareFile.</span></span>
- <span data-ttu-id="f765e-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Citrix ShareFile (logowanie jednokrotne) z konta usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f765e-107">You can enable your users to automatically get signed-on to Citrix ShareFile (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="f765e-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f765e-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="f765e-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f765e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f765e-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f765e-110">Prerequisites</span></span>

<span data-ttu-id="f765e-111">Aby skonfigurować integrację usługi Azure AD z Citrix ShareFile, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="f765e-111">To configure Azure AD integration with Citrix ShareFile, you need the following items:</span></span>

- <span data-ttu-id="f765e-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f765e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f765e-113">Citrix ShareFile logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="f765e-113">A Citrix ShareFile single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f765e-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="f765e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f765e-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="f765e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f765e-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="f765e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f765e-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f765e-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f765e-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="f765e-118">Scenario description</span></span>
<span data-ttu-id="f765e-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="f765e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f765e-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="f765e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f765e-121">Dodaj Citrix ShareFile z galerii</span><span class="sxs-lookup"><span data-stu-id="f765e-121">Add Citrix ShareFile from the gallery</span></span>
2. <span data-ttu-id="f765e-122">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="f765e-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-citrix-sharefile-from-the-gallery"></a><span data-ttu-id="f765e-123">Dodaj Citrix ShareFile z galerii</span><span class="sxs-lookup"><span data-stu-id="f765e-123">Add Citrix ShareFile from the gallery</span></span>
<span data-ttu-id="f765e-124">Aby skonfigurować integrację usługi Azure AD Citrix ShareFile, należy dodać Citrix ShareFile z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="f765e-124">To configure the integration of Citrix ShareFile into Azure AD, you need to add Citrix ShareFile from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f765e-125">**Aby dodać Citrix ShareFile z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f765e-125">**To add Citrix ShareFile from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f765e-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="f765e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Przycisk usługi Azure Active Directory][1]

2. <span data-ttu-id="f765e-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="f765e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f765e-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="f765e-129">Then go to **All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa][2]
    
3. <span data-ttu-id="f765e-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f765e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Nowy przycisk aplikacji][3]

4. <span data-ttu-id="f765e-133">W polu wyszukiwania wpisz **Citrix ShareFile**, wybierz pozycję **Citrix ShareFile** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="f765e-133">In the search box, type **Citrix ShareFile**, select **Citrix ShareFile** from result panel then click **Add** button to add the application.</span></span>

    ![Citrix ShareFile na liście wyników](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="f765e-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="f765e-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="f765e-136">W tej sekcji możesz skonfigurować i test usługi Azure AD rejestracji jednokrotnej z Citrix ShareFile w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="f765e-136">In this section, you configure and test Azure AD single sign-on with Citrix ShareFile based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f765e-137">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Citrix ShareFile jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f765e-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Citrix ShareFile is to a user in Azure AD.</span></span> <span data-ttu-id="f765e-138">Innymi słowy musi można ustanowić łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="f765e-138">In other words, a link relationship between an Azure AD user and the related user in Citrix ShareFile needs to be established.</span></span>

<span data-ttu-id="f765e-139">W Citrix ShareFile, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="f765e-139">In Citrix ShareFile, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f765e-140">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Citrix ShareFile, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="f765e-140">To configure and test Azure AD single sign-on with Citrix ShareFile, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f765e-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="f765e-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f765e-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="f765e-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f765e-143">**[Tworzenie użytkownika testowego Citrix ShareFile](#create-a-citrix-sharefile-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Citrix ShareFile, połączonej z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f765e-143">**[Create a Citrix ShareFile test user](#create-a-citrix-sharefile-test-user)** - to have a counterpart of Britta Simon in Citrix ShareFile that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f765e-144">**[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="f765e-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f765e-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="f765e-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="f765e-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="f765e-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="f765e-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="f765e-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Citrix ShareFile application.</span></span>

<span data-ttu-id="f765e-148">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Citrix ShareFile, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f765e-148">**To configure Azure AD single sign-on with Citrix ShareFile, perform the following steps:**</span></span>

1. <span data-ttu-id="f765e-149">W portalu Azure na **Citrix ShareFile** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="f765e-149">In the Azure portal, on the **Citrix ShareFile** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="f765e-151">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="f765e-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_samlbase.png)

3. <span data-ttu-id="f765e-153">Na **Citrix ShareFile domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="f765e-153">On the **Citrix ShareFile Domain and URLs** section, perform the following steps:</span></span>

    ![Adresy URL i domeny ShareFile Citrix pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_url.png)
    
    <span data-ttu-id="f765e-155">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<tenant-name>.sharefile.com/saml/login`</span><span class="sxs-lookup"><span data-stu-id="f765e-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.sharefile.com/saml/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f765e-156">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="f765e-156">This value is not real.</span></span> <span data-ttu-id="f765e-157">Zaktualizuj tę wartość przy rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="f765e-157">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="f765e-158">Skontaktuj się z [zespołem pomocy technicznej klienta ShareFile Citrix](https://www.citrix.co.in/products/sharefile/support.html) aby zyskać tę wartość.</span><span class="sxs-lookup"><span data-stu-id="f765e-158">Contact [Citrix ShareFile Client support team](https://www.citrix.co.in/products/sharefile/support.html) to get this value.</span></span> 

4. <span data-ttu-id="f765e-159">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="f765e-159">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Łącze pobierania certyfikatu](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_certificate.png) 

5. <span data-ttu-id="f765e-161">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f765e-161">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-sharefile-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f765e-163">Na **konfigurację serwera Citrix ShareFile** , kliknij przycisk **skonfigurować Citrix ShareFile** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="f765e-163">On the **Citrix ShareFile Configuration** section, click **Configure Citrix ShareFile** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f765e-164">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="f765e-164">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfiguracja Citrix ShareFile](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_configure.png) 

7. <span data-ttu-id="f765e-166">W oknie przeglądarki innej witryny sieci web, zaloguj się do Twojego **Citrix ShareFile** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="f765e-166">In a different web browser window, log into your **Citrix ShareFile** company site as an administrator.</span></span>

8. <span data-ttu-id="f765e-167">Na pasku narzędzi u góry kliknij **Admin**.</span><span class="sxs-lookup"><span data-stu-id="f765e-167">In the toolbar on the top, click **Admin**.</span></span>

9. <span data-ttu-id="f765e-168">W lewym okienku nawigacji, wybierz **skonfigurować logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="f765e-168">In the left navigation pane, select **Configure Single Sign-On**.</span></span>
   
    <span data-ttu-id="f765e-169">![Konto administracji](./media/active-directory-saas-sharefile-tutorial/ic773627.png "konta administracji")</span><span class="sxs-lookup"><span data-stu-id="f765e-169">![Account Administration](./media/active-directory-saas-sharefile-tutorial/ic773627.png "Account Administration")</span></span>

10. <span data-ttu-id="f765e-170">Na **rejestracji jednokrotnej / Konfiguracja SAML 2.0** strony okna dialogowego, w obszarze **podstawowe ustawienia**, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="f765e-170">On the **Single Sign-On/ SAML 2.0 Configuration** dialog page under **Basic Settings**, perform the following steps:</span></span>
   
    <span data-ttu-id="f765e-171">![Logowanie jednokrotne](./media/active-directory-saas-sharefile-tutorial/ic773628.png "logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="f765e-171">![Single sign-on](./media/active-directory-saas-sharefile-tutorial/ic773628.png "Single sign-on")</span></span>
   
    <span data-ttu-id="f765e-172">a.</span><span class="sxs-lookup"><span data-stu-id="f765e-172">a.</span></span> <span data-ttu-id="f765e-173">Kliknij przycisk **Włącz SAML**.</span><span class="sxs-lookup"><span data-stu-id="f765e-173">Click **Enable SAML**.</span></span>
    
    <span data-ttu-id="f765e-174">b.</span><span class="sxs-lookup"><span data-stu-id="f765e-174">b.</span></span> <span data-ttu-id="f765e-175">W **Your wystawcy IDP / identyfikator jednostki** pole tekstowe, Wklej wartość **identyfikator jednostki SAML** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f765e-175">In **Your IDP Issuer/ Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="f765e-176">c.</span><span class="sxs-lookup"><span data-stu-id="f765e-176">c.</span></span> <span data-ttu-id="f765e-177">Kliknij przycisk **zmiany** obok **certyfikatu X.509** pola, a następnie przekaż certyfikat pobrany z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f765e-177">Click **Change** next to the **X.509 Certificate** field and then upload the certificate you downloaded from the Azure portal.</span></span>
    
    <span data-ttu-id="f765e-178">d.</span><span class="sxs-lookup"><span data-stu-id="f765e-178">d.</span></span> <span data-ttu-id="f765e-179">W **adres URL logowania** pole tekstowe, Wklej wartość **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f765e-179">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="f765e-180">e.</span><span class="sxs-lookup"><span data-stu-id="f765e-180">e.</span></span> <span data-ttu-id="f765e-181">W **adresu URL wylogowania** pole tekstowe, Wklej wartość **Sign-Out URL** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f765e-181">In **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

11. <span data-ttu-id="f765e-182">Kliknij przycisk **zapisać** w portalu zarządzania Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="f765e-182">Click **Save** on the Citrix ShareFile management portal.</span></span>

> [!TIP]
> <span data-ttu-id="f765e-183">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="f765e-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f765e-184">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="f765e-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f765e-185">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f765e-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="f765e-186">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f765e-186">Create an Azure AD test user</span></span>

<span data-ttu-id="f765e-187">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="f765e-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="f765e-189">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f765e-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f765e-190">W portalu Azure, w okienku po lewej stronie kliknij **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f765e-190">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Przycisk usługi Azure Active Directory](./media/active-directory-saas-sharefile-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="f765e-192">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="f765e-192">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-sharefile-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="f765e-194">Aby otworzyć **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** w górnej części **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="f765e-194">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Przycisk Dodaj](./media/active-directory-saas-sharefile-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="f765e-196">W **użytkownika** okna dialogowego wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="f765e-196">In the **User** dialog box, perform the following steps:</span></span>

    ![Okno dialogowe użytkownika](./media/active-directory-saas-sharefile-tutorial/create_aaduser_04.png)

    <span data-ttu-id="f765e-198">a.</span><span class="sxs-lookup"><span data-stu-id="f765e-198">a.</span></span> <span data-ttu-id="f765e-199">W **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f765e-199">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f765e-200">b.</span><span class="sxs-lookup"><span data-stu-id="f765e-200">b.</span></span> <span data-ttu-id="f765e-201">W **nazwy użytkownika** wpisz adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="f765e-201">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="f765e-202">c.</span><span class="sxs-lookup"><span data-stu-id="f765e-202">c.</span></span> <span data-ttu-id="f765e-203">Wybierz **Pokaż hasło** pole wyboru, a następnie zanotuj wartość, która jest wyświetlana w **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="f765e-203">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="f765e-204">d.</span><span class="sxs-lookup"><span data-stu-id="f765e-204">d.</span></span> <span data-ttu-id="f765e-205">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="f765e-205">Click **Create**.</span></span>
 
### <a name="create-a-citrix-sharefile-test-user"></a><span data-ttu-id="f765e-206">Tworzenie użytkownika testowego Citrix ShareFile</span><span class="sxs-lookup"><span data-stu-id="f765e-206">Create a Citrix ShareFile test user</span></span>

<span data-ttu-id="f765e-207">Aby włączyć użytkowników usługi Azure AD zalogować się do Citrix ShareFile, musi być przygotowana do Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="f765e-207">In order to enable Azure AD users to log into Citrix ShareFile, they must be provisioned into Citrix ShareFile.</span></span> <span data-ttu-id="f765e-208">W przypadku Citrix ShareFile Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="f765e-208">In the case of Citrix ShareFile, provisioning is a manual task.</span></span>

<span data-ttu-id="f765e-209">**Aby udostępnić konta użytkownika, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f765e-209">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="f765e-210">Zaloguj się do Twojego **Citrix ShareFile** dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="f765e-210">Log in to your **Citrix ShareFile** tenant.</span></span>

2. <span data-ttu-id="f765e-211">Kliknij przycisk **Zarządzanie użytkownikami \> Zarządzanie główną użytkowników \> + Tworzenie pracownika**.</span><span class="sxs-lookup"><span data-stu-id="f765e-211">Click **Manage Users \> Manage Users Home \> + Create Employee**.</span></span>
   
   <span data-ttu-id="f765e-212">![Tworzenie pracownika](./media/active-directory-saas-sharefile-tutorial/IC781050.png "Tworzenie pracownika")</span><span class="sxs-lookup"><span data-stu-id="f765e-212">![Create Employee](./media/active-directory-saas-sharefile-tutorial/IC781050.png "Create Employee")</span></span>

3. <span data-ttu-id="f765e-213">Na **podstawowe informacje** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="f765e-213">On the **Basic Information** section, perform below steps:</span></span>
   
   <span data-ttu-id="f765e-214">![Podstawowe informacje](./media/active-directory-saas-sharefile-tutorial/IC799951.png "podstawowe informacje")</span><span class="sxs-lookup"><span data-stu-id="f765e-214">![Basic Information](./media/active-directory-saas-sharefile-tutorial/IC799951.png "Basic Information")</span></span>
   
   <span data-ttu-id="f765e-215">a.</span><span class="sxs-lookup"><span data-stu-id="f765e-215">a.</span></span> <span data-ttu-id="f765e-216">W **adres E-mail** tekstowym, wpisz adres e-mail Simona Britta jako  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="f765e-216">In the **Email Address** textbox, type the email address of Britta Simon as **brittasimon@contoso.com**.</span></span>
   
   <span data-ttu-id="f765e-217">b.</span><span class="sxs-lookup"><span data-stu-id="f765e-217">b.</span></span> <span data-ttu-id="f765e-218">W **imię** pole tekstowe, typ **imię** użytkownika jako **Britta**.</span><span class="sxs-lookup"><span data-stu-id="f765e-218">In the **First Name** textbox, type **first name** of user as **Britta**.</span></span>
   
   <span data-ttu-id="f765e-219">c.</span><span class="sxs-lookup"><span data-stu-id="f765e-219">c.</span></span> <span data-ttu-id="f765e-220">W **nazwisko** pole tekstowe, typ **nazwisko** użytkownika jako **Simona**.</span><span class="sxs-lookup"><span data-stu-id="f765e-220">In the **Last Name** textbox, type **last name** of user as **Simon**.</span></span>

4. <span data-ttu-id="f765e-221">Kliknij przycisk **dodać użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="f765e-221">Click **Add User**.</span></span>
  
   >[!NOTE]
   ><span data-ttu-id="f765e-222">Właścicielem konta usługi Azure AD otrzymasz wiadomość e-mail, a następnie kliknij łącze, aby potwierdzić swoje konto, zanim staje się aktywny. Inne narzędzia do tworzenia konta użytkownika Citrix ShareFile lub interfejsów API dostarczonych przez Citrix ShareFile można użyć do udostępnienia konta użytkownika usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f765e-222">The Azure AD account holder will receive an email and follow a link to confirm their account before it becomes active.You can use any other Citrix ShareFile user account creation tools or APIs provided by Citrix ShareFile to provision Azure AD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="f765e-223">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f765e-223">Assign the Azure AD test user</span></span>

<span data-ttu-id="f765e-224">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="f765e-224">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Citrix ShareFile.</span></span>

![Przypisanie roli użytkownika][200] 

<span data-ttu-id="f765e-226">**Aby przypisać Simona Britta Citrix ShareFile, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f765e-226">**To assign Britta Simon to Citrix ShareFile, perform the following steps:**</span></span>

1. <span data-ttu-id="f765e-227">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="f765e-227">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="f765e-229">Na liście aplikacji zaznacz **Citrix ShareFile**.</span><span class="sxs-lookup"><span data-stu-id="f765e-229">In the applications list, select **Citrix ShareFile**.</span></span>

    ![Łącze Citrix ShareFile na liście aplikacji](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_app.png)  

3. <span data-ttu-id="f765e-231">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="f765e-231">In the menu on the left, click **Users and groups**.</span></span>

    ![Łącze "Użytkownicy i grupy"][202]

4. <span data-ttu-id="f765e-233">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f765e-233">Click **Add** button.</span></span> <span data-ttu-id="f765e-234">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f765e-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![W okienku Dodaj przydziału][203]

5. <span data-ttu-id="f765e-236">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="f765e-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f765e-237">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f765e-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f765e-238">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f765e-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="f765e-239">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="f765e-239">Test single sign-on</span></span>

<span data-ttu-id="f765e-240">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="f765e-240">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f765e-241">Po kliknięciu kafelka Citrix ShareFile w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="f765e-241">When you click the Citrix ShareFile tile in the Access Panel, you should get automatically signed-on to your Citrix ShareFile application.</span></span>
<span data-ttu-id="f765e-242">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f765e-242">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f765e-243">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="f765e-243">Additional resources</span></span>

* [<span data-ttu-id="f765e-244">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f765e-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f765e-245">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f765e-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_203.png

