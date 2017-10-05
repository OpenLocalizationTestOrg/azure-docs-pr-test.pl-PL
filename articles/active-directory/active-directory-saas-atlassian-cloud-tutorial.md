---
title: "Samouczek: Integracji Azure Active Directory z chmurą Atlassian | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i w chmurze Atlassian."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 729b8eb6-efc4-47fb-9f34-8998ca2c9545
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 2891838b56dd15cb5f97dcae391770143a80c781
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-atlassian-cloud"></a><span data-ttu-id="190eb-103">Samouczek: Integracji Azure Active Directory z chmurą Atlassian</span><span class="sxs-lookup"><span data-stu-id="190eb-103">Tutorial: Azure Active Directory integration with Atlassian Cloud</span></span>

<span data-ttu-id="190eb-104">Z tego samouczka dowiesz się integrowanie Atlassian chmury w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="190eb-104">In this tutorial, you learn how to integrate Atlassian Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="190eb-105">Integrowanie Atlassian chmurze z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="190eb-105">Integrating Atlassian Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="190eb-106">Można kontrolować w usłudze Azure AD, który ma dostęp do chmury Atlassian</span><span class="sxs-lookup"><span data-stu-id="190eb-106">You can control in Azure AD who has access to Atlassian Cloud</span></span>
- <span data-ttu-id="190eb-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do chmury Atlassian (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="190eb-107">You can enable your users to automatically get signed-on to Atlassian Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="190eb-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="190eb-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="190eb-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="190eb-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="190eb-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="190eb-110">Prerequisites</span></span>

<span data-ttu-id="190eb-111">Aby skonfigurować integrację usługi Azure AD z chmurą Atlassian, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="190eb-111">To configure Azure AD integration with Atlassian Cloud, you need the following items:</span></span>

- <span data-ttu-id="190eb-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="190eb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="190eb-113">Chmura Atlassian logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="190eb-113">An Atlassian Cloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="190eb-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="190eb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="190eb-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="190eb-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="190eb-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="190eb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="190eb-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna tutaj: [oferta wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="190eb-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="190eb-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="190eb-118">Scenario description</span></span>
<span data-ttu-id="190eb-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="190eb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="190eb-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="190eb-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="190eb-121">Dodawanie Atlassian chmury z galerii</span><span class="sxs-lookup"><span data-stu-id="190eb-121">Adding Atlassian Cloud from the gallery</span></span>
2. <span data-ttu-id="190eb-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="190eb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-atlassian-cloud-from-the-gallery"></a><span data-ttu-id="190eb-123">Dodawanie Atlassian chmury z galerii</span><span class="sxs-lookup"><span data-stu-id="190eb-123">Adding Atlassian Cloud from the gallery</span></span>
<span data-ttu-id="190eb-124">Aby skonfigurować integrację usługi Azure AD Atlassian Cloud, należy dodać Atlassian chmury z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="190eb-124">To configure the integration of Atlassian Cloud into Azure AD, you need to add Atlassian Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="190eb-125">**Aby dodać Atlassian chmury z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="190eb-125">**To add Atlassian Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="190eb-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="190eb-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="190eb-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="190eb-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="190eb-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="190eb-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="190eb-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="190eb-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="190eb-133">W polu wyszukiwania wpisz **chmury Atlassian**.</span><span class="sxs-lookup"><span data-stu-id="190eb-133">In the search box, type **Atlassian Cloud**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_search.png)

5. <span data-ttu-id="190eb-135">W panelu wyników wybierz **chmury Atlassian**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="190eb-135">In the results panel, select **Atlassian Cloud**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="190eb-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="190eb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="190eb-138">W tej sekcji możesz skonfigurować i test usługi Azure AD rejestracji jednokrotnej z chmurą Atlassian oparte na użytkownika testowego o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="190eb-138">In this section, you configure and test Azure AD single sign-on with Atlassian Cloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="190eb-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w chmurze Atlassian jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="190eb-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Atlassian Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="190eb-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w chmurze Atlassian musi się.</span><span class="sxs-lookup"><span data-stu-id="190eb-140">In other words, a link relationship between an Azure AD user and the related user in Atlassian Cloud needs to be established.</span></span>

