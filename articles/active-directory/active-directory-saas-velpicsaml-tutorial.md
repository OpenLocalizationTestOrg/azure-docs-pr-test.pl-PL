---
title: 'Samouczek: Integracji Azure Active Directory z Velpic SAML | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Velpic SAML."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 5325f3cca00167e6b7b687509ce43435447ad2f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-velpic-saml"></a><span data-ttu-id="9ff24-103">Samouczek: Integracji Azure Active Directory z Velpic SAML</span><span class="sxs-lookup"><span data-stu-id="9ff24-103">Tutorial: Azure Active Directory integration with Velpic SAML</span></span>

<span data-ttu-id="9ff24-104">W tym samouczku Dowiedz się jak integrację Velpic SAML w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9ff24-104">In this tutorial, you learn how to integrate Velpic SAML with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9ff24-105">Integrację Velpic SAML z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="9ff24-105">Integrating Velpic SAML with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9ff24-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Velpic SAML</span><span class="sxs-lookup"><span data-stu-id="9ff24-106">You can control in Azure AD who has access to Velpic SAML</span></span>
- <span data-ttu-id="9ff24-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Velpic SAML (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9ff24-107">You can enable your users to automatically get signed-on to Velpic SAML (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9ff24-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu zarządzania Azure</span><span class="sxs-lookup"><span data-stu-id="9ff24-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="9ff24-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9ff24-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9ff24-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9ff24-110">Prerequisites</span></span>

<span data-ttu-id="9ff24-111">Aby skonfigurować integrację usługi Azure AD z Velpic SAML, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="9ff24-111">To configure Azure AD integration with Velpic SAML, you need the following items:</span></span>

- <span data-ttu-id="9ff24-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9ff24-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9ff24-113">Velpic SAML jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="9ff24-113">A Velpic SAML single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9ff24-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="9ff24-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9ff24-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="9ff24-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9ff24-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="9ff24-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="9ff24-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9ff24-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9ff24-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="9ff24-118">Scenario description</span></span>
<span data-ttu-id="9ff24-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="9ff24-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9ff24-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="9ff24-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9ff24-121">Dodawanie Velpic SAML z galerii</span><span class="sxs-lookup"><span data-stu-id="9ff24-121">Adding Velpic SAML from the gallery</span></span>
2. <span data-ttu-id="9ff24-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="9ff24-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-velpic-saml-from-the-gallery"></a><span data-ttu-id="9ff24-123">Dodawanie Velpic SAML z galerii</span><span class="sxs-lookup"><span data-stu-id="9ff24-123">Adding Velpic SAML from the gallery</span></span>
<span data-ttu-id="9ff24-124">Aby skonfigurować integrację Velpic SAML do usługi Azure AD, należy dodać Velpic SAML z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="9ff24-124">To configure the integration of Velpic SAML into Azure AD, you need to add Velpic SAML from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9ff24-125">**Aby dodać Velpic SAML z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="9ff24-125">**To add Velpic SAML from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9ff24-126">W  **[portalu zarządzania Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="9ff24-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="9ff24-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="9ff24-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9ff24-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="9ff24-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="9ff24-131">Kliknij przycisk **Dodaj** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9ff24-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="9ff24-133">W polu wyszukiwania wpisz **Velpic SAML**.</span><span class="sxs-lookup"><span data-stu-id="9ff24-133">In the search box, type **Velpic SAML**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_search.png)

5. <span data-ttu-id="9ff24-135">W panelu wyników wybierz **Velpic SAML**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="9ff24-135">In the results panel, select **Velpic SAML**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9ff24-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="9ff24-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9ff24-138">W tej sekcji możesz skonfigurować i test usługi Azure AD rejestracji jednokrotnej z Velpic SAML w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="9ff24-138">In this section, you configure and test Azure AD single sign-on with Velpic SAML based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9ff24-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Velpic SAML jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9ff24-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Velpic SAML is to a user in Azure AD.</span></span> <span data-ttu-id="9ff24-140">Innymi słowy musi można ustanowić łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="9ff24-140">In other words, a link relationship between an Azure AD user and the related user in Velpic SAML needs to be established.</span></span>

<span data-ttu-id="9ff24-141">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="9ff24-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Velpic SAML.</span></span>

<span data-ttu-id="9ff24-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Velpic SAML, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="9ff24-142">To configure and test Azure AD single sign-on with Velpic SAML, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9ff24-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="9ff24-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9ff24-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="9ff24-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9ff24-145">**[Tworzenie użytkownika testowego Velpic SAML](#creating-a-velpic-saml-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta SAML Velpic, połączonej z jej reprezentacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9ff24-145">**[Creating a Velpic SAML test user](#creating-a-velpic-saml-test-user)** - to have a counterpart of Britta Simon in Velpic SAML that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="9ff24-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="9ff24-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9ff24-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="9ff24-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9ff24-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9ff24-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9ff24-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu zarządzania Azure i skonfigurować logowanie jednokrotne w aplikacji Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="9ff24-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Velpic SAML application.</span></span>

<span data-ttu-id="9ff24-150">**Aby skonfigurować usługi Azure AD logowania jednokrotnego Velpic SAML, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="9ff24-150">**To configure Azure AD single sign-on with Velpic SAML, perform the following steps:**</span></span>

1. <span data-ttu-id="9ff24-151">W portalu zarządzania Azure na **Velpic SAML** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="9ff24-151">In the Azure Management portal, on the **Velpic SAML** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="9ff24-153">Na **logowanie jednokrotne** okna dialogowego, jako **tryb** wybierz **na języku SAML logowania jednokrotnego** Włącz funkcji logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="9ff24-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_samlbase.png)

3. <span data-ttu-id="9ff24-155">Wprowadź szczegóły w **Velpic SAML domeny i adres URL** sekcji -</span><span class="sxs-lookup"><span data-stu-id="9ff24-155">Enter the details in the **Velpic SAML Domain and URLs** section-</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_url.png)

    <span data-ttu-id="9ff24-157">a.</span><span class="sxs-lookup"><span data-stu-id="9ff24-157">a.</span></span> <span data-ttu-id="9ff24-158">W **adres URL logowania** tekstowym, wpisz wartość, jak:`https://<sub-domain>.velpicsaml.net`</span><span class="sxs-lookup"><span data-stu-id="9ff24-158">In the **Sign-on URL** textbox, type the value as: `https://<sub-domain>.velpicsaml.net`</span></span>

    <span data-ttu-id="9ff24-159">b.</span><span class="sxs-lookup"><span data-stu-id="9ff24-159">b.</span></span> <span data-ttu-id="9ff24-160">W **identyfikator** pole tekstowe, Wklej **"Rejestracja jednokrotna w adresie URL"** wartość`https://auth.velpic.com/saml/v2/<entity-id>/login`</span><span class="sxs-lookup"><span data-stu-id="9ff24-160">In the **Identifier** textbox, paste the **‘Single sign on URL’** value `https://auth.velpic.com/saml/v2/<entity-id>/login`</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="9ff24-161">Należy pamiętać, że znaku w adresie URL, które będą udostępniane przez zespół Velpic SAML i wartość identyfikatora będzie dostępna podczas konfigurowania rejestracji Jednokrotnej wtyczki po stronie Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="9ff24-161">Please note that the Sign on URL will be provided by the Velpic SAML team and Identifier value will be available when you configure the SSO Plugin on Velpic SAML side.</span></span> <span data-ttu-id="9ff24-162">Musisz skopiować tę wartość ze strony aplikacji Velpic SAML i wklej go w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="9ff24-162">You need to copy that value from Velpic SAML application  page and paste it here.</span></span>

4. <span data-ttu-id="9ff24-163">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="9ff24-163">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_certificate.png) 

