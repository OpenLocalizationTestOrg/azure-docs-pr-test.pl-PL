---
title: 'Samouczek: Integracji Azure Active Directory z Datahug | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Datahug."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5c0dc1ea-7ff4-4554-b60b-0f2fa9f5abaa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/18/2017
ms.author: jeedes
ms.openlocfilehash: ec431dd5ccfa53e4b975e46da247704dd1e15c2c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-datahug"></a><span data-ttu-id="72a1d-103">Samouczek: Integracji Azure Active Directory z Datahug</span><span class="sxs-lookup"><span data-stu-id="72a1d-103">Tutorial: Azure Active Directory integration with Datahug</span></span>

<span data-ttu-id="72a1d-104">Z tego samouczka dowiesz się integrowanie Datahug z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="72a1d-104">In this tutorial, you learn how to integrate Datahug with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="72a1d-105">Integracja z usługą Azure AD Datahug zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="72a1d-105">Integrating Datahug with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="72a1d-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Datahug</span><span class="sxs-lookup"><span data-stu-id="72a1d-106">You can control in Azure AD who has access to Datahug</span></span>
- <span data-ttu-id="72a1d-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Datahug (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="72a1d-107">You can enable your users to automatically get signed-on to Datahug (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="72a1d-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="72a1d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="72a1d-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz.</span><span class="sxs-lookup"><span data-stu-id="72a1d-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="72a1d-110">[Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="72a1d-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="72a1d-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="72a1d-111">Prerequisites</span></span>

<span data-ttu-id="72a1d-112">Aby skonfigurować integrację usługi Azure AD z Datahug, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="72a1d-112">To configure Azure AD integration with Datahug, you need the following items:</span></span>

- <span data-ttu-id="72a1d-113">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="72a1d-113">An Azure AD subscription</span></span>
- <span data-ttu-id="72a1d-114">Datahug jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="72a1d-114">A Datahug single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="72a1d-115">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="72a1d-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="72a1d-116">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="72a1d-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="72a1d-117">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="72a1d-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="72a1d-118">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="72a1d-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="72a1d-119">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="72a1d-119">Scenario description</span></span>
<span data-ttu-id="72a1d-120">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="72a1d-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="72a1d-121">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="72a1d-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="72a1d-122">Dodawanie Datahug z galerii</span><span class="sxs-lookup"><span data-stu-id="72a1d-122">Adding Datahug from the gallery</span></span>
2. <span data-ttu-id="72a1d-123">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="72a1d-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-datahug-from-the-gallery"></a><span data-ttu-id="72a1d-124">Dodawanie Datahug z galerii</span><span class="sxs-lookup"><span data-stu-id="72a1d-124">Adding Datahug from the gallery</span></span>
<span data-ttu-id="72a1d-125">Aby skonfigurować integrację usługi Azure AD Datahug, należy dodać Datahug z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="72a1d-125">To configure the integration of Datahug into Azure AD, you need to add Datahug from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="72a1d-126">**Aby dodać Datahug z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="72a1d-126">**To add Datahug from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="72a1d-127">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="72a1d-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="72a1d-129">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="72a1d-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="72a1d-130">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="72a1d-130">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="72a1d-132">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="72a1d-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="72a1d-134">W polu wyszukiwania wpisz **Datahug**.</span><span class="sxs-lookup"><span data-stu-id="72a1d-134">In the search box, type **Datahug**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_search.png)

5. <span data-ttu-id="72a1d-136">W panelu wyników wybierz **Datahug**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="72a1d-136">In the results panel, select **Datahug**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="72a1d-138">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="72a1d-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="72a1d-139">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Datahug na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="72a1d-139">In this section, you configure and test Azure AD single sign-on with Datahug based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="72a1d-140">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Datahug jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="72a1d-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Datahug is to a user in Azure AD.</span></span> <span data-ttu-id="72a1d-141">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Datahug musi się.</span><span class="sxs-lookup"><span data-stu-id="72a1d-141">In other words, a link relationship between an Azure AD user and the related user in Datahug needs to be established.</span></span>