<span data-ttu-id="190eb-141">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w chmurze Atlassian.</span><span class="sxs-lookup"><span data-stu-id="190eb-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Atlassian Cloud.</span></span>

<span data-ttu-id="190eb-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z chmurą Atlassian, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="190eb-142">To configure and test Azure AD single sign-on with Atlassian Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="190eb-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="190eb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="190eb-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="190eb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="190eb-145">**[Tworzenie użytkownika testowego chmury Atlassian](#creating-an-atlassian-cloud-test-user)**  — aby odpowiednikiem Simona Britta w chmurze Atlassian, która jest połączona z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="190eb-145">**[Creating an Atlassian Cloud test user](#creating-an-atlassian-cloud-test-user)** - to have a counterpart of Britta Simon in Atlassian Cloud that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="190eb-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="190eb-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="190eb-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="190eb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="190eb-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="190eb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="190eb-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne do aplikacji w chmurze Atlassian.</span><span class="sxs-lookup"><span data-stu-id="190eb-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Atlassian Cloud application.</span></span>

<span data-ttu-id="190eb-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z chmurą Atlassian, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="190eb-150">**To configure Azure AD single sign-on with Atlassian Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="190eb-151">W portalu Azure na **chmury Atlassian** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="190eb-151">In the Azure portal, on the **Atlassian Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="190eb-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="190eb-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_samlbase.png)

3. <span data-ttu-id="190eb-155">Na **adresy URL i domenę chmury Atlassian** sekcji, wykonaj następujące kroki, aby skonfigurować aplikację w **IDP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="190eb-155">On the **Atlassian Cloud Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_url.png)

    <span data-ttu-id="190eb-157">a.</span><span class="sxs-lookup"><span data-stu-id="190eb-157">a.</span></span> <span data-ttu-id="190eb-158">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<instancename>.atlassian.net/admin/saml/edit`</span><span class="sxs-lookup"><span data-stu-id="190eb-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<instancename>.atlassian.net/admin/saml/edit`</span></span>

    <span data-ttu-id="190eb-159">b.</span><span class="sxs-lookup"><span data-stu-id="190eb-159">b.</span></span> <span data-ttu-id="190eb-160">W **adres URL odpowiedzi** tekstowym, wpisz adres URL jako:`https://id.atlassian.com/login/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="190eb-160">In the **Reply URL** textbox, type a URL as: `https://id.atlassian.com/login/saml/acs`</span></span>

