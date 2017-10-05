---
title: 'Samouczek: Integracji Azure Active Directory z Netsuite | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Netsuite."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dafa0864-aef2-4f5e-9eac-770504688ef4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 4a19ab310212b93a53495a6fc6c25c77dfb82e79
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-netsuite"></a><span data-ttu-id="17a9c-103">Samouczek: Integracji Azure Active Directory z Netsuite</span><span class="sxs-lookup"><span data-stu-id="17a9c-103">Tutorial: Azure Active Directory integration with Netsuite</span></span>

<span data-ttu-id="17a9c-104">Z tego samouczka dowiesz się integrowanie Netsuite z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="17a9c-104">In this tutorial, you learn how to integrate Netsuite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="17a9c-105">Integracja z usługą Azure AD Netsuite zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="17a9c-105">Integrating Netsuite with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="17a9c-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Netsuite</span><span class="sxs-lookup"><span data-stu-id="17a9c-106">You can control in Azure AD who has access to Netsuite</span></span>
- <span data-ttu-id="17a9c-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Netsuite (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="17a9c-107">You can enable your users to automatically get signed-on to Netsuite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="17a9c-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="17a9c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="17a9c-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="17a9c-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="17a9c-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="17a9c-110">Prerequisites</span></span>

<span data-ttu-id="17a9c-111">Aby skonfigurować integrację usługi Azure AD z Netsuite, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="17a9c-111">To configure Azure AD integration with Netsuite, you need the following items:</span></span>

- <span data-ttu-id="17a9c-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="17a9c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="17a9c-113">Netsuite jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="17a9c-113">A Netsuite single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="17a9c-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="17a9c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="17a9c-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="17a9c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="17a9c-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="17a9c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="17a9c-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="17a9c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="17a9c-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="17a9c-118">Scenario description</span></span>
<span data-ttu-id="17a9c-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="17a9c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="17a9c-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="17a9c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="17a9c-121">Dodawanie Netsuite z galerii</span><span class="sxs-lookup"><span data-stu-id="17a9c-121">Adding Netsuite from the gallery</span></span>
2. <span data-ttu-id="17a9c-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="17a9c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-netsuite-from-the-gallery"></a><span data-ttu-id="17a9c-123">Dodawanie Netsuite z galerii</span><span class="sxs-lookup"><span data-stu-id="17a9c-123">Adding Netsuite from the gallery</span></span>
<span data-ttu-id="17a9c-124">Aby skonfigurować integrację usługi Azure AD Netsuite, należy dodać Netsuite z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="17a9c-124">To configure the integration of Netsuite into Azure AD, you need to add Netsuite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="17a9c-125">**Aby dodać Netsuite z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="17a9c-125">**To add Netsuite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="17a9c-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="17a9c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="17a9c-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="17a9c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="17a9c-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="17a9c-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="17a9c-131">Kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="17a9c-131">Click **New application** button on the top of the dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="17a9c-133">W polu wyszukiwania wpisz **Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="17a9c-133">In the search box, type **Netsuite**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_search.png)

5. <span data-ttu-id="17a9c-135">W panelu wyników wybierz **Netsuite**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="17a9c-135">In the results panel, select **Netsuite**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="17a9c-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="17a9c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="17a9c-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Netsuite na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="17a9c-138">In this section, you configure and test Azure AD single sign-on with Netsuite based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="17a9c-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Netsuite jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="17a9c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Netsuite is to a user in Azure AD.</span></span> <span data-ttu-id="17a9c-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Netsuite musi się.</span><span class="sxs-lookup"><span data-stu-id="17a9c-140">In other words, a link relationship between an Azure AD user and the related user in Netsuite needs to be established.</span></span>

<span data-ttu-id="17a9c-141">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w Netsuite.</span><span class="sxs-lookup"><span data-stu-id="17a9c-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Netsuite.</span></span>

