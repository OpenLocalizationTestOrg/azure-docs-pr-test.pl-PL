---
title: "Samouczek: Integracji Azure Active Directory z chmurą Creative Adobe | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Adobe Creative chmury."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9ba1171e-56b1-4475-b308-58637d35e5a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 3d13608612c77236346b0e98551d7fc427d602e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-creative-cloud"></a><span data-ttu-id="92cab-103">Samouczek: Integracji Azure Active Directory z chmurą Creative Adobe</span><span class="sxs-lookup"><span data-stu-id="92cab-103">Tutorial: Azure Active Directory integration with Adobe Creative Cloud</span></span>

<span data-ttu-id="92cab-104">Z tego samouczka dowiesz się integrowanie Adobe Creative chmurze z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="92cab-104">In this tutorial, you learn how to integrate Adobe Creative Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="92cab-105">Integrowanie Adobe Creative chmurze z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="92cab-105">Integrating Adobe Creative Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="92cab-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do programu Adobe Creative chmury</span><span class="sxs-lookup"><span data-stu-id="92cab-106">You can control in Azure AD who has access to Adobe Creative Cloud</span></span>
- <span data-ttu-id="92cab-107">Umożliwia użytkownikom automatycznie pobrać zalogowane Adobe Creative chmurą (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="92cab-107">You can enable your users to automatically get signed-on to Adobe Creative Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="92cab-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu zarządzania Azure</span><span class="sxs-lookup"><span data-stu-id="92cab-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="92cab-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="92cab-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="92cab-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="92cab-110">Prerequisites</span></span>

<span data-ttu-id="92cab-111">Aby skonfigurować integrację usługi Azure AD z chmurą Creative Adobe, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="92cab-111">To configure Azure AD integration with Adobe Creative Cloud, you need the following items:</span></span>

- <span data-ttu-id="92cab-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="92cab-112">An Azure AD subscription</span></span>
- <span data-ttu-id="92cab-113">Adobe Creative chmury jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="92cab-113">A Adobe Creative Cloud single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="92cab-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="92cab-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="92cab-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="92cab-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="92cab-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="92cab-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="92cab-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="92cab-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="92cab-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="92cab-118">Scenario description</span></span>
<span data-ttu-id="92cab-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="92cab-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="92cab-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="92cab-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="92cab-121">Dodawanie Adobe Creative chmury z galerii</span><span class="sxs-lookup"><span data-stu-id="92cab-121">Adding Adobe Creative Cloud from the gallery</span></span>
2. <span data-ttu-id="92cab-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="92cab-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adobe-creative-cloud-from-the-gallery"></a><span data-ttu-id="92cab-123">Dodawanie Adobe Creative chmury z galerii</span><span class="sxs-lookup"><span data-stu-id="92cab-123">Adding Adobe Creative Cloud from the gallery</span></span>
<span data-ttu-id="92cab-124">Aby skonfigurować integrację Adobe Creative chmury do usługi Azure AD, należy dodać Adobe Creative chmury z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="92cab-124">To configure the integration of Adobe Creative Cloud into Azure AD, you need to add Adobe Creative Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="92cab-125">**Aby dodać Adobe Creative chmury z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="92cab-125">**To add Adobe Creative Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="92cab-126">W  **[portalu zarządzania Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="92cab-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="92cab-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="92cab-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="92cab-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="92cab-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="92cab-131">Kliknij przycisk **Dodaj** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="92cab-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="92cab-133">W polu wyszukiwania wpisz **chmury Creative Adobe**.</span><span class="sxs-lookup"><span data-stu-id="92cab-133">In the search box, type **Adobe Creative Cloud**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_000.png)

5. <span data-ttu-id="92cab-135">W panelu wyników wybierz **chmury Creative Adobe**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="92cab-135">In the results panel, select **Adobe Creative Cloud**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_0001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="92cab-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="92cab-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="92cab-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Adobe Creative w chmurze na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="92cab-138">In this section, you configure and test Azure AD single sign-on with Adobe Creative Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="92cab-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w chmurze Creative Adobe jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="92cab-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Adobe Creative Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="92cab-140">Innymi słowy łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w chmurze Creative Adobe musi się.</span><span class="sxs-lookup"><span data-stu-id="92cab-140">In other words, a link relationship between an Azure AD user and the related user in Adobe Creative Cloud needs to be established.</span></span>

<span data-ttu-id="92cab-141">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w chmurze Creative Adobe.</span><span class="sxs-lookup"><span data-stu-id="92cab-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Adobe Creative Cloud.</span></span>

<span data-ttu-id="92cab-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z chmurą Creative Adobe, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="92cab-142">To configure and test Azure AD single sign-on with Adobe Creative Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="92cab-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="92cab-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="92cab-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="92cab-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="92cab-145">**[Tworzenie użytkownika testowego chmury Creative Adobe](#creating-an-adobe-creative-cloud-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Adobe Creative chmurze, która jest połączona z jej reprezentacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="92cab-145">**[Creating an Adobe Creative Cloud test user](#creating-an-adobe-creative-cloud-test-user)** - to have a counterpart of Britta Simon in Adobe Creative Cloud that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="92cab-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="92cab-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="92cab-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="92cab-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="92cab-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="92cab-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="92cab-149">W tej sekcji możesz włączyć usługi Azure AD rejestracji jednokrotnej w portalu zarządzania Azure i skonfigurować logowanie jednokrotne do aplikacji w chmurze Creative Adobe.</span><span class="sxs-lookup"><span data-stu-id="92cab-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Adobe Creative Cloud application.</span></span>

<span data-ttu-id="92cab-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z chmurą Creative Adobe, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="92cab-150">**To configure Azure AD single sign-on with Adobe Creative Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="92cab-151">W portalu zarządzania Azure na **chmury Creative Adobe** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="92cab-151">In the Azure Management portal, on the **Adobe Creative Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="92cab-153">Na **logowanie jednokrotne** okna dialogowego, jako **tryb** wybierz **na języku SAML logowania jednokrotnego** Włącz funkcji logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="92cab-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_01.png)

