---
title: "Samouczek: Integracji Azure Active Directory z chmurą Lifesize | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i w chmurze Lifesize."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 75fab335-fdcd-4066-b42c-cc738fcb6513
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 7542360f9c75786bf400553090ba0a891d9c2fcc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lifesize-cloud"></a><span data-ttu-id="f3c6b-103">Samouczek: Integracji Azure Active Directory z chmurą Lifesize</span><span class="sxs-lookup"><span data-stu-id="f3c6b-103">Tutorial: Azure Active Directory integration with Lifesize Cloud</span></span>

<span data-ttu-id="f3c6b-104">Z tego samouczka dowiesz się integrowanie Lifesize chmury w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f3c6b-104">In this tutorial, you learn how to integrate Lifesize Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f3c6b-105">Integrowanie Lifesize chmurze z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="f3c6b-105">Integrating Lifesize Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f3c6b-106">Można kontrolować w usłudze Azure AD, który ma dostęp do chmury Lifesize</span><span class="sxs-lookup"><span data-stu-id="f3c6b-106">You can control in Azure AD who has access to Lifesize Cloud</span></span>
- <span data-ttu-id="f3c6b-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do chmury Lifesize (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f3c6b-107">You can enable your users to automatically get signed-on to Lifesize Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f3c6b-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="f3c6b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f3c6b-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f3c6b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f3c6b-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f3c6b-110">Prerequisites</span></span>

<span data-ttu-id="f3c6b-111">Aby skonfigurować integrację usługi Azure AD z chmurą Lifesize, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="f3c6b-111">To configure Azure AD integration with Lifesize Cloud, you need the following items:</span></span>

- <span data-ttu-id="f3c6b-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f3c6b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f3c6b-113">Chmura Lifesize logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="f3c6b-113">A Lifesize Cloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f3c6b-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f3c6b-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="f3c6b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f3c6b-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f3c6b-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f3c6b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f3c6b-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="f3c6b-118">Scenario description</span></span>
<span data-ttu-id="f3c6b-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f3c6b-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="f3c6b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f3c6b-121">Dodawanie Lifesize chmury z galerii</span><span class="sxs-lookup"><span data-stu-id="f3c6b-121">Adding Lifesize Cloud from the gallery</span></span>
2. <span data-ttu-id="f3c6b-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="f3c6b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lifesize-cloud-from-the-gallery"></a><span data-ttu-id="f3c6b-123">Dodawanie Lifesize chmury z galerii</span><span class="sxs-lookup"><span data-stu-id="f3c6b-123">Adding Lifesize Cloud from the gallery</span></span>
<span data-ttu-id="f3c6b-124">Aby skonfigurować integrację usługi Azure AD Lifesize Cloud, należy dodać Lifesize chmury z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-124">To configure the integration of Lifesize Cloud into Azure AD, you need to add Lifesize Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f3c6b-125">**Aby dodać Lifesize chmury z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f3c6b-125">**To add Lifesize Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f3c6b-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="f3c6b-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f3c6b-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="f3c6b-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="f3c6b-133">W polu wyszukiwania wpisz **chmury Lifesize**.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-133">In the search box, type **Lifesize Cloud**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_search.png)

5. <span data-ttu-id="f3c6b-135">W panelu wyników wybierz **chmury Lifesize**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-135">In the results panel, select **Lifesize Cloud**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f3c6b-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="f3c6b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f3c6b-138">W tej sekcji możesz skonfigurować i test usługi Azure AD rejestracji jednokrotnej z chmurą Lifesize w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-138">In this section, you configure and test Azure AD single sign-on with Lifesize Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f3c6b-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w chmurze Lifesize jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Lifesize Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="f3c6b-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w chmurze Lifesize musi się.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-140">In other words, a link relationship between an Azure AD user and the related user in Lifesize Cloud needs to be established.</span></span>

