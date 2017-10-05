---
title: 'Samouczek: Integracji Azure Active Directory z PurelyHR | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i PurelyHR."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 86a9c454-596d-4902-829a-fe126708f739
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: jeedes
ms.openlocfilehash: a9075b1759ebd39f164bfe288fb0a365acdcc44c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-purelyhr"></a><span data-ttu-id="8b233-103">Samouczek: Integracji Azure Active Directory z PurelyHR</span><span class="sxs-lookup"><span data-stu-id="8b233-103">Tutorial: Azure Active Directory integration with PurelyHR</span></span>

<span data-ttu-id="8b233-104">Z tego samouczka dowiesz się integrowanie PurelyHR z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8b233-104">In this tutorial, you learn how to integrate PurelyHR with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8b233-105">Integracja z usługą Azure AD PurelyHR zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="8b233-105">Integrating PurelyHR with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8b233-106">Można kontrolować w usłudze Azure AD, który ma dostęp do PurelyHR</span><span class="sxs-lookup"><span data-stu-id="8b233-106">You can control in Azure AD who has access to PurelyHR</span></span>
- <span data-ttu-id="8b233-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do PurelyHR (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b233-107">You can enable your users to automatically get signed-on to PurelyHR (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8b233-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="8b233-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8b233-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8b233-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8b233-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8b233-110">Prerequisites</span></span>

<span data-ttu-id="8b233-111">Aby skonfigurować integrację usługi Azure AD z PurelyHR, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="8b233-111">To configure Azure AD integration with PurelyHR, you need the following items:</span></span>

- <span data-ttu-id="8b233-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b233-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8b233-113">PurelyHR jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="8b233-113">A PurelyHR single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8b233-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="8b233-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8b233-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="8b233-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8b233-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="8b233-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8b233-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8b233-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8b233-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="8b233-118">Scenario description</span></span>
<span data-ttu-id="8b233-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="8b233-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8b233-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="8b233-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8b233-121">Dodawanie PurelyHR z galerii</span><span class="sxs-lookup"><span data-stu-id="8b233-121">Adding PurelyHR from the gallery</span></span>
2. <span data-ttu-id="8b233-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="8b233-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-purelyhr-from-the-gallery"></a><span data-ttu-id="8b233-123">Dodawanie PurelyHR z galerii</span><span class="sxs-lookup"><span data-stu-id="8b233-123">Adding PurelyHR from the gallery</span></span>
<span data-ttu-id="8b233-124">Aby skonfigurować integrację usługi Azure AD PurelyHR, należy dodać PurelyHR z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="8b233-124">To configure the integration of PurelyHR into Azure AD, you need to add PurelyHR from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8b233-125">**Aby dodać PurelyHR z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="8b233-125">**To add PurelyHR from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8b233-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="8b233-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="8b233-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="8b233-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8b233-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="8b233-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="8b233-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8b233-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="8b233-133">W polu wyszukiwania wpisz **PurelyHR**.</span><span class="sxs-lookup"><span data-stu-id="8b233-133">In the search box, type **PurelyHR**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_search.png)

5. <span data-ttu-id="8b233-135">W panelu wyników wybierz **PurelyHR**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="8b233-135">In the results panel, select **PurelyHR**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8b233-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="8b233-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8b233-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z PurelyHR na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="8b233-138">In this section, you configure and test Azure AD single sign-on with PurelyHR based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8b233-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w PurelyHR jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8b233-139">For single sign-on to work, Azure AD needs to know what the counterpart user in PurelyHR is to a user in Azure AD.</span></span> <span data-ttu-id="8b233-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w PurelyHR musi się.</span><span class="sxs-lookup"><span data-stu-id="8b233-140">In other words, a link relationship between an Azure AD user and the related user in PurelyHR needs to be established.</span></span>

<span data-ttu-id="8b233-141">W PurelyHR, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="8b233-141">In PurelyHR, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8b233-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z PurelyHR, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="8b233-142">To configure and test Azure AD single sign-on with PurelyHR, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8b233-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="8b233-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8b233-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="8b233-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8b233-145">**[Tworzenie użytkownika testowego PurelyHR](#creating-a-purelyhr-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta PurelyHR połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8b233-145">**[Creating a PurelyHR test user](#creating-a-purelyhr-test-user)** - to have a counterpart of Britta Simon in PurelyHR that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8b233-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="8b233-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8b233-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="8b233-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8b233-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8b233-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8b233-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="8b233-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your PurelyHR application.</span></span>

<span data-ttu-id="8b233-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z PurelyHR, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="8b233-150">**To configure Azure AD single sign-on with PurelyHR, perform the following steps:**</span></span>

1. <span data-ttu-id="8b233-151">W portalu Azure na **PurelyHR** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="8b233-151">In the Azure portal, on the **PurelyHR** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="8b233-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="8b233-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_samlbase.png)

