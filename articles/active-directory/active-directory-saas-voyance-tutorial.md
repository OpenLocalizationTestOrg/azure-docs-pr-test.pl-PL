---
title: 'Samouczek: Integracji Azure Active Directory z Voyance | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Voyance."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 539dc1f9-64c9-4dce-b259-2b0b49dcf857
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2017
ms.author: jeedes
ms.openlocfilehash: e860b810904fb7972d75d55d913d5622ff9a406a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-voyance"></a><span data-ttu-id="73821-103">Samouczek: Integracji Azure Active Directory z Voyance</span><span class="sxs-lookup"><span data-stu-id="73821-103">Tutorial: Azure Active Directory integration with Voyance</span></span>

<span data-ttu-id="73821-104">Z tego samouczka dowiesz się integrowanie Voyance z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="73821-104">In this tutorial, you learn how to integrate Voyance with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="73821-105">Integracja z usługą Azure AD Voyance zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="73821-105">Integrating Voyance with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="73821-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Voyance</span><span class="sxs-lookup"><span data-stu-id="73821-106">You can control in Azure AD who has access to Voyance</span></span>
- <span data-ttu-id="73821-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Voyance (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="73821-107">You can enable your users to automatically get signed-on to Voyance (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="73821-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="73821-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="73821-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="73821-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="73821-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="73821-110">Prerequisites</span></span>

<span data-ttu-id="73821-111">Aby skonfigurować integrację usługi Azure AD z Voyance, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="73821-111">To configure Azure AD integration with Voyance, you need the following items:</span></span>

- <span data-ttu-id="73821-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="73821-112">An Azure AD subscription</span></span>
- <span data-ttu-id="73821-113">Voyance logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="73821-113">A Voyance single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="73821-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="73821-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="73821-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="73821-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="73821-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="73821-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="73821-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="73821-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="73821-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="73821-118">Scenario description</span></span>
<span data-ttu-id="73821-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="73821-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="73821-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="73821-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="73821-121">Dodawanie Voyance z galerii</span><span class="sxs-lookup"><span data-stu-id="73821-121">Adding Voyance from the gallery</span></span>
2. <span data-ttu-id="73821-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="73821-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-voyance-from-the-gallery"></a><span data-ttu-id="73821-123">Dodawanie Voyance z galerii</span><span class="sxs-lookup"><span data-stu-id="73821-123">Adding Voyance from the gallery</span></span>
<span data-ttu-id="73821-124">Aby skonfigurować integrację usługi Azure AD Voyance, należy dodać Voyance z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="73821-124">To configure the integration of Voyance into Azure AD, you need to add Voyance from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="73821-125">**Aby dodać Voyance z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="73821-125">**To add Voyance from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="73821-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="73821-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Przycisk usługi Azure Active Directory][1]

2. <span data-ttu-id="73821-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="73821-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="73821-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="73821-129">Then go to **All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa][2]
    
3. <span data-ttu-id="73821-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="73821-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Nowy przycisk aplikacji][3]