3. <span data-ttu-id="92cab-155">Na **adresy URL i Adobe Creative domenę chmury** sekcji, wykonaj następujące kroki, aby skonfigurować aplikację w **IDP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="92cab-155">On the **Adobe Creative Cloud Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url1.png)

    <span data-ttu-id="92cab-157">a.</span><span class="sxs-lookup"><span data-stu-id="92cab-157">a.</span></span> <span data-ttu-id="92cab-158">W **identyfikator** tekstowym, wpisz wartość, jak:`https://www.okta.com/saml2/service-provider/<token>`</span><span class="sxs-lookup"><span data-stu-id="92cab-158">In the **Identifier** textbox, type the value as: `https://www.okta.com/saml2/service-provider/<token>`</span></span>

    <span data-ttu-id="92cab-159">b.</span><span class="sxs-lookup"><span data-stu-id="92cab-159">b.</span></span> <span data-ttu-id="92cab-160">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<company name>.okta.com/auth/saml20/accauthlinktest`</span><span class="sxs-lookup"><span data-stu-id="92cab-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.okta.com/auth/saml20/accauthlinktest`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="92cab-161">Należy pamiętać, że nie są one rzeczywiste wartości.</span><span class="sxs-lookup"><span data-stu-id="92cab-161">Please note that these are not the real values.</span></span> <span data-ttu-id="92cab-162">Należy zaktualizować te wartości z rzeczywistego identyfikatora i adres URL odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="92cab-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="92cab-163">W tym miejscu zalecamy można używać unikatowej wartości ciągu w identyfikatorze.</span><span class="sxs-lookup"><span data-stu-id="92cab-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="92cab-164">Należy ręcznie utworzyć użytkownika, należy skontaktować się z zespołem pomocy technicznej Adobe Creative chmury.</span><span class="sxs-lookup"><span data-stu-id="92cab-164">If you need to create an user manually, you need to contact the Adobe Creative Cloud support team.</span></span>