<span data-ttu-id="f3c6b-141">W chmurze Lifesize przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-141">In Lifesize Cloud, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f3c6b-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z chmurą Lifesize, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="f3c6b-142">To configure and test Azure AD single sign-on with Lifesize Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f3c6b-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f3c6b-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f3c6b-145">**[Tworzenie użytkownika testowego chmury Lifesize](#creating-a-lifesize-cloud-test-user)**  — aby odpowiednikiem Simona Britta w chmurze Lifesize, która jest połączona z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-145">**[Creating a Lifesize Cloud test user](#creating-a-lifesize-cloud-test-user)** - to have a counterpart of Britta Simon in Lifesize Cloud that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f3c6b-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f3c6b-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f3c6b-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="f3c6b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f3c6b-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne do aplikacji w chmurze Lifesize.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Lifesize Cloud application.</span></span>

<span data-ttu-id="f3c6b-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z chmurą Lifesize, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f3c6b-150">**To configure Azure AD single sign-on with Lifesize Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="f3c6b-151">W portalu Azure na **chmury Lifesize** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-151">In the Azure portal, on the **Lifesize Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="f3c6b-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_samlbase.png)

3. <span data-ttu-id="f3c6b-155">Na **adresy URL i domenę chmury Lifesize** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="f3c6b-155">On the **Lifesize Cloud Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_url.png)

    <span data-ttu-id="f3c6b-157">a.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-157">a.</span></span> <span data-ttu-id="f3c6b-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://login.lifesizecloud.com/ls/?acs`</span><span class="sxs-lookup"><span data-stu-id="f3c6b-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://login.lifesizecloud.com/ls/?acs`</span></span>

    <span data-ttu-id="f3c6b-159">b.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-159">b.</span></span> <span data-ttu-id="f3c6b-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://login.lifesizecloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="f3c6b-160">In the **Identifier** textbox, type a URL using the following pattern: `https://login.lifesizecloud.com/<companyname>`</span></span>

     
4. <span data-ttu-id="f3c6b-161">Sprawdź **Pokaż zaawansowane ustawienia adresu URL**, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="f3c6b-161">Check **Show advanced URL settings**, perform the following step:</span></span>    
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_url1.png)

    <span data-ttu-id="f3c6b-163">W **przekazywania stanu** tekstowym, wpisz adres URL, używając następującego wzorca:`https://webapp.lifesizecloud.com/?ent=<identifier>`</span><span class="sxs-lookup"><span data-stu-id="f3c6b-163">In the **Relay state** textbox, type a URL using the following pattern: `https://webapp.lifesizecloud.com/?ent=<identifier>`</span></span>
   
   > [!NOTE] 
   ><span data-ttu-id="f3c6b-164">Należy pamiętać, że nie są one rzeczywiste wartości.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-164">Please note that these are not the real values.</span></span> <span data-ttu-id="f3c6b-165">należy zaktualizować te wartości z rzeczywisty adres URL logowania, stan przekazywania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-165">you have to update these values with the actual Sign-On URL, Relay State, and Identifier.</span></span> <span data-ttu-id="f3c6b-166">Skontaktuj się z [zespołem pomocy technicznej klienta chmury Lifesize](https://www.lifesize.com/support) uzyskać adres URL logowania, a wartości identyfikatora i można uzyskać stanu przekazywania wartości z konfiguracji logowania jednokrotnego, który znajduje się w dalszej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-166">Contact [Lifesize Cloud Client support team](https://www.lifesize.com/support) to get Sign-On URL, and Identifier values and you can get Relay State  value from SSO Configuration that is explained later in the tutorial.</span></span>

4. <span data-ttu-id="f3c6b-167">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-167">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_certificate.png) 

5. <span data-ttu-id="f3c6b-169">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-169">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f3c6b-171">Na **konfiguracji chmury Lifesize** , kliknij przycisk **Konfigurowanie chmury Lifesize** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-171">On the **Lifesize Cloud Configuration** section, click **Configure Lifesize Cloud** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f3c6b-172">Kopiuj **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="f3c6b-172">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_configure.png) 

