---
title: "Samouczek: Integracji Azure Active Directory z usługi Zendesk | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i usługi Zendesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9d7c91e5-78f5-4016-862f-0f3242b00680
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 51c06d838c5ed6286dfb99ea25faaaf33bad5f3c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zendesk"></a><span data-ttu-id="e002a-103">Samouczek: Integracji Azure Active Directory z usługi Zendesk</span><span class="sxs-lookup"><span data-stu-id="e002a-103">Tutorial: Azure Active Directory integration with Zendesk</span></span>

<span data-ttu-id="e002a-104">Z tego samouczka dowiesz się Integrowanie usługi Zendesk w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e002a-104">In this tutorial, you learn how to integrate Zendesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e002a-105">Integrowanie usługi Zendesk z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="e002a-105">Integrating Zendesk with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e002a-106">Można kontrolować w usłudze Azure AD, który ma dostęp do usługi Zendesk</span><span class="sxs-lookup"><span data-stu-id="e002a-106">You can control in Azure AD who has access to Zendesk</span></span>
- <span data-ttu-id="e002a-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Zendesk (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e002a-107">You can enable your users to automatically get signed-on to Zendesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e002a-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="e002a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e002a-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e002a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e002a-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e002a-110">Prerequisites</span></span>

<span data-ttu-id="e002a-111">Aby skonfigurować integrację usługi Azure AD z usługi Zendesk, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="e002a-111">To configure Azure AD integration with Zendesk, you need the following items:</span></span>