4. <span data-ttu-id="73821-133">W polu wyszukiwania wpisz **Voyance**, wybierz pozycję **Voyance** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="73821-133">In the search box, type **Voyance**, select  **Voyance**  from result panel then click **Add** button to add the application.</span></span>

    ![Voyance na liście wyników](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="73821-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="73821-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="73821-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Voyance w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="73821-136">In this section, you configure and test Azure AD single sign-on with Voyance based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="73821-137">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Voyance jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="73821-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Voyance is to a user in Azure AD.</span></span> <span data-ttu-id="73821-138">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Voyance musi się.</span><span class="sxs-lookup"><span data-stu-id="73821-138">In other words, a link relationship between an Azure AD user and the related user in Voyance needs to be established.</span></span>

<span data-ttu-id="73821-139">W Voyance, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="73821-139">In Voyance, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="73821-140">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Voyance, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="73821-140">To configure and test Azure AD single sign-on with Voyance, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="73821-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="73821-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="73821-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="73821-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="73821-143">**[Tworzenie użytkownika testowego Voyance](#create-a-voyance-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Voyance połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="73821-143">**[Create a Voyance test user](#create-a-voyance-test-user)** - to have a counterpart of Britta Simon in Voyance that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="73821-144">**[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="73821-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="73821-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="73821-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="73821-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="73821-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="73821-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Voyance.</span><span class="sxs-lookup"><span data-stu-id="73821-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Voyance application.</span></span>

<span data-ttu-id="73821-148">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Voyance, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="73821-148">**To configure Azure AD single sign-on with Voyance, perform the following steps:**</span></span>

1. <span data-ttu-id="73821-149">W portalu Azure na **Voyance** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="73821-149">In the Azure portal, on the **Voyance** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="73821-151">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="73821-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_samlbase.png)

3. <span data-ttu-id="73821-153">Na **Voyance domeny i adres URL** sekcji, wykonaj następujące kroki, aby skonfigurować aplikację w **IDP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="73821-153">On the **Voyance Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Adresy URL i domeny Voyance pojedynczy informacje logowania dla dostawców tożsamości](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_url1.png)

    <span data-ttu-id="73821-155">a.</span><span class="sxs-lookup"><span data-stu-id="73821-155">a.</span></span> <span data-ttu-id="73821-156">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.nyansa.com`</span><span class="sxs-lookup"><span data-stu-id="73821-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.nyansa.com`</span></span>

    <span data-ttu-id="73821-157">b.</span><span class="sxs-lookup"><span data-stu-id="73821-157">b.</span></span> <span data-ttu-id="73821-158">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.nyansa.com/saml/create/`</span><span class="sxs-lookup"><span data-stu-id="73821-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.nyansa.com/saml/create/`</span></span>

4. <span data-ttu-id="73821-159">Sprawdź **Pokaż zaawansowane ustawienia adresu URL** i wykonać następujący krok, jeśli chcesz skonfigurować aplikację w **SP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="73821-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Adresy URL i domeny Voyance pojedynczy informacje logowania dla dostawcy](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_url2.png)

    <span data-ttu-id="73821-161">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.nyansa.com/`</span><span class="sxs-lookup"><span data-stu-id="73821-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.nyansa.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="73821-162">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="73821-162">These values are not real.</span></span> <span data-ttu-id="73821-163">Rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="73821-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="73821-164">Skontaktuj się z [zespołem pomocy technicznej klienta Voyance](mailto:support@nyansa.com) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="73821-164">Contact [Voyance Client support team](mailto:support@nyansa.com) to get these values.</span></span> 

5. <span data-ttu-id="73821-165">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="73821-165">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Łącze pobierania certyfikatu](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_certificate.png) 

6. <span data-ttu-id="73821-167">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="73821-167">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-voyance-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="73821-169">Na **konfiguracji Voyance** , kliknij przycisk **skonfigurować Voyance** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="73821-169">On the **Voyance Configuration** section, click **Configure Voyance** to open **Configure sign-on** window.</span></span> <span data-ttu-id="73821-170">Kopiuj **SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="73821-170">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfiguracja Voyance](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_configure.png) 

8. <span data-ttu-id="73821-172">W oknie przeglądarki innej witryny sieci web logowanie do dzierżawy Voyance jako administrator.</span><span class="sxs-lookup"><span data-stu-id="73821-172">In a different web browser window, sign-on to your Voyance tenant as an administrator.</span></span>

9. <span data-ttu-id="73821-173">Przejdź do prawym górnym rogu paska nawigacji i kliknij listę rozwijaną informujący "**University xyz**".</span><span class="sxs-lookup"><span data-stu-id="73821-173">Go to the top right corner of the navigation bar and click on the drop-down that says "**Acme University**".</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej w aplikacji po stronie xyz University](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_001.png) 

10. <span data-ttu-id="73821-175">Kliknij przycisk "**ustawienia administratora**".</span><span class="sxs-lookup"><span data-stu-id="73821-175">Click "**Admin Settings**".</span></span>

    ![Konfigurowanie rejestracji jednokrotnej ustawieniami aplikacji po stronie administratora](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_002.png)

11. <span data-ttu-id="73821-177">Kliknij przycisk "**dostępu użytkownika**" kartę.</span><span class="sxs-lookup"><span data-stu-id="73821-177">Click "**User Access**" tab.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej na dostęp do aplikacji po stronie użytkownika](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_003.png)

12. <span data-ttu-id="73821-179">Kliknij przycisk "**wyłączeniu logowania jednokrotnego**" przycisk, aby skonfigurować usługi Azure AD jako dostawca tożsamości przy użyciu SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="73821-179">Click the "**SSO is disabled**" button to configure Azure AD as an IdP using SAML 2.0.</span></span>

    ![Konfigurowanie jednego logowania w aplikacji po stronie rejestracji Jednokrotnej jest wyłączony przycisk](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_004.png)

13. <span data-ttu-id="73821-181">Przejdź do **SAML v2** sekcji i wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="73821-181">Go to **SAML v2** section and perform below steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej w aplikacji po stronie SAML v2](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_005.png)
    
    <span data-ttu-id="73821-183">a.</span><span class="sxs-lookup"><span data-stu-id="73821-183">a.</span></span> <span data-ttu-id="73821-184">Wybierz **włączone**.</span><span class="sxs-lookup"><span data-stu-id="73821-184">Select **Enabled**.</span></span>
    
    <span data-ttu-id="73821-185">b.</span><span class="sxs-lookup"><span data-stu-id="73821-185">b.</span></span> <span data-ttu-id="73821-186">Wklej **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure do **adres URL logowania IdP** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="73821-186">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal Into the **IdP Login URL** textbox.</span></span>

    <span data-ttu-id="73821-187">c.</span><span class="sxs-lookup"><span data-stu-id="73821-187">c.</span></span> <span data-ttu-id="73821-188">Otwórz w Notatniku z pobranego certyfikatu szyfrowania Base64, skopiuj zawartość go do Schowka, a następnie wklej go do **IdP Cert** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="73821-188">Open your downloaded Base64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **IdP Cert** textbox.</span></span>
    
    <span data-ttu-id="73821-189">d.</span><span class="sxs-lookup"><span data-stu-id="73821-189">d.</span></span> <span data-ttu-id="73821-190">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="73821-190">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="73821-191">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="73821-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="73821-192">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="73821-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="73821-193">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="73821-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="73821-194">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="73821-194">Create an Azure AD test user</span></span>

<span data-ttu-id="73821-195">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="73821-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="73821-197">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="73821-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="73821-198">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="73821-198">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Przycisk usługi Azure Active Directory](./media/active-directory-saas-voyance-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="73821-200">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="73821-200">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    !["Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-voyance-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="73821-202">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="73821-202">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Przycisk Dodaj](./media/active-directory-saas-voyance-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="73821-204">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="73821-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Okno dialogowe użytkownika](./media/active-directory-saas-voyance-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="73821-206">a.</span><span class="sxs-lookup"><span data-stu-id="73821-206">a.</span></span> <span data-ttu-id="73821-207">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="73821-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="73821-208">b.</span><span class="sxs-lookup"><span data-stu-id="73821-208">b.</span></span> <span data-ttu-id="73821-209">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="73821-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="73821-210">c.</span><span class="sxs-lookup"><span data-stu-id="73821-210">c.</span></span> <span data-ttu-id="73821-211">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="73821-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="73821-212">d.</span><span class="sxs-lookup"><span data-stu-id="73821-212">d.</span></span> <span data-ttu-id="73821-213">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="73821-213">Click **Create**.</span></span>
 
### <a name="create-a-voyance-test-user"></a><span data-ttu-id="73821-214">Tworzenie użytkownika testowego Voyance</span><span class="sxs-lookup"><span data-stu-id="73821-214">Create a Voyance test user</span></span>

<span data-ttu-id="73821-215">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w Voyance.</span><span class="sxs-lookup"><span data-stu-id="73821-215">The objective of this section is to create a user called Britta Simon in Voyance.</span></span> <span data-ttu-id="73821-216">Voyance obsługę w czasie, który jest domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="73821-216">Voyance supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="73821-217">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="73821-217">There is no action item for you in this section.</span></span> <span data-ttu-id="73821-218">Nowy użytkownik został utworzony podczas próby dostępu Voyance, jeśli go jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="73821-218">A new user is created during an attempt to access Voyance if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="73821-219">Jeśli trzeba ręcznie utworzyć użytkownika, należy skontaktować się [zespołem pomocy technicznej Voyance](maiLto:support@nyansa.com).</span><span class="sxs-lookup"><span data-stu-id="73821-219">If you need to create a user manually, you need to contact [Voyance support team](maiLto:support@nyansa.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="73821-220">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="73821-220">Assign the Azure AD test user</span></span>

<span data-ttu-id="73821-221">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Voyance.</span><span class="sxs-lookup"><span data-stu-id="73821-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Voyance.</span></span>

![Przypisanie roli użytkownika][200]

<span data-ttu-id="73821-223">**Aby przypisać Simona Britta Voyance, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="73821-223">**To assign Britta Simon to Voyance, perform the following steps:**</span></span>

1. <span data-ttu-id="73821-224">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="73821-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="73821-226">Na liście aplikacji zaznacz **Voyance**.</span><span class="sxs-lookup"><span data-stu-id="73821-226">In the applications list, select **Voyance**.</span></span>

    ![Łącze Voyance na liście aplikacji](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_app.png) 

3. <span data-ttu-id="73821-228">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="73821-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Łącze "Użytkownicy i grupy"][202]

4. <span data-ttu-id="73821-230">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="73821-230">Click **Add** button.</span></span> <span data-ttu-id="73821-231">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="73821-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![W okienku Dodaj przydziału][203]

5. <span data-ttu-id="73821-233">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="73821-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="73821-234">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="73821-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="73821-235">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="73821-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="73821-236">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="73821-236">Test single sign-on</span></span>

<span data-ttu-id="73821-237">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="73821-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="73821-238">Po kliknięciu kafelka Voyance w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Voyance.</span><span class="sxs-lookup"><span data-stu-id="73821-238">When you click the Voyance tile in the Access Panel, you should get automatically signed-on to your Voyance application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="73821-239">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="73821-239">Additional resources</span></span>

* [<span data-ttu-id="73821-240">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="73821-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="73821-241">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="73821-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_203.png