5. <span data-ttu-id="9ff24-165">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9ff24-165">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9ff24-167">W sekcji konfiguracyjnej SAML Velpic kliknij przycisk Konfiguruj Velpic SAML, można otworzyć Konfigurowanie logowania jednokrotnego okna.</span><span class="sxs-lookup"><span data-stu-id="9ff24-167">On the Velpic SAML Configuration section, click Configure Velpic SAML to open Configure sign-on window.</span></span> <span data-ttu-id="9ff24-168">Skopiuj identyfikator jednostki SAML z sekcji krótkimi opisami.</span><span class="sxs-lookup"><span data-stu-id="9ff24-168">Copy the SAML Entity ID from the Quick Reference section.</span></span>

7. <span data-ttu-id="9ff24-169">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy Velpic SAML jako administrator.</span><span class="sxs-lookup"><span data-stu-id="9ff24-169">In a different web browser window, log into your Velpic SAML company site as an administrator.</span></span>

8. <span data-ttu-id="9ff24-170">Polecenie **Zarządzaj** karcie i przejdź do **integracji** sekcji, w którym należy kliknąć pozycję **wtyczek** przycisk, aby utworzyć nowej wtyczki dla logowania.</span><span class="sxs-lookup"><span data-stu-id="9ff24-170">Click on **Manage** tab and go to **Integration** section where you need to click on **Plugins** button to create new plugin for Sign-In.</span></span>

    ![Wtyczki](./media/active-directory-saas-velpicsaml-tutorial/velpic_1.png)

