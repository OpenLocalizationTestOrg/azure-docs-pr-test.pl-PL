---
title: 'Samouczek: Integracji Azure Active Directory z obrazu przekazywania | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i przekazywania obrazu."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 65bb5990-07ef-4244-9f41-cd28fc2cb5a2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 0bfbbaee7a74df6508584b7c8846fd07c2dc15c9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-image-relay"></a><span data-ttu-id="8184f-103">Samouczek: Integracji Azure Active Directory z przekaźnika obrazu</span><span class="sxs-lookup"><span data-stu-id="8184f-103">Tutorial: Azure Active Directory integration with Image Relay</span></span>

<span data-ttu-id="8184f-104">Z tego samouczka dowiesz integrowanie przekazywania obrazu z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8184f-104">In this tutorial, you learn how to integrate Image Relay with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8184f-105">Integrowanie przekazywania obrazu z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="8184f-105">Integrating Image Relay with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8184f-106">Można kontrolować w usłudze Azure AD, który ma dostęp do przekazywania obrazu</span><span class="sxs-lookup"><span data-stu-id="8184f-106">You can control in Azure AD who has access to Image Relay</span></span>
- <span data-ttu-id="8184f-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do przekazywania obrazu (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8184f-107">You can enable your users to automatically get signed-on to Image Relay (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8184f-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="8184f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8184f-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8184f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8184f-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8184f-110">Prerequisites</span></span>

<span data-ttu-id="8184f-111">Aby skonfigurować integrację usługi Azure AD z obrazu przekazywania, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="8184f-111">To configure Azure AD integration with Image Relay, you need the following items:</span></span>

- <span data-ttu-id="8184f-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8184f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8184f-113">Obraz przekazywania logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="8184f-113">An Image Relay single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8184f-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="8184f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8184f-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="8184f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8184f-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="8184f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8184f-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8184f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8184f-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="8184f-118">Scenario description</span></span>
<span data-ttu-id="8184f-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="8184f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8184f-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="8184f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8184f-121">Dodawanie obrazu przekazywania z galerii</span><span class="sxs-lookup"><span data-stu-id="8184f-121">Adding Image Relay from the gallery</span></span>
2. <span data-ttu-id="8184f-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="8184f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-image-relay-from-the-gallery"></a><span data-ttu-id="8184f-123">Dodawanie obrazu przekazywania z galerii</span><span class="sxs-lookup"><span data-stu-id="8184f-123">Adding Image Relay from the gallery</span></span>
<span data-ttu-id="8184f-124">Aby skonfigurować integrację usługi Azure AD przekazywania obrazu, należy dodać przekazywania obraz w galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="8184f-124">To configure the integration of Image Relay into Azure AD, you need to add Image Relay from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8184f-125">**Aby dodać przekazywania obraz w galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="8184f-125">**To add Image Relay from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8184f-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="8184f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="8184f-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="8184f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8184f-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="8184f-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="8184f-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8184f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="8184f-133">W polu wyszukiwania wpisz **przekazywania obrazu**.</span><span class="sxs-lookup"><span data-stu-id="8184f-133">In the search box, type **Image Relay**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_search.png)

5. <span data-ttu-id="8184f-135">W panelu wyników wybierz **przekazywania obrazu**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="8184f-135">In the results panel, select **Image Relay**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8184f-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="8184f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8184f-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z przekaźnika obraz w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="8184f-138">In this section, you configure and test Azure AD single sign-on with Image Relay based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8184f-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w przekazywania obrazu jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8184f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Image Relay is to a user in Azure AD.</span></span> <span data-ttu-id="8184f-140">Innymi słowy musi można ustanowić łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w przekazywania obrazu.</span><span class="sxs-lookup"><span data-stu-id="8184f-140">In other words, a link relationship between an Azure AD user and the related user in Image Relay needs to be established.</span></span>