4. <span data-ttu-id="92cab-165">Na **adresy URL i Adobe Creative domenę chmury** sekcji, wykonaj następujące kroki, aby skonfigurować aplikację w **SP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="92cab-165">On the **Adobe Creative Cloud Domain and URLs** section, perform the following steps if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url2.png)

    <span data-ttu-id="92cab-167">a.</span><span class="sxs-lookup"><span data-stu-id="92cab-167">a.</span></span> <span data-ttu-id="92cab-168">Polecenie **Pokaż zaawansowane ustawienia adresu URL** opcji</span><span class="sxs-lookup"><span data-stu-id="92cab-168">Click on the **Show advanced URL settings** option</span></span>

    <span data-ttu-id="92cab-169">b.</span><span class="sxs-lookup"><span data-stu-id="92cab-169">b.</span></span> <span data-ttu-id="92cab-170">W **adres URL logowania** tekstowym, wpisz wartość, jak:`https://adobe.com`</span><span class="sxs-lookup"><span data-stu-id="92cab-170">In the **Sign-on URL** textbox, type the value as: `https://adobe.com`</span></span>

5. <span data-ttu-id="92cab-171">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="92cab-171">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_05.png) 

6. <span data-ttu-id="92cab-173">Na **Adobe Creative konfiguracji chmury** kliknij **Konfigurowanie chmury Creative Adobe** otworzyć **konfigurowania rejestracji** okna.</span><span class="sxs-lookup"><span data-stu-id="92cab-173">On the **Adobe Creative Cloud Configuration** section, click **Configure Adobe Creative Cloud** to open **Configure sign-on** window.</span></span> <span data-ttu-id="92cab-174">Skopiuj **identyfikator jednostki SAML** i **adres URL usługi logowania jednokrotnego SAML** z krótkimi opisami sekcji.</span><span class="sxs-lookup"><span data-stu-id="92cab-174">Please copy the **SAML Entity Id** and **SAML SSO Service URL** from Quick Reference section.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_06.png) 

7. <span data-ttu-id="92cab-176">W oknie przeglądarki innej witryny sieci web logowania z dzierżawą chmury Creative Adobe jako administrator.</span><span class="sxs-lookup"><span data-stu-id="92cab-176">In a different web browser window, sign-on to your Adobe Creative Cloud tenant as an administrator.</span></span>

8.  <span data-ttu-id="92cab-177">Przejdź do **tożsamości** w okienku nawigacji po lewej stronie i kliknij domenę.</span><span class="sxs-lookup"><span data-stu-id="92cab-177">Go to **Identity** on the left navigation pane and click your domain.</span></span> <span data-ttu-id="92cab-178">Następnie wykonaj następujące czynności na **pojedynczy znak na wymagana konfiguracja** sekcji.</span><span class="sxs-lookup"><span data-stu-id="92cab-178">Then perform the following steps on **Single Sign On Configuration Required** section.</span></span>

    <span data-ttu-id="92cab-179">![Ustawienia](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "ustawienia")</span><span class="sxs-lookup"><span data-stu-id="92cab-179">![Settings](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "Settings")</span></span>

9. <span data-ttu-id="92cab-180">Kliknij przycisk **Przeglądaj** można przekazać certyfikatu pobrane z usługi Azure AD do **certyfikatu IDP**.</span><span class="sxs-lookup"><span data-stu-id="92cab-180">Click **Browse** to upload the downloaded certificate from Azure AD to **IDP Certificate**.</span></span>

10. <span data-ttu-id="92cab-181">W **wystawcy IDP** pole tekstowe, umieścić wartość elementu **identyfikator jednostki SAML** którego skopiowany z **Konfigurowanie logowania jednokrotnego** sekcji w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="92cab-181">In the **IDP issuer** textbox, put the value of **SAML Entity Id** which you copied from **Configure sign-on** section in Azure portal.</span></span>

11. <span data-ttu-id="92cab-182">W **adres URL logowania IDP** pole tekstowe, umieścić wartość elementu **adres URL usługi logowania jednokrotnego SAML** , które zostały skopiowane z **Konfigurowanie logowania jednokrotnego** sekcji w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="92cab-182">In the **IDP Login URL** textbox, put the value of **SAML SSO Service URL** which you copied from **Configure sign-on** section in Azure portal.</span></span>

