---
title: 'Samouczek: Integracji Azure Active Directory z IdeaScale | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i IdeaScale."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e16dda6b-fdf9-43cc-9bbb-a523f085a8af
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 88099e942319f16dd721da83e4e69b8fcb836c0d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ideascale"></a><span data-ttu-id="37c23-103">Samouczek: Integracji Azure Active Directory z IdeaScale</span><span class="sxs-lookup"><span data-stu-id="37c23-103">Tutorial: Azure Active Directory integration with IdeaScale</span></span>

<span data-ttu-id="37c23-104">Z tego samouczka dowiesz się integrowanie IdeaScale z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="37c23-104">In this tutorial, you learn how to integrate IdeaScale with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="37c23-105">Integracja z usługą Azure AD IdeaScale zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="37c23-105">Integrating IdeaScale with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="37c23-106">Można kontrolować w usłudze Azure AD, który ma dostęp do IdeaScale</span><span class="sxs-lookup"><span data-stu-id="37c23-106">You can control in Azure AD who has access to IdeaScale</span></span>
- <span data-ttu-id="37c23-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do IdeaScale (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="37c23-107">You can enable your users to automatically get signed-on to IdeaScale (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="37c23-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="37c23-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="37c23-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="37c23-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="37c23-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="37c23-110">Prerequisites</span></span>

<span data-ttu-id="37c23-111">Aby skonfigurować integrację usługi Azure AD z IdeaScale, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="37c23-111">To configure Azure AD integration with IdeaScale, you need the following items:</span></span>

- <span data-ttu-id="37c23-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="37c23-112">An Azure AD subscription</span></span>
- <span data-ttu-id="37c23-113">IdeaScale jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="37c23-113">An IdeaScale single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="37c23-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="37c23-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="37c23-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="37c23-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="37c23-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="37c23-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="37c23-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="37c23-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="37c23-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="37c23-118">Scenario description</span></span>
<span data-ttu-id="37c23-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="37c23-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="37c23-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="37c23-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="37c23-121">Dodawanie IdeaScale z galerii</span><span class="sxs-lookup"><span data-stu-id="37c23-121">Adding IdeaScale from the gallery</span></span>
2. <span data-ttu-id="37c23-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="37c23-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ideascale-from-the-gallery"></a><span data-ttu-id="37c23-123">Dodawanie IdeaScale z galerii</span><span class="sxs-lookup"><span data-stu-id="37c23-123">Adding IdeaScale from the gallery</span></span>
<span data-ttu-id="37c23-124">Aby skonfigurować integrację usługi Azure AD IdeaScale, należy dodać IdeaScale z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="37c23-124">To configure the integration of IdeaScale into Azure AD, you need to add IdeaScale from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="37c23-125">**Aby dodać IdeaScale z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="37c23-125">**To add IdeaScale from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="37c23-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="37c23-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="37c23-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="37c23-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="37c23-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="37c23-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="37c23-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="37c23-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="37c23-133">W polu wyszukiwania wpisz **IdeaScale**.</span><span class="sxs-lookup"><span data-stu-id="37c23-133">In the search box, type **IdeaScale**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_search.png)

5. <span data-ttu-id="37c23-135">W panelu wyników wybierz **IdeaScale**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="37c23-135">In the results panel, select **IdeaScale**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="37c23-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="37c23-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="37c23-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z IdeaScale na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="37c23-138">In this section, you configure and test Azure AD single sign-on with IdeaScale based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="37c23-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w IdeaScale jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="37c23-139">For single sign-on to work, Azure AD needs to know what the counterpart user in IdeaScale is to a user in Azure AD.</span></span> <span data-ttu-id="37c23-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w IdeaScale musi się.</span><span class="sxs-lookup"><span data-stu-id="37c23-140">In other words, a link relationship between an Azure AD user and the related user in IdeaScale needs to be established.</span></span>

<span data-ttu-id="37c23-141">W IdeaScale, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="37c23-141">In IdeaScale, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="37c23-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z IdeaScale, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="37c23-142">To configure and test Azure AD single sign-on with IdeaScale, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="37c23-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="37c23-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="37c23-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="37c23-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="37c23-145">**[Tworzenie użytkownika testowego IdeaScale](#creating-an-ideascale-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta IdeaScale połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="37c23-145">**[Creating an IdeaScale test user](#creating-an-ideascale-test-user)** - to have a counterpart of Britta Simon in IdeaScale that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="37c23-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="37c23-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="37c23-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="37c23-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="37c23-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="37c23-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="37c23-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji IdeaScale.</span><span class="sxs-lookup"><span data-stu-id="37c23-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your IdeaScale application.</span></span>