<span data-ttu-id="8184f-141">W przekazywania obrazu, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="8184f-141">In Image Relay, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8184f-142">Do konfigurowania i testowania usługi Azure AD rejestracji jednokrotnej z przekaźnika obrazu, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="8184f-142">To configure and test Azure AD single sign-on with Image Relay, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8184f-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="8184f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8184f-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="8184f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8184f-145">**[Tworzenie użytkownika testowego przekazywania obrazu](#creating-an-image-relay-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Relay obrazu jest połączony z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8184f-145">**[Creating an Image Relay test user](#creating-an-image-relay-test-user)** - to have a counterpart of Britta Simon in Image Relay that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8184f-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="8184f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8184f-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="8184f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8184f-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8184f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8184f-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji przekaźnika obrazu.</span><span class="sxs-lookup"><span data-stu-id="8184f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Image Relay application.</span></span>

<span data-ttu-id="8184f-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z obrazu przekazywania, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="8184f-150">**To configure Azure AD single sign-on with Image Relay, perform the following steps:**</span></span>

1. <span data-ttu-id="8184f-151">W portalu Azure na **przekazywania obrazu** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="8184f-151">In the Azure portal, on the **Image Relay** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="8184f-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="8184f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_samlbase.png)

3. <span data-ttu-id="8184f-155">Na **obrazu przekazywania domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="8184f-155">On the **Image Relay Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_url.png)

    <span data-ttu-id="8184f-157">a.</span><span class="sxs-lookup"><span data-stu-id="8184f-157">a.</span></span> <span data-ttu-id="8184f-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.imagerelay.com/`</span><span class="sxs-lookup"><span data-stu-id="8184f-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.imagerelay.com/`</span></span>

    <span data-ttu-id="8184f-159">b.</span><span class="sxs-lookup"><span data-stu-id="8184f-159">b.</span></span> <span data-ttu-id="8184f-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.imagerelay.com/sso/metadata`</span><span class="sxs-lookup"><span data-stu-id="8184f-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.imagerelay.com/sso/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8184f-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="8184f-161">These values are not real.</span></span> <span data-ttu-id="8184f-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="8184f-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8184f-163">Skontaktuj się z [zespołem pomocy technicznej klienta przekazywania obrazu](http://support.imagerelay.com/) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="8184f-163">Contact [Image Relay Client support team](http://support.imagerelay.com/) to get these values.</span></span> 
 


4. <span data-ttu-id="8184f-164">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="8184f-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_certificate.png) 

5. <span data-ttu-id="8184f-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8184f-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8184f-168">Na **Konfiguracja przekazywania obrazu** , kliknij przycisk **Konfigurowanie przekazywania obrazu** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="8184f-168">On the **Image Relay Configuration** section, click **Configure Image Relay** to open **Configure sign-on** window.</span></span> <span data-ttu-id="8184f-169">Kopiuj **Sign-Out adres URL usługi i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="8184f-169">Copy the **Sign-Out Service URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_configure.png) 

7. <span data-ttu-id="8184f-171">W innym oknie przeglądarki należy zalogować się jako administrator do witryny firmy przekazywania obrazu.</span><span class="sxs-lookup"><span data-stu-id="8184f-171">In another browser window, sign in to your Image Relay company site as an administrator.</span></span>

8. <span data-ttu-id="8184f-172">Na pasku narzędzi u góry kliknij **użytkowników i uprawnienia** obciążenia.</span><span class="sxs-lookup"><span data-stu-id="8184f-172">In the toolbar on the top, click the **Users & Permissions** workload.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_06.png) 

9. <span data-ttu-id="8184f-174">Kliknij przycisk **utworzyć nowe uprawnienie**.</span><span class="sxs-lookup"><span data-stu-id="8184f-174">Click **Create New Permission**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_08.png)

10. <span data-ttu-id="8184f-176">W **pojedynczy znak na ustawienia** obciążenie, wybierz opcję **tej grupie można tylko logowania za pomocą rejestracji jednokrotnej** pole wyboru, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="8184f-176">In the **Single Sign On Settings** workload, select the **This Group can only sign-in via Single Sign On** check box, and then click **Save**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_09.png) 

11. <span data-ttu-id="8184f-178">Przejdź do **ustawienia konta**.</span><span class="sxs-lookup"><span data-stu-id="8184f-178">Go to **Account Settings**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_10.png) 

12. <span data-ttu-id="8184f-180">Przejdź do **pojedynczy znak na ustawienia** obciążenia.</span><span class="sxs-lookup"><span data-stu-id="8184f-180">Go to the **Single Sign On Settings** workload.</span></span>
    
     ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_11.png)

