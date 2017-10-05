---
title: 'Samouczek: Integracji Azure Active Directory z rozpoznawanie | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i rozpoznawanie."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cfad939e-c8f4-45a0-bd25-c4eb9701acaa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: 97d85183d0307c41a3b879d440d87a6fb0c53190
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-recognize"></a><span data-ttu-id="f3196-103">Samouczek: Integracji Azure Active Directory z rozpoznawanie</span><span class="sxs-lookup"><span data-stu-id="f3196-103">Tutorial: Azure Active Directory integration with Recognize</span></span>

<span data-ttu-id="f3196-104">Z tego samouczka dowiesz się sposobu integracji z usługą Azure Active Directory (Azure AD) rozpoznawanie.</span><span class="sxs-lookup"><span data-stu-id="f3196-104">In this tutorial, you learn how to integrate Recognize with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f3196-105">Integracja z usługą Azure AD rozpoznawanie zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="f3196-105">Integrating Recognize with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f3196-106">Można kontrolować w usłudze Azure AD, który ma dostęp do uznania</span><span class="sxs-lookup"><span data-stu-id="f3196-106">You can control in Azure AD who has access to Recognize</span></span>
- <span data-ttu-id="f3196-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do uznania (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f3196-107">You can enable your users to automatically get signed-on to Recognize (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f3196-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="f3196-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f3196-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f3196-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f3196-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f3196-110">Prerequisites</span></span>

<span data-ttu-id="f3196-111">Aby skonfigurować integrację usługi Azure AD z rozpoznawanie, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="f3196-111">To configure Azure AD integration with Recognize, you need the following items:</span></span>

- <span data-ttu-id="f3196-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f3196-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f3196-113">Rozpoznaj logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="f3196-113">A Recognize single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f3196-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="f3196-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f3196-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="f3196-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f3196-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="f3196-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f3196-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna tutaj: [oferta wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f3196-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f3196-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="f3196-118">Scenario description</span></span>
<span data-ttu-id="f3196-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="f3196-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f3196-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="f3196-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f3196-121">Dodawanie rozpoznawaj z galerii</span><span class="sxs-lookup"><span data-stu-id="f3196-121">Adding Recognize from the gallery</span></span>
2. <span data-ttu-id="f3196-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="f3196-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-recognize-from-the-gallery"></a><span data-ttu-id="f3196-123">Dodawanie rozpoznawaj z galerii</span><span class="sxs-lookup"><span data-stu-id="f3196-123">Adding Recognize from the gallery</span></span>
<span data-ttu-id="f3196-124">Aby skonfigurować integrację usługi Azure AD rozpoznawanie, musisz dodać rozpoznawaj z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="f3196-124">To configure the integration of Recognize into Azure AD, you need to add Recognize from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f3196-125">**Aby dodać rozpoznawaj z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f3196-125">**To add Recognize from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f3196-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="f3196-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="f3196-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="f3196-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f3196-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="f3196-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="f3196-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f3196-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="f3196-133">W polu wyszukiwania wpisz **rozpoznawanie**.</span><span class="sxs-lookup"><span data-stu-id="f3196-133">In the search box, type **Recognize**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_search.png)

5. <span data-ttu-id="f3196-135">W panelu wyników wybierz **rozpoznawanie**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="f3196-135">In the results panel, select **Recognize**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f3196-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="f3196-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f3196-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z rozpoznawanie w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="f3196-138">In this section, you configure and test Azure AD single sign-on with Recognize based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f3196-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w rozpoznawanie jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f3196-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Recognize is to a user in Azure AD.</span></span> <span data-ttu-id="f3196-140">Innymi słowy łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w rozpoznawanie musi się.</span><span class="sxs-lookup"><span data-stu-id="f3196-140">In other words, a link relationship between an Azure AD user and the related user in Recognize needs to be established.</span></span>

<span data-ttu-id="f3196-141">Rozpoznaj, przypisywanie wartości **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="f3196-141">In Recognize, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f3196-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z rozpoznawanie, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="f3196-142">To configure and test Azure AD single sign-on with Recognize, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f3196-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="f3196-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f3196-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="f3196-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f3196-145">**[Tworzenie użytkownika testowego rozpoznawanie](#creating-a-recognize-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta rozpoznawanie połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f3196-145">**[Creating a Recognize test user](#creating-a-recognize-test-user)** - to have a counterpart of Britta Simon in Recognize that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f3196-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="f3196-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f3196-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="f3196-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f3196-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="f3196-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f3196-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji rozpoznawanie.</span><span class="sxs-lookup"><span data-stu-id="f3196-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Recognize application.</span></span>

<span data-ttu-id="f3196-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z rozpoznawanie, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f3196-150">**To configure Azure AD single sign-on with Recognize, perform the following steps:**</span></span>

1. <span data-ttu-id="f3196-151">W portalu Azure na **rozpoznawanie** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="f3196-151">In the Azure portal, on the **Recognize** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="f3196-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="f3196-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_samlbase.png)

3. <span data-ttu-id="f3196-155">Na **adresy URL i rozpoznać domeny** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="f3196-155">On the **Recognize Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_url.png)

    <span data-ttu-id="f3196-157">a.</span><span class="sxs-lookup"><span data-stu-id="f3196-157">a.</span></span> <span data-ttu-id="f3196-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://recognizeapp.com/<your-domain>/saml/sso`</span><span class="sxs-lookup"><span data-stu-id="f3196-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://recognizeapp.com/<your-domain>/saml/sso`</span></span>

    <span data-ttu-id="f3196-159">b.</span><span class="sxs-lookup"><span data-stu-id="f3196-159">b.</span></span> <span data-ttu-id="f3196-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://recognizeapp.com/<your-domain>`</span><span class="sxs-lookup"><span data-stu-id="f3196-160">In the **Identifier** textbox, type a URL using the following pattern: `https://recognizeapp.com/<your-domain>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f3196-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="f3196-161">These values are not real.</span></span> <span data-ttu-id="f3196-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="f3196-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f3196-163">Skontaktuj się z [zespołem pomocy technicznej klienta rozpoznaje](mailto:support@recognizeapp.com) uzyskać adres URL logowania i może uzyskać wartość identyfikatora otwierania adresu URL metadanych dostawcy usług w sekcji Ustawienia logowania jednokrotnego, opisanej w dalszej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="f3196-163">Contact [Recognize Client support team](mailto:support@recognizeapp.com) to get Sign-On URL and you can get Identifier value by opening the Service Provider Metadata URL from the SSO Settings section that is explained later in the tutorial.</span></span> <span data-ttu-id="f3196-164">.</span><span class="sxs-lookup"><span data-stu-id="f3196-164">.</span></span> 
 