7. <span data-ttu-id="f3c6b-174">Aby uzyskać logowania jednokrotnego skonfigurowane dla danej aplikacji, zaloguj się do aplikacji w chmurze Lifesize z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-174">To get SSO configured for your application, login into the Lifesize Cloud application with Admin privileges.</span></span>

8. <span data-ttu-id="f3c6b-175">W prawym górnym rogu kliknij swoją nazwę, a następnie kliknij polecenie **ustawienia zaawansowane**.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-175">In the top right corner click on your name and then click on the **Advance Settings**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_06.png)

9. <span data-ttu-id="f3c6b-177">W ustawieniach wcześniejszym teraz kliknij **konfiguracji logowania jednokrotnego** łącza.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-177">In the Advance Settings now click on the **SSO Configuration** link.</span></span> <span data-ttu-id="f3c6b-178">Go zostanie otwarta strona konfiguracji logowania jednokrotnego dla swojego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-178">It will open the SSO Configuration page for your instance.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_07.png)

10. <span data-ttu-id="f3c6b-180">Teraz można skonfigurować następujące wartości w interfejsie użytkownika konfiguracji logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-180">Now configure the following values in the SSO configuration UI.</span></span>    
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_08.png)
    
    <span data-ttu-id="f3c6b-182">a.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-182">a.</span></span> <span data-ttu-id="f3c6b-183">W **wystawcy dostawcy tożsamości** pole tekstowe, Wklej wartość **identyfikator jednostki SAML** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-183">In **Identity Provider Issuer** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="f3c6b-184">b.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-184">b.</span></span>  <span data-ttu-id="f3c6b-185">W **adres URL logowania** pole tekstowe, Wklej wartość **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-185">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="f3c6b-186">c.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-186">c.</span></span> <span data-ttu-id="f3c6b-187">Otwórz w Notatniku pobrany z portalu Azure certyfikatu zakodowanego base-64, skopiuj zawartość go do Schowka, a następnie wklej go do **certyfikatu X.509** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-187">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox.</span></span>
  
    <span data-ttu-id="f3c6b-188">d.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-188">d.</span></span> <span data-ttu-id="f3c6b-189">W atrybucie SAML mapowania pola tekstowego imię wprowadź wartości jako **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**</span><span class="sxs-lookup"><span data-stu-id="f3c6b-189">In the SAML Attribute mappings for the First Name text box enter the value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**</span></span>
    
    <span data-ttu-id="f3c6b-190">e.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-190">e.</span></span> <span data-ttu-id="f3c6b-191">Mapowanie atrybutu SAML dla **nazwisko** polu tekstowym wprowadź wartości jako **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**</span><span class="sxs-lookup"><span data-stu-id="f3c6b-191">In the SAML Attribute mapping for the **Last Name** text box enter the value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**</span></span>
    
    <span data-ttu-id="f3c6b-192">f.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-192">f.</span></span> <span data-ttu-id="f3c6b-193">Mapowanie atrybutu SAML dla **E-mail** polu tekstowym wprowadź wartości jako **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**</span><span class="sxs-lookup"><span data-stu-id="f3c6b-193">In the SAML Attribute mapping for the **Email** text box enter the value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**</span></span>

11. <span data-ttu-id="f3c6b-194">Aby sprawdzić konfigurację, możesz kliknąć **testu** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-194">To check the configuration you can click on the **Test** button.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="f3c6b-195">Pomyślne testowania należy zakończyć działanie Kreatora konfiguracji w usłudze Azure AD i również zapewnić dostęp do użytkowników lub grupy, które można wykonać testu.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-195">For successful testing you need to complete the configuration wizard in Azure AD and also provide access to users or groups who can perform the test.</span></span>

12. <span data-ttu-id="f3c6b-196">Włączenia funkcji logowania jednokrotnego, sprawdzając na **włączenia logowania jednokrotnego** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-196">Enable the SSO by checking on the **Enable SSO** button.</span></span>

