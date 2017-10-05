---
title: "Samouczek: Integrację usługi Azure Active Directory ze ScaleX | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i ScaleX Enterprise."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2379a8d-a659-45f1-87db-9ba156d83183
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: jeedes
ms.openlocfilehash: 0ebed0c2605862426384c0e219e52c9d626b6246
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scalex-enterprise"></a><span data-ttu-id="79c23-103">Samouczek: Integrację usługi Azure Active Directory ze ScaleX</span><span class="sxs-lookup"><span data-stu-id="79c23-103">Tutorial: Azure Active Directory integration with ScaleX Enterprise</span></span>

<span data-ttu-id="79c23-104">Z tego samouczka dowiesz się integrowanie ScaleX przedsiębiorstwa w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="79c23-104">In this tutorial, you learn how to integrate ScaleX Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="79c23-105">Integrowanie ScaleX organizacji z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="79c23-105">Integrating ScaleX Enterprise with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="79c23-106">Można kontrolować w usłudze Azure AD, który ma dostęp do ScaleX Enterprise</span><span class="sxs-lookup"><span data-stu-id="79c23-106">You can control in Azure AD who has access to ScaleX Enterprise</span></span>
- <span data-ttu-id="79c23-107">Umożliwia użytkownikom automatycznie pobrać zalogowane ScaleX przedsiębiorstwem (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="79c23-107">You can enable your users to automatically get signed-on to ScaleX Enterprise (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="79c23-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="79c23-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="79c23-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz.</span><span class="sxs-lookup"><span data-stu-id="79c23-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="79c23-110">Co to jest dostęp do aplikacji i logowanie jednokrotne z [usługi Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="79c23-110">What is application access and single sign-on with [Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79c23-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="79c23-111">Prerequisites</span></span>

<span data-ttu-id="79c23-112">Aby skonfigurować integrację usługi Azure AD z ScaleX przedsiębiorstwa, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="79c23-112">To configure Azure AD integration with ScaleX Enterprise, you need the following items:</span></span>

- <span data-ttu-id="79c23-113">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="79c23-113">An Azure AD subscription</span></span>
- <span data-ttu-id="79c23-114">ScaleX Enterprise jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="79c23-114">A ScaleX Enterprise single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="79c23-115">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="79c23-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="79c23-116">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="79c23-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="79c23-117">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="79c23-117">Do not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="79c23-118">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="79c23-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="79c23-119">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="79c23-119">Scenario description</span></span>
<span data-ttu-id="79c23-120">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="79c23-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="79c23-121">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="79c23-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="79c23-122">Dodawanie ScaleX przedsiębiorstwa z galerii</span><span class="sxs-lookup"><span data-stu-id="79c23-122">Adding ScaleX Enterprise from the gallery</span></span>
2. <span data-ttu-id="79c23-123">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="79c23-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-scalex-enterprise-from-the-gallery"></a><span data-ttu-id="79c23-124">Dodawanie ScaleX przedsiębiorstwa z galerii</span><span class="sxs-lookup"><span data-stu-id="79c23-124">Adding ScaleX Enterprise from the gallery</span></span>
<span data-ttu-id="79c23-125">Aby skonfigurować integrację ScaleX przedsiębiorstwa w usłudze Azure AD, należy dodać ScaleX przedsiębiorstwa z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="79c23-125">To configure the integration of ScaleX Enterprise in to Azure AD, you need to add ScaleX Enterprise from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="79c23-126">**Aby dodać ScaleX przedsiębiorstwa z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="79c23-126">**To add ScaleX Enterprise from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="79c23-127">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="79c23-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="79c23-129">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="79c23-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="79c23-130">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="79c23-130">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="79c23-132">Kliknij przycisk **Dodaj** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="79c23-132">Click **Add** button on the top of the dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="79c23-134">W polu wyszukiwania wpisz **ScaleX Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="79c23-134">In the search box, type **ScaleX Enterprise**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_search.png)

5. <span data-ttu-id="79c23-136">W panelu wyników wybierz **ScaleX Enterprise**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="79c23-136">In the results panel, select **ScaleX Enterprise**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="79c23-138">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="79c23-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="79c23-139">W tej sekcji możesz skonfigurować i test usługi Azure AD rejestracji jednokrotnej z ScaleX Enterprise oparte na użytkownika testowego o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="79c23-139">In this section, you configure and test Azure AD single sign-on with ScaleX Enterprise based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="79c23-140">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w przedsiębiorstwie ScaleX jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="79c23-140">For single sign-on to work, Azure AD needs to know what the counterpart user in ScaleX Enterprise is to a user in Azure AD.</span></span> <span data-ttu-id="79c23-141">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w przedsiębiorstwie ScaleX musi się.</span><span class="sxs-lookup"><span data-stu-id="79c23-141">In other words, a link relationship between an Azure AD user and the related user in ScaleX Enterprise needs to be established.</span></span>

<span data-ttu-id="79c23-142">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w przedsiębiorstwie ScaleX.</span><span class="sxs-lookup"><span data-stu-id="79c23-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ScaleX Enterprise.</span></span>

<span data-ttu-id="79c23-143">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z ScaleX przedsiębiorstwa, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="79c23-143">To configure and test Azure AD single sign-on with ScaleX Enterprise, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="79c23-144">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="79c23-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="79c23-145">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="79c23-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="79c23-146">**[Tworzenie użytkownika testowego ScaleX Enterprise](#creating-a-scalex-enterprise-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta ScaleX przedsiębiorstwo, które jest połączone z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="79c23-146">**[Creating a ScaleX Enterprise test user](#creating-a-scalex-enterprise-test-user)** - to have a counterpart of Britta Simon in ScaleX Enterprise that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="79c23-147">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="79c23-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="79c23-148">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="79c23-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="79c23-149">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="79c23-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="79c23-150">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji przedsiębiorstwa ScaleX.</span><span class="sxs-lookup"><span data-stu-id="79c23-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ScaleX Enterprise application.</span></span>

<span data-ttu-id="79c23-151">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z ScaleX przedsiębiorstwa, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="79c23-151">**To configure Azure AD single sign-on with ScaleX Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="79c23-152">W portalu Azure na **ScaleX Enterprise** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="79c23-152">In the Azure portal, on the **ScaleX Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="79c23-154">Na **logowanie jednokrotne** okna dialogowego, jako **tryb** wybierz **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="79c23-154">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_samlbase.png)

3. <span data-ttu-id="79c23-156">Na **ScaleX domeny przedsiębiorstwa i adres URL** sekcji, wykonaj następujące kroki, aby skonfigurować aplikację w **IDP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="79c23-156">On the **ScaleX Enterprise Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url1.png)

    <span data-ttu-id="79c23-158">a.</span><span class="sxs-lookup"><span data-stu-id="79c23-158">a.</span></span> <span data-ttu-id="79c23-159">W **identyfikator** tekstowym, wpisz wartość, przy użyciu następującego wzorca:`https://platform.rescale.com/saml2/<company id>/`</span><span class="sxs-lookup"><span data-stu-id="79c23-159">In the **Identifier** textbox, type the value using the following pattern: `https://platform.rescale.com/saml2/<company id>/`</span></span>

    <span data-ttu-id="79c23-160">b.</span><span class="sxs-lookup"><span data-stu-id="79c23-160">b.</span></span> <span data-ttu-id="79c23-161">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://platform.rescale.com/saml2/<company id>/acs/`</span><span class="sxs-lookup"><span data-stu-id="79c23-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://platform.rescale.com/saml2/<company id>/acs/`</span></span>

4. <span data-ttu-id="79c23-162">Sprawdź **Pokaż zaawansowane ustawienia adresu URL**, jeśli chcesz skonfigurować aplikację w **SP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="79c23-162">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url2.png)

    <span data-ttu-id="79c23-164">W **adres URL logowania** tekstowym, wpisz wartość, przy użyciu następującego wzorca:`https://platform.rescale.com/saml2/<company id>/sso/`</span><span class="sxs-lookup"><span data-stu-id="79c23-164">In the **Sign-on URL** textbox, type the value using the following pattern: `https://platform.rescale.com/saml2/<company id>/sso/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="79c23-165">Nie są to rzeczywiste wartości.</span><span class="sxs-lookup"><span data-stu-id="79c23-165">These are not the real values.</span></span> <span data-ttu-id="79c23-166">Rzeczywisty identyfikator, adres URL odpowiedzi lub adres URL logowania, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="79c23-166">Update these values with the actual Identifier, Reply URL or Sign-On URL.</span></span> <span data-ttu-id="79c23-167">Skontaktuj się z [zespołem pomocy technicznej klienta Enterprise ScaleX](http://info.rescale.com/contact_sales) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="79c23-167">Contact [ScaleX Enterprise Client support team](http://info.rescale.com/contact_sales) to get these values.</span></span> 

5. <span data-ttu-id="79c23-168">Aplikacja ScaleX oczekuje potwierdzenia języka SAML w określonym formacie, który wymaga zmodyfikowania mapowań atrybutów niestandardowych do konfiguracji atrybuty tokenu SAML.</span><span class="sxs-lookup"><span data-stu-id="79c23-168">Your ScaleX application expects the SAML assertions in a specific format, which requires you to modify custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="79c23-169">Kliknij przycisk **widoku i edytować wszystkie atrybuty użytkowników** wyboru umożliwiające otwarcie niestandardowe atrybuty ustawień.</span><span class="sxs-lookup"><span data-stu-id="79c23-169">Click **View and edit all other user attributes** checkbox to open the custom attributes settings.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scalexenterprise-tutorial/scalex_attributes.png)
    
    <span data-ttu-id="79c23-171">a.</span><span class="sxs-lookup"><span data-stu-id="79c23-171">a.</span></span> <span data-ttu-id="79c23-172">Kliknij prawym przyciskiem myszy atrybut **nazwa** i kliknij przycisk Usuń.</span><span class="sxs-lookup"><span data-stu-id="79c23-172">Right click the attribute **name** and click delete.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scalexenterprise-tutorial/delete_attribute_name.png)

    <span data-ttu-id="79c23-174">b.</span><span class="sxs-lookup"><span data-stu-id="79c23-174">b.</span></span> <span data-ttu-id="79c23-175">Kliknij przycisk **emailaddress** atrybutu, aby otworzyć okno edycji atrybucie.</span><span class="sxs-lookup"><span data-stu-id="79c23-175">Click **emailaddress** attribute to open the Edit Attribute window.</span></span> <span data-ttu-id="79c23-176">Zmień wartość z **user.mail** do **user.userprincipalname** i kliknij przycisk Ok.</span><span class="sxs-lookup"><span data-stu-id="79c23-176">Change its value from **user.mail** to **user.userprincipalname** and click Ok.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scalexenterprise-tutorial/edit_email_attribute.png)   
    
5. <span data-ttu-id="79c23-178">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="79c23-178">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the Certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_certificate.png) 

6. <span data-ttu-id="79c23-180">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="79c23-180">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="79c23-182">Na **konfiguracja dla przedsiębiorstw ScaleX** , kliknij przycisk **skonfigurować ScaleX Enterprise** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="79c23-182">On the **ScaleX Enterprise Configuration** section, click **Configure ScaleX Enterprise** to open **Configure sign-on** window.</span></span> <span data-ttu-id="79c23-183">Kopiuj **SAML identyfikator jednostki** i **SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="79c23-183">Copy the **SAML Entity ID** and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_configure.png) 

8. <span data-ttu-id="79c23-185">Aby skonfigurować logowanie jednokrotne w **ScaleX Enterprise** strona, zaloguj się do witryny internetowej firmy ScaleX Enterprise jako administrator.</span><span class="sxs-lookup"><span data-stu-id="79c23-185">To configure single sign-on on **ScaleX Enterprise** side, login to the ScaleX Enterprise company website as an administrator.</span></span>

9. <span data-ttu-id="79c23-186">Kliknij menu w górnym prawym rogu i wybierz pozycję **administracji Contoso**.</span><span class="sxs-lookup"><span data-stu-id="79c23-186">Click the menu in the upper right and select **Contoso Administration**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="79c23-187">Firma Contoso jest tylko przykładowe.</span><span class="sxs-lookup"><span data-stu-id="79c23-187">Contoso is just an example.</span></span> <span data-ttu-id="79c23-188">Powinno to być rzeczywista nazwa firmy.</span><span class="sxs-lookup"><span data-stu-id="79c23-188">This should be your actual Company Name.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scalexenterprise-tutorial/Test_Admin.png) 

10. <span data-ttu-id="79c23-190">Wybierz **integracji** z górnego menu i wybierz **rejestracji jednokrotnej**.</span><span class="sxs-lookup"><span data-stu-id="79c23-190">Select **Integrations** from the top menu and select **Single Sign-On**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scalexenterprise-tutorial/admin_sso.png) 

11. <span data-ttu-id="79c23-192">Wypełnij formularz w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="79c23-192">Complete the form as follows:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scalexenterprise-tutorial/scalex_admin_save.png) 
    
    <span data-ttu-id="79c23-194">a.</span><span class="sxs-lookup"><span data-stu-id="79c23-194">a.</span></span> <span data-ttu-id="79c23-195">Wybierz **"Utwórz każdy użytkownik, który może uwierzytelniać z logowania jednokrotnego."**</span><span class="sxs-lookup"><span data-stu-id="79c23-195">Select **“Create any user who can authenticate with SSO.”**</span></span>

    <span data-ttu-id="79c23-196">b.</span><span class="sxs-lookup"><span data-stu-id="79c23-196">b.</span></span> <span data-ttu-id="79c23-197">**Saml dostawcy usług**: wkleić wartość ***urn: oasis: nazwy: tc: SAML:2.0:nameid-format: stałe***</span><span class="sxs-lookup"><span data-stu-id="79c23-197">**Service Provider saml**: Paste the value ***urn:oasis:names:tc:SAML:2.0:nameid-format:persistent***</span></span>

    <span data-ttu-id="79c23-198">c.</span><span class="sxs-lookup"><span data-stu-id="79c23-198">c.</span></span> <span data-ttu-id="79c23-199">**Nazwa dostawcy tożsamości pola wiadomości e-mail w odpowiedzi ACS**: wkleić wartość`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span><span class="sxs-lookup"><span data-stu-id="79c23-199">**Name of Identity Provider email field in ACS response**: Paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span></span>

    <span data-ttu-id="79c23-200">d.</span><span class="sxs-lookup"><span data-stu-id="79c23-200">d.</span></span> <span data-ttu-id="79c23-201">**Identyfikator jednostki EntityDescriptor dostawcy tożsamości:** Wklej **identyfikator jednostki SAML** wartość skopiowany z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="79c23-201">**Identity Provider EntityDescriptor Entity ID:** Paste the **SAML Entity ID** value copied from the Azure portal.</span></span>

    <span data-ttu-id="79c23-202">e.</span><span class="sxs-lookup"><span data-stu-id="79c23-202">e.</span></span> <span data-ttu-id="79c23-203">**Adres URL SingleSignOnService dostawcy tożsamości:** Wklej **SAML pojedynczy znak na adres URL usługi** z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="79c23-203">**Identity Provider SingleSignOnService URL:** Paste the **SAML Single Sign-On Service URL** from the Azure portal.</span></span>

    <span data-ttu-id="79c23-204">f.</span><span class="sxs-lookup"><span data-stu-id="79c23-204">f.</span></span> <span data-ttu-id="79c23-205">**Certyfikat publiczny X509 dostawcy tożsamości:** Otwórz X509 certyfikat pobrany z platformy Azure w programie Notatnik i Wklej zawartość w tym polu.</span><span class="sxs-lookup"><span data-stu-id="79c23-205">**Identity Provider public X509 certificate:** Open the X509 certificate downloaded from the Azure in notepad and paste the contents in this box.</span></span> <span data-ttu-id="79c23-206">Upewnić się, że nie podziały wierszy w środku zawartości certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="79c23-206">Ensure there are no line breaks in the middle of the certificate contents.</span></span>
    
    <span data-ttu-id="79c23-207">g.</span><span class="sxs-lookup"><span data-stu-id="79c23-207">g.</span></span> <span data-ttu-id="79c23-208">Sprawdź poniższe pola wyboru: **włączone, NameID szyfrowania i AuthnRequests logowania.**</span><span class="sxs-lookup"><span data-stu-id="79c23-208">Check the following checkboxes: **Enabled, Encrypt NameID and Sign AuthnRequests.**</span></span>

    <span data-ttu-id="79c23-209">h.</span><span class="sxs-lookup"><span data-stu-id="79c23-209">h.</span></span> <span data-ttu-id="79c23-210">Kliknij przycisk **ustawienia logowania jednokrotnego aktualizacji** Aby zapisać ustawienia.</span><span class="sxs-lookup"><span data-stu-id="79c23-210">Click **Update SSO Settings** to save the settings.</span></span>

> [!TIP]
> <span data-ttu-id="79c23-211">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="79c23-211">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="79c23-212">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="79c23-212">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="79c23-213">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="79c23-213">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="79c23-214">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="79c23-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="79c23-215">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="79c23-215">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="79c23-217">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="79c23-217">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="79c23-218">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="79c23-218">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="79c23-220">Przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** do wyświetlenia na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="79c23-220">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="79c23-222">W górnej części okna dialogowego, kliknij przycisk **Dodaj** otworzyć **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="79c23-222">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="79c23-224">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="79c23-224">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="79c23-226">a.</span><span class="sxs-lookup"><span data-stu-id="79c23-226">a.</span></span> <span data-ttu-id="79c23-227">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="79c23-227">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="79c23-228">b.</span><span class="sxs-lookup"><span data-stu-id="79c23-228">b.</span></span> <span data-ttu-id="79c23-229">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="79c23-229">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="79c23-230">c.</span><span class="sxs-lookup"><span data-stu-id="79c23-230">c.</span></span> <span data-ttu-id="79c23-231">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="79c23-231">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="79c23-232">d.</span><span class="sxs-lookup"><span data-stu-id="79c23-232">d.</span></span> <span data-ttu-id="79c23-233">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="79c23-233">Click **Create**.</span></span>
 
### <a name="creating-a-scalex-enterprise-test-user"></a><span data-ttu-id="79c23-234">Tworzenie użytkownika testowego ScaleX Enterprise</span><span class="sxs-lookup"><span data-stu-id="79c23-234">Creating a ScaleX Enterprise test user</span></span>

<span data-ttu-id="79c23-235">Aby umożliwić użytkownikom usługi Azure AD do logowania do organizacji ScaleX, ich należy udostępnić w ScaleX przedsiębiorstwem.</span><span class="sxs-lookup"><span data-stu-id="79c23-235">To enable Azure AD users to log in to ScaleX Enterprise, they must be provisioned in to ScaleX Enterprise.</span></span> <span data-ttu-id="79c23-236">W przypadku organizacji ScaleX Inicjowanie obsługi to zadanie automatycznej i nie są wymagane żadne czynności ręcznych.</span><span class="sxs-lookup"><span data-stu-id="79c23-236">In the case of ScaleX Enterprise, provisioning is an automatic task and no manual steps are required.</span></span> <span data-ttu-id="79c23-237">Każdy użytkownik, który może pomyślnie wykonać uwierzytelnienia przy użyciu poświadczeń logowania jednokrotnego będą automatycznie udostępniane na stronie ScaleX.</span><span class="sxs-lookup"><span data-stu-id="79c23-237">Any user who can successfully authenticate with SSO credentials will be automatically provisioned on the ScaleX side.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="79c23-238">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="79c23-238">Assigning the Azure AD test user</span></span>

<span data-ttu-id="79c23-239">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu użytkownika do ScaleX przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="79c23-239">In this section, you enable Britta Simon to use Azure single sign-on by granting user access to ScaleX Enterprise.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="79c23-241">**Aby przypisać Simona Britta ScaleX przedsiębiorstwa, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="79c23-241">**To assign Britta Simon to ScaleX Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="79c23-242">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="79c23-242">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="79c23-244">Na liście aplikacji zaznacz **ScaleX Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="79c23-244">In the applications list, select **ScaleX Enterprise**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_app.png) 

3. <span data-ttu-id="79c23-246">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="79c23-246">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="79c23-248">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="79c23-248">Click **Add** button.</span></span> <span data-ttu-id="79c23-249">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="79c23-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="79c23-251">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="79c23-251">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="79c23-252">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="79c23-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="79c23-253">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="79c23-253">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="79c23-254">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="79c23-254">Testing single sign-on</span></span>

<span data-ttu-id="79c23-255">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="79c23-255">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="79c23-256">Kliknij Kafelek ScaleX przedsiębiorstwa w panelu dostępu, można będzie uzyskać automatycznie zalogowane do aplikacji ScaleX przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="79c23-256">Click the ScaleX Enterprise tile in the Access Panel, you will get automatically signed-on to your ScaleX Enterprise application.</span></span> <span data-ttu-id="79c23-257">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="79c23-257">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="79c23-258">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="79c23-258">Additional resources</span></span>

* [<span data-ttu-id="79c23-259">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="79c23-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="79c23-260">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="79c23-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_203.png