<span data-ttu-id="72a1d-142">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w Datahug.</span><span class="sxs-lookup"><span data-stu-id="72a1d-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Datahug.</span></span>

<span data-ttu-id="72a1d-143">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Datahug, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="72a1d-143">To configure and test Azure AD single sign-on with Datahug, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="72a1d-144">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="72a1d-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="72a1d-145">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="72a1d-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="72a1d-146">**[Tworzenie użytkownika testowego Datahug](#creating-a-datahug-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Datahug połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="72a1d-146">**[Creating a Datahug test user](#creating-a-datahug-test-user)** - to have a counterpart of Britta Simon in Datahug that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="72a1d-147">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="72a1d-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="72a1d-148">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="72a1d-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="72a1d-149">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="72a1d-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="72a1d-150">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Datahug.</span><span class="sxs-lookup"><span data-stu-id="72a1d-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Datahug application.</span></span>

<span data-ttu-id="72a1d-151">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Datahug, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="72a1d-151">**To configure Azure AD single sign-on with Datahug, perform the following steps:**</span></span>

1. <span data-ttu-id="72a1d-152">W portalu Azure na **Datahug** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="72a1d-152">In the Azure portal, on the **Datahug** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="72a1d-154">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="72a1d-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_samlbase.png)

3. <span data-ttu-id="72a1d-156">Na **Datahug domeny i adres URL** sekcji, jeśli chcesz skonfigurować aplikację w **IDP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="72a1d-156">On the **Datahug Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_ur1.png)

    <span data-ttu-id="72a1d-158">a.</span><span class="sxs-lookup"><span data-stu-id="72a1d-158">a.</span></span> <span data-ttu-id="72a1d-159">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://apps.datahug.com/identity/<uniqueID>`</span><span class="sxs-lookup"><span data-stu-id="72a1d-159">In the **Identifier** textbox, type a URL using the following pattern: `https://apps.datahug.com/identity/<uniqueID>`</span></span>

    <span data-ttu-id="72a1d-160">b.</span><span class="sxs-lookup"><span data-stu-id="72a1d-160">b.</span></span> <span data-ttu-id="72a1d-161">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://apps.datahug.com/identity/<uniqueID>/acs`</span><span class="sxs-lookup"><span data-stu-id="72a1d-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://apps.datahug.com/identity/<uniqueID>/acs`</span></span>