4. <span data-ttu-id="f3196-165">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="f3196-165">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_certificate.png) 

5. <span data-ttu-id="f3196-167">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f3196-167">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-recognize-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f3196-169">Na **rozpoznaje konfiguracji** , kliknij przycisk **skonfigurować rozpoznaje** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="f3196-169">On the **Recognize Configuration** section, click **Configure Recognize** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f3196-170">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="f3196-170">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_configure.png) 

7. <span data-ttu-id="f3196-172">W oknie przeglądarki innej witryny sieci web logowanie do dzierżawy rozpoznawanie jako administrator.</span><span class="sxs-lookup"><span data-stu-id="f3196-172">In a different web browser window, sign-on to your Recognize tenant as an administrator.</span></span>

8. <span data-ttu-id="f3196-173">W prawym górnym rogu kliknij **Menu**.</span><span class="sxs-lookup"><span data-stu-id="f3196-173">On the upper right corner, click **Menu**.</span></span> <span data-ttu-id="f3196-174">Przejdź do **firmy Admin**.</span><span class="sxs-lookup"><span data-stu-id="f3196-174">Go to **Company Admin**.</span></span>
   
    ![Konfigurowanie jednej logowania w aplikacji po stronie](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_000.png)

9. <span data-ttu-id="f3196-176">W lewym okienku nawigacji, kliknij polecenie **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="f3196-176">On the left navigation pane, click **Settings**.</span></span>
   
    ![Konfigurowanie jednej logowania w aplikacji po stronie](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_001.png)

