---
title: 'Samouczek: Integracji Azure Active Directory z Egnyte | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Egnyte."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8c2101d4-1779-4b36-8464-5c1ff780da18
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 62d01333b61e73c83588d2d1701c0c300df4ab1c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-egnyte"></a><span data-ttu-id="caf75-103">Samouczek: Integracji Azure Active Directory z Egnyte</span><span class="sxs-lookup"><span data-stu-id="caf75-103">Tutorial: Azure Active Directory integration with Egnyte</span></span>

<span data-ttu-id="caf75-104">Z tego samouczka dowiesz się integrowanie Egnyte z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="caf75-104">In this tutorial, you learn how to integrate Egnyte with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="caf75-105">Integracja z usługą Azure AD Egnyte zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="caf75-105">Integrating Egnyte with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="caf75-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Egnyte</span><span class="sxs-lookup"><span data-stu-id="caf75-106">You can control in Azure AD who has access to Egnyte</span></span>
- <span data-ttu-id="caf75-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Egnyte (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="caf75-107">You can enable your users to automatically get signed-on to Egnyte (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="caf75-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="caf75-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="caf75-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="caf75-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="caf75-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="caf75-110">Prerequisites</span></span>

<span data-ttu-id="caf75-111">Aby skonfigurować integrację usługi Azure AD z Egnyte, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="caf75-111">To configure Azure AD integration with Egnyte, you need the following items:</span></span>

- <span data-ttu-id="caf75-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="caf75-112">An Azure AD subscription</span></span>
- <span data-ttu-id="caf75-113">Egnyte logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="caf75-113">An Egnyte single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="caf75-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="caf75-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="caf75-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="caf75-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="caf75-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="caf75-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="caf75-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="caf75-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="caf75-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="caf75-118">Scenario description</span></span>
<span data-ttu-id="caf75-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="caf75-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="caf75-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="caf75-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="caf75-121">Dodawanie Egnyte z galerii</span><span class="sxs-lookup"><span data-stu-id="caf75-121">Adding Egnyte from the gallery</span></span>
2. <span data-ttu-id="caf75-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="caf75-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-egnyte-from-the-gallery"></a><span data-ttu-id="caf75-123">Dodawanie Egnyte z galerii</span><span class="sxs-lookup"><span data-stu-id="caf75-123">Adding Egnyte from the gallery</span></span>
<span data-ttu-id="caf75-124">Aby skonfigurować integrację usługi Azure AD Egnyte, należy dodać Egnyte z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="caf75-124">To configure the integration of Egnyte into Azure AD, you need to add Egnyte from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="caf75-125">**Aby dodać Egnyte z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="caf75-125">**To add Egnyte from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="caf75-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="caf75-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="caf75-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="caf75-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="caf75-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="caf75-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="caf75-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="caf75-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="caf75-133">W polu wyszukiwania wpisz **Egnyte**.</span><span class="sxs-lookup"><span data-stu-id="caf75-133">In the search box, type **Egnyte**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_search.png)

5. <span data-ttu-id="caf75-135">W panelu wyników wybierz **Egnyte**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="caf75-135">In the results panel, select **Egnyte**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="caf75-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="caf75-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="caf75-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Egnyte na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="caf75-138">In this section, you configure and test Azure AD single sign-on with Egnyte based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="caf75-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Egnyte jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="caf75-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Egnyte is to a user in Azure AD.</span></span> <span data-ttu-id="caf75-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Egnyte musi się.</span><span class="sxs-lookup"><span data-stu-id="caf75-140">In other words, a link relationship between an Azure AD user and the related user in Egnyte needs to be established.</span></span>

<span data-ttu-id="caf75-141">W Egnyte, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="caf75-141">In Egnyte, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="caf75-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Egnyte, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="caf75-142">To configure and test Azure AD single sign-on with Egnyte, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="caf75-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="caf75-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="caf75-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="caf75-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="caf75-145">**[Tworzenie użytkownika testowego Egnyte](#creating-an-egnyte-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Egnyte połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="caf75-145">**[Creating an Egnyte test user](#creating-an-egnyte-test-user)** - to have a counterpart of Britta Simon in Egnyte that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="caf75-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="caf75-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="caf75-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="caf75-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="caf75-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="caf75-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="caf75-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Egnyte.</span><span class="sxs-lookup"><span data-stu-id="caf75-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Egnyte application.</span></span>

<span data-ttu-id="caf75-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Egnyte, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="caf75-150">**To configure Azure AD single sign-on with Egnyte, perform the following steps:**</span></span>

