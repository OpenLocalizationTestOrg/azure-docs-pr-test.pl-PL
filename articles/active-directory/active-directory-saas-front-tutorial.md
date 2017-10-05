---
title: 'Samouczek: Integracji Azure Active Directory z przodu | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między Azure Active Directory i do przodu."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 88270b6d-2571-434a-b139-b6ccc3a2b19f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: d936bc50a66ac2a3c17038ff08351edf9902c99f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-front"></a><span data-ttu-id="eedf2-103">Samouczek: Integracji Azure Active Directory z przodu</span><span class="sxs-lookup"><span data-stu-id="eedf2-103">Tutorial: Azure Active Directory integration with Front</span></span>

<span data-ttu-id="eedf2-104">Z tego samouczka dowiesz integrowanie przodu z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="eedf2-104">In this tutorial, you learn how to integrate Front with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="eedf2-105">Integrowanie przodu z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="eedf2-105">Integrating Front with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="eedf2-106">Można kontrolować w usłudze Azure AD, który ma dostęp do przodu.</span><span class="sxs-lookup"><span data-stu-id="eedf2-106">You can control in Azure AD who has access to Front.</span></span>
- <span data-ttu-id="eedf2-107">Umożliwia użytkownikom automatycznie pobrać zalogowane na wierzch (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eedf2-107">You can enable your users to automatically get signed-on to Front (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="eedf2-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="eedf2-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="eedf2-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="eedf2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eedf2-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="eedf2-110">Prerequisites</span></span>

<span data-ttu-id="eedf2-111">Aby skonfigurować integrację usługi Azure AD z przodu, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="eedf2-111">To configure Azure AD integration with Front, you need the following items:</span></span>

- <span data-ttu-id="eedf2-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="eedf2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="eedf2-113">Front logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="eedf2-113">A Front single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="eedf2-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="eedf2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="eedf2-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="eedf2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="eedf2-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="eedf2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="eedf2-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="eedf2-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="eedf2-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="eedf2-118">Scenario description</span></span>
<span data-ttu-id="eedf2-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="eedf2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="eedf2-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="eedf2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="eedf2-121">Dodawanie przodu z galerii</span><span class="sxs-lookup"><span data-stu-id="eedf2-121">Adding Front from the gallery</span></span>
2. <span data-ttu-id="eedf2-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="eedf2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-front-from-the-gallery"></a><span data-ttu-id="eedf2-123">Dodawanie przodu z galerii</span><span class="sxs-lookup"><span data-stu-id="eedf2-123">Adding Front from the gallery</span></span>
<span data-ttu-id="eedf2-124">Aby skonfigurować integrację z przodu do usługi Azure AD, należy dodać przodu z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="eedf2-124">To configure the integration of Front into Azure AD, you need to add Front from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="eedf2-125">**Aby dodać przodu z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="eedf2-125">**To add Front from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="eedf2-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="eedf2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Przycisk usługi Azure Active Directory][1]

2. <span data-ttu-id="eedf2-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="eedf2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="eedf2-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="eedf2-129">Then go to **All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa][2]
    
3. <span data-ttu-id="eedf2-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="eedf2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Nowy przycisk aplikacji][3]