4. <span data-ttu-id="72a1d-162">Sprawdź **Pokaż zaawansowane ustawienia adresu URL**.</span><span class="sxs-lookup"><span data-stu-id="72a1d-162">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="72a1d-163">Jeśli chcesz skonfigurować aplikację w **SP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="72a1d-163">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_url2.png)

    <span data-ttu-id="72a1d-165">W **adres URL logowania** tekstowym, wpisz adres URL jako:`https://apps.datahug.com/`</span><span class="sxs-lookup"><span data-stu-id="72a1d-165">In the **Sign-on URL** textbox, type a URL as: `https://apps.datahug.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="72a1d-166">Wartości te nie są rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="72a1d-166">These values are not the real.</span></span> <span data-ttu-id="72a1d-167">Rzeczywisty identyfikator i adres URL odpowiedzi, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="72a1d-167">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="72a1d-168">W tym miejscu zalecamy można używać unikatowej wartości ciągu identyfikatora i adres URL odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="72a1d-168">Here we suggest you to use the unique value of string in the Identifier and Reply URL.</span></span> <span data-ttu-id="72a1d-169">Skontaktuj się z [zespołem pomocy technicznej klienta Datahug](http://datahug.com/about/contact-us/) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="72a1d-169">Contact [Datahug Client support team](http://datahug.com/about/contact-us/) to get these values.</span></span> 

5. <span data-ttu-id="72a1d-170">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="72a1d-170">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_certificate.png) 

6.  <span data-ttu-id="72a1d-172">Sprawdź **"Pokaż zaawansowane ustawienia podpisywania certyfikatu"** i wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="72a1d-172">Check **“Show advanced certificate signing settings”** and perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_cert.png)

    <span data-ttu-id="72a1d-174">a.</span><span class="sxs-lookup"><span data-stu-id="72a1d-174">a.</span></span> <span data-ttu-id="72a1d-175">W **opcja podpisywania**, wybierz pozycję **potwierdzenia języka SAML logowania**.</span><span class="sxs-lookup"><span data-stu-id="72a1d-175">In **Signing Option**, select **Sign SAML assertion**.</span></span>
    
    <span data-ttu-id="72a1d-176">b.</span><span class="sxs-lookup"><span data-stu-id="72a1d-176">b.</span></span> <span data-ttu-id="72a1d-177">W **algorytm podpisywania**, wybierz pozycję **SHA1**.</span><span class="sxs-lookup"><span data-stu-id="72a1d-177">In **Signing algorithm**, select **SHA1**.</span></span>
 
7. <span data-ttu-id="72a1d-178">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="72a1d-178">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-datahug-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="72a1d-180">Na **konfiguracji Datahug** , kliknij przycisk **skonfigurować Datahug** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="72a1d-180">On the **Datahug Configuration** section, click **Configure Datahug** to open **Configure sign-on** window.</span></span> <span data-ttu-id="72a1d-181">Kopiuj **SAML identyfikator jednostki** i **SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="72a1d-181">Copy the **SAML Entity ID** and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_configure.png) 

9. <span data-ttu-id="72a1d-183">Aby skonfigurować logowanie jednokrotne w **Datahug** stronie, musisz wysłać pobrany **XML metadanych**, **SAML identyfikator jednostki** i **SAML pojedynczy znak na adres URL usługi**  do [Obsługa Datahug](http://datahug.com/about/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="72a1d-183">To configure single sign-on on **Datahug** side, you need to send the downloaded **Metadata XML**, **SAML Entity ID** and **SAML Single Sign-On Service URL** to [Datahug support](http://datahug.com/about/contact-us/).</span></span> <span data-ttu-id="72a1d-184">Połączenia logowania jednokrotnego SAML prawidłowo po obu stronach instalacji tej aplikacji programu.</span><span class="sxs-lookup"><span data-stu-id="72a1d-184">They set this application up to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="72a1d-185">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="72a1d-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="72a1d-186">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="72a1d-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="72a1d-187">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="72a1d-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="72a1d-188">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="72a1d-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="72a1d-189">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="72a1d-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="72a1d-191">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="72a1d-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="72a1d-192">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="72a1d-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-datahug-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="72a1d-194">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="72a1d-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-datahug-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="72a1d-196">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="72a1d-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-datahug-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="72a1d-198">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="72a1d-198">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-datahug-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="72a1d-200">a.</span><span class="sxs-lookup"><span data-stu-id="72a1d-200">a.</span></span> <span data-ttu-id="72a1d-201">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="72a1d-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="72a1d-202">b.</span><span class="sxs-lookup"><span data-stu-id="72a1d-202">b.</span></span> <span data-ttu-id="72a1d-203">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="72a1d-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="72a1d-204">c.</span><span class="sxs-lookup"><span data-stu-id="72a1d-204">c.</span></span> <span data-ttu-id="72a1d-205">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="72a1d-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="72a1d-206">d.</span><span class="sxs-lookup"><span data-stu-id="72a1d-206">d.</span></span> <span data-ttu-id="72a1d-207">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="72a1d-207">Click **Create**.</span></span>
 
### <a name="creating-a-datahug-test-user"></a><span data-ttu-id="72a1d-208">Tworzenie użytkownika testowego Datahug</span><span class="sxs-lookup"><span data-stu-id="72a1d-208">Creating a Datahug test user</span></span>

<span data-ttu-id="72a1d-209">Aby umożliwić użytkownikom usługi Azure AD zalogować się do Datahug, musi być przygotowana do Datahug.</span><span class="sxs-lookup"><span data-stu-id="72a1d-209">To enable Azure AD users to log in to Datahug, they must be provisioned into Datahug.</span></span>  
<span data-ttu-id="72a1d-210">Gdy Datahug, inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="72a1d-210">When Datahug, provisioning is a manual task.</span></span>

<span data-ttu-id="72a1d-211">**Aby udostępnić konta użytkownika, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="72a1d-211">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="72a1d-212">Zaloguj się do witryny firmy Datahug jako administrator.</span><span class="sxs-lookup"><span data-stu-id="72a1d-212">Log in to your Datahug company site as an administrator.</span></span>

2. <span data-ttu-id="72a1d-213">Umieść kursor nad **koło zębate** w prawym górnym rogu i kliknij **ustawienia**</span><span class="sxs-lookup"><span data-stu-id="72a1d-213">Hover over the **cog** in the top right-hand corner and click **Settings**</span></span>
   
   ![Dodawanie pracownika](./media/active-directory-saas-datahug-tutorial/1.png)

3. <span data-ttu-id="72a1d-215">Wybierz **osób** i kliknij przycisk **Dodaj użytkowników** kartę</span><span class="sxs-lookup"><span data-stu-id="72a1d-215">Choose **People** and click the **Add Users** tab</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-datahug-tutorial/2.png)

4. <span data-ttu-id="72a1d-217">Wpisz adres e-mail osoby, które chcesz utworzyć konto, a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="72a1d-217">Type the email of the person you would like to create an account for and click **Add**.</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-datahug-tutorial/3.png)

    > [!NOTE] 
    > <span data-ttu-id="72a1d-219">Wiadomość e-mail rejestracji można wysłać do użytkownika, wybierając **wysyłania powitalnej wiadomości e-mail** wyboru.</span><span class="sxs-lookup"><span data-stu-id="72a1d-219">You can send registration mail to user by selecting **Send welcome email** checkbox.</span></span>  
    > <span data-ttu-id="72a1d-220">Jeśli tworzysz konto Salesforce bez wysyłania powitalnej wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="72a1d-220">If you are creating an account for Salesforce do not send the welcome email.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="72a1d-221">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="72a1d-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="72a1d-222">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Datahug.</span><span class="sxs-lookup"><span data-stu-id="72a1d-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Datahug.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="72a1d-224">**Aby przypisać Simona Britta Datahug, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="72a1d-224">**To assign Britta Simon to Datahug, perform the following steps:**</span></span>

1. <span data-ttu-id="72a1d-225">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="72a1d-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="72a1d-227">Na liście aplikacji zaznacz **Datahug**.</span><span class="sxs-lookup"><span data-stu-id="72a1d-227">In the applications list, select **Datahug**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_app.png) 

3. <span data-ttu-id="72a1d-229">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="72a1d-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="72a1d-231">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="72a1d-231">Click **Add** button.</span></span> <span data-ttu-id="72a1d-232">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="72a1d-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="72a1d-234">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="72a1d-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="72a1d-235">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="72a1d-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="72a1d-236">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="72a1d-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="72a1d-237">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="72a1d-237">Testing single sign-on</span></span>

<span data-ttu-id="72a1d-238">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="72a1d-238">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
<span data-ttu-id="72a1d-239">Po kliknięciu kafelka Datahug w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Datahug.</span><span class="sxs-lookup"><span data-stu-id="72a1d-239">When you click the Datahug tile in the Access Panel, you should get automatically signed-on to your Datahug application.</span></span> <span data-ttu-id="72a1d-240">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="72a1d-240">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="72a1d-241">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="72a1d-241">Additional resources</span></span>

* [<span data-ttu-id="72a1d-242">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="72a1d-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="72a1d-243">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="72a1d-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_203.png