10. <span data-ttu-id="f3196-178">Wykonaj następujące czynności na **ustawienia logowania jednokrotnego** sekcji.</span><span class="sxs-lookup"><span data-stu-id="f3196-178">Perform the following steps on **SSO Settings** section.</span></span>
   
    ![Konfigurowanie jednej logowania w aplikacji po stronie](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_002.png)
    
    <span data-ttu-id="f3196-180">a.</span><span class="sxs-lookup"><span data-stu-id="f3196-180">a.</span></span> <span data-ttu-id="f3196-181">Jako **włączenia logowania jednokrotnego**, wybierz pozycję **ON**.</span><span class="sxs-lookup"><span data-stu-id="f3196-181">As **Enable SSO**, select **ON**.</span></span>

    <span data-ttu-id="f3196-182">b.</span><span class="sxs-lookup"><span data-stu-id="f3196-182">b.</span></span> <span data-ttu-id="f3196-183">W **identyfikator jednostki IDP** pole tekstowe, Wklej wartość **identyfikator jednostki SAML** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f3196-183">In the **IDP Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="f3196-184">c.</span><span class="sxs-lookup"><span data-stu-id="f3196-184">c.</span></span> <span data-ttu-id="f3196-185">W **logowania jednokrotnego, docelowy adres url** pole tekstowe, Wklej wartość **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f3196-185">In the **Sso target url** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="f3196-186">d.</span><span class="sxs-lookup"><span data-stu-id="f3196-186">d.</span></span> <span data-ttu-id="f3196-187">W **Slo docelowy adres url** pole tekstowe, Wklej wartość **Sign-Out URL** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f3196-187">In the **Slo target url** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span> 
    
    <span data-ttu-id="f3196-188">e.</span><span class="sxs-lookup"><span data-stu-id="f3196-188">e.</span></span> <span data-ttu-id="f3196-189">Otwórz z pobranego **certyfikatu (Base64)** plików w programie Notatnik, skopiuj zawartość go do Schowka, a następnie wklej go do **certyfikatu** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="f3196-189">Open your downloaded **Certificate (Base64)** file in notepad, copy the content of it into your clipboard, and then paste it to the **Certificate** textbox.</span></span>
    
    <span data-ttu-id="f3196-190">f.</span><span class="sxs-lookup"><span data-stu-id="f3196-190">f.</span></span> <span data-ttu-id="f3196-191">Kliknij przycisk **Zapisz ustawienia** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f3196-191">Click the **Save settings** button.</span></span> 

11. <span data-ttu-id="f3196-192">Obok **ustawienia logowania jednokrotnego** sekcji, skopiuj adres URL, pod **adres url usługi dostawcy metadanych**.</span><span class="sxs-lookup"><span data-stu-id="f3196-192">Beside the **SSO Settings** section, copy the URL under **Service Provider Metadata url**.</span></span>
   
    ![Konfigurowanie jednej logowania w aplikacji po stronie](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_003.png)

12. <span data-ttu-id="f3196-194">Otwórz **łącze URL metadanych** w obszarze puste przeglądarki, aby pobrać dokumentu metadanych.</span><span class="sxs-lookup"><span data-stu-id="f3196-194">Open the **Metadata URL link** under a blank browser to download the metadata document.</span></span> <span data-ttu-id="f3196-195">Następnie skopiuj EntityDescriptor value(entityID) z pliku i wklej go w **identyfikator** textbox w **sekcji rozpoznać domeny i adresy URL** w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f3196-195">Then copy the EntityDescriptor value(entityID) from the file and paste it in **Identifier** textbox in **Recognize Domain and URLs section** on Azure portal.</span></span>
    
    ![Konfigurowanie jednej logowania w aplikacji po stronie](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_004.png)

> [!TIP]
> <span data-ttu-id="f3196-197">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="f3196-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f3196-198">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="f3196-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f3196-199">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f3196-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f3196-200">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f3196-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="f3196-201">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="f3196-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="f3196-203">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f3196-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f3196-204">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="f3196-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-recognize-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f3196-206">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="f3196-206">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-recognize-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f3196-208">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f3196-208">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-recognize-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f3196-210">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="f3196-210">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-recognize-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f3196-212">a.</span><span class="sxs-lookup"><span data-stu-id="f3196-212">a.</span></span> <span data-ttu-id="f3196-213">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f3196-213">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f3196-214">b.</span><span class="sxs-lookup"><span data-stu-id="f3196-214">b.</span></span> <span data-ttu-id="f3196-215">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f3196-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f3196-216">c.</span><span class="sxs-lookup"><span data-stu-id="f3196-216">c.</span></span> <span data-ttu-id="f3196-217">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="f3196-217">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f3196-218">d.</span><span class="sxs-lookup"><span data-stu-id="f3196-218">d.</span></span> <span data-ttu-id="f3196-219">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="f3196-219">Click **Create**.</span></span>
 
### <a name="creating-a-recognize-test-user"></a><span data-ttu-id="f3196-220">Tworzenie użytkownika testowego rozpoznawanie</span><span class="sxs-lookup"><span data-stu-id="f3196-220">Creating a Recognize test user</span></span>

<span data-ttu-id="f3196-221">Aby umożliwić użytkownikom zalogować się na rozpoznawanie usługi Azure AD, musi być przygotowana do uznania.</span><span class="sxs-lookup"><span data-stu-id="f3196-221">In order to enable Azure AD users to log into Recognize, they must be provisioned into Recognize.</span></span> <span data-ttu-id="f3196-222">W przypadku uznania Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="f3196-222">In the case of Recognize, provisioning is a manual task.</span></span>