<span data-ttu-id="17a9c-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Netsuite, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="17a9c-142">To configure and test Azure AD single sign-on with Netsuite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="17a9c-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="17a9c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="17a9c-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="17a9c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="17a9c-145">**[Tworzenie użytkownika testowego Netsuite](#creating-a-netsuite-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Netsuite połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="17a9c-145">**[Creating a Netsuite test user](#creating-a-netsuite-test-user)** - to have a counterpart of Britta Simon in Netsuite that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="17a9c-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="17a9c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="17a9c-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="17a9c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="17a9c-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="17a9c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="17a9c-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Netsuite.</span><span class="sxs-lookup"><span data-stu-id="17a9c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Netsuite application.</span></span>

<span data-ttu-id="17a9c-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Netsuite, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="17a9c-150">**To configure Azure AD single sign-on with Netsuite, perform the following steps:**</span></span>

1. <span data-ttu-id="17a9c-151">W portalu Azure na **Netsuite** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="17a9c-151">In the Azure portal, on the **Netsuite** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="17a9c-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="17a9c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_samlbase.png)

3. <span data-ttu-id="17a9c-155">Na **Netsuite domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="17a9c-155">On the **Netsuite Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_url.png)

    <span data-ttu-id="17a9c-157">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca: `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs``https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`</span><span class="sxs-lookup"><span data-stu-id="17a9c-157">In the **Reply URL** textbox, type a URL using the following pattern:   `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="17a9c-158">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="17a9c-158">This value is not real value.</span></span> <span data-ttu-id="17a9c-159">Zaktualizuj tę wartość do rzeczywistego adresu URL odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="17a9c-159">Update the value with the actual Reply URL.</span></span> <span data-ttu-id="17a9c-160">Skontaktuj się z [zespołem pomocy technicznej Netsuite](http://www.netsuite.com/portal/services/support.shtml) aby zyskać tę wartość.</span><span class="sxs-lookup"><span data-stu-id="17a9c-160">Contact [Netsuite support team](http://www.netsuite.com/portal/services/support.shtml) to get this value.</span></span>
 
4. <span data-ttu-id="17a9c-161">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="17a9c-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_certificate.png) 

5. <span data-ttu-id="17a9c-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="17a9c-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-netsuite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="17a9c-165">Na **konfiguracji Netsuite** , kliknij przycisk **skonfigurować Netsuite** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="17a9c-165">On the **Netsuite Configuration** section, click **Configure Netsuite** to open **Configure sign-on** window.</span></span> <span data-ttu-id="17a9c-166">Kopiuj **SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="17a9c-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_configure.png) 

7. <span data-ttu-id="17a9c-168">Otwórz nową kartę w przeglądarce i zaloguj się do witryny firmy Netsuite jako administrator.</span><span class="sxs-lookup"><span data-stu-id="17a9c-168">Open a new tab in your browser, and sign into your Netsuite company site as an administrator.</span></span>

8. <span data-ttu-id="17a9c-169">Na pasku narzędzi w górnej części strony kliknij **Instalator**, następnie kliknij przycisk **Menedżer instalacji**.</span><span class="sxs-lookup"><span data-stu-id="17a9c-169">In the toolbar at the top of the page, click **Setup**, then click **Setup Manager**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

9. <span data-ttu-id="17a9c-171">Z **zadań konfiguracyjnych** listy, wybierz **integracji**.</span><span class="sxs-lookup"><span data-stu-id="17a9c-171">From the **Setup Tasks** list, select **Integration**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Netsuite-tutorial/ns-integration.png)

10. <span data-ttu-id="17a9c-173">W **Zarządzanie uwierzytelniania** kliknij **SAML logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="17a9c-173">In the **Manage Authentication** section, click **SAML Single Sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Netsuite-tutorial/ns-saml.png)

11. <span data-ttu-id="17a9c-175">Na **Instalatora SAML** wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="17a9c-175">On the **SAML Setup** page, perform the following steps:</span></span>
   
    <span data-ttu-id="17a9c-176">a.</span><span class="sxs-lookup"><span data-stu-id="17a9c-176">a.</span></span> <span data-ttu-id="17a9c-177">Kopia **SAML pojedynczy znak na adres URL usługi** wartość z **krótkimi opisami** sekcji **Konfigurowanie logowania jednokrotnego** i wklej ją do **strony logowania dostawcy tożsamości** w Netsuite.</span><span class="sxs-lookup"><span data-stu-id="17a9c-177">Copy the **SAML Single Sign-On Service URL** value from **Quick Reference** section of **Configure sign-on** and paste it into the **Identity Provider Login Page** field in Netsuite.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-netsuite-tutorial/ns-saml-setup.png)
  
    <span data-ttu-id="17a9c-179">b.</span><span class="sxs-lookup"><span data-stu-id="17a9c-179">b.</span></span> <span data-ttu-id="17a9c-180">Netsuite, wybierz **podstawowej metody uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="17a9c-180">In Netsuite, select **Primary Authentication Method**.</span></span>

    <span data-ttu-id="17a9c-181">c.</span><span class="sxs-lookup"><span data-stu-id="17a9c-181">c.</span></span> <span data-ttu-id="17a9c-182">W polu z etykietą **metadanych dostawcy tożsamości SAMLV2**, wybierz pozycję **Przekaż plik metadanych IDP**.</span><span class="sxs-lookup"><span data-stu-id="17a9c-182">For the field labeled **SAMLV2 Identity Provider Metadata**, select **Upload IDP Metadata File**.</span></span> <span data-ttu-id="17a9c-183">Następnie kliknij przycisk **Przeglądaj** można przekazać pliku metadanych, który został pobrany z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="17a9c-183">Then click **Browse** to upload the metadata file that you downloaded from Azure portal.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-netsuite-tutorial/ns-sso-setup.png)

    <span data-ttu-id="17a9c-185">d.</span><span class="sxs-lookup"><span data-stu-id="17a9c-185">d.</span></span> <span data-ttu-id="17a9c-186">Kliknij przycisk **przesłać**.</span><span class="sxs-lookup"><span data-stu-id="17a9c-186">Click **Submit**.</span></span>

12. <span data-ttu-id="17a9c-187">W usłudze Azure AD, kliknij **widoku i edytować wszystkie atrybuty użytkowników** pole wyboru i dodać atrybut.</span><span class="sxs-lookup"><span data-stu-id="17a9c-187">In Azure AD, Click on **View and edit all other user attributes** check-box and add attribute.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Netsuite-tutorial/ns-attributes.png)

13. <span data-ttu-id="17a9c-189">Aby uzyskać **nazwa atrybutu** wpisz w `account`.</span><span class="sxs-lookup"><span data-stu-id="17a9c-189">For the **Attribute Name** field, type in `account`.</span></span> <span data-ttu-id="17a9c-190">Aby uzyskać **wartość atrybutu** wpisz w identyfikatora konta Netsuite Ta wartość jest stała i zmianę konta.</span><span class="sxs-lookup"><span data-stu-id="17a9c-190">For the **Attribute Value** field, type in your Netsuite account ID.This value is constant and change with account.</span></span> <span data-ttu-id="17a9c-191">Poniżej znajdują się instrukcje dotyczące sposobu Znajdź identyfikator konta:</span><span class="sxs-lookup"><span data-stu-id="17a9c-191">Instructions on how to find your account ID are included below:</span></span>

      ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Netsuite-tutorial/ns-add-attribute.png)

    <span data-ttu-id="17a9c-193">a.</span><span class="sxs-lookup"><span data-stu-id="17a9c-193">a.</span></span> <span data-ttu-id="17a9c-194">W Netsuite, kliknij przycisk **Instalator** w menu górnym menu nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="17a9c-194">In Netsuite, click **Setup** from the top navigation menu.</span></span>

    <span data-ttu-id="17a9c-195">b.</span><span class="sxs-lookup"><span data-stu-id="17a9c-195">b.</span></span> <span data-ttu-id="17a9c-196">Kliknięcie w obszarze **zadań konfiguracyjnych** części menu nawigacji po lewej stronie wybierz **integracji** sekcji, a następnie kliknij polecenie **preferencje usług sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="17a9c-196">Then click under the **Setup Tasks** section of the left navigation menu, select the **Integration** section, and click **Web Services Preferences**.</span></span>

    <span data-ttu-id="17a9c-197">c.</span><span class="sxs-lookup"><span data-stu-id="17a9c-197">c.</span></span> <span data-ttu-id="17a9c-198">Identyfikator konta Netsuite skopiuj i wklej ją do **wartość atrybutu** pole w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="17a9c-198">Copy your Netsuite Account ID and paste it into the **Attribute Value** field in Azure AD.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Netsuite-tutorial/ns-account-id.png)

14. <span data-ttu-id="17a9c-200">Zanim użytkownicy mogą wykonywać logowania jednokrotnego do Netsuite, ich należy przypisać odpowiednie uprawnienia w Netsuite.</span><span class="sxs-lookup"><span data-stu-id="17a9c-200">Before users can perform single sign-on into Netsuite, they must first be assigned the appropriate permissions in Netsuite.</span></span> <span data-ttu-id="17a9c-201">Postępuj zgodnie z instrukcjami poniżej, aby przypisać te uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="17a9c-201">Follow the instructions below to assign these permissions.</span></span>

    <span data-ttu-id="17a9c-202">a.</span><span class="sxs-lookup"><span data-stu-id="17a9c-202">a.</span></span> <span data-ttu-id="17a9c-203">W menu górnym menu nawigacyjnym kliknij **Instalator**, następnie kliknij przycisk **Menedżer instalacji**.</span><span class="sxs-lookup"><span data-stu-id="17a9c-203">On the top navigation menu, click **Setup**, then click **Setup Manager**.</span></span>
      
      ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    <span data-ttu-id="17a9c-205">b.</span><span class="sxs-lookup"><span data-stu-id="17a9c-205">b.</span></span> <span data-ttu-id="17a9c-206">W menu nawigacji po lewej stronie wybierz **użytkownicy i role**, następnie kliknij przycisk **Zarządzanie rolami**.</span><span class="sxs-lookup"><span data-stu-id="17a9c-206">On the left navigation menu, select **Users/Roles**, then click **Manage Roles**.</span></span>
      
      ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Netsuite-tutorial/ns-manage-roles.png)

    <span data-ttu-id="17a9c-208">c.</span><span class="sxs-lookup"><span data-stu-id="17a9c-208">c.</span></span> <span data-ttu-id="17a9c-209">Kliknij przycisk **nową rolę**.</span><span class="sxs-lookup"><span data-stu-id="17a9c-209">Click **New Role**.</span></span>

    <span data-ttu-id="17a9c-210">d.</span><span class="sxs-lookup"><span data-stu-id="17a9c-210">d.</span></span> <span data-ttu-id="17a9c-211">Wpisz w **nazwa** dla nowej roli, a wybierz **pojedynczego logowania tylko** wyboru.</span><span class="sxs-lookup"><span data-stu-id="17a9c-211">Type in a **Name** for your new role, and select the **Single Sign-On Only** checkbox.</span></span>
      
      ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Netsuite-tutorial/ns-new-role.png)

    <span data-ttu-id="17a9c-213">e.</span><span class="sxs-lookup"><span data-stu-id="17a9c-213">e.</span></span> <span data-ttu-id="17a9c-214">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="17a9c-214">Click **Save**.</span></span>

    <span data-ttu-id="17a9c-215">f.</span><span class="sxs-lookup"><span data-stu-id="17a9c-215">f.</span></span> <span data-ttu-id="17a9c-216">W menu u góry kliknij **uprawnienia**.</span><span class="sxs-lookup"><span data-stu-id="17a9c-216">In the menu on the top, click **Permissions**.</span></span> <span data-ttu-id="17a9c-217">Następnie kliknij przycisk **Instalatora**.</span><span class="sxs-lookup"><span data-stu-id="17a9c-217">Then click **Setup**.</span></span>
      
       ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Netsuite-tutorial/ns-sso.png)

    <span data-ttu-id="17a9c-219">g.</span><span class="sxs-lookup"><span data-stu-id="17a9c-219">g.</span></span> <span data-ttu-id="17a9c-220">Wybierz **ustawić się SAM rejestracji jednokrotnej**, a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="17a9c-220">Select **Set Up SAM Single Sign-on**, and then click **Add**.</span></span>

    <span data-ttu-id="17a9c-221">h.</span><span class="sxs-lookup"><span data-stu-id="17a9c-221">h.</span></span> <span data-ttu-id="17a9c-222">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="17a9c-222">Click **Save**.</span></span>

    <span data-ttu-id="17a9c-223">i.</span><span class="sxs-lookup"><span data-stu-id="17a9c-223">i.</span></span> <span data-ttu-id="17a9c-224">W menu górnym menu nawigacyjnym kliknij **Instalator**, następnie kliknij przycisk **Menedżer instalacji**.</span><span class="sxs-lookup"><span data-stu-id="17a9c-224">On the top navigation menu, click **Setup**, then click **Setup Manager**.</span></span>
      
       ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    <span data-ttu-id="17a9c-226">j.</span><span class="sxs-lookup"><span data-stu-id="17a9c-226">j.</span></span> <span data-ttu-id="17a9c-227">W menu nawigacji po lewej stronie wybierz **użytkownicy i role**, następnie kliknij przycisk **Zarządzanie użytkownikami**.</span><span class="sxs-lookup"><span data-stu-id="17a9c-227">On the left navigation menu, select **Users/Roles**, then click **Manage Users**.</span></span>
      
       ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Netsuite-tutorial/ns-manage-users.png)

    <span data-ttu-id="17a9c-229">k.</span><span class="sxs-lookup"><span data-stu-id="17a9c-229">k.</span></span> <span data-ttu-id="17a9c-230">Wybierz użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="17a9c-230">Select a test user.</span></span> <span data-ttu-id="17a9c-231">Następnie kliknij przycisk **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="17a9c-231">Then click **Edit**.</span></span>
      
       ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Netsuite-tutorial/ns-edit-user.png)

    <span data-ttu-id="17a9c-233">l.</span><span class="sxs-lookup"><span data-stu-id="17a9c-233">l.</span></span> <span data-ttu-id="17a9c-234">W oknie dialogowym ról, wybierz rolę, którą utworzono i kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="17a9c-234">On the Roles dialog, select the role that you have created and click **Add**.</span></span>
      
       ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Netsuite-tutorial/ns-add-role.png)

    <span data-ttu-id="17a9c-236">m.</span><span class="sxs-lookup"><span data-stu-id="17a9c-236">m.</span></span> <span data-ttu-id="17a9c-237">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="17a9c-237">Click **Save**.</span></span>
    
> [!TIP]
> <span data-ttu-id="17a9c-238">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="17a9c-238">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="17a9c-239">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="17a9c-239">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="17a9c-240">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="17a9c-240">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="17a9c-241">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="17a9c-241">Creating an Azure AD test user</span></span>
<span data-ttu-id="17a9c-242">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="17a9c-242">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="17a9c-244">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="17a9c-244">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="17a9c-245">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="17a9c-245">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="17a9c-247">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="17a9c-247">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="17a9c-249">W górnej części okna dialogowego, kliknij przycisk **Dodaj** otworzyć **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="17a9c-249">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="17a9c-251">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="17a9c-251">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="17a9c-253">a.</span><span class="sxs-lookup"><span data-stu-id="17a9c-253">a.</span></span> <span data-ttu-id="17a9c-254">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="17a9c-254">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="17a9c-255">b.</span><span class="sxs-lookup"><span data-stu-id="17a9c-255">b.</span></span> <span data-ttu-id="17a9c-256">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="17a9c-256">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="17a9c-257">c.</span><span class="sxs-lookup"><span data-stu-id="17a9c-257">c.</span></span> <span data-ttu-id="17a9c-258">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="17a9c-258">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="17a9c-259">d.</span><span class="sxs-lookup"><span data-stu-id="17a9c-259">d.</span></span> <span data-ttu-id="17a9c-260">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="17a9c-260">Click **Create**.</span></span> 

### <a name="creating-a-netsuite-test-user"></a><span data-ttu-id="17a9c-261">Tworzenie użytkownika testowego Netsuite</span><span class="sxs-lookup"><span data-stu-id="17a9c-261">Creating a Netsuite test user</span></span>

<span data-ttu-id="17a9c-262">W tej sekcji użytkownika o nazwie Simona Britta jest tworzony w Netsuite.</span><span class="sxs-lookup"><span data-stu-id="17a9c-262">In this section, a user called Britta Simon is created in Netsuite.</span></span> <span data-ttu-id="17a9c-263">Netsuite obsługę w czasie, który jest domyślnie włączona.</span><span class="sxs-lookup"><span data-stu-id="17a9c-263">Netsuite supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="17a9c-264">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="17a9c-264">There is no action item for you in this section.</span></span> <span data-ttu-id="17a9c-265">Jeśli użytkownik nie istnieje w Netsuite, nowy jest tworzony podczas próby uzyskania dostępu Netsuite.</span><span class="sxs-lookup"><span data-stu-id="17a9c-265">If a user doesn't already exist in Netsuite, a new one is created when you attempt to access Netsuite.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="17a9c-266">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="17a9c-266">Assigning the Azure AD test user</span></span>

<span data-ttu-id="17a9c-267">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Netsuite.</span><span class="sxs-lookup"><span data-stu-id="17a9c-267">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Netsuite.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="17a9c-269">**Aby przypisać Simona Britta Netsuite, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="17a9c-269">**To assign Britta Simon to Netsuite, perform the following steps:**</span></span>

1. <span data-ttu-id="17a9c-270">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="17a9c-270">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="17a9c-272">Na liście aplikacji zaznacz **Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="17a9c-272">In the applications list, select **Netsuite**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_app.png) 

3. <span data-ttu-id="17a9c-274">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="17a9c-274">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="17a9c-276">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="17a9c-276">Click **Add** button.</span></span> <span data-ttu-id="17a9c-277">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="17a9c-277">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="17a9c-279">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="17a9c-279">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="17a9c-280">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="17a9c-280">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="17a9c-281">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="17a9c-281">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="17a9c-282">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="17a9c-282">Testing single sign-on</span></span>

<span data-ttu-id="17a9c-283">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="17a9c-283">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="17a9c-284">Aby przetestować jednego ustawienia logowania jednokrotnego, otwórz Panel dostępu w [https://myapps.microsoft.com](https://myapps.microsoft.com/), zaloguj się do konta testowego i kliknij przycisk **Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="17a9c-284">To test your single sign-on settings, open the Access Panel at [https://myapps.microsoft.com](https://myapps.microsoft.com/), sign into the test account, and click **Netsuite**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="17a9c-285">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="17a9c-285">Additional resources</span></span>

* [<span data-ttu-id="17a9c-286">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="17a9c-286">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="17a9c-287">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="17a9c-287">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="17a9c-288">Skonfiguruj Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="17a9c-288">Configure User Provisioning</span></span>](active-directory-saas-netsuite-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_203.png