9. <span data-ttu-id="9ff24-172">Polecenie **"Dodawanie wtyczki"** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9ff24-172">Click on the **‘Add plugin’** button.</span></span>
    
    ![Wtyczki](./media/active-directory-saas-velpicsaml-tutorial/velpic_2.png)

10. <span data-ttu-id="9ff24-174">Polecenie **SAML** kafelka na stronie Dodawanie wtyczki.</span><span class="sxs-lookup"><span data-stu-id="9ff24-174">Click on the **SAML** tile in the Add Plugin page.</span></span>
    
    ![Wtyczki](./media/active-directory-saas-velpicsaml-tutorial/velpic_3.png)

11. <span data-ttu-id="9ff24-176">Wprowadź nazwę nowej wtyczki SAML i kliknij przycisk **"Dodaj"** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9ff24-176">Enter the name of the new SAML plugin and click the **‘Add’** button.</span></span>

    ![Wtyczki](./media/active-directory-saas-velpicsaml-tutorial/velpic_4.png)

12. <span data-ttu-id="9ff24-178">Wprowadź szczegóły w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="9ff24-178">Enter the details as follows:</span></span>

    ![Wtyczki](./media/active-directory-saas-velpicsaml-tutorial/velpic_5.png)

    <span data-ttu-id="9ff24-180">a.</span><span class="sxs-lookup"><span data-stu-id="9ff24-180">a.</span></span> <span data-ttu-id="9ff24-181">W **nazwa** tekstowym, wpisz nazwę wtyczki SAML.</span><span class="sxs-lookup"><span data-stu-id="9ff24-181">In the **Name** textbox, type the name of SAML plugin.</span></span>

    <span data-ttu-id="9ff24-182">b.</span><span class="sxs-lookup"><span data-stu-id="9ff24-182">b.</span></span> <span data-ttu-id="9ff24-183">W **adres URL wystawcy** pole tekstowe, Wklej **identyfikator jednostki SAML** skopiowane z **Konfigurowanie logowania jednokrotnego** okna portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="9ff24-183">In the **Issuer URL** textbox, paste the **SAML Entity ID** you copied from the **Configure sign-on** window of the Azure portal.</span></span>

    <span data-ttu-id="9ff24-184">c.</span><span class="sxs-lookup"><span data-stu-id="9ff24-184">c.</span></span> <span data-ttu-id="9ff24-185">W **dostawcy metadanych konfiguracji** przekazać plik XML metadanych, który został pobrany z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="9ff24-185">In the **Provider Metadata Config** upload the Metadata XML file which you downloaded from Azure portal.</span></span>

    <span data-ttu-id="9ff24-186">d.</span><span class="sxs-lookup"><span data-stu-id="9ff24-186">d.</span></span> <span data-ttu-id="9ff24-187">Można również włączyć tylko w czasie inicjowania obsługi administracyjnej, należy włączyć SAML **"Automatyczne tworzenie nowych użytkowników"** pola wyboru.</span><span class="sxs-lookup"><span data-stu-id="9ff24-187">You can also choose to enable SAML just in time provisioning by enabling the **‘Auto create new users’** checkbox.</span></span> <span data-ttu-id="9ff24-188">Jeśli użytkownik nie istnieje w Velpic, ta flaga nie jest włączone logowanie z Azure zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="9ff24-188">If a user doesn’t exist in Velpic and this flag is not enabled, the login from Azure will fail.</span></span> <span data-ttu-id="9ff24-189">Jeśli włączono flagę użytkownika będą automatycznie udostępniane w Velpic podczas logowania.</span><span class="sxs-lookup"><span data-stu-id="9ff24-189">If the flag is enabled the user will automatically be provisioned into Velpic at the time of login.</span></span> 

    <span data-ttu-id="9ff24-190">e.</span><span class="sxs-lookup"><span data-stu-id="9ff24-190">e.</span></span> <span data-ttu-id="9ff24-191">Kopiuj **Rejestracja jednokrotna w adresie URL** z tekstu pola i wklej go w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="9ff24-191">Copy the **Single sign on URL** from the text box and paste it in the Azure portal.</span></span>
    
    <span data-ttu-id="9ff24-192">f.</span><span class="sxs-lookup"><span data-stu-id="9ff24-192">f.</span></span> <span data-ttu-id="9ff24-193">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="9ff24-193">Click **Save**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9ff24-194">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9ff24-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="9ff24-195">Celem tej sekcji jest tworzenie użytkownika testowego w portalu zarządzania Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="9ff24-195">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="9ff24-197">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="9ff24-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9ff24-198">W **portalu zarządzania Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="9ff24-198">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9ff24-200">Przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** do wyświetlenia na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="9ff24-200">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9ff24-202">W górnej części okna dialogowego kliknij **Dodaj** otworzyć **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9ff24-202">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9ff24-204">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9ff24-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9ff24-206">a.</span><span class="sxs-lookup"><span data-stu-id="9ff24-206">a.</span></span> <span data-ttu-id="9ff24-207">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9ff24-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9ff24-208">b.</span><span class="sxs-lookup"><span data-stu-id="9ff24-208">b.</span></span> <span data-ttu-id="9ff24-209">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9ff24-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9ff24-210">c.</span><span class="sxs-lookup"><span data-stu-id="9ff24-210">c.</span></span> <span data-ttu-id="9ff24-211">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="9ff24-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9ff24-212">d.</span><span class="sxs-lookup"><span data-stu-id="9ff24-212">d.</span></span> <span data-ttu-id="9ff24-213">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="9ff24-213">Click **Create**.</span></span>
 
