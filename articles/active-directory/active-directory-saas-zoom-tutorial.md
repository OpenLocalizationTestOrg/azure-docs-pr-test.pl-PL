---
title: "Samouczek: Integracji Azure Active Directory z powiększenia | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i powiększenia."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0ebdab6c-83a8-4737-a86a-974f37269c31
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: aab491f162fd4d24c6ff4d8858f2edd96dda30d4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zoom"></a><span data-ttu-id="ed8a4-103">Samouczek: Integracji Azure Active Directory z powiększenia</span><span class="sxs-lookup"><span data-stu-id="ed8a4-103">Tutorial: Azure Active Directory integration with Zoom</span></span>

<span data-ttu-id="ed8a4-104">Z tego samouczka dowiesz się integrowanie powiększenia w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ed8a4-104">In this tutorial, you learn how to integrate Zoom with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ed8a4-105">Integracja z usługą Azure AD powiększenia zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="ed8a4-105">Integrating Zoom with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ed8a4-106">Można kontrolować w usłudze Azure AD, który ma dostęp do powiększenia.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-106">You can control in Azure AD who has access to Zoom.</span></span>
- <span data-ttu-id="ed8a4-107">Umożliwia użytkownikom automatycznie pobrać zalogowane powiększenie (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-107">You can enable your users to automatically get signed-on to Zoom (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="ed8a4-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="ed8a4-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ed8a4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ed8a4-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ed8a4-110">Prerequisites</span></span>

<span data-ttu-id="ed8a4-111">Aby skonfigurować integrację usługi Azure AD z powiększenia, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="ed8a4-111">To configure Azure AD integration with Zoom, you need the following items:</span></span>

- <span data-ttu-id="ed8a4-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed8a4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ed8a4-113">Powiększenie logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="ed8a4-113">A Zoom single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ed8a4-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ed8a4-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="ed8a4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ed8a4-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ed8a4-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ed8a4-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ed8a4-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="ed8a4-118">Scenario description</span></span>
<span data-ttu-id="ed8a4-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ed8a4-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="ed8a4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ed8a4-121">Dodawanie powiększenia z galerii</span><span class="sxs-lookup"><span data-stu-id="ed8a4-121">Adding Zoom from the gallery</span></span>
2. <span data-ttu-id="ed8a4-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="ed8a4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zoom-from-the-gallery"></a><span data-ttu-id="ed8a4-123">Dodawanie powiększenia z galerii</span><span class="sxs-lookup"><span data-stu-id="ed8a4-123">Adding Zoom from the gallery</span></span>
<span data-ttu-id="ed8a4-124">Aby skonfigurować integrację powiększenia do usługi Azure AD, należy dodać powiększenia z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-124">To configure the integration of Zoom into Azure AD, you need to add Zoom from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ed8a4-125">**Aby dodać powiększenia z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="ed8a4-125">**To add Zoom from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ed8a4-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Przycisk usługi Azure Active Directory][1]

2. <span data-ttu-id="ed8a4-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ed8a4-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-129">Then go to **All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa][2]
    
3. <span data-ttu-id="ed8a4-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Nowy przycisk aplikacji][3]