13. <span data-ttu-id="8184f-182">Na **ustawienia SAML** okna dialogowego, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="8184f-182">On the **SAML Settings** dialog, perform the following steps:</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_12.png)
    
    <span data-ttu-id="8184f-184">a.</span><span class="sxs-lookup"><span data-stu-id="8184f-184">a.</span></span> <span data-ttu-id="8184f-185">W **adres URL logowania** pole tekstowe, Wklej wartość **pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="8184f-185">In **Login URL** textbox, paste the value of **Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="8184f-186">b.</span><span class="sxs-lookup"><span data-stu-id="8184f-186">b.</span></span> <span data-ttu-id="8184f-187">W **adresu URL wylogowania** pole tekstowe, Wklej wartość **pojedynczy adres URL usługi Sign-Out** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="8184f-187">In **Logout URL**  textbox, paste the value of **Single Sign-Out Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="8184f-188">c.</span><span class="sxs-lookup"><span data-stu-id="8184f-188">c.</span></span> <span data-ttu-id="8184f-189">Jako **Format identyfikatora nazwy**, wybierz pozycję **urn: oasis: nazwy: tc: SAML:1.1:nameid-format: emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="8184f-189">As **Name Id Format**, select **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="8184f-190">d.</span><span class="sxs-lookup"><span data-stu-id="8184f-190">d.</span></span> <span data-ttu-id="8184f-191">Jako **powiązanie opcje żądania od dostawcy usług (obraz przekazywania)**, wybierz pozycję **powiązanie POST**.</span><span class="sxs-lookup"><span data-stu-id="8184f-191">As **Binding Options for Requests from the Service Provider (Image Relay)**, select **POST Binding**.</span></span>

    <span data-ttu-id="8184f-192">e.</span><span class="sxs-lookup"><span data-stu-id="8184f-192">e.</span></span> <span data-ttu-id="8184f-193">W obszarze **certyfikatu x.509**, kliknij przycisk **certyfikatu aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="8184f-193">Under **x.509 Certificate**, click **Update Certificate**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_17.png)

    <span data-ttu-id="8184f-195">f.</span><span class="sxs-lookup"><span data-stu-id="8184f-195">f.</span></span> <span data-ttu-id="8184f-196">Otwórz w Notatniku pobranego certyfikatu, skopiuj zawartość, a następnie wklej go w polu tekstowym certyfikatu x.509.</span><span class="sxs-lookup"><span data-stu-id="8184f-196">Open the downloaded certificate in notepad, copy the content, and then paste it into the x.509 Certificate textbox.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_18.png)

    <span data-ttu-id="8184f-198">g.</span><span class="sxs-lookup"><span data-stu-id="8184f-198">g.</span></span> <span data-ttu-id="8184f-199">W **Inicjowanie obsługi użytkowników just in Time** zaznacz **włączyć just in Time Inicjowanie obsługi użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="8184f-199">In **Just-In-Time User Provisioning** section, select the **Enable Just-In-Time User Provisioning**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_19.png)

    <span data-ttu-id="8184f-201">h.</span><span class="sxs-lookup"><span data-stu-id="8184f-201">h.</span></span> <span data-ttu-id="8184f-202">Wybierz grupę uprawnienia (na przykład **logowania jednokrotnego podstawowe**) który jest zezwolenia na logowanie tylko za pośrednictwem rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="8184f-202">Select the permission group (for example, **SSO Basic**) which is allowed to sign in only through single sign-on.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_20.png)

    <span data-ttu-id="8184f-204">i.</span><span class="sxs-lookup"><span data-stu-id="8184f-204">i.</span></span> <span data-ttu-id="8184f-205">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="8184f-205">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="8184f-206">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="8184f-206">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8184f-207">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="8184f-207">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8184f-208">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8184f-208">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8184f-209">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8184f-209">Creating an Azure AD test user</span></span>