<span data-ttu-id="37c23-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z IdeaScale, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="37c23-150">**To configure Azure AD single sign-on with IdeaScale, perform the following steps:**</span></span>

1. <span data-ttu-id="37c23-151">W portalu Azure na **IdeaScale** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="37c23-151">In the Azure portal, on the **IdeaScale** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="37c23-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="37c23-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_samlbase.png)

3. <span data-ttu-id="37c23-155">Na **IdeaScale domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="37c23-155">On the **IdeaScale Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_url.png)

    <span data-ttu-id="37c23-157">a.</span><span class="sxs-lookup"><span data-stu-id="37c23-157">a.</span></span> <span data-ttu-id="37c23-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.ideascale.com`</span><span class="sxs-lookup"><span data-stu-id="37c23-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.ideascale.com`</span></span>

    <span data-ttu-id="37c23-159">b.</span><span class="sxs-lookup"><span data-stu-id="37c23-159">b.</span></span> <span data-ttu-id="37c23-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="37c23-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `http://<companyname>.ideascale.com`  |
    | `https://<companyname>.ideascale.com` |

    > [!NOTE] 
    > <span data-ttu-id="37c23-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="37c23-161">These values are not real.</span></span> <span data-ttu-id="37c23-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="37c23-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="37c23-163">Skontaktuj się z [zespołem pomocy technicznej klienta IdeaScale](http://support.ideascale.com/) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="37c23-163">Contact [IdeaScale Client support team](http://support.ideascale.com/) to get these values.</span></span> 
 
4. <span data-ttu-id="37c23-164">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="37c23-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_certificate.png) 

5. <span data-ttu-id="37c23-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="37c23-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ideascale-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="37c23-168">Na **konfiguracji IdeaScale** , kliknij przycisk **skonfigurować IdeaScale** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="37c23-168">On the **IdeaScale Configuration** section, click **Configure IdeaScale** to open **Configure sign-on** window.</span></span> <span data-ttu-id="37c23-169">Kopiuj **Sign-Out adresu URL i identyfikator jednostki SAML** z **sekcji krótkimi opisami**.</span><span class="sxs-lookup"><span data-stu-id="37c23-169">Copy the **Sign-Out URL, and SAML Entity ID** from the **Quick Reference section**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_configure.png) 

7. <span data-ttu-id="37c23-171">W oknie przeglądarki innej witryny sieci web należy zalogować się jako administrator do witryny firmy IdeaScale.</span><span class="sxs-lookup"><span data-stu-id="37c23-171">In a different web browser window, log in to your IdeaScale company site as an administrator.</span></span>