4. <span data-ttu-id="eedf2-133">W polu wyszukiwania wpisz **Front**, wybierz pozycję **Front** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="eedf2-133">In the search box, type **Front**, select **Front** from result panel then click **Add** button to add the application.</span></span>

    ![Front na liście wyników](./media/active-directory-saas-front-tutorial/tutorial_front_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="eedf2-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="eedf2-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="eedf2-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z przodu w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="eedf2-136">In this section, you configure and test Azure AD single sign-on with Front based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="eedf2-137">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć z przodu użytkownik odpowiednikiem jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eedf2-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Front is to a user in Azure AD.</span></span> <span data-ttu-id="eedf2-138">Innymi słowy musi można ustanowić łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi na wierzchu.</span><span class="sxs-lookup"><span data-stu-id="eedf2-138">In other words, a link relationship between an Azure AD user and the related user in Front needs to be established.</span></span>

<span data-ttu-id="eedf2-139">Na wierzchu przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="eedf2-139">In Front, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="eedf2-140">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z przodu, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="eedf2-140">To configure and test Azure AD single sign-on with Front, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="eedf2-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="eedf2-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="eedf2-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="eedf2-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="eedf2-143">**[Tworzenie użytkownika testowego przodu](#create-a-front-test-user)**  — aby odpowiednikiem Simona Britta na wierzchu połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="eedf2-143">**[Create a Front test user](#create-a-front-test-user)** - to have a counterpart of Britta Simon in Front that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="eedf2-144">**[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="eedf2-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="eedf2-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="eedf2-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="eedf2-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="eedf2-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="eedf2-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne do przodu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="eedf2-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Front application.</span></span>

<span data-ttu-id="eedf2-148">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z przodu, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="eedf2-148">**To configure Azure AD single sign-on with Front, perform the following steps:**</span></span>

1. <span data-ttu-id="eedf2-149">W portalu Azure na **Front** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="eedf2-149">In the Azure portal, on the **Front** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="eedf2-151">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="eedf2-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-front-tutorial/tutorial_front_samlbase.png)

3. <span data-ttu-id="eedf2-153">Na **Front domeny i adres URL** sekcji, jeśli chcesz skonfigurować aplikację w **IDP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="eedf2-153">On the **Front Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-front-tutorial/tutorial_front_url1.png)

    <span data-ttu-id="eedf2-155">a.</span><span class="sxs-lookup"><span data-stu-id="eedf2-155">a.</span></span> <span data-ttu-id="eedf2-156">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.frontapp.com`</span><span class="sxs-lookup"><span data-stu-id="eedf2-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.frontapp.com`</span></span>

    <span data-ttu-id="eedf2-157">b.</span><span class="sxs-lookup"><span data-stu-id="eedf2-157">b.</span></span> <span data-ttu-id="eedf2-158">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.frontapp.com/sso/saml/callback`</span><span class="sxs-lookup"><span data-stu-id="eedf2-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.frontapp.com/sso/saml/callback`</span></span>

4. <span data-ttu-id="eedf2-159">Sprawdź **Pokaż zaawansowane ustawienia adresu URL**, jeśli chcesz skonfigurować aplikację w **SP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="eedf2-159">Check **Show advanced URL settings**, If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-front-tutorial/tutorial_front_url2.png)

    <span data-ttu-id="eedf2-161">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.frontapp.com`</span><span class="sxs-lookup"><span data-stu-id="eedf2-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.frontapp.com`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="eedf2-162">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="eedf2-162">These values are not real.</span></span> <span data-ttu-id="eedf2-163">Zaktualizować te wartości z rzeczywistego identyfikatora, adres URL odpowiedzi i adres URL logowania, które opisano szczegółowo w dalszej części samouczka lub skontaktuj się z [zespołem pomocy technicznej klienta Front](mailto:support@frontapp.com) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="eedf2-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL which are explained later in tutorial or contact [Front Client support team](mailto:support@frontapp.com) to get these values.</span></span> 

5. <span data-ttu-id="eedf2-164">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="eedf2-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-front-tutorial/tutorial_front_certificate.png) 

6. <span data-ttu-id="eedf2-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="eedf2-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-front-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="eedf2-168">Na **konfiguracji frontonu** kliknij **skonfigurować Front** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="eedf2-168">On the **Front Configuration** section, click **Configure Front** to open **Configure sign-on** window.</span></span> <span data-ttu-id="eedf2-169">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="eedf2-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-front-tutorial/tutorial_front_configure.png) 

8. <span data-ttu-id="eedf2-171">Logowanie do przodu dzierżawy z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="eedf2-171">Sign-on to your Front tenant as an administrator.</span></span>

9. <span data-ttu-id="eedf2-172">Przejdź do **ustawień (koło zębate ikonę na dole po lewej stronie paska bocznego) > Preferencje**.</span><span class="sxs-lookup"><span data-stu-id="eedf2-172">Go to **Settings (cog icon at the bottom of the left sidebar) > Preferences**.</span></span>
   
    ![Konfigurowanie jednej logowania w aplikacji po stronie](./media/active-directory-saas-front-tutorial/tutorial_front_000.png)