1. <span data-ttu-id="caf75-151">W portalu Azure na **Egnyte** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="caf75-151">In the Azure portal, on the **Egnyte** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="caf75-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="caf75-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_samlbase.png)

3. <span data-ttu-id="caf75-155">Na **Egnyte domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="caf75-155">On the **Egnyte Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_url.png)

    <span data-ttu-id="caf75-157">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.egnyte.com`</span><span class="sxs-lookup"><span data-stu-id="caf75-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.egnyte.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="caf75-158">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="caf75-158">This value is not real.</span></span> <span data-ttu-id="caf75-159">Zaktualizuj tę wartość przy rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="caf75-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="caf75-160">Skontaktuj się z [zespołem pomocy technicznej klienta Egnyte](https://www.egnyte.com/corp/contact_egnyte.html) aby zyskać tę wartość.</span><span class="sxs-lookup"><span data-stu-id="caf75-160">Contact [Egnyte Client support team](https://www.egnyte.com/corp/contact_egnyte.html) to get this value.</span></span> 
 
4. <span data-ttu-id="caf75-161">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="caf75-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_certificate.png) 

5. <span data-ttu-id="caf75-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="caf75-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-egnyte-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="caf75-165">Na **konfiguracji Egnyte** , kliknij przycisk **skonfigurować Egnyte** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="caf75-165">On the **Egnyte Configuration** section, click **Configure Egnyte** to open **Configure sign-on** window.</span></span> <span data-ttu-id="caf75-166">Kopiuj **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="caf75-166">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_configure.png) 

7. <span data-ttu-id="caf75-168">W oknie przeglądarki innej witryny sieci web należy zalogować się jako administrator do witryny firmy Egnyte.</span><span class="sxs-lookup"><span data-stu-id="caf75-168">In a different web browser window, log in to your Egnyte company site as an administrator.</span></span>

8. <span data-ttu-id="caf75-169">Kliknij przycisk **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="caf75-169">Click **Settings**.</span></span>
   
   <span data-ttu-id="caf75-170">![Ustawienia](./media/active-directory-saas-egnyte-tutorial/ic787819.png "ustawienia")</span><span class="sxs-lookup"><span data-stu-id="caf75-170">![Settings](./media/active-directory-saas-egnyte-tutorial/ic787819.png "Settings")</span></span>

9. <span data-ttu-id="caf75-171">W menu, kliknij przycisk **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="caf75-171">In the menu, click **Settings**.</span></span>

   <span data-ttu-id="caf75-172">![Ustawienia](./media/active-directory-saas-egnyte-tutorial/ic787820.png "ustawienia")</span><span class="sxs-lookup"><span data-stu-id="caf75-172">![Settings](./media/active-directory-saas-egnyte-tutorial/ic787820.png "Settings")</span></span>

10. <span data-ttu-id="caf75-173">Kliknij przycisk **konfiguracji** , a następnie kliknij pozycję **zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="caf75-173">Click the **Configuration** tab, and then click **Security**.</span></span>

    <span data-ttu-id="caf75-174">![Zabezpieczenia](./media/active-directory-saas-egnyte-tutorial/ic787821.png "zabezpieczeń")</span><span class="sxs-lookup"><span data-stu-id="caf75-174">![Security](./media/active-directory-saas-egnyte-tutorial/ic787821.png "Security")</span></span>

11. <span data-ttu-id="caf75-175">W **uwierzytelniania rejestracji jednokrotnej** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="caf75-175">In the **Single Sign-On Authentication** section, perform the following steps:</span></span>

    <span data-ttu-id="caf75-176">![Rejestracja jednokrotna na uwierzytelnianie](./media/active-directory-saas-egnyte-tutorial/ic787822.png "Rejestracja jednokrotna dotyczących uwierzytelniania")</span><span class="sxs-lookup"><span data-stu-id="caf75-176">![Single Sign On Authentication](./media/active-directory-saas-egnyte-tutorial/ic787822.png "Single Sign On Authentication")</span></span>   
    
    <span data-ttu-id="caf75-177">a.</span><span class="sxs-lookup"><span data-stu-id="caf75-177">a.</span></span> <span data-ttu-id="caf75-178">Jako **uwierzytelniania rejestracji jednokrotnej**, wybierz pozycję **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="caf75-178">As **Single sign-on authentication**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="caf75-179">b.</span><span class="sxs-lookup"><span data-stu-id="caf75-179">b.</span></span> <span data-ttu-id="caf75-180">Jako **dostawcy tożsamości**, wybierz pozycję **AzureAD**.</span><span class="sxs-lookup"><span data-stu-id="caf75-180">As **Identity provider**, select **AzureAD**.</span></span>
   
    <span data-ttu-id="caf75-181">c.</span><span class="sxs-lookup"><span data-stu-id="caf75-181">c.</span></span> <span data-ttu-id="caf75-182">Wklej **SAML pojedynczy znak na adres URL usługi** skopiowany z portalu Azure do **adresu URL logowania do dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="caf75-182">Paste **SAML Single Sign-On Service URL** copied from Azure portal into the **Identity provider login URL** textbox.</span></span>
   
    <span data-ttu-id="caf75-183">d.</span><span class="sxs-lookup"><span data-stu-id="caf75-183">d.</span></span> <span data-ttu-id="caf75-184">Wklej **identyfikator jednostki SAML** , które zostały skopiowane z portalu Azure do **identyfikator jednostki dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="caf75-184">Paste **SAML Entity ID** which you have copied from Azure portal into the **Identity provider entity ID** textbox.</span></span>
      
    <span data-ttu-id="caf75-185">e.</span><span class="sxs-lookup"><span data-stu-id="caf75-185">e.</span></span> <span data-ttu-id="caf75-186">Otwórz w Notatniku pobrany z portalu Azure certyfikatu zakodowanego base-64, skopiuj zawartość go do Schowka, a następnie wklej go do **certyfikat dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="caf75-186">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **Identity provider certificate** textbox.</span></span>
   
    <span data-ttu-id="caf75-187">f.</span><span class="sxs-lookup"><span data-stu-id="caf75-187">f.</span></span> <span data-ttu-id="caf75-188">Jako **domyślne mapowanie użytkownika**, wybierz pozycję **adres E-mail**.</span><span class="sxs-lookup"><span data-stu-id="caf75-188">As **Default user mapping**, select **Email address**.</span></span>
   
    <span data-ttu-id="caf75-189">g.</span><span class="sxs-lookup"><span data-stu-id="caf75-189">g.</span></span> <span data-ttu-id="caf75-190">Jako **Użyj wartości wystawcy specyficznego dla domeny**, wybierz pozycję **wyłączone**.</span><span class="sxs-lookup"><span data-stu-id="caf75-190">As **Use domain-specific issuer value**, select **disabled**.</span></span>
   
    <span data-ttu-id="caf75-191">h.</span><span class="sxs-lookup"><span data-stu-id="caf75-191">h.</span></span> <span data-ttu-id="caf75-192">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="caf75-192">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="caf75-193">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="caf75-193">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="caf75-194">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="caf75-194">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="caf75-195">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="caf75-195">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="caf75-196">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="caf75-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="caf75-197">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="caf75-197">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="caf75-199">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="caf75-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="caf75-200">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="caf75-200">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="caf75-202">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="caf75-202">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="caf75-204">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="caf75-204">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="caf75-206">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="caf75-206">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="caf75-208">a.</span><span class="sxs-lookup"><span data-stu-id="caf75-208">a.</span></span> <span data-ttu-id="caf75-209">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="caf75-209">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="caf75-210">b.</span><span class="sxs-lookup"><span data-stu-id="caf75-210">b.</span></span> <span data-ttu-id="caf75-211">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="caf75-211">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="caf75-212">c.</span><span class="sxs-lookup"><span data-stu-id="caf75-212">c.</span></span> <span data-ttu-id="caf75-213">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="caf75-213">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="caf75-214">d.</span><span class="sxs-lookup"><span data-stu-id="caf75-214">d.</span></span> <span data-ttu-id="caf75-215">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="caf75-215">Click **Create**.</span></span>
 
### <a name="creating-an-egnyte-test-user"></a><span data-ttu-id="caf75-216">Tworzenie użytkownika testowego Egnyte</span><span class="sxs-lookup"><span data-stu-id="caf75-216">Creating an Egnyte test user</span></span>

<span data-ttu-id="caf75-217">Aby umożliwić użytkownikom usługi Azure AD zalogować się do Egnyte, musi być przygotowana do Egnyte.</span><span class="sxs-lookup"><span data-stu-id="caf75-217">To enable Azure AD users to log in to Egnyte, they must be provisioned into Egnyte.</span></span> <span data-ttu-id="caf75-218">W przypadku Egnyte Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="caf75-218">In the case of Egnyte, provisioning is a manual task.</span></span>

<span data-ttu-id="caf75-219">**Aby udostępnić konta użytkowników, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="caf75-219">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="caf75-220">Zaloguj się do Twojego **Egnyte** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="caf75-220">Log in to your **Egnyte** company site as administrator.</span></span>

2. <span data-ttu-id="caf75-221">Przejdź do **ustawienia \> użytkownicy i grupy**.</span><span class="sxs-lookup"><span data-stu-id="caf75-221">Go to **Settings \> Users & Groups**.</span></span>

3. <span data-ttu-id="caf75-222">Kliknij przycisk **Dodaj nowego użytkownika**, a następnie wybierz typ użytkownika, które chcesz dodać.</span><span class="sxs-lookup"><span data-stu-id="caf75-222">Click **Add New User**, and then select the type of user you want to add.</span></span>
   
   <span data-ttu-id="caf75-223">![Użytkownicy](./media/active-directory-saas-egnyte-tutorial/ic787824.png "użytkowników")</span><span class="sxs-lookup"><span data-stu-id="caf75-223">![Users](./media/active-directory-saas-egnyte-tutorial/ic787824.png "Users")</span></span>

4. <span data-ttu-id="caf75-224">W **nowego użytkownika standardowego** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="caf75-224">In the **New Standard User** section, perform the following steps:</span></span>
   
   <span data-ttu-id="caf75-225">![Nowy użytkownik standardowy](./media/active-directory-saas-egnyte-tutorial/ic787825.png "nowego użytkownika standardowego")</span><span class="sxs-lookup"><span data-stu-id="caf75-225">![New Standard User](./media/active-directory-saas-egnyte-tutorial/ic787825.png "New Standard User")</span></span>   

   <span data-ttu-id="caf75-226">a.</span><span class="sxs-lookup"><span data-stu-id="caf75-226">a.</span></span> <span data-ttu-id="caf75-227">Typ **E-mail**, **Username**oraz innych szczegółów prawidłowe konto usługi Azure Active Directory, aby udostępnić.</span><span class="sxs-lookup"><span data-stu-id="caf75-227">Type the **Email**, **Username**, and other details of a valid Azure Active Directory account you want to provision.</span></span>
   
   <span data-ttu-id="caf75-228">b.</span><span class="sxs-lookup"><span data-stu-id="caf75-228">b.</span></span> <span data-ttu-id="caf75-229">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="caf75-229">Click **Save**.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="caf75-230">Właściciel konta usługi Azure Active Directory, otrzymają wiadomość e-mail z powiadomieniem.</span><span class="sxs-lookup"><span data-stu-id="caf75-230">The Azure Active Directory account holder will receive a notification email.</span></span>
    >

>[!NOTE]
><span data-ttu-id="caf75-231">Możesz użyć innych Egnyte użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Egnyte do kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="caf75-231">You can use any other Egnyte user account creation tools or APIs provided by Egnyte to provision AAD user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="caf75-232">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="caf75-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="caf75-233">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Egnyte.</span><span class="sxs-lookup"><span data-stu-id="caf75-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Egnyte.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="caf75-235">**Aby przypisać Simona Britta Egnyte, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="caf75-235">**To assign Britta Simon to Egnyte, perform the following steps:**</span></span>

1. <span data-ttu-id="caf75-236">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="caf75-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="caf75-238">Na liście aplikacji zaznacz **Egnyte**.</span><span class="sxs-lookup"><span data-stu-id="caf75-238">In the applications list, select **Egnyte**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_app.png) 

3. <span data-ttu-id="caf75-240">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="caf75-240">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="caf75-242">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="caf75-242">Click **Add** button.</span></span> <span data-ttu-id="caf75-243">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="caf75-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="caf75-245">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="caf75-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="caf75-246">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="caf75-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="caf75-247">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="caf75-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="caf75-248">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="caf75-248">Testing single sign-on</span></span>

<span data-ttu-id="caf75-249">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="caf75-249">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="caf75-250">Po kliknięciu kafelka Egnyte w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Egnyte.</span><span class="sxs-lookup"><span data-stu-id="caf75-250">When you click the Egnyte tile in the Access Panel, you should get automatically signed-on to your Egnyte application.</span></span>
<span data-ttu-id="caf75-251">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="caf75-251">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="caf75-252">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="caf75-252">Additional resources</span></span>

* [<span data-ttu-id="caf75-253">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="caf75-253">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="caf75-254">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="caf75-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_203.png