8. <span data-ttu-id="37c23-172">Przejdź do **ustawienia społeczności**.</span><span class="sxs-lookup"><span data-stu-id="37c23-172">Go to **Community Settings**.</span></span>
   
    <span data-ttu-id="37c23-173">![Ustawienia społeczności](./media/active-directory-saas-ideascale-tutorial/ic790847.png "ustawienia społeczności")</span><span class="sxs-lookup"><span data-stu-id="37c23-173">![Community Settings](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Community Settings")</span></span>

9. <span data-ttu-id="37c23-174">Przejdź do **zabezpieczeń \> pojedynczy ustawienia logować**.</span><span class="sxs-lookup"><span data-stu-id="37c23-174">Go to **Security \> Single Signon Settings**.</span></span>
   
    <span data-ttu-id="37c23-175">![Pojedyncze ustawienia logować](./media/active-directory-saas-ideascale-tutorial/ic790848.png "pojedynczy logować ustawienia")</span><span class="sxs-lookup"><span data-stu-id="37c23-175">![Single Signon Settings](./media/active-directory-saas-ideascale-tutorial/ic790848.png "Single Signon Settings")</span></span>

10. <span data-ttu-id="37c23-176">Jako **typu Pojedyncza**, wybierz pozycję **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="37c23-176">As **Single-Signon Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="37c23-177">![Pojedynczy typ logować](./media/active-directory-saas-ideascale-tutorial/ic790849.png "pojedynczy typ logować")</span><span class="sxs-lookup"><span data-stu-id="37c23-177">![Single Signon Type](./media/active-directory-saas-ideascale-tutorial/ic790849.png "Single Signon Type")</span></span>

11. <span data-ttu-id="37c23-178">Na **jednego ustawienia logować** okna dialogowego, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="37c23-178">On the **Single Signon Settings** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="37c23-179">![Pojedyncze ustawienia logować](./media/active-directory-saas-ideascale-tutorial/ic790850.png "pojedynczy logować ustawienia")</span><span class="sxs-lookup"><span data-stu-id="37c23-179">![Single Signon Settings](./media/active-directory-saas-ideascale-tutorial/ic790850.png "Single Signon Settings")</span></span>
   
    <span data-ttu-id="37c23-180">a.</span><span class="sxs-lookup"><span data-stu-id="37c23-180">a.</span></span> <span data-ttu-id="37c23-181">W **identyfikator jednostki IdP SAML** pole tekstowe, Wklej wartość **identyfikator jednostki SAML** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="37c23-181">In **SAML IdP Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="37c23-182">b.</span><span class="sxs-lookup"><span data-stu-id="37c23-182">b.</span></span> <span data-ttu-id="37c23-183">Skopiuj zawartość pliku metadanych pobranych z portalu Azure i wklej ją do **metadanych IdP SAML** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="37c23-183">Copy the content of your downloaded metadata file from Azure portal, and paste it into the **SAML IdP Metadata** textbox.</span></span>

    <span data-ttu-id="37c23-184">c.</span><span class="sxs-lookup"><span data-stu-id="37c23-184">c.</span></span> <span data-ttu-id="37c23-185">W **URL Powodzenie wylogowania** pole tekstowe, Wklej wartość **Sign-Out URL** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="37c23-185">In **Logout Success URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="37c23-186">d.</span><span class="sxs-lookup"><span data-stu-id="37c23-186">d.</span></span> <span data-ttu-id="37c23-187">Kliknij przycisk **zapisać zmiany**.</span><span class="sxs-lookup"><span data-stu-id="37c23-187">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="37c23-188">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="37c23-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="37c23-189">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="37c23-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="37c23-190">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="37c23-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="37c23-191">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="37c23-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="37c23-192">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="37c23-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="37c23-194">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="37c23-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="37c23-195">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="37c23-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="37c23-197">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="37c23-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="37c23-199">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="37c23-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="37c23-201">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="37c23-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="37c23-203">a.</span><span class="sxs-lookup"><span data-stu-id="37c23-203">a.</span></span> <span data-ttu-id="37c23-204">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="37c23-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="37c23-205">b.</span><span class="sxs-lookup"><span data-stu-id="37c23-205">b.</span></span> <span data-ttu-id="37c23-206">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="37c23-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="37c23-207">c.</span><span class="sxs-lookup"><span data-stu-id="37c23-207">c.</span></span> <span data-ttu-id="37c23-208">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="37c23-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="37c23-209">d.</span><span class="sxs-lookup"><span data-stu-id="37c23-209">d.</span></span> <span data-ttu-id="37c23-210">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="37c23-210">Click **Create**.</span></span>
 
### <a name="creating-an-ideascale-test-user"></a><span data-ttu-id="37c23-211">Tworzenie użytkownika testowego IdeaScale</span><span class="sxs-lookup"><span data-stu-id="37c23-211">Creating an IdeaScale test user</span></span>

<span data-ttu-id="37c23-212">Aby włączyć użytkowników usługi Azure AD zalogować się do IdeaScale, ich należy udostępnić w celu IdeaScale.</span><span class="sxs-lookup"><span data-stu-id="37c23-212">To enable Azure AD users to log into IdeaScale, they must be provisioned in to IdeaScale.</span></span> <span data-ttu-id="37c23-213">W przypadku IdeaScale Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="37c23-213">In the case of IdeaScale, provisioning is a manual task.</span></span>

<span data-ttu-id="37c23-214">**Aby skonfigurować, inicjowanie obsługi użytkowników, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="37c23-214">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="37c23-215">Zaloguj się do Twojego **IdeaScale** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="37c23-215">Log in to your **IdeaScale** company site as administrator.</span></span>

2. <span data-ttu-id="37c23-216">Przejdź do **ustawienia społeczności**.</span><span class="sxs-lookup"><span data-stu-id="37c23-216">Go to **Community Settings**.</span></span>
   
    <span data-ttu-id="37c23-217">![Ustawienia społeczności](./media/active-directory-saas-ideascale-tutorial/ic790847.png "ustawienia społeczności")</span><span class="sxs-lookup"><span data-stu-id="37c23-217">![Community Settings](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Community Settings")</span></span>

3. <span data-ttu-id="37c23-218">Przejdź do **podstawowe ustawienia \> zarządzania elementu członkowskiego**.</span><span class="sxs-lookup"><span data-stu-id="37c23-218">Go to **Basic Settings \> Member Management**.</span></span>

4. <span data-ttu-id="37c23-219">Kliknij przycisk **dodać członka**.</span><span class="sxs-lookup"><span data-stu-id="37c23-219">Click **Add Member**.</span></span>
   
    <span data-ttu-id="37c23-220">![Element członkowski zarządzania](./media/active-directory-saas-ideascale-tutorial/ic790852.png "zarządzania elementu członkowskiego")</span><span class="sxs-lookup"><span data-stu-id="37c23-220">![Member Management](./media/active-directory-saas-ideascale-tutorial/ic790852.png "Member Management")</span></span>

5. <span data-ttu-id="37c23-221">W sekcji Dodaj nowy element członkowski wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="37c23-221">In the Add New Member section, perform the following steps:</span></span>
   
    <span data-ttu-id="37c23-222">![Dodaj nowy element członkowski](./media/active-directory-saas-ideascale-tutorial/ic790853.png "Dodaj nowy element członkowski")</span><span class="sxs-lookup"><span data-stu-id="37c23-222">![Add New Member](./media/active-directory-saas-ideascale-tutorial/ic790853.png "Add New Member")</span></span>
   
    <span data-ttu-id="37c23-223">a.</span><span class="sxs-lookup"><span data-stu-id="37c23-223">a.</span></span> <span data-ttu-id="37c23-224">W **adresy E-mail** tekstowym, wpisz adres e-mail prawidłowego konta usługi AAD chcesz udostępnić.</span><span class="sxs-lookup"><span data-stu-id="37c23-224">In the **Email Addresses** textbox, type the email address of a valid AAD account you want to provision.</span></span>
   
    <span data-ttu-id="37c23-225">b.</span><span class="sxs-lookup"><span data-stu-id="37c23-225">b.</span></span> <span data-ttu-id="37c23-226">Kliknij przycisk **zapisać zmiany**.</span><span class="sxs-lookup"><span data-stu-id="37c23-226">Click **Save Changes**.</span></span> 
   
    >[!NOTE]
    ><span data-ttu-id="37c23-227">Właściciel konta usługi Azure Active Directory pobiera wiadomość e-mail z łączem do potwierdzenia konta, zanim staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="37c23-227">The Azure Active Directory account holder gets an email with a link to confirm the account before it becomes active.</span></span>
      
>[!NOTE]
><span data-ttu-id="37c23-228">Możesz użyć innych IdeaScale użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez IdeaScale do kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="37c23-228">You can use any other IdeaScale user account creation tools or APIs provided by IdeaScale to provision AAD user accounts.</span></span>
 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="37c23-229">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="37c23-229">Assigning the Azure AD test user</span></span>

<span data-ttu-id="37c23-230">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu IdeaScale.</span><span class="sxs-lookup"><span data-stu-id="37c23-230">In this section, you enable Britta Simon to use Azure single sign-on by granting access to IdeaScale.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="37c23-232">**Aby przypisać Simona Britta IdeaScale, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="37c23-232">**To assign Britta Simon to IdeaScale, perform the following steps:**</span></span>

1. <span data-ttu-id="37c23-233">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="37c23-233">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="37c23-235">Na liście aplikacji zaznacz **IdeaScale**.</span><span class="sxs-lookup"><span data-stu-id="37c23-235">In the applications list, select **IdeaScale**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_app.png) 

3. <span data-ttu-id="37c23-237">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="37c23-237">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="37c23-239">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="37c23-239">Click **Add** button.</span></span> <span data-ttu-id="37c23-240">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="37c23-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="37c23-242">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="37c23-242">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="37c23-243">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="37c23-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="37c23-244">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="37c23-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="37c23-245">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="37c23-245">Testing single sign-on</span></span>


<span data-ttu-id="37c23-246">Celem tej sekcji służy do testowania konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="37c23-246">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="37c23-247">Po kliknięciu kafelka IdeaScale w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji IdeaScale.</span><span class="sxs-lookup"><span data-stu-id="37c23-247">When you click the IdeaScale tile in the Access Panel, you should get automatically signed-on to your IdeaScale application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="37c23-248">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="37c23-248">Additional resources</span></span>

* [<span data-ttu-id="37c23-249">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="37c23-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="37c23-250">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="37c23-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_203.png