10. <span data-ttu-id="eedf2-174">Kliknij przycisk **rejestracji jednokrotnej** łącza.</span><span class="sxs-lookup"><span data-stu-id="eedf2-174">Click **Single Sign On** link.</span></span>
   
    ![Konfigurowanie jednej logowania w aplikacji po stronie](./media/active-directory-saas-front-tutorial/tutorial_front_001.png)

11. <span data-ttu-id="eedf2-176">Wybierz **SAML** na liście rozwijanej **rejestracji jednokrotnej**.</span><span class="sxs-lookup"><span data-stu-id="eedf2-176">Select **SAML** in the drop-down list of **Single Sign On**.</span></span>
   
    ![Konfigurowanie jednej logowania w aplikacji po stronie](./media/active-directory-saas-front-tutorial/tutorial_front_002.png)

12. <span data-ttu-id="eedf2-178">W **punktu wejścia** pole tekstowe umieścić wartość elementu **pojedynczy znak na adres URL usługi** z Kreatora konfiguracji aplikacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eedf2-178">In the **Entry Point** textbox put the value of **Single Sign-on Service URL** from Azure AD application configuration wizard.</span></span>
    
    ![Konfigurowanie jednej logowania w aplikacji po stronie](./media/active-directory-saas-front-tutorial/tutorial_front_003.png)

13. <span data-ttu-id="eedf2-180">Otwórz z pobranego **Certificate(Base64)** plików w programie Notatnik, skopiuj zawartość go do Schowka, a następnie wklej go do **certyfikatu podpisywania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="eedf2-180">Open your downloaded **Certificate(Base64)** file in notepad, copy the content of it into your clipboard, and then paste it to the **Signing certificate** textbox.</span></span>
    
    ![Konfigurowanie jednej logowania w aplikacji po stronie](./media/active-directory-saas-front-tutorial/tutorial_front_004.png)

14. <span data-ttu-id="eedf2-182">Na **ustawień dostawcy usług** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="eedf2-182">On the **Service provider settings** section, perform the following steps:</span></span>

    ![Konfigurowanie jednej logowania w aplikacji po stronie](./media/active-directory-saas-front-tutorial/tutorial_front_005.png)

    <span data-ttu-id="eedf2-184">a.</span><span class="sxs-lookup"><span data-stu-id="eedf2-184">a.</span></span> <span data-ttu-id="eedf2-185">Skopiuj wartość **identyfikator jednostki** i wklej ją do **identyfikator** textbox w **Front domeny i adres URL** sekcji w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="eedf2-185">Copy the value of **Entity ID** and paste it into the **Identifier** textbox in **Front Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="eedf2-186">b.</span><span class="sxs-lookup"><span data-stu-id="eedf2-186">b.</span></span> <span data-ttu-id="eedf2-187">Skopiuj wartość **adres URL usługi ACS** i wklej ją do **adres URL logowania** textbox w **Front domeny i adres URL** sekcji w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="eedf2-187">Copy the value of **ACS URL** and paste it into the **Sign-on URL** textbox in **Front Domain and URLs** section in Azure portal.</span></span>
    
15. <span data-ttu-id="eedf2-188">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="eedf2-188">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="eedf2-189">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="eedf2-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="eedf2-190">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="eedf2-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="eedf2-191">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="eedf2-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="eedf2-192">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="eedf2-192">Create an Azure AD test user</span></span>