<span data-ttu-id="f3196-223">Ta aplikacja nie obsługuje udostępniania SCIM, ale ma synchronizacji alternatywny użytkownika, która udostępnia użytkownikom.</span><span class="sxs-lookup"><span data-stu-id="f3196-223">This app doesn't support SCIM provisioning but has an alternate user sync that provisions users.</span></span> 

<span data-ttu-id="f3196-224">**Aby udostępnić konta użytkownika, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f3196-224">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="f3196-225">Zaloguj się do witryny firmy rozpoznawanie jako administrator.</span><span class="sxs-lookup"><span data-stu-id="f3196-225">Log into your Recognize company site as an administrator.</span></span>

2. <span data-ttu-id="f3196-226">W prawym górnym rogu kliknij **Menu**.</span><span class="sxs-lookup"><span data-stu-id="f3196-226">On the upper right corner, click **Menu**.</span></span> <span data-ttu-id="f3196-227">Przejdź do **firmy Admin**.</span><span class="sxs-lookup"><span data-stu-id="f3196-227">Go to **Company Admin**.</span></span>

3. <span data-ttu-id="f3196-228">W lewym okienku nawigacji, kliknij polecenie **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="f3196-228">On the left navigation pane, click **Settings**.</span></span>

4. <span data-ttu-id="f3196-229">Wykonaj następujące czynności na **synchronizacji użytkownika** sekcji.</span><span class="sxs-lookup"><span data-stu-id="f3196-229">Perform the following steps on **User Sync** section.</span></span>
   
   <span data-ttu-id="f3196-230">![Nowy użytkownik](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_005.png "nowego użytkownika")</span><span class="sxs-lookup"><span data-stu-id="f3196-230">![New User](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_005.png "New User")</span></span>
   
   <span data-ttu-id="f3196-231">a.</span><span class="sxs-lookup"><span data-stu-id="f3196-231">a.</span></span> <span data-ttu-id="f3196-232">Jako **włączona synchronizacja**, wybierz pozycję **ON**.</span><span class="sxs-lookup"><span data-stu-id="f3196-232">As **Sync Enabled**, select **ON**.</span></span>
   
   <span data-ttu-id="f3196-233">b.</span><span class="sxs-lookup"><span data-stu-id="f3196-233">b.</span></span> <span data-ttu-id="f3196-234">Jako **dostawcy synchronizacji wybierz**, wybierz pozycję **Microsoft / usługi Office 365**.</span><span class="sxs-lookup"><span data-stu-id="f3196-234">As **Choose sync provider**, select **Microsoft / Office 365**.</span></span>
   
   <span data-ttu-id="f3196-235">c.</span><span class="sxs-lookup"><span data-stu-id="f3196-235">c.</span></span> <span data-ttu-id="f3196-236">Kliknij przycisk **Przeprowadź synchronizację użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="f3196-236">Click **Run User Sync**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f3196-237">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f3196-237">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f3196-238">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do uznania.</span><span class="sxs-lookup"><span data-stu-id="f3196-238">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Recognize.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="f3196-240">**Aby przypisać Simona Britta rozpoznawanie, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f3196-240">**To assign Britta Simon to Recognize, perform the following steps:**</span></span>

1. <span data-ttu-id="f3196-241">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="f3196-241">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="f3196-243">Na liście aplikacji zaznacz **rozpoznawanie**.</span><span class="sxs-lookup"><span data-stu-id="f3196-243">In the applications list, select **Recognize**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_app.png) 

3. <span data-ttu-id="f3196-245">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="f3196-245">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="f3196-247">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f3196-247">Click **Add** button.</span></span> <span data-ttu-id="f3196-248">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f3196-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="f3196-250">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="f3196-250">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f3196-251">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f3196-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f3196-252">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f3196-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f3196-253">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="f3196-253">Testing single sign-on</span></span>

<span data-ttu-id="f3196-254">Celem tej sekcji służy do testowania konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="f3196-254">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f3196-255">Po kliknięciu kafelka rozpoznawanie w panelu dostępu należy należy pobrać automatycznie zalogowane do uznania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f3196-255">When you click the Recognize tile in the Access Panel, you should get automatically signed-on to your Recognize application.</span></span> <span data-ttu-id="f3196-256">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f3196-256">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f3196-257">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="f3196-257">Additional resources</span></span>

* [<span data-ttu-id="f3196-258">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f3196-258">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f3196-259">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f3196-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_203.png