- <span data-ttu-id="e002a-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e002a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e002a-113">Zendesk logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="e002a-113">A Zendesk single sign-on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="e002a-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="e002a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="e002a-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="e002a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e002a-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="e002a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e002a-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e002a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="e002a-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="e002a-118">Scenario description</span></span>
<span data-ttu-id="e002a-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="e002a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e002a-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="e002a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e002a-121">Dodawanie Zendesk z galerii</span><span class="sxs-lookup"><span data-stu-id="e002a-121">Adding Zendesk from the gallery</span></span>
2. <span data-ttu-id="e002a-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="e002a-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-zendesk-from-the-gallery"></a><span data-ttu-id="e002a-123">Dodawanie Zendesk z galerii</span><span class="sxs-lookup"><span data-stu-id="e002a-123">Adding Zendesk from the gallery</span></span>
<span data-ttu-id="e002a-124">Aby skonfigurować integrację usługi Zendesk w usłudze Azure Active Directory, należy dodać Zendesk z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="e002a-124">To configure the integration of Zendesk into Azure AD, you need to add Zendesk from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e002a-125">**Aby dodać Zendesk z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="e002a-125">**To add Zendesk from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e002a-126">W  **[Azure Portal](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="e002a-126">In the **[Azure Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="e002a-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="e002a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e002a-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="e002a-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="e002a-131">Kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e002a-131">Click **New application** button on the top of the dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="e002a-133">W polu wyszukiwania wpisz **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="e002a-133">In the search box, type **Zendesk**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_search.png)

5. <span data-ttu-id="e002a-135">W panelu wyników wybierz **Zendesk**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="e002a-135">In the results panel, select **Zendesk**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e002a-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="e002a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e002a-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z usługi Zendesk w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="e002a-138">In this section, you configure and test Azure AD single sign-on with Zendesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e002a-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Zendesk jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e002a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Zendesk is to a user in Azure AD.</span></span> <span data-ttu-id="e002a-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Zendesk musi się.</span><span class="sxs-lookup"><span data-stu-id="e002a-140">In other words, a link relationship between an Azure AD user and the related user in Zendesk needs to be established.</span></span>

<span data-ttu-id="e002a-141">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w Zendesk.</span><span class="sxs-lookup"><span data-stu-id="e002a-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Zendesk.</span></span>

<span data-ttu-id="e002a-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z usługi Zendesk, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="e002a-142">To configure and test Azure AD single sign-on with Zendesk, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e002a-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="e002a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e002a-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="e002a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e002a-145">**[Tworzenie użytkownika testowego Zendesk](#creating-a-zendesk-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Zendesk połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e002a-145">**[Creating a Zendesk test user](#creating-a-zendesk-test-user)** - to have a counterpart of Britta Simon in Zendesk that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e002a-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="e002a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e002a-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="e002a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e002a-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e002a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e002a-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Zendesk.</span><span class="sxs-lookup"><span data-stu-id="e002a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zendesk application.</span></span>

<span data-ttu-id="e002a-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z usługi Zendesk, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="e002a-150">**To configure Azure AD single sign-on with Zendesk, perform the following steps:**</span></span>

1. <span data-ttu-id="e002a-151">W portalu Azure na **Zendesk** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="e002a-151">In the Azure portal, on the **Zendesk** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="e002a-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="e002a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_samlbase.png)

3. <span data-ttu-id="e002a-155">Na **Zendesk domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="e002a-155">On the **Zendesk Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_url.png)

    <span data-ttu-id="e002a-157">a.</span><span class="sxs-lookup"><span data-stu-id="e002a-157">a.</span></span> <span data-ttu-id="e002a-158">W **adres URL logowania** tekstowym, wpisz wartość, przy użyciu następującego wzorca:`https://<subdomain>.zendesk.com`</span><span class="sxs-lookup"><span data-stu-id="e002a-158">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<subdomain>.zendesk.com`</span></span>

    <span data-ttu-id="e002a-159">b.</span><span class="sxs-lookup"><span data-stu-id="e002a-159">b.</span></span> <span data-ttu-id="e002a-160">W **identyfikator** tekstowym, wpisz wartość, przy użyciu następującego wzorca:`https://<subdomain>.zendesk.com`</span><span class="sxs-lookup"><span data-stu-id="e002a-160">In the **Identifier** textbox, type the value using the following pattern: `https://<subdomain>.zendesk.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e002a-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="e002a-161">These values are not real.</span></span> <span data-ttu-id="e002a-162">Rzeczywisty adres URL logowania i adres URL identyfikatora, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="e002a-162">Update these values with the actual Sign-on URL and Identifier URL.</span></span> <span data-ttu-id="e002a-163">Skontaktuj się z [zespołem pomocy technicznej usługi Zendesk](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="e002a-163">Contact [Zendesk support team](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise) to get these values.</span></span> 

