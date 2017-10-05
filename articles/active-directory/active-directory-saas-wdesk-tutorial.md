---
title: 'Samouczek: Integracji Azure Active Directory z Wdesk | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Wdesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 06900a91-a326-4663-8ba6-69ae741a536e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 37660b80cfb01d6a3105aea5ce248f1e03c46695
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wdesk"></a><span data-ttu-id="9e781-103">Samouczek: Integracji Azure Active Directory z Wdesk</span><span class="sxs-lookup"><span data-stu-id="9e781-103">Tutorial: Azure Active Directory integration with Wdesk</span></span>

<span data-ttu-id="9e781-104">Z tego samouczka dowiesz się integrowanie Wdesk z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9e781-104">In this tutorial, you learn how to integrate Wdesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9e781-105">Integracja z usługą Azure AD Wdesk zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="9e781-105">Integrating Wdesk with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9e781-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Wdesk</span><span class="sxs-lookup"><span data-stu-id="9e781-106">You can control in Azure AD who has access to Wdesk</span></span>
- <span data-ttu-id="9e781-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Wdesk (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e781-107">You can enable your users to automatically get signed-on to Wdesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9e781-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="9e781-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9e781-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz.</span><span class="sxs-lookup"><span data-stu-id="9e781-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="9e781-110">[Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9e781-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9e781-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9e781-111">Prerequisites</span></span>

<span data-ttu-id="9e781-112">Aby skonfigurować integrację usługi Azure AD z Wdesk, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="9e781-112">To configure Azure AD integration with Wdesk, you need the following items:</span></span>

- <span data-ttu-id="9e781-113">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e781-113">An Azure AD subscription</span></span>
- <span data-ttu-id="9e781-114">Wdesk jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="9e781-114">A Wdesk single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9e781-115">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="9e781-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9e781-116">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="9e781-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9e781-117">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="9e781-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9e781-118">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9e781-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9e781-119">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="9e781-119">Scenario description</span></span>
<span data-ttu-id="9e781-120">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="9e781-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9e781-121">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="9e781-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9e781-122">Dodawanie Wdesk z galerii</span><span class="sxs-lookup"><span data-stu-id="9e781-122">Adding Wdesk from the gallery</span></span>
2. <span data-ttu-id="9e781-123">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="9e781-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-wdesk-from-the-gallery"></a><span data-ttu-id="9e781-124">Dodawanie Wdesk z galerii</span><span class="sxs-lookup"><span data-stu-id="9e781-124">Adding Wdesk from the gallery</span></span>
<span data-ttu-id="9e781-125">Aby skonfigurować integrację usługi Azure AD Wdesk, należy dodać Wdesk z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="9e781-125">To configure the integration of Wdesk into Azure AD, you need to add Wdesk from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9e781-126">**Aby dodać Wdesk z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="9e781-126">**To add Wdesk from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9e781-127">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="9e781-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="9e781-129">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="9e781-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9e781-130">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="9e781-130">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="9e781-132">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9e781-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="9e781-134">W polu wyszukiwania wpisz **Wdesk**.</span><span class="sxs-lookup"><span data-stu-id="9e781-134">In the search box, type **Wdesk**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_search.png)

5. <span data-ttu-id="9e781-136">W panelu wyników wybierz **Wdesk**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="9e781-136">In the results panel, select **Wdesk**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9e781-138">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="9e781-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9e781-139">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Wdesk na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="9e781-139">In this section, you configure and test Azure AD single sign-on with Wdesk based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9e781-140">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Wdesk jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9e781-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Wdesk is to a user in Azure AD.</span></span> <span data-ttu-id="9e781-141">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Wdesk musi się.</span><span class="sxs-lookup"><span data-stu-id="9e781-141">In other words, a link relationship between an Azure AD user and the related user in Wdesk needs to be established.</span></span>

<span data-ttu-id="9e781-142">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w Wdesk.</span><span class="sxs-lookup"><span data-stu-id="9e781-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Wdesk.</span></span>

<span data-ttu-id="9e781-143">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Wdesk, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="9e781-143">To configure and test Azure AD single sign-on with Wdesk, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9e781-144">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="9e781-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9e781-145">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="9e781-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9e781-146">**[Tworzenie użytkownika testowego Wdesk](#creating-a-wdesk-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Wdesk połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9e781-146">**[Creating a Wdesk test user](#creating-a-wdesk-test-user)** - to have a counterpart of Britta Simon in Wdesk that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9e781-147">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="9e781-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9e781-148">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="9e781-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9e781-149">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9e781-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9e781-150">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Wdesk.</span><span class="sxs-lookup"><span data-stu-id="9e781-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Wdesk application.</span></span>

<span data-ttu-id="9e781-151">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Wdesk, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="9e781-151">**To configure Azure AD single sign-on with Wdesk, perform the following steps:**</span></span>

1. <span data-ttu-id="9e781-152">W portalu Azure na **Wdesk** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="9e781-152">In the Azure portal, on the **Wdesk** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="9e781-154">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="9e781-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_samlbase.png)

3. <span data-ttu-id="9e781-156">Na **Wdesk domeny i adres URL** sekcji, jeśli chcesz skonfigurować aplikację w **IDP** tryb inicjowane, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9e781-156">On the **Wdesk Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url.png)

    <span data-ttu-id="9e781-158">a.</span><span class="sxs-lookup"><span data-stu-id="9e781-158">a.</span></span> <span data-ttu-id="9e781-159">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<subdomain>.wdesk.com/auth/saml/sp/metadata/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="9e781-159">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.wdesk.com/auth/saml/sp/metadata/<instancename>`</span></span>

    <span data-ttu-id="9e781-160">b.</span><span class="sxs-lookup"><span data-stu-id="9e781-160">b.</span></span> <span data-ttu-id="9e781-161">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<subdomain>.wdesk.com/auth/saml/sp/consumer/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="9e781-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.wdesk.com/auth/saml/sp/consumer/<instancename>`</span></span>

4. <span data-ttu-id="9e781-162">Sprawdź **Pokaż zaawansowane ustawienia adresu URL**.</span><span class="sxs-lookup"><span data-stu-id="9e781-162">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="9e781-163">Jeśli chcesz skonfigurować aplikację w **SP** inicjowane tryb, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="9e781-163">If you wish to configure the application in **SP** initiated mode, perform the following step:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url1.png)

    <span data-ttu-id="9e781-165">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<subdomain>.wdesk.com/auth/login/saml/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="9e781-165">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.wdesk.com/auth/login/saml/<instancename>`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="9e781-166">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="9e781-166">These values are not real.</span></span> <span data-ttu-id="9e781-167">Rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="9e781-167">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="9e781-168">Te wartości można uzyskać od WDesk portalu, po skonfigurowaniu logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="9e781-168">You get these values from WDesk portal when you configure the SSO.</span></span> 
  
5. <span data-ttu-id="9e781-169">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="9e781-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_certificate.png) 

6. <span data-ttu-id="9e781-171">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9e781-171">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-wdesk-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="9e781-173">W oknie przeglądarki innej witryny sieci web, zaloguj się jako Administrator zabezpieczeń Wdesk.</span><span class="sxs-lookup"><span data-stu-id="9e781-173">In a different web browser window, login to Wdesk as a Security Administrator.</span></span>

8. <span data-ttu-id="9e781-174">W lewym dolnym rogu, kliknij przycisk **Admin** i wybierz polecenie **administrator konta**:</span><span class="sxs-lookup"><span data-stu-id="9e781-174">In the bottom left, click **Admin** and choose **Account Admin**:</span></span>
 
     ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

9. <span data-ttu-id="9e781-176">W Wdesk administratora, przejdź do **zabezpieczeń**, następnie **SAML** > **ustawienia SAML**:</span><span class="sxs-lookup"><span data-stu-id="9e781-176">In Wdesk Admin, navigate to **Security**, then **SAML** > **SAML Settings**:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig2.png)

10. <span data-ttu-id="9e781-178">W obszarze **ustawienia ogólne**, sprawdź **Włącz SAML rejestrację jednokrotną**:</span><span class="sxs-lookup"><span data-stu-id="9e781-178">Under **General Settings**, check the **Enable SAML Single Sign On**:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig3.png)

11. <span data-ttu-id="9e781-180">W obszarze **szczegóły dostawcy usług**, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9e781-180">Under **Service Provider Details**, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig4.png)

      <span data-ttu-id="9e781-182">a.</span><span class="sxs-lookup"><span data-stu-id="9e781-182">a.</span></span> <span data-ttu-id="9e781-183">Kopiuj **adres URL logowania** i wklej go w **adres Url logowania** textbox w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="9e781-183">Copy the **Login URL** and paste it in **Sign-on Url** textbox on Azure portal.</span></span>
   
      <span data-ttu-id="9e781-184">b.</span><span class="sxs-lookup"><span data-stu-id="9e781-184">b.</span></span> <span data-ttu-id="9e781-185">Kopiuj **adres Url metadanych** i wklej go w **identyfikator** textbox w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="9e781-185">Copy the **Metadata Url** and paste it in **Identifier** textbox on Azure portal.</span></span>
       
      <span data-ttu-id="9e781-186">c.</span><span class="sxs-lookup"><span data-stu-id="9e781-186">c.</span></span> <span data-ttu-id="9e781-187">Kopiuj **adres url klienta** i wklej go w **adres Url odpowiedzi** textbox w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="9e781-187">Copy the **Consumer url** and paste it in **Reply Url** textbox on Azure portal.</span></span>
   
      <span data-ttu-id="9e781-188">d.</span><span class="sxs-lookup"><span data-stu-id="9e781-188">d.</span></span> <span data-ttu-id="9e781-189">Kliknij przycisk **zapisać** w portalu Azure, aby zapisać zmiany.</span><span class="sxs-lookup"><span data-stu-id="9e781-189">Click **Save** on Azure portal to save the changes.</span></span>      

12. <span data-ttu-id="9e781-190">Kliknij przycisk **Konfigurowanie ustawień IdP** otworzyć **edytowanie ustawień dostawców tożsamości** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9e781-190">Click **Configure IdP Settings** to open **Edit IdP Settings** dialog.</span></span> <span data-ttu-id="9e781-191">Kliknij przycisk **wybierz plik** zlokalizować **Metadata.xml** następnie przekazać plik zapisany w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="9e781-191">Click **Choose File** to locate the **Metadata.xml** file you saved from Azure portal, then upload it.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig5.png)
  
13. <span data-ttu-id="9e781-193">Kliknij przycisk **zapisać zmiany**.</span><span class="sxs-lookup"><span data-stu-id="9e781-193">Click **Save changes**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfigsavebutton.png)

> [!TIP]
> <span data-ttu-id="9e781-195">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="9e781-195">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9e781-196">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="9e781-196">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9e781-197">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9e781-197">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9e781-198">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e781-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="9e781-199">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="9e781-199">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="9e781-201">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="9e781-201">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9e781-202">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="9e781-202">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9e781-204">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="9e781-204">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9e781-206">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9e781-206">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9e781-208">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9e781-208">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9e781-210">a.</span><span class="sxs-lookup"><span data-stu-id="9e781-210">a.</span></span> <span data-ttu-id="9e781-211">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9e781-211">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9e781-212">b.</span><span class="sxs-lookup"><span data-stu-id="9e781-212">b.</span></span> <span data-ttu-id="9e781-213">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9e781-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9e781-214">c.</span><span class="sxs-lookup"><span data-stu-id="9e781-214">c.</span></span> <span data-ttu-id="9e781-215">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="9e781-215">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9e781-216">d.</span><span class="sxs-lookup"><span data-stu-id="9e781-216">d.</span></span> <span data-ttu-id="9e781-217">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="9e781-217">Click **Create**.</span></span>
 
### <a name="creating-a-wdesk-test-user"></a><span data-ttu-id="9e781-218">Tworzenie użytkownika testowego Wdesk</span><span class="sxs-lookup"><span data-stu-id="9e781-218">Creating a Wdesk test user</span></span>

<span data-ttu-id="9e781-219">Aby umożliwić użytkownikom usługi Azure AD zalogować się do Wdesk, musi być przygotowana do Wdesk.</span><span class="sxs-lookup"><span data-stu-id="9e781-219">To enable Azure AD users to log in to Wdesk, they must be provisioned into Wdesk.</span></span> <span data-ttu-id="9e781-220">W Wdesk Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="9e781-220">In Wdesk, provisioning is a manual task.</span></span>

<span data-ttu-id="9e781-221">**Aby udostępnić konta użytkownika, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="9e781-221">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="9e781-222">Zaloguj się jako Administrator zabezpieczeń Wdesk.</span><span class="sxs-lookup"><span data-stu-id="9e781-222">Log in to Wdesk as a Security Administrator.</span></span>
2. <span data-ttu-id="9e781-223">Przejdź do **Admin** > **konto administratora**.</span><span class="sxs-lookup"><span data-stu-id="9e781-223">Navigate to **Admin** > **Account Admin**.</span></span>

     ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

3. <span data-ttu-id="9e781-225">Kliknij przycisk **członków** w obszarze **osób**.</span><span class="sxs-lookup"><span data-stu-id="9e781-225">Click **Members** under **People**.</span></span>

4. <span data-ttu-id="9e781-226">Teraz kliknij **dodać element członkowski** otworzyć **dodać element członkowski** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="9e781-226">Now click **Add Member** to open **Add Member** dialog box.</span></span> 
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser1.png)  

5. <span data-ttu-id="9e781-228">W **użytkownika** tekst Wprowadź nazwa użytkownika, takich jak  **brittasimon@contoso.com**  i kliknij przycisk **Kontynuuj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9e781-228">In **User** text box, enter the username of user like **brittasimon@contoso.com** and click **Continue** button.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser3.png)

6.  <span data-ttu-id="9e781-230">Wprowadź szczegóły, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="9e781-230">Enter the details as shown below:</span></span>
  
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser4.png)
 
    <span data-ttu-id="9e781-232">a.</span><span class="sxs-lookup"><span data-stu-id="9e781-232">a.</span></span> <span data-ttu-id="9e781-233">W **E-mail** tekstowym wprowadź adres e-mail użytkownika, takich jak  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="9e781-233">In **E-mail** text box, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="9e781-234">b.</span><span class="sxs-lookup"><span data-stu-id="9e781-234">b.</span></span> <span data-ttu-id="9e781-235">W **imię** tekst Wprowadź imię użytkownika, takich jak **Britta**.</span><span class="sxs-lookup"><span data-stu-id="9e781-235">In **First Name** text box, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="9e781-236">c.</span><span class="sxs-lookup"><span data-stu-id="9e781-236">c.</span></span> <span data-ttu-id="9e781-237">W **nazwisko** tekst Wprowadź nazwisko użytkownika, takich jak **Simona**.</span><span class="sxs-lookup"><span data-stu-id="9e781-237">In **Last Name** text box, enter the last name of user like **Simon**.</span></span>

7. <span data-ttu-id="9e781-238">Kliknij przycisk **zapisać element członkowski** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9e781-238">Click **Save Member** button.</span></span>  

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser5.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9e781-240">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e781-240">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9e781-241">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Wdesk.</span><span class="sxs-lookup"><span data-stu-id="9e781-241">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Wdesk.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="9e781-243">**Aby przypisać Simona Britta Wdesk, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="9e781-243">**To assign Britta Simon to Wdesk, perform the following steps:**</span></span>

1. <span data-ttu-id="9e781-244">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="9e781-244">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="9e781-246">Na liście aplikacji zaznacz **Wdesk**.</span><span class="sxs-lookup"><span data-stu-id="9e781-246">In the applications list, select **Wdesk**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_app.png) 

3. <span data-ttu-id="9e781-248">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="9e781-248">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="9e781-250">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9e781-250">Click **Add** button.</span></span> <span data-ttu-id="9e781-251">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9e781-251">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="9e781-253">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="9e781-253">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9e781-254">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9e781-254">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9e781-255">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9e781-255">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9e781-256">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9e781-256">Testing single sign-on</span></span>

<span data-ttu-id="9e781-257">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="9e781-257">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9e781-258">Po kliknięciu kafelka Wdesk w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Wdesk.</span><span class="sxs-lookup"><span data-stu-id="9e781-258">When you click the Wdesk tile in the Access Panel, you should get automatically signed-on to your Wdesk application.</span></span>
<span data-ttu-id="9e781-259">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9e781-259">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="9e781-260">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="9e781-260">Additional resources</span></span>

* [<span data-ttu-id="9e781-261">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9e781-261">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9e781-262">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9e781-262">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_203.png