13. <span data-ttu-id="f3c6b-197">Teraz kliknij **aktualizacji** przycisk Tak, aby wszystkie ustawienia są zapisywane.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-197">Now click on the **Update** button so that all the settings are saved.</span></span> <span data-ttu-id="f3c6b-198">Spowoduje to wygenerowanie wartość RelayState.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-198">This will generate the RelayState value.</span></span> <span data-ttu-id="f3c6b-199">Kopiuj wartość RelayState, która jest generowana w polu tekstowym, wklej go w **stan przekazywania** pole tekstowe, w obszarze **Lifesize chmury domeny i adres URL** sekcji.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-199">Copy the RelayState value, which is generated in the text box, paste it in the **Relay State** textbox under **Lifesize Cloud Domain and URLs** section.</span></span> 

> [!TIP]
> <span data-ttu-id="f3c6b-200">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="f3c6b-200">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f3c6b-201">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-201">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f3c6b-202">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f3c6b-202">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f3c6b-203">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f3c6b-203">Creating an Azure AD test user</span></span>

<span data-ttu-id="f3c6b-204">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="f3c6b-206">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f3c6b-206">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f3c6b-207">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-207">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f3c6b-209">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-209">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f3c6b-211">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-211">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f3c6b-213">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="f3c6b-213">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f3c6b-215">a.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-215">a.</span></span> <span data-ttu-id="f3c6b-216">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-216">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f3c6b-217">b.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-217">b.</span></span> <span data-ttu-id="f3c6b-218">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-218">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f3c6b-219">c.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-219">c.</span></span> <span data-ttu-id="f3c6b-220">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-220">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f3c6b-221">d.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-221">d.</span></span> <span data-ttu-id="f3c6b-222">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-222">Click **Create**.</span></span>
 
### <a name="creating-a-lifesize-cloud-test-user"></a><span data-ttu-id="f3c6b-223">Tworzenie użytkownika testowego Lifesize chmury</span><span class="sxs-lookup"><span data-stu-id="f3c6b-223">Creating a Lifesize Cloud test user</span></span>

<span data-ttu-id="f3c6b-224">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w chmurze Lifesize.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-224">In this section, you create a user called Britta Simon in Lifesize Cloud.</span></span> <span data-ttu-id="f3c6b-225">Chmura Lifesize obsługę użytkowników.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-225">Lifesize cloud does support automatic user provisioning.</span></span> <span data-ttu-id="f3c6b-226">Po pomyślnym uwierzytelnieniu w usłudze Azure AD użytkownika będą automatycznie udostępniane w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-226">After successful authentication at Azure AD, the user will be automatically provisioned in the application.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f3c6b-227">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f3c6b-227">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f3c6b-228">W tej sekcji musisz włączyć Simona Britta do użycia usługi Azure logowania jednokrotnego za udzielanie dostępu do chmury Lifesize.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-228">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Lifesize Cloud.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="f3c6b-230">**Aby przypisać Simona Britta Lifesize chmury, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f3c6b-230">**To assign Britta Simon to Lifesize Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="f3c6b-231">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-231">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="f3c6b-233">Na liście aplikacji zaznacz **chmury Lifesize**.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-233">In the applications list, select **Lifesize Cloud**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_app.png) 

3. <span data-ttu-id="f3c6b-235">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-235">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="f3c6b-237">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-237">Click **Add** button.</span></span> <span data-ttu-id="f3c6b-238">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="f3c6b-240">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f3c6b-241">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f3c6b-242">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f3c6b-243">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="f3c6b-243">Testing single sign-on</span></span>

<span data-ttu-id="f3c6b-244">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-244">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f3c6b-245">Po kliknięciu kafelka Lifesize chmury w panelu dostępu, należy pobrać stronę logowania w chmurze Lifesize aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f3c6b-245">When you click the Lifesize Cloud tile in the Access Panel, you should get login page of Lifesize Cloud application.</span></span>
<span data-ttu-id="f3c6b-246">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f3c6b-246">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f3c6b-247">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="f3c6b-247">Additional resources</span></span>

* [<span data-ttu-id="f3c6b-248">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f3c6b-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f3c6b-249">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f3c6b-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_203.png