4. <span data-ttu-id="e002a-164">Zendesk oczekuje potwierdzenia języka SAML w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="e002a-164">Zendesk expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="e002a-165">Nie obowiązkowych atrybutów SAML, ale Opcjonalnie można dodać atrybutu z **atrybuty użytkownika** sekcji, wykonując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="e002a-165">There are no mandatory SAML attributes but optionally you can add an attribute from **User Attributes** section by following the below steps:</span></span> 

     ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes1.png)

    <span data-ttu-id="e002a-167">a.</span><span class="sxs-lookup"><span data-stu-id="e002a-167">a.</span></span> <span data-ttu-id="e002a-168">Kliknij przycisk **wyświetlanie i edytowanie wszystkimi innymi atrybutami** pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="e002a-168">Click the **View and edit all the other attributes** check box.</span></span>
     
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes2.png)
   
    <span data-ttu-id="e002a-170">b.</span><span class="sxs-lookup"><span data-stu-id="e002a-170">b.</span></span> <span data-ttu-id="e002a-171">Kliknij przycisk **Dodawanie atrybutu** otworzyć **Dodaj atrybut** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e002a-171">Click the **Add Attribute** to open **Add attribute** dialog.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zendesk-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="e002a-173">c.</span><span class="sxs-lookup"><span data-stu-id="e002a-173">c.</span></span> <span data-ttu-id="e002a-174">W **nazwa** tekstowym, wpisz nazwę atrybutu (na przykład **emailaddress**).</span><span class="sxs-lookup"><span data-stu-id="e002a-174">In the **Name** textbox, type the attribute name (for example **emailaddress**).</span></span>
    
    <span data-ttu-id="e002a-175">d.</span><span class="sxs-lookup"><span data-stu-id="e002a-175">d.</span></span> <span data-ttu-id="e002a-176">Z **wartość** , wybierz wartość atrybutu na liście (jako **user.mail**).</span><span class="sxs-lookup"><span data-stu-id="e002a-176">From the **Value** list, select the attribute value (as **user.mail**).</span></span>
    
    <span data-ttu-id="e002a-177">e.</span><span class="sxs-lookup"><span data-stu-id="e002a-177">e.</span></span> <span data-ttu-id="e002a-178">Kliknij przycisk **Ok**</span><span class="sxs-lookup"><span data-stu-id="e002a-178">Click **Ok**</span></span>
 
    > [!NOTE] 
    > <span data-ttu-id="e002a-179">Atrybuty rozszerzenia umożliwia dodawanie atrybutów, które nie znajdują się w usłudze Azure AD domyślnie.</span><span class="sxs-lookup"><span data-stu-id="e002a-179">You use extension attributes to add attributes that are not in Azure AD by default.</span></span> <span data-ttu-id="e002a-180">Kliknij przycisk [atrybutów użytkowników, które można ustawić w SAML](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) Aby uzyskać pełną listę SAML atrybuty, które **Zendesk** akceptuje.</span><span class="sxs-lookup"><span data-stu-id="e002a-180">Click [User attributes that can be set in SAML](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) to get the complete list of SAML attributes that **Zendesk** accepts.</span></span> 

5. <span data-ttu-id="e002a-181">Na **certyfikat podpisywania SAML** sekcji, skopiuj **odcisk PALCA** wartości certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="e002a-181">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_certificate.png) 

6. <span data-ttu-id="e002a-183">Na **konfiguracji Zendesk** , kliknij przycisk **skonfigurować Zendesk** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="e002a-183">On the **Zendesk Configuration** section, click **Configure Zendesk** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e002a-184">Kopiuj **Sign-Out adresu URL i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="e002a-184">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_configure.png) 

7. <span data-ttu-id="e002a-186">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy Zendesk jako administrator.</span><span class="sxs-lookup"><span data-stu-id="e002a-186">In a different web browser window, log into your Zendesk company site as an administrator.</span></span>

8. <span data-ttu-id="e002a-187">Kliknij przycisk **Admin**.</span><span class="sxs-lookup"><span data-stu-id="e002a-187">Click **Admin**.</span></span>

9. <span data-ttu-id="e002a-188">W okienku nawigacji po lewej stronie kliknij **ustawienia**, a następnie kliknij przycisk **zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="e002a-188">In the left navigation pane, click **Settings**, and then click **Security**.</span></span>