### <a name="creating-a-velpic-saml-test-user"></a><span data-ttu-id="9ff24-214">Tworzenie użytkownika testowego Velpic SAML</span><span class="sxs-lookup"><span data-stu-id="9ff24-214">Creating a Velpic SAML test user</span></span>

<span data-ttu-id="9ff24-215">Ten krok zazwyczaj nie jest wymagana aplikacja obsługuje tylko w czasie Inicjowanie obsługi użytkowników.</span><span class="sxs-lookup"><span data-stu-id="9ff24-215">This step is usually not required as the application supports just in time user provisioning.</span></span> <span data-ttu-id="9ff24-216">Jeśli nie włączono obsługi automatycznego użytkownika tworzenie ręczne użytkownika można wykonać zgodnie z poniższym opisem.</span><span class="sxs-lookup"><span data-stu-id="9ff24-216">If the automatic user provisioning is not enabled then manual user creation can be done as described below.</span></span>

<span data-ttu-id="9ff24-217">Zaloguj się do witryny firmy Velpic SAML jako administrator i wykonać następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="9ff24-217">Log into your Velpic SAML company site as an administrator and perform following steps:</span></span>
    
1. <span data-ttu-id="9ff24-218">Kliknij na karcie zarządzania i przejdź do sekcji użytkownicy, a następnie kliknij przycisk Nowa, aby dodać użytkowników.</span><span class="sxs-lookup"><span data-stu-id="9ff24-218">Click on Manage tab and go to Users section, then click on New button to add users.</span></span>

    ![Dodaj użytkownika](./media/active-directory-saas-velpicsaml-tutorial/velpic_7.png)