3. <span data-ttu-id="8b233-155">Na **PurelyHR domeny i adres URL** sekcji, wykonaj następujące kroki, aby skonfigurować aplikację w **IDP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="8b233-155">On the **PurelyHR Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_url.png)
   
    <span data-ttu-id="8b233-157">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyID>.purelyhr.com/sso-consume`</span><span class="sxs-lookup"><span data-stu-id="8b233-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyID>.purelyhr.com/sso-consume`</span></span>

4. <span data-ttu-id="8b233-158">Sprawdź **Pokaż zaawansowane ustawienia adresu URL**, jeśli chcesz skonfigurować aplikację w **SP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="8b233-158">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_url1.png)
    
    <span data-ttu-id="8b233-160">W **adres URL logowania** tekstowym, wpisz wartość, przy użyciu następującego wzorca:`https://<companyID>.purelyhr.com/sso-initiate`</span><span class="sxs-lookup"><span data-stu-id="8b233-160">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<companyID>.purelyhr.com/sso-initiate`</span></span>
     
    > [!NOTE]
    > <span data-ttu-id="8b233-161">Wartości te nie są rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="8b233-161">These values are not the real.</span></span> <span data-ttu-id="8b233-162">Rzeczywisty adres URL odpowiedzi i adres URL logowania, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="8b233-162">Update these values with the actual Reply URL and Sign-On URL.</span></span> <span data-ttu-id="8b233-163">Skontaktuj się z [zespołem pomocy technicznej klienta PurelyHR](http://support.purelyhr.com/) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="8b233-163">Contact [PurelyHR Client support team](http://support.purelyhr.com/) to get these values.</span></span> 

5. <span data-ttu-id="8b233-164">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="8b233-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_certificate.png) 

6. <span data-ttu-id="8b233-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8b233-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-purelyhr-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="8b233-168">Na **konfiguracji PurelyHR** , kliknij przycisk **skonfigurować PurelyHR** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="8b233-168">On the **PurelyHR Configuration** section, click **Configure PurelyHR** to open **Configure sign-on** window.</span></span> <span data-ttu-id="8b233-169">Kopiuj **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="8b233-169">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_configure.png) 

8. <span data-ttu-id="8b233-171">Aby skonfigurować logowanie jednokrotne w **PurelyHR** strona, zaloguj się do witryny sieci Web jako administrator.</span><span class="sxs-lookup"><span data-stu-id="8b233-171">To configure single sign-on on **PurelyHR** side, login to their website as an administrator.</span></span>

9. <span data-ttu-id="8b233-172">Otwórz **pulpitu nawigacyjnego** z opcji narzędzi i kliknij przycisk **ustawienia logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="8b233-172">Open the **Dashboard** from the options in the toolbar and click **SSO Settings**.</span></span>

10. <span data-ttu-id="8b233-173">Wklej wartości w polach, zgodnie z opisem poniżej-</span><span class="sxs-lookup"><span data-stu-id="8b233-173">Paste the values in the boxes as described below-</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-purelyhr-tutorial/purelyhr-dashboard-sso-settings.png)    

    <span data-ttu-id="8b233-175">a.</span><span class="sxs-lookup"><span data-stu-id="8b233-175">a.</span></span> <span data-ttu-id="8b233-176">Otwórz **Certificate(Bas64)** pobrany z portalu Azure w programie Notatnik i skopiuj wartość certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="8b233-176">Open the **Certificate(Bas64)** downloaded from the Azure portal in notepad and copy the certificate value.</span></span> <span data-ttu-id="8b233-177">Wklej skopiowane wartości do **certyfikatu X.509** pole.</span><span class="sxs-lookup"><span data-stu-id="8b233-177">Paste the copied value into the **X.509 Certificate** box.</span></span>

    <span data-ttu-id="8b233-178">b.</span><span class="sxs-lookup"><span data-stu-id="8b233-178">b.</span></span> <span data-ttu-id="8b233-179">W **adres URL wystawcy Idp** Wklej **identyfikator jednostki SAML** skopiowany z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="8b233-179">In the **Idp Issuer URL** box, paste the **SAML Entity ID** copied from the Azure portal.</span></span>

    <span data-ttu-id="8b233-180">c.</span><span class="sxs-lookup"><span data-stu-id="8b233-180">c.</span></span> <span data-ttu-id="8b233-181">W **adres URL punktu końcowego Idp** Wklej **SAML pojedynczy znak na adres URL usługi** skopiowany z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="8b233-181">In the **Idp Endpoint URL** box, paste the **SAML Single Sign-On Service URL** copied from the Azure portal.</span></span> 

    <span data-ttu-id="8b233-182">d.</span><span class="sxs-lookup"><span data-stu-id="8b233-182">d.</span></span> <span data-ttu-id="8b233-183">Sprawdź **automatyczne tworzenie użytkowników** pole wyboru, aby włączyć automatyczne użytkownika udostępnianie w PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="8b233-183">Check the **Auto-Create Users** checkbox to enable automatic user provisioning in PurelyHR.</span></span>

    <span data-ttu-id="8b233-184">e.</span><span class="sxs-lookup"><span data-stu-id="8b233-184">e.</span></span> <span data-ttu-id="8b233-185">Kliknij przycisk **Zapisz zmiany** Aby zapisać ustawienia.</span><span class="sxs-lookup"><span data-stu-id="8b233-185">Click **Save Changes** to save the settings.</span></span>

> [!TIP]
> <span data-ttu-id="8b233-186">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="8b233-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8b233-187">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="8b233-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8b233-188">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8b233-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8b233-189">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b233-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="8b233-190">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="8b233-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="8b233-192">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="8b233-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8b233-193">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="8b233-193">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8b233-195">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="8b233-195">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8b233-197">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8b233-197">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8b233-199">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="8b233-199">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8b233-201">a.</span><span class="sxs-lookup"><span data-stu-id="8b233-201">a.</span></span> <span data-ttu-id="8b233-202">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8b233-202">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8b233-203">b.</span><span class="sxs-lookup"><span data-stu-id="8b233-203">b.</span></span> <span data-ttu-id="8b233-204">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8b233-204">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8b233-205">c.</span><span class="sxs-lookup"><span data-stu-id="8b233-205">c.</span></span> <span data-ttu-id="8b233-206">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="8b233-206">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8b233-207">d.</span><span class="sxs-lookup"><span data-stu-id="8b233-207">d.</span></span> <span data-ttu-id="8b233-208">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="8b233-208">Click **Create**.</span></span>
 
### <a name="creating-a-purelyhr-test-user"></a><span data-ttu-id="8b233-209">Tworzenie użytkownika testowego PurelyHR</span><span class="sxs-lookup"><span data-stu-id="8b233-209">Creating a PurelyHR test user</span></span>

<span data-ttu-id="8b233-210">Aby umożliwić użytkownikom usługi Azure AD zalogować się do PurelyHR, musi być przygotowana do PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="8b233-210">To enable Azure AD users to log in to PurelyHR, they must be provisioned into PurelyHR.</span></span> <span data-ttu-id="8b233-211">W PurelyHR Inicjowanie obsługi to zadanie automatycznej i są wymagane żadne czynności ręczne włączenie użytkownika automatycznego inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="8b233-211">In PurelyHR, provisioning is an automatic task and no manual steps are required when automatic user provisioning is enabled.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8b233-212">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b233-212">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8b233-213">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="8b233-213">In this section, you enable Britta Simon to use Azure single sign-on by granting access to PurelyHR.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="8b233-215">**Aby przypisać Simona Britta PurelyHR, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="8b233-215">**To assign Britta Simon to PurelyHR, perform the following steps:**</span></span>

1. <span data-ttu-id="8b233-216">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="8b233-216">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="8b233-218">Na liście aplikacji zaznacz **PurelyHR**.</span><span class="sxs-lookup"><span data-stu-id="8b233-218">In the applications list, select **PurelyHR**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_app.png) 

3. <span data-ttu-id="8b233-220">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="8b233-220">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="8b233-222">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8b233-222">Click **Add** button.</span></span> <span data-ttu-id="8b233-223">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8b233-223">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="8b233-225">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="8b233-225">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8b233-226">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8b233-226">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8b233-227">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8b233-227">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8b233-228">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8b233-228">Testing single sign-on</span></span>

<span data-ttu-id="8b233-229">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="8b233-229">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8b233-230">Kliknij Kafelek LMS przyjęcia w panelu dostępu, możesz pobrać automatycznie zalogowane do przyjęcia LMS aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8b233-230">Click the Absorb LMS tile in the Access Panel, you get automatically signed-on to your Absorb LMS application.</span></span>

<span data-ttu-id="8b233-231">Aby uzyskać więcej informacji na temat panelu dostępu Zobacz.</span><span class="sxs-lookup"><span data-stu-id="8b233-231">For more information about the Access Panel, see.</span></span> <span data-ttu-id="8b233-232">[Wprowadzenie do panelu dostępu](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="8b233-232">[Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8b233-233">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="8b233-233">Additional resources</span></span>

* [<span data-ttu-id="8b233-234">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8b233-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8b233-235">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8b233-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_203.png