10. <span data-ttu-id="e002a-189">Na **zabezpieczeń** wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="e002a-189">On the **Security** page, perform the following steps:</span></span> 
   
     <span data-ttu-id="e002a-190">![Zabezpieczenia](./media/active-directory-saas-zendesk-tutorial/ic773089.png "zabezpieczeń")</span><span class="sxs-lookup"><span data-stu-id="e002a-190">![Security](./media/active-directory-saas-zendesk-tutorial/ic773089.png "Security")</span></span>

    <span data-ttu-id="e002a-191">![Logowanie jednokrotne](./media/active-directory-saas-zendesk-tutorial/ic773090.png "logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="e002a-191">![Single sign-on](./media/active-directory-saas-zendesk-tutorial/ic773090.png "Single sign-on")</span></span>

     <span data-ttu-id="e002a-192">a.</span><span class="sxs-lookup"><span data-stu-id="e002a-192">a.</span></span> <span data-ttu-id="e002a-193">Kliknij przycisk **Admin & agentów** kartę.</span><span class="sxs-lookup"><span data-stu-id="e002a-193">Click the **Admin & Agents** tab.</span></span>

     <span data-ttu-id="e002a-194">b.</span><span class="sxs-lookup"><span data-stu-id="e002a-194">b.</span></span> <span data-ttu-id="e002a-195">Wybierz **logowanie jednokrotne (SSO) oraz SAML**, a następnie wybierz **SAML**.</span><span class="sxs-lookup"><span data-stu-id="e002a-195">Select **Single sign-on (SSO) and SAML**, and then select **SAML**.</span></span>

     <span data-ttu-id="e002a-196">c.</span><span class="sxs-lookup"><span data-stu-id="e002a-196">c.</span></span> <span data-ttu-id="e002a-197">W **adres URL logowania jednokrotnego SAML** pole tekstowe, Wklej wartość **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e002a-197">In **SAML SSO URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

     <span data-ttu-id="e002a-198">d.</span><span class="sxs-lookup"><span data-stu-id="e002a-198">d.</span></span> <span data-ttu-id="e002a-199">W **zdalnego adresu URL wylogowania** pole tekstowe, Wklej wartość **Sign-Out URL** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e002a-199">In **Remote Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
        
     <span data-ttu-id="e002a-200">e.</span><span class="sxs-lookup"><span data-stu-id="e002a-200">e.</span></span> <span data-ttu-id="e002a-201">W **odcisk palca certyfikatu** pole tekstowe, Wklej **odcisk palca** wartość certyfikatów, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e002a-201">In **Certificate Fingerprint** textbox, paste the **Thumbprint** value of certificate which you have copied from Azure portal.</span></span>
     
     <span data-ttu-id="e002a-202">f.</span><span class="sxs-lookup"><span data-stu-id="e002a-202">f.</span></span> <span data-ttu-id="e002a-203">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="e002a-203">Click **Save**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e002a-204">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e002a-204">Creating an Azure AD test user</span></span>
<span data-ttu-id="e002a-205">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="e002a-205">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="e002a-207">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="e002a-207">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e002a-208">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="e002a-208">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e002a-210">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="e002a-210">To display the list of users go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e002a-212">W górnej części okna dialogowego, kliknij przycisk **Dodaj** otworzyć **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e002a-212">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e002a-214">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="e002a-214">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e002a-216">a.</span><span class="sxs-lookup"><span data-stu-id="e002a-216">a.</span></span> <span data-ttu-id="e002a-217">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e002a-217">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e002a-218">b.</span><span class="sxs-lookup"><span data-stu-id="e002a-218">b.</span></span> <span data-ttu-id="e002a-219">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e002a-219">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e002a-220">c.</span><span class="sxs-lookup"><span data-stu-id="e002a-220">c.</span></span> <span data-ttu-id="e002a-221">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="e002a-221">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e002a-222">d.</span><span class="sxs-lookup"><span data-stu-id="e002a-222">d.</span></span> <span data-ttu-id="e002a-223">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="e002a-223">Click **Create**.</span></span> 

### <a name="creating-a-zendesk-test-user"></a><span data-ttu-id="e002a-224">Tworzenie użytkownika testowego Zendesk</span><span class="sxs-lookup"><span data-stu-id="e002a-224">Creating a Zendesk test user</span></span>

<span data-ttu-id="e002a-225">Aby umożliwić użytkownikom zalogować się do usługi Azure AD **Zendesk**, muszą mieć przydzielone do **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="e002a-225">To enable Azure AD users to log into **Zendesk**, they must be provisioned into **Zendesk**.</span></span>  
<span data-ttu-id="e002a-226">W zależności od roli przypisanej w aplikacji jest oczekiwane zachowanie:</span><span class="sxs-lookup"><span data-stu-id="e002a-226">Depending on the role assigned in the apps, it's the expected behavior:</span></span>

 1. <span data-ttu-id="e002a-227">**Użytkownik końcowy** konta są automatycznie konfigurowani podczas logowania.</span><span class="sxs-lookup"><span data-stu-id="e002a-227">**End-user** accounts are automatically provisioned when signing in.</span></span>
 2. <span data-ttu-id="e002a-228">**Agent** i **Admin** należy ręcznie udostępniane w kont **Zendesk** przed zarejestrowaniem się.</span><span class="sxs-lookup"><span data-stu-id="e002a-228">**Agent** and **Admin** accounts need to be manually provisioned in **Zendesk** before signing in.</span></span>
 
<span data-ttu-id="e002a-229">**Aby udostępnić konta użytkownika, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="e002a-229">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="e002a-230">Zaloguj się do Twojego **Zendesk** dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="e002a-230">Log in to your **Zendesk** tenant.</span></span>

2. <span data-ttu-id="e002a-231">Wybierz **listy odbiorców** kartę.</span><span class="sxs-lookup"><span data-stu-id="e002a-231">Select the **Customer List** tab.</span></span>

3. <span data-ttu-id="e002a-232">Wybierz **użytkownika** , a następnie kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="e002a-232">Select the **User** tab, and click **Add**.</span></span>
   
    <span data-ttu-id="e002a-233">![Dodaj użytkownika](./media/active-directory-saas-zendesk-tutorial/ic773632.png "Dodaj użytkownika")</span><span class="sxs-lookup"><span data-stu-id="e002a-233">![Add user](./media/active-directory-saas-zendesk-tutorial/ic773632.png "Add user")</span></span>
4. <span data-ttu-id="e002a-234">Wpisz adres e-mail istniejącego konta usługi Azure AD do udostępniania, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="e002a-234">Type the email address of an existing Azure AD account you want to provision, and then click **Save**.</span></span>
   
    <span data-ttu-id="e002a-235">![Nowy użytkownik](./media/active-directory-saas-zendesk-tutorial/ic773633.png "nowego użytkownika")</span><span class="sxs-lookup"><span data-stu-id="e002a-235">![New user](./media/active-directory-saas-zendesk-tutorial/ic773633.png "New user")</span></span>

> [!NOTE]
> <span data-ttu-id="e002a-236">Możesz użyć innych Zendesk użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Zendesk do kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="e002a-236">You can use any other Zendesk user account creation tools or APIs provided by Zendesk to provision AAD user accounts.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e002a-237">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e002a-237">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e002a-238">W tej sekcji musisz włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do usługi Zendesk.</span><span class="sxs-lookup"><span data-stu-id="e002a-238">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zendesk.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="e002a-240">**Aby przypisać Simona Britta Zendesk, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="e002a-240">**To assign Britta Simon to Zendesk, perform the following steps:**</span></span>

1. <span data-ttu-id="e002a-241">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="e002a-241">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="e002a-243">Na liście aplikacji zaznacz **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="e002a-243">In the applications list, select **Zendesk**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_app.png) 

3. <span data-ttu-id="e002a-245">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="e002a-245">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="e002a-247">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e002a-247">Click **Add** button.</span></span> <span data-ttu-id="e002a-248">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e002a-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="e002a-250">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="e002a-250">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e002a-251">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e002a-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e002a-252">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e002a-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e002a-253">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e002a-253">Testing single sign-on</span></span>

<span data-ttu-id="e002a-254">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="e002a-254">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e002a-255">Po kliknięciu kafelka Zendesk w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji usługi Zendesk.</span><span class="sxs-lookup"><span data-stu-id="e002a-255">When you click the Zendesk tile in the Access Panel, you should get automatically signed-on to your Zendesk application.</span></span>
<span data-ttu-id="e002a-256">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e002a-256">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e002a-257">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="e002a-257">Additional resources</span></span>

* [<span data-ttu-id="e002a-258">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e002a-258">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e002a-259">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e002a-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_203.png