12. <span data-ttu-id="92cab-183">Wybierz **HTTP - przekierowania** jako **powiązania IDP**.</span><span class="sxs-lookup"><span data-stu-id="92cab-183">Select **HTTP - Redirect** as **IDP Binding**.</span></span>

13. <span data-ttu-id="92cab-184">Wybierz **adres E-mail** jako **ustawienia logowania użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="92cab-184">Select **Email Address** as **User Login Setting**.</span></span>
 
14. <span data-ttu-id="92cab-185">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="92cab-185">Click **Save** button.</span></span>

15. <span data-ttu-id="92cab-186">Pulpit nawigacyjny teraz przedstawi XML **"Pobieranie metadanych"** pliku.</span><span class="sxs-lookup"><span data-stu-id="92cab-186">The dashboard will now present the XML **"Download Metadata"** file.</span></span> <span data-ttu-id="92cab-187">Zawiera adres URL EntityDescriptor Adobe i AssertionConsumerService adresu URL.</span><span class="sxs-lookup"><span data-stu-id="92cab-187">It contains Adobe’s EntityDescriptor URL and AssertionConsumerService URL.</span></span> <span data-ttu-id="92cab-188">Otwórz plik i skonfigurować je w aplikacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="92cab-188">Please open the file and configure them in the Azure AD application.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_002.png)

    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_003.png)

    <span data-ttu-id="92cab-191">a.</span><span class="sxs-lookup"><span data-stu-id="92cab-191">a.</span></span> <span data-ttu-id="92cab-192">Użyj wartości EntityDescriptor Adobe dostarczył dla **identyfikator** na **Konfigurowanie ustawień aplikacji** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="92cab-192">Use the EntityDescriptor value Adobe provided you for **Identifier** on the **Configure App Settings** dialog.</span></span>

    <span data-ttu-id="92cab-193">b.</span><span class="sxs-lookup"><span data-stu-id="92cab-193">b.</span></span> <span data-ttu-id="92cab-194">Użyj wartości AssertionConsumerService Adobe dostarczył dla **adres URL odpowiedzi** na **Konfigurowanie ustawień aplikacji** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="92cab-194">Use the AssertionConsumerService value Adobe provided you for **Reply URL** on the **Configure App Settings** dialog.</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="92cab-195">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="92cab-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="92cab-196">Celem tej sekcji jest tworzenie użytkownika testowego w portalu zarządzania Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="92cab-196">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="92cab-198">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="92cab-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="92cab-199">W **portalu zarządzania Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="92cab-199">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="92cab-201">Przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** do wyświetlenia na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="92cab-201">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="92cab-203">W górnej części okna dialogowego kliknij **Dodaj** otworzyć **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="92cab-203">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="92cab-205">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="92cab-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="92cab-207">a.</span><span class="sxs-lookup"><span data-stu-id="92cab-207">a.</span></span> <span data-ttu-id="92cab-208">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="92cab-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="92cab-209">b.</span><span class="sxs-lookup"><span data-stu-id="92cab-209">b.</span></span> <span data-ttu-id="92cab-210">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="92cab-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="92cab-211">c.</span><span class="sxs-lookup"><span data-stu-id="92cab-211">c.</span></span> <span data-ttu-id="92cab-212">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="92cab-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="92cab-213">d.</span><span class="sxs-lookup"><span data-stu-id="92cab-213">d.</span></span> <span data-ttu-id="92cab-214">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="92cab-214">Click **Create**.</span></span> 

### <a name="creating-an-adobe-creative-cloud-test-user"></a><span data-ttu-id="92cab-215">Tworzenie użytkownika testowego Adobe Creative chmury</span><span class="sxs-lookup"><span data-stu-id="92cab-215">Creating an Adobe Creative Cloud test user</span></span>