4. <span data-ttu-id="190eb-161">Sprawdź **Pokaż zaawansowane ustawienia adresu URL** i wykonać następujący krok, jeśli chcesz skonfigurować aplikację w **SP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="190eb-161">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_url1.png)

    <span data-ttu-id="190eb-163">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<instancename>.atlassian.net`</span><span class="sxs-lookup"><span data-stu-id="190eb-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instancename>.atlassian.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="190eb-164">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="190eb-164">These values are not real.</span></span> <span data-ttu-id="190eb-165">Rzeczywisty identyfikator i adres URL logowania, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="190eb-165">Update these values with the actual Identifier and Sign-On URL.</span></span> <span data-ttu-id="190eb-166">Możesz uzyskać dokładne wartości z konfiguracji SAML chmury Atlassian ekranu.</span><span class="sxs-lookup"><span data-stu-id="190eb-166">You can get the exact values from Atlassian Cloud SAML Configuration screen.</span></span>
 
5. <span data-ttu-id="190eb-167">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="190eb-167">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_certificate.png) 

6. <span data-ttu-id="190eb-169">Na **konfiguracji chmury Atlassian** , kliknij przycisk **Konfigurowanie chmury Atlassian** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="190eb-169">On the **Atlassian Cloud Configuration** section, click **Configure Atlassian Cloud** to open **Configure sign-on** window.</span></span> <span data-ttu-id="190eb-170">Kopiuj **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="190eb-170">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_configure.png) 

7. <span data-ttu-id="190eb-172">Aby uzyskać logowania jednokrotnego skonfigurowane dla danej aplikacji, należy zalogować się do portalu Atlassian przy użyciu uprawnień administratora.</span><span class="sxs-lookup"><span data-stu-id="190eb-172">To get SSO configured for your application, login to the Atlassian Portal using the administrator rights.</span></span>

8. <span data-ttu-id="190eb-173">W sekcji uwierzytelnianie nawigacji po lewej stronie kliknij **domen**.</span><span class="sxs-lookup"><span data-stu-id="190eb-173">In the Authentication section of the left navigation click **Domains**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_06.png)

    <span data-ttu-id="190eb-175">a.</span><span class="sxs-lookup"><span data-stu-id="190eb-175">a.</span></span> <span data-ttu-id="190eb-176">W polu tekstowym, wpisz nazwę domeny, a następnie kliknij przycisk **Dodaj domenę**.</span><span class="sxs-lookup"><span data-stu-id="190eb-176">In the textbox, type your domain name, and then click **Add domain**.</span></span>
        
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_07.png)

    <span data-ttu-id="190eb-178">b.</span><span class="sxs-lookup"><span data-stu-id="190eb-178">b.</span></span> <span data-ttu-id="190eb-179">Aby zweryfikować domeny, kliknij przycisk **Sprawdź**.</span><span class="sxs-lookup"><span data-stu-id="190eb-179">To verify the domain, click **Verify**.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_08.png)

    <span data-ttu-id="190eb-181">c.</span><span class="sxs-lookup"><span data-stu-id="190eb-181">c.</span></span> <span data-ttu-id="190eb-182">Pobierz plik html weryfikacji domeny, przekaż go do folderu głównego witryny sieci Web w danej domenie, a następnie kliknij **weryfikowanie domeny**.</span><span class="sxs-lookup"><span data-stu-id="190eb-182">Download the domain verification html file, upload it to the root folder of your domain's website, and then click **Verify domain**.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_09.png)

    <span data-ttu-id="190eb-184">d.</span><span class="sxs-lookup"><span data-stu-id="190eb-184">d.</span></span> <span data-ttu-id="190eb-185">Po zweryfikowaniu domeny wartość **stan** pole jest **zweryfikowano**.</span><span class="sxs-lookup"><span data-stu-id="190eb-185">Once the domain is verified, the value of the **Status** field is **Verified**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_10.png)

9. <span data-ttu-id="190eb-187">Na pasku nawigacyjnym po lewej stronie kliknij **SAML**.</span><span class="sxs-lookup"><span data-stu-id="190eb-187">In the left navigation bar, click **SAML**.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_11.png)

10. <span data-ttu-id="190eb-189">Utwórz Konfiguracja SAML i Dodaj konfigurację dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="190eb-189">Create a SAML Configuration and add the Identity provider configuration.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_12.png)

    <span data-ttu-id="190eb-191">a.</span><span class="sxs-lookup"><span data-stu-id="190eb-191">a.</span></span> <span data-ttu-id="190eb-192">W **dostawcy tożsamości identyfikator jednostki** tekst Wklej wartość **identyfikator jednostki SAML** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="190eb-192">In the **Identity provider Entity ID** text box, paste the value of  **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="190eb-193">b.</span><span class="sxs-lookup"><span data-stu-id="190eb-193">b.</span></span> <span data-ttu-id="190eb-194">W **dostawcy tożsamości adresu URL logowania jednokrotnego** tekst Wklej wartość **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="190eb-194">In the **Identity provider SSO URL** text box, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="190eb-195">c.</span><span class="sxs-lookup"><span data-stu-id="190eb-195">c.</span></span> <span data-ttu-id="190eb-196">Otwórz certyfikat pobrany z portalu Azure i skopiuj wartości bez rozpoczęcia i zakończenia wierszy i wklej go w **X509 publicznego certyfikatu** pole.</span><span class="sxs-lookup"><span data-stu-id="190eb-196">Open the downloaded certificate from Azure portal and copy the values without the Begin and End lines and paste it in the **Public X509 certificate** box.</span></span>
    
    <span data-ttu-id="190eb-197">d.</span><span class="sxs-lookup"><span data-stu-id="190eb-197">d.</span></span> <span data-ttu-id="190eb-198">Kliknij przycisk **Zapisz konfigurację** Aby zapisać ustawienia.</span><span class="sxs-lookup"><span data-stu-id="190eb-198">Click **Save Configuration**  to Save the settings.</span></span>
     
11. <span data-ttu-id="190eb-199">Zaktualizuj ustawienia usługi Azure AD, aby upewnić się, że skonfigurowano poprawny adres URL identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="190eb-199">Update the Azure AD settings to make sure that you have setup the correct Identifier URL.</span></span>
  
    <span data-ttu-id="190eb-200">a.</span><span class="sxs-lookup"><span data-stu-id="190eb-200">a.</span></span> <span data-ttu-id="190eb-201">Kopiuj **Identyfikatora tożsamości SP** z SAML ekranu i wklej go w usłudze Azure AD jako **identyfikator** wartość.</span><span class="sxs-lookup"><span data-stu-id="190eb-201">Copy the **SP Identity ID** from the SAML screen and paste it in Azure AD as the **Identifier** value.</span></span>

    <span data-ttu-id="190eb-202">b.</span><span class="sxs-lookup"><span data-stu-id="190eb-202">b.</span></span> <span data-ttu-id="190eb-203">Zaloguj się na adres URL jest adresem URL dzierżawy Atlassian chmury.</span><span class="sxs-lookup"><span data-stu-id="190eb-203">Sign On URL is the tenant URL of your Atlassian Cloud.</span></span>   

     ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_13.png)
    
12. <span data-ttu-id="190eb-205">W portalu Azure kliknij **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="190eb-205">In the Azure portal, Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_400.png)

> [!TIP]
> <span data-ttu-id="190eb-207">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="190eb-207">You can now read a concise version of these instructions inside the [Azure  portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="190eb-208">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="190eb-208">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="190eb-209">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="190eb-209">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="190eb-210">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="190eb-210">Creating an Azure AD test user</span></span>
<span data-ttu-id="190eb-211">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="190eb-211">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="190eb-213">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="190eb-213">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="190eb-214">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="190eb-214">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="190eb-216">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="190eb-216">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="190eb-218">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="190eb-218">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="190eb-220">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="190eb-220">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="190eb-222">a.</span><span class="sxs-lookup"><span data-stu-id="190eb-222">a.</span></span> <span data-ttu-id="190eb-223">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="190eb-223">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="190eb-224">b.</span><span class="sxs-lookup"><span data-stu-id="190eb-224">b.</span></span> <span data-ttu-id="190eb-225">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="190eb-225">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="190eb-226">c.</span><span class="sxs-lookup"><span data-stu-id="190eb-226">c.</span></span> <span data-ttu-id="190eb-227">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="190eb-227">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="190eb-228">d.</span><span class="sxs-lookup"><span data-stu-id="190eb-228">d.</span></span> <span data-ttu-id="190eb-229">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="190eb-229">Click **Create**.</span></span>
 
### <a name="creating-an-atlassian-cloud-test-user"></a><span data-ttu-id="190eb-230">Tworzenie użytkownika testowego Atlassian chmury</span><span class="sxs-lookup"><span data-stu-id="190eb-230">Creating an Atlassian Cloud test user</span></span>

<span data-ttu-id="190eb-231">Aby umożliwić użytkownikom usługi Azure AD do logowania się w chmurze Atlassian, muszą mieć przydzielone do Atlassian chmury.</span><span class="sxs-lookup"><span data-stu-id="190eb-231">To enable Azure AD users to log in to Atlassian Cloud, they must be provisioned into Atlassian Cloud.</span></span>  
<span data-ttu-id="190eb-232">W przypadku Atlassian chmury Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="190eb-232">In case of Atlassian Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="190eb-233">**Aby udostępnić konta użytkownika, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="190eb-233">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="190eb-234">W sekcji Administracja witryny kliknij **użytkowników** przycisku</span><span class="sxs-lookup"><span data-stu-id="190eb-234">In the Site administration section, click the **Users** button</span></span>

    ![Utwórz użytkownika Atlassian chmury](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_14.png) 

2. <span data-ttu-id="190eb-236">Kliknij przycisk **Tworzenie użytkownika** przycisk, aby utworzyć użytkownika w chmurze Atlassian</span><span class="sxs-lookup"><span data-stu-id="190eb-236">Click the **Create User** button to create a user in the Atlassian Cloud</span></span>

    ![Utwórz użytkownika Atlassian chmury](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_15.png) 

3. <span data-ttu-id="190eb-238">Wprowadź nazwę danego użytkownika **adres E-mail**, **Username**, i **imię i nazwisko** i przypisz dostęp do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="190eb-238">Enter the user's **Email address**, **Username**, and **Full Name** and assign the application access.</span></span> 

    ![Utwórz użytkownika Atlassian chmury](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_16.png)
 
4. <span data-ttu-id="190eb-240">Kliknij przycisk **tworzenia użytkownika** przycisku będzie wysyłać wiadomości e-mail z zaproszeniem dla użytkownika i po zaakceptowaniu zaproszenia użytkownik będzie aktywny w systemie.</span><span class="sxs-lookup"><span data-stu-id="190eb-240">Click **Create user** button, it will send the email invitation to the user and after accepting the invitation the user will be active in the system.</span></span> 

>[!NOTE] 
><span data-ttu-id="190eb-241">Zbiorcze użytkowników można również tworzyć przez kliknięcie **Tworzenie zbiorczego** przycisk w sekcji użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="190eb-241">You can also create the bulk users by clicking the **Bulk Create** button in the Users section.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="190eb-242">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="190eb-242">Assigning the Azure AD test user</span></span>

<span data-ttu-id="190eb-243">W tej sekcji musisz włączyć Simona Britta do użycia usługi Azure logowania jednokrotnego za udzielanie dostępu do chmury Atlassian.</span><span class="sxs-lookup"><span data-stu-id="190eb-243">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Atlassian Cloud.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="190eb-245">**Aby przypisać Simona Britta Atlassian chmury, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="190eb-245">**To assign Britta Simon to Atlassian Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="190eb-246">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="190eb-246">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="190eb-248">Na liście aplikacji zaznacz **chmury Atlassian**.</span><span class="sxs-lookup"><span data-stu-id="190eb-248">In the applications list, select **Atlassian Cloud**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_app.png) 

3. <span data-ttu-id="190eb-250">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="190eb-250">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="190eb-252">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="190eb-252">Click **Add** button.</span></span> <span data-ttu-id="190eb-253">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="190eb-253">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="190eb-255">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="190eb-255">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="190eb-256">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="190eb-256">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="190eb-257">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="190eb-257">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="190eb-258">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="190eb-258">Testing single sign-on</span></span>

<span data-ttu-id="190eb-259">W tej sekcji można przetestować konfigurację usługi Azure AD z logowania jednokrotnego za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="190eb-259">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="190eb-260">Po kliknięciu kafelka Atlassian chmury w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji w chmurze Atlassian.</span><span class="sxs-lookup"><span data-stu-id="190eb-260">When you click the Atlassian Cloud tile in the Access Panel, you should get automatically signed-on to your Atlassian Cloud application.</span></span> <span data-ttu-id="190eb-261">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="190eb-261">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="190eb-262">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="190eb-262">Additional resources</span></span>

* [<span data-ttu-id="190eb-263">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="190eb-263">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="190eb-264">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="190eb-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_203.png