4. <span data-ttu-id="ed8a4-133">W polu wyszukiwania wpisz **powiększenie**, wybierz pozycję **powiększenie** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-133">In the search box, type **Zoom**, select **Zoom** from result panel then click **Add** button to add the application.</span></span>

    ![Powiększenie na liście wyników](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ed8a4-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ed8a4-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="ed8a4-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z powiększenia w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-136">In this section, you configure and test Azure AD single sign-on with Zoom based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ed8a4-137">Do rejestracji jednokrotnej do pracy usługi Azure AD musi ustalić użytkownika odpowiednika w powiększenia do użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Zoom is to a user in Azure AD.</span></span> <span data-ttu-id="ed8a4-138">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w powiększenia musi się.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-138">In other words, a link relationship between an Azure AD user and the related user in Zoom needs to be established.</span></span>

<span data-ttu-id="ed8a4-139">Powiększenie, przypisywanie wartości **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-139">In Zoom, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ed8a4-140">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z powiększenia, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="ed8a4-140">To configure and test Azure AD single sign-on with Zoom, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ed8a4-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ed8a4-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ed8a4-143">**[Tworzenie użytkownika testowego powiększenia](#create-a-zoom-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta powiększenia połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-143">**[Create a Zoom test user](#create-a-zoom-test-user)** - to have a counterpart of Britta Simon in Zoom that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ed8a4-144">**[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ed8a4-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="ed8a4-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ed8a4-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="ed8a4-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji powiększenia.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zoom application.</span></span>

<span data-ttu-id="ed8a4-148">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z powiększenia, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="ed8a4-148">**To configure Azure AD single sign-on with Zoom, perform the following steps:**</span></span>

1. <span data-ttu-id="ed8a4-149">W portalu Azure na **powiększenie** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-149">In the Azure portal, on the **Zoom** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="ed8a4-151">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_samlbase.png)

3. <span data-ttu-id="ed8a4-153">Na **powiększenie domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ed8a4-153">On the **Zoom Domain and URLs** section, perform the following steps:</span></span>

    ![Adresy URL i powiększenia domeny pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_url.png)

    <span data-ttu-id="ed8a4-155">a.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-155">a.</span></span> <span data-ttu-id="ed8a4-156">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.zoom.us`</span><span class="sxs-lookup"><span data-stu-id="ed8a4-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.zoom.us`</span></span>

    <span data-ttu-id="ed8a4-157">b.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-157">b.</span></span> <span data-ttu-id="ed8a4-158">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.zoom.us`</span><span class="sxs-lookup"><span data-stu-id="ed8a4-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.zoom.us`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ed8a4-159">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-159">These values are not real.</span></span> <span data-ttu-id="ed8a4-160">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="ed8a4-161">Skontaktuj się z [zespołem pomocy technicznej klienta powiększenie](https://support.zoom.us/hc) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-161">Contact [Zoom Client support team](https://support.zoom.us/hc) to get these values.</span></span> 
 
4. <span data-ttu-id="ed8a4-162">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-162">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Łącze pobierania certyfikatu](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_certificate.png) 

5. <span data-ttu-id="ed8a4-164">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-164">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-zoom-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ed8a4-166">Na **powiększenie konfiguracji** , kliknij przycisk **skonfigurować powiększenie** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-166">On the **Zoom Configuration** section, click **Configure Zoom** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ed8a4-167">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="ed8a4-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfiguracja powiększenia](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_configure.png) 

7. <span data-ttu-id="ed8a4-169">W oknie przeglądarki innej witryny sieci web należy zalogować się jako administrator do witryny firmy powiększenia.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-169">In a different web browser window, log in to your Zoom company site as an administrator.</span></span>

8. <span data-ttu-id="ed8a4-170">Kliknij przycisk **rejestracji jednokrotnej** kartę.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-170">Click the **Single Sign-On** tab.</span></span>
   
    <span data-ttu-id="ed8a4-171">![Karta rejestracji jednokrotnej](./media/active-directory-saas-zoom-tutorial/IC784700.png "logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="ed8a4-171">![Single sign-on tab](./media/active-directory-saas-zoom-tutorial/IC784700.png "Single sign-on")</span></span>

9. <span data-ttu-id="ed8a4-172">Kliknij przycisk **zabezpieczeniem** karcie, a następnie przejdź do **rejestracji jednokrotnej** ustawienia.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-172">Click the **Security Control** tab, and then go to the **Single Sign-On** settings.</span></span>

10. <span data-ttu-id="ed8a4-173">W sekcji rejestracji jednokrotnej wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ed8a4-173">In the Single Sign-On section, perform the following steps:</span></span>
   
    <span data-ttu-id="ed8a4-174">![Pojedynczy znak w sekcji](./media/active-directory-saas-zoom-tutorial/IC784701.png "logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="ed8a4-174">![Single sign-on section](./media/active-directory-saas-zoom-tutorial/IC784701.png "Single sign-on")</span></span>
   
    <span data-ttu-id="ed8a4-175">a.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-175">a.</span></span> <span data-ttu-id="ed8a4-176">W **adres URL logowania strony** pole tekstowe, Wklej wartość **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-176">In the **Sign-in page URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="ed8a4-177">b.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-177">b.</span></span> <span data-ttu-id="ed8a4-178">W **adres URL strony wylogowania** pole tekstowe, Wklej wartość **Sign-Out URL**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-178">In the **Sign-out page URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
     
    <span data-ttu-id="ed8a4-179">c.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-179">c.</span></span> <span data-ttu-id="ed8a4-180">Otwórz w Notatniku certyfikatu zakodowanego base-64, skopiuj zawartość go do Schowka, a następnie wklej go do **certyfikat dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-180">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Identity provider certificate** textbox.</span></span>

    <span data-ttu-id="ed8a4-181">d.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-181">d.</span></span> <span data-ttu-id="ed8a4-182">W **wystawcy** pole tekstowe, Wklej wartość **identyfikator jednostki SAML**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-182">In the **Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="ed8a4-183">e.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-183">e.</span></span> <span data-ttu-id="ed8a4-184">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-184">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="ed8a4-185">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="ed8a4-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ed8a4-186">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ed8a4-187">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ed8a4-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ed8a4-188">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed8a4-188">Create an Azure AD test user</span></span>

<span data-ttu-id="ed8a4-189">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="ed8a4-191">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="ed8a4-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ed8a4-192">W portalu Azure, w okienku po lewej stronie kliknij **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-192">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Przycisk usługi Azure Active Directory](./media/active-directory-saas-zoom-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="ed8a4-194">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-194">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-zoom-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="ed8a4-196">Aby otworzyć **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** w górnej części **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-196">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Przycisk Dodaj](./media/active-directory-saas-zoom-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="ed8a4-198">W **użytkownika** okna dialogowego wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ed8a4-198">In the **User** dialog box, perform the following steps:</span></span>

    ![Okno dialogowe użytkownika](./media/active-directory-saas-zoom-tutorial/create_aaduser_04.png)

    <span data-ttu-id="ed8a4-200">a.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-200">a.</span></span> <span data-ttu-id="ed8a4-201">W **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-201">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ed8a4-202">b.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-202">b.</span></span> <span data-ttu-id="ed8a4-203">W **nazwy użytkownika** wpisz adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-203">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="ed8a4-204">c.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-204">c.</span></span> <span data-ttu-id="ed8a4-205">Wybierz **Pokaż hasło** pole wyboru, a następnie zanotuj wartość, która jest wyświetlana w **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-205">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="ed8a4-206">d.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-206">d.</span></span> <span data-ttu-id="ed8a4-207">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-207">Click **Create**.</span></span>
 
### <a name="create-a-zoom-test-user"></a><span data-ttu-id="ed8a4-208">Tworzenie użytkownika testowego powiększenia</span><span class="sxs-lookup"><span data-stu-id="ed8a4-208">Create a Zoom test user</span></span>

<span data-ttu-id="ed8a4-209">Aby umożliwić użytkownikom zalogować się do powiększenia usługi Azure AD, musi być przygotowana do powiększenia.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-209">In order to enable Azure AD users to log in to Zoom, they must be provisioned into Zoom.</span></span> <span data-ttu-id="ed8a4-210">W przypadku powiększenia Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-210">In the case of Zoom, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="ed8a4-211">Aby udostępnić konta użytkownika, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ed8a4-211">To provision a user account, perform the following steps:</span></span>

1. <span data-ttu-id="ed8a4-212">Zaloguj się do Twojego **powiększenie** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-212">Log in to your **Zoom** company site as an administrator.</span></span>
 
2. <span data-ttu-id="ed8a4-213">Kliknij przycisk **zarządzania kontami** , a następnie kliknij pozycję **Zarządzanie użytkownikami**.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-213">Click the **Account Management** tab, and then click **User Management**.</span></span>

3. <span data-ttu-id="ed8a4-214">W sekcji Zarządzanie użytkownikami kliknij **dodawania użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-214">In the User Management section, click **Add users**.</span></span>
   
    <span data-ttu-id="ed8a4-215">![Zarządzanie użytkownikami](./media/active-directory-saas-zoom-tutorial/IC784703.png "Zarządzanie użytkownikami")</span><span class="sxs-lookup"><span data-stu-id="ed8a4-215">![User management](./media/active-directory-saas-zoom-tutorial/IC784703.png "User management")</span></span>

4. <span data-ttu-id="ed8a4-216">Na **dodawania użytkowników** wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ed8a4-216">On the **Add users** page, perform the following steps:</span></span>
   
    <span data-ttu-id="ed8a4-217">![Dodawanie użytkowników](./media/active-directory-saas-zoom-tutorial/IC784704.png "Dodawanie użytkowników")</span><span class="sxs-lookup"><span data-stu-id="ed8a4-217">![Add users](./media/active-directory-saas-zoom-tutorial/IC784704.png "Add users")</span></span>
   
    <span data-ttu-id="ed8a4-218">a.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-218">a.</span></span> <span data-ttu-id="ed8a4-219">Jako **typ użytkownika**, wybierz pozycję **podstawowe**.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-219">As **User Type**, select **Basic**.</span></span>

    <span data-ttu-id="ed8a4-220">b.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-220">b.</span></span> <span data-ttu-id="ed8a4-221">W **wiadomości E-mail** tekstowym, wpisz adres e-mail prawidłowe usługi Azure AD konto ma chcesz udostępnić.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-221">In the **Emails** textbox, type the email address of a valid Azure AD account you want to provision.</span></span>

    <span data-ttu-id="ed8a4-222">c.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-222">c.</span></span> <span data-ttu-id="ed8a4-223">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-223">Click **Add**.</span></span>

> [!NOTE]
> <span data-ttu-id="ed8a4-224">Możesz użyć innych powiększenia użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez powiększenia do świadczenia usługi Azure Active Directory kont użytkowników.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-224">You can use any other Zoom user account creation tools or APIs provided by Zoom to provision Azure Active Directory user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="ed8a4-225">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed8a4-225">Assign the Azure AD test user</span></span>

<span data-ttu-id="ed8a4-226">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do powiększenia.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zoom.</span></span>

![Przypisanie roli użytkownika][200] 

<span data-ttu-id="ed8a4-228">**Aby przypisać powiększenia Simona Britta, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="ed8a4-228">**To assign Britta Simon to Zoom, perform the following steps:**</span></span>

1. <span data-ttu-id="ed8a4-229">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="ed8a4-231">Na liście aplikacji zaznacz **powiększenie**.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-231">In the applications list, select **Zoom**.</span></span>

    ![Łącze powiększenia na liście aplikacji](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_app.png)  

3. <span data-ttu-id="ed8a4-233">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-233">In the menu on the left, click **Users and groups**.</span></span>

    ![Łącze "Użytkownicy i grupy"][202]

4. <span data-ttu-id="ed8a4-235">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-235">Click **Add** button.</span></span> <span data-ttu-id="ed8a4-236">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![W okienku Dodaj przydziału][203]

5. <span data-ttu-id="ed8a4-238">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ed8a4-239">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ed8a4-240">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="ed8a4-241">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ed8a4-241">Test single sign-on</span></span>

<span data-ttu-id="ed8a4-242">Celem tej sekcji służy do testowania konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-242">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ed8a4-243">Po kliknięciu kafelka powiększenia w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji powiększenia.</span><span class="sxs-lookup"><span data-stu-id="ed8a4-243">When you click the Zoom tile in the Access Panel, you should get automatically signed-on to your Zoom application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ed8a4-244">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="ed8a4-244">Additional resources</span></span>

* [<span data-ttu-id="ed8a4-245">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ed8a4-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ed8a4-246">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ed8a4-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_203.png