<span data-ttu-id="eedf2-193">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="eedf2-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="eedf2-195">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="eedf2-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="eedf2-196">W portalu Azure, w okienku po lewej stronie kliknij **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="eedf2-196">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Przycisk usługi Azure Active Directory](./media/active-directory-saas-front-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="eedf2-198">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="eedf2-198">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-front-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="eedf2-200">Aby otworzyć **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** w górnej części **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="eedf2-200">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Przycisk Dodaj](./media/active-directory-saas-front-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="eedf2-202">W **użytkownika** okna dialogowego wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="eedf2-202">In the **User** dialog box, perform the following steps:</span></span>

    ![Okno dialogowe użytkownika](./media/active-directory-saas-front-tutorial/create_aaduser_04.png)

    <span data-ttu-id="eedf2-204">a.</span><span class="sxs-lookup"><span data-stu-id="eedf2-204">a.</span></span> <span data-ttu-id="eedf2-205">W **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="eedf2-205">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="eedf2-206">b.</span><span class="sxs-lookup"><span data-stu-id="eedf2-206">b.</span></span> <span data-ttu-id="eedf2-207">W **nazwy użytkownika** wpisz adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="eedf2-207">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="eedf2-208">c.</span><span class="sxs-lookup"><span data-stu-id="eedf2-208">c.</span></span> <span data-ttu-id="eedf2-209">Wybierz **Pokaż hasło** pole wyboru, a następnie zanotuj wartość, która jest wyświetlana w **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="eedf2-209">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="eedf2-210">d.</span><span class="sxs-lookup"><span data-stu-id="eedf2-210">d.</span></span> <span data-ttu-id="eedf2-211">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="eedf2-211">Click **Create**.</span></span>
 
### <a name="create-a-front-test-user"></a><span data-ttu-id="eedf2-212">Tworzenie użytkownika testowego przodu</span><span class="sxs-lookup"><span data-stu-id="eedf2-212">Create a Front test user</span></span>

<span data-ttu-id="eedf2-213">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta na wierzchu.</span><span class="sxs-lookup"><span data-stu-id="eedf2-213">In this section, you create a user called Britta Simon in Front.</span></span> <span data-ttu-id="eedf2-214">Praca z [zespołem pomocy technicznej klienta Front](mailto:support@frontapp.com) Aby dodać użytkowników do przodu platformy.</span><span class="sxs-lookup"><span data-stu-id="eedf2-214">Work with [Front Client support team](mailto:support@frontapp.com) to add the users in the Front platform.</span></span> <span data-ttu-id="eedf2-215">Użytkownicy muszą utworzyć i aktywowana, aby użyć rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="eedf2-215">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="eedf2-216">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="eedf2-216">Assign the Azure AD test user</span></span>

<span data-ttu-id="eedf2-217">W tej sekcji musisz włączyć Simona Britta do użycia usługi Azure logowania jednokrotnego za udzielanie dostępu do przodu.</span><span class="sxs-lookup"><span data-stu-id="eedf2-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Front.</span></span>

![Przypisanie roli użytkownika][200] 

<span data-ttu-id="eedf2-219">**Aby przypisać Simona Britta do przodu, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="eedf2-219">**To assign Britta Simon to Front, perform the following steps:**</span></span>

1. <span data-ttu-id="eedf2-220">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="eedf2-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="eedf2-222">Na liście aplikacji zaznacz **Front**.</span><span class="sxs-lookup"><span data-stu-id="eedf2-222">In the applications list, select **Front**.</span></span>

    ![Łącze przodu na liście aplikacji](./media/active-directory-saas-front-tutorial/tutorial_front_app.png)  

3. <span data-ttu-id="eedf2-224">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="eedf2-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Łącze "Użytkownicy i grupy"][202]

4. <span data-ttu-id="eedf2-226">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="eedf2-226">Click **Add** button.</span></span> <span data-ttu-id="eedf2-227">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="eedf2-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![W okienku Dodaj przydziału][203]

5. <span data-ttu-id="eedf2-229">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="eedf2-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="eedf2-230">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="eedf2-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="eedf2-231">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="eedf2-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="eedf2-232">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="eedf2-232">Test single sign-on</span></span>

<span data-ttu-id="eedf2-233">Celem tej sekcji służy do testowania programu Azure AD SSOconfiguration, za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="eedf2-233">The objective of this section is to test your Azure AD SSOconfiguration using the Access Panel.</span></span>

<span data-ttu-id="eedf2-234">Po kliknięciu kafelka przodu w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do przodu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="eedf2-234">When you click the Front tile in the Access Panel, you should get automatically signed-on to your Front application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="eedf2-235">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="eedf2-235">Additional resources</span></span>

* [<span data-ttu-id="eedf2-236">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="eedf2-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="eedf2-237">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="eedf2-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-front-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-front-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-front-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-front-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-front-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-front-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-front-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-front-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-front-tutorial/tutorial_general_203.png