<span data-ttu-id="8184f-210">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="8184f-210">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="8184f-212">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="8184f-212">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8184f-213">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="8184f-213">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8184f-215">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="8184f-215">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8184f-217">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8184f-217">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8184f-219">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="8184f-219">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8184f-221">a.</span><span class="sxs-lookup"><span data-stu-id="8184f-221">a.</span></span> <span data-ttu-id="8184f-222">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8184f-222">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8184f-223">b.</span><span class="sxs-lookup"><span data-stu-id="8184f-223">b.</span></span> <span data-ttu-id="8184f-224">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8184f-224">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8184f-225">c.</span><span class="sxs-lookup"><span data-stu-id="8184f-225">c.</span></span> <span data-ttu-id="8184f-226">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="8184f-226">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8184f-227">d.</span><span class="sxs-lookup"><span data-stu-id="8184f-227">d.</span></span> <span data-ttu-id="8184f-228">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="8184f-228">Click **Create**.</span></span>
 
### <a name="creating-an-image-relay-test-user"></a><span data-ttu-id="8184f-229">Tworzenie użytkownika testowego przekazywania obrazu</span><span class="sxs-lookup"><span data-stu-id="8184f-229">Creating an Image Relay test user</span></span>

<span data-ttu-id="8184f-230">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w przekazywania obrazu.</span><span class="sxs-lookup"><span data-stu-id="8184f-230">The objective of this section is to create a user called Britta Simon in Image Relay.</span></span>

<span data-ttu-id="8184f-231">**Aby utworzyć użytkownika o nazwie Simona Britta w przekazywania obrazu, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="8184f-231">**To create a user called Britta Simon in Image Relay, perform the following steps:**</span></span>

1. <span data-ttu-id="8184f-232">Logowanie do przekazywania obrazu witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="8184f-232">Sign-on to your Image Relay company site as an administrator.</span></span>

2. <span data-ttu-id="8184f-233">Przejdź do **użytkowników i uprawnienia** i wybierz **Tworzenie użytkownika logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="8184f-233">Go to **Users & Permissions**     and select **Create SSO User**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_21.png) 

3. <span data-ttu-id="8184f-235">Wprowadź **E-mail**, **imię**, **nazwisko**, i **firmy** użytkownika chcesz udostępnić, a następnie wybierz grupę uprawnień, (na przykład logowania jednokrotnego podstawowe) jest grupa, który można zalogować się tylko za pośrednictwem rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="8184f-235">Enter the **Email**, **First Name**, **Last Name**, and **Company** of the user you want to provision and select the permission group (for example, SSO Basic) which is the group that can sign in only through single sign-on.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_22.png) 

4. <span data-ttu-id="8184f-237">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="8184f-237">Click **Create**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8184f-238">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8184f-238">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8184f-239">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do obrazu przekaźnika.</span><span class="sxs-lookup"><span data-stu-id="8184f-239">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Image Relay.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="8184f-241">**Aby przypisać Simona Britta do przekazywania obraz, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="8184f-241">**To assign Britta Simon to Image Relay, perform the following steps:**</span></span>

1. <span data-ttu-id="8184f-242">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="8184f-242">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="8184f-244">Na liście aplikacji zaznacz **przekazywania obrazu**.</span><span class="sxs-lookup"><span data-stu-id="8184f-244">In the applications list, select **Image Relay**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_app.png) 

3. <span data-ttu-id="8184f-246">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="8184f-246">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="8184f-248">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8184f-248">Click **Add** button.</span></span> <span data-ttu-id="8184f-249">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8184f-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="8184f-251">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="8184f-251">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8184f-252">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8184f-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8184f-253">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8184f-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8184f-254">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8184f-254">Testing single sign-on</span></span>

<span data-ttu-id="8184f-255">Celem tej sekcji służy do testowania konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="8184f-255">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>    

<span data-ttu-id="8184f-256">Po kliknięciu kafelka przekazywania obrazu w panelu dostępu należy należy pobrać automatycznie zalogowane do aplikacji przekaźnika obrazu.</span><span class="sxs-lookup"><span data-stu-id="8184f-256">When you click the Image Relay tile in the Access Panel, you should get automatically signed-on to your Image Relay application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="8184f-257">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="8184f-257">Additional resources</span></span>

* [<span data-ttu-id="8184f-258">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8184f-258">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8184f-259">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8184f-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_04.png


[100]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_203.png