<span data-ttu-id="92cab-216">Aby włączyć użytkowników usługi Azure AD zalogować się do chmury Creative Adobe, muszą mieć przydzielone do programu Adobe Creative chmury.</span><span class="sxs-lookup"><span data-stu-id="92cab-216">In order to enable Azure AD users to log into Adobe Creative Cloud, they must be provisioned into Adobe Creative Cloud.</span></span>  
<span data-ttu-id="92cab-217">W przypadku Adobe Creative chmury Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="92cab-217">In the case of Adobe Creative Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="92cab-218">**Aby udostępnić konta użytkowników, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="92cab-218">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="92cab-219">Zaloguj się do witryny firmy Adobe Creative chmurze jako administrator.</span><span class="sxs-lookup"><span data-stu-id="92cab-219">Log in to your Adobe Creative Cloud company site as an administrator.</span></span>

2. <span data-ttu-id="92cab-220">Kliknij przycisk **osób**.</span><span class="sxs-lookup"><span data-stu-id="92cab-220">Click **People**.</span></span>

    <span data-ttu-id="92cab-221">![Osoby](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "osób")</span><span class="sxs-lookup"><span data-stu-id="92cab-221">![People](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "People")</span></span>

3. <span data-ttu-id="92cab-222">Kliknij przycisk **zaprosić użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="92cab-222">Click **Invite User**.</span></span>

    <span data-ttu-id="92cab-223">![Zaprosić użytkowników](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "zaprosić użytkowników")</span><span class="sxs-lookup"><span data-stu-id="92cab-223">![Invite Users](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "Invite Users")</span></span>

4. <span data-ttu-id="92cab-224">Na **zaprosić użytkowników** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="92cab-224">On the **Invite People** dialog page, perform the following steps:</span></span>

    <span data-ttu-id="92cab-225">![Zaproś inne osoby](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "Zaproś inne osoby")</span><span class="sxs-lookup"><span data-stu-id="92cab-225">![Invite People](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "Invite People")</span></span>

    <span data-ttu-id="92cab-226">a.</span><span class="sxs-lookup"><span data-stu-id="92cab-226">a.</span></span> <span data-ttu-id="92cab-227">W **E-mail** tekstowym, wpisz adres e-mail konta Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="92cab-227">In the **Email** textbox, type the email address of Britta Simon account.</span></span>
    
    <span data-ttu-id="92cab-228">b.</span><span class="sxs-lookup"><span data-stu-id="92cab-228">b.</span></span> <span data-ttu-id="92cab-229">Kliknij przycisk **zaprosić**.</span><span class="sxs-lookup"><span data-stu-id="92cab-229">Click **Invite**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="92cab-230">Właścicielem konta usługi Azure Active Directory otrzymasz wiadomość e-mail, a następnie kliknij łącze, aby potwierdzić swoje konto, zanim staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="92cab-230">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="92cab-231">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="92cab-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="92cab-232">W tej sekcji można włączyć Simona Britta na udostępnienie jej do chmury Creative Adobe za pomocą usługi Azure rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="92cab-232">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Adobe Creative Cloud.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="92cab-234">**Aby przypisać Simona Britta Adobe Creative chmury, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="92cab-234">**To assign Britta Simon to Adobe Creative Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="92cab-235">Otwórz widok aplikacji w portalu zarządzania Azure, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="92cab-235">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="92cab-237">Na liście aplikacji zaznacz **chmury Creative Adobe**.</span><span class="sxs-lookup"><span data-stu-id="92cab-237">In the applications list, select **Adobe Creative Cloud**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_50.png) 

3. <span data-ttu-id="92cab-239">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="92cab-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="92cab-241">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="92cab-241">Click **Add** button.</span></span> <span data-ttu-id="92cab-242">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="92cab-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="92cab-244">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="92cab-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="92cab-245">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="92cab-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="92cab-246">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="92cab-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="92cab-247">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="92cab-247">Testing single sign-on</span></span>

<span data-ttu-id="92cab-248">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="92cab-248">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="92cab-249">Po kliknięciu kafelka Adobe Creative chmury w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji w chmurze Creative Adobe.</span><span class="sxs-lookup"><span data-stu-id="92cab-249">When you click the Adobe Creative Cloud tile in the Access Panel, you should get automatically signed-on to your Adobe Creative Cloud application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="92cab-250">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="92cab-250">Additional resources</span></span>

* [<span data-ttu-id="92cab-251">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="92cab-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="92cab-252">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="92cab-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_203.png