2. <span data-ttu-id="9ff24-220">Na **"Tworzenie nowego użytkownika"** okna dialogowego wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="9ff24-220">On the **“Create New User”** dialog page, perform the following steps.</span></span>

    ![Użytkownika](./media/active-directory-saas-velpicsaml-tutorial/velpic_8.png)
    
    <span data-ttu-id="9ff24-222">a.</span><span class="sxs-lookup"><span data-stu-id="9ff24-222">a.</span></span> <span data-ttu-id="9ff24-223">W **imię** pole tekstowe, nazwa typu pierwszy Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="9ff24-223">In the **First Name** textbox, type the first name of Britta Simon.</span></span>

    <span data-ttu-id="9ff24-224">b.</span><span class="sxs-lookup"><span data-stu-id="9ff24-224">b.</span></span> <span data-ttu-id="9ff24-225">W **nazwisko** tekstowym, wpisz nazwisko Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="9ff24-225">In the **Last Name** textbox, type the last name of Britta Simon.</span></span>

    <span data-ttu-id="9ff24-226">c.</span><span class="sxs-lookup"><span data-stu-id="9ff24-226">c.</span></span> <span data-ttu-id="9ff24-227">W **nazwy użytkownika** tekstowym, wpisz nazwę użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="9ff24-227">In the **User Name** textbox, type the user name of Britta Simon.</span></span>

    <span data-ttu-id="9ff24-228">d.</span><span class="sxs-lookup"><span data-stu-id="9ff24-228">d.</span></span> <span data-ttu-id="9ff24-229">W **E-mail** tekstowym, wpisz adres e-mail konta Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="9ff24-229">In the **Email** textbox, type the email address of Britta Simon account.</span></span>

    <span data-ttu-id="9ff24-230">e.</span><span class="sxs-lookup"><span data-stu-id="9ff24-230">e.</span></span> <span data-ttu-id="9ff24-231">Pozostała część informacji jest opcjonalne, można go wypełnić, w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="9ff24-231">Rest of the information is optional, you can fill it if needed.</span></span>
    
    <span data-ttu-id="9ff24-232">f.</span><span class="sxs-lookup"><span data-stu-id="9ff24-232">f.</span></span> <span data-ttu-id="9ff24-233">Kliknij przycisk **SAVE** (Zapisz).</span><span class="sxs-lookup"><span data-stu-id="9ff24-233">Click **SAVE**.</span></span>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9ff24-234">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9ff24-234">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9ff24-235">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu jej Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="9ff24-235">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Velpic SAML.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="9ff24-237">**Aby przypisać Simona Britta Velpic SAML, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="9ff24-237">**To assign Britta Simon to Velpic SAML, perform the following steps:**</span></span>

1. <span data-ttu-id="9ff24-238">Otwórz widok aplikacji w portalu zarządzania Azure, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="9ff24-238">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="9ff24-240">Na liście aplikacji zaznacz **Velpic SAML**.</span><span class="sxs-lookup"><span data-stu-id="9ff24-240">In the applications list, select **Velpic SAML**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_app.png) 

3. <span data-ttu-id="9ff24-242">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="9ff24-242">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="9ff24-244">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9ff24-244">Click **Add** button.</span></span> <span data-ttu-id="9ff24-245">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9ff24-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="9ff24-247">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="9ff24-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9ff24-248">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9ff24-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9ff24-249">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9ff24-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9ff24-250">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9ff24-250">Testing single sign-on</span></span>

<span data-ttu-id="9ff24-251">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="9ff24-251">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

1. <span data-ttu-id="9ff24-252">Po kliknięciu kafelka Velpic SAML w panelu dostępu, należy pobrać strony logowania Velpic SAML aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9ff24-252">When you click the Velpic SAML tile in the Access Panel, you should get login page of Velpic SAML application.</span></span> <span data-ttu-id="9ff24-253">Powinny pojawić się **"Zaloguj się za pomocą usługi Azure AD"** przycisk na stronie logowania.</span><span class="sxs-lookup"><span data-stu-id="9ff24-253">You should see the **‘Log In With Azure AD’** button on the sign in page.</span></span>

    ![Wtyczki](./media/active-directory-saas-velpicsaml-tutorial/velpic_6.png)

2. <span data-ttu-id="9ff24-255">Polecenie **"Zaloguj się za pomocą usługi Azure AD"** przycisk, aby zalogować się do Velpic przy użyciu konta usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9ff24-255">Click on the **‘Log In With Azure AD’** button to log in to Velpic using your Azure AD account.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="9ff24-256">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="9ff24-256">Additional resources</span></span>

* [<span data-ttu-id="9ff24-257">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9ff24-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9ff24-258">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9ff24-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_203.png

