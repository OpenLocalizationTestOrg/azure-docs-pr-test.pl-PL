---
title: 'Samouczek: Integracji Azure Active Directory z centralnego Cerner | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Cerner centralnego."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2bc549d-d286-4679-854e-bb67c62b0475
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 77b5fb94cdfa5722081198aabc59fbf86229c2b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cerner-central"></a><span data-ttu-id="d7068-103">Samouczek: Integracji Azure Active Directory z centralnego Cerner</span><span class="sxs-lookup"><span data-stu-id="d7068-103">Tutorial: Azure Active Directory integration with Cerner Central</span></span>

<span data-ttu-id="d7068-104">Z tego samouczka dowiesz sposobu integracji z usługą Azure Active Directory (Azure AD) Cerner centralnego.</span><span class="sxs-lookup"><span data-stu-id="d7068-104">In this tutorial, you learn how to integrate Cerner Central with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d7068-105">Integracja z usługą Azure AD Cerner centralnego zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="d7068-105">Integrating Cerner Central with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d7068-106">Można kontrolować w usłudze Azure AD, który ma dostęp do centralnego Cerner</span><span class="sxs-lookup"><span data-stu-id="d7068-106">You can control in Azure AD who has access to Cerner Central</span></span>
- <span data-ttu-id="d7068-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do centralnego Cerner (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7068-107">You can enable your users to automatically get signed-on to Cerner Central (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d7068-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="d7068-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d7068-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d7068-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d7068-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d7068-110">Prerequisites</span></span>

<span data-ttu-id="d7068-111">Aby skonfigurować integrację usługi Azure AD z centralnego Cerner, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="d7068-111">To configure Azure AD integration with Cerner Central, you need the following items:</span></span>

- <span data-ttu-id="d7068-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7068-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d7068-113">Zatwierdzone Cerner centralna konta systemu</span><span class="sxs-lookup"><span data-stu-id="d7068-113">An approved Cerner Central System Account</span></span>

> [!NOTE]
> <span data-ttu-id="d7068-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="d7068-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d7068-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="d7068-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d7068-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="d7068-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d7068-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d7068-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d7068-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="d7068-118">Scenario description</span></span>
<span data-ttu-id="d7068-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="d7068-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d7068-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="d7068-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d7068-121">Dodawanie centralnego Cerner z galerii</span><span class="sxs-lookup"><span data-stu-id="d7068-121">Adding Cerner Central from the gallery</span></span>
2. <span data-ttu-id="d7068-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="d7068-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cerner-central-from-the-gallery"></a><span data-ttu-id="d7068-123">Dodawanie centralnego Cerner z galerii</span><span class="sxs-lookup"><span data-stu-id="d7068-123">Adding Cerner Central from the gallery</span></span>
<span data-ttu-id="d7068-124">Aby skonfigurować integrację usługi Azure AD centralnego Cerner, należy dodać centralnego Cerner z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="d7068-124">To configure the integration of Cerner Central into Azure AD, you need to add Cerner Central from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d7068-125">**Aby dodać centralnego Cerner z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="d7068-125">**To add Cerner Central from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d7068-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="d7068-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="d7068-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="d7068-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d7068-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="d7068-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="d7068-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d7068-131">To add new application, click **New application** button on top of the dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="d7068-133">W polu wyszukiwania wpisz **centralnego Cerner**.</span><span class="sxs-lookup"><span data-stu-id="d7068-133">In the search box, type **Cerner Central**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_search.png)

5. <span data-ttu-id="d7068-135">W panelu wyników wybierz **centralnego Cerner**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="d7068-135">In the results panel, select **Cerner Central**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d7068-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="d7068-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d7068-138">W tej sekcji możesz skonfigurować i test usługi Azure AD rejestracji jednokrotnej z centralnego Cerner oparte na użytkownika testowego o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="d7068-138">In this section, you configure and test Azure AD single sign-on with Cerner Central based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d7068-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w środkowej Cerner jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d7068-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Cerner Central is to a user in Azure AD.</span></span> <span data-ttu-id="d7068-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i danemu użytkownikowi w środkowej Cerner musi określone.</span><span class="sxs-lookup"><span data-stu-id="d7068-140">In other words, a link relationship between an Azure AD user and the related user in Cerner Central needs to be established.</span></span>

<span data-ttu-id="d7068-141">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z centralnego Cerner, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="d7068-141">To configure and test Azure AD single sign-on with Cerner Central, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d7068-142">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="d7068-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d7068-143">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="d7068-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d7068-144">**[Tworzenie użytkownika testowego centralnego Cerner](#creating-a-cerner-central-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta centralnego Cerner, połączonej z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d7068-144">**[Creating a Cerner Central test user](#creating-a-cerner-central-test-user)** - to have a counterpart of Britta Simon in Cerner Central that is linked to the Azure AD representation of the user.</span></span>
4. <span data-ttu-id="d7068-145">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="d7068-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d7068-146">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="d7068-146">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d7068-147">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d7068-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d7068-148">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Cerner centralnego.</span><span class="sxs-lookup"><span data-stu-id="d7068-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cerner Central application.</span></span>

<span data-ttu-id="d7068-149">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z centralnego Cerner, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="d7068-149">**To configure Azure AD single sign-on with Cerner Central, perform the following steps:**</span></span>

1. <span data-ttu-id="d7068-150">W portalu Azure na **centralnego Cerner** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="d7068-150">In the Azure portal, on the **Cerner Central** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="d7068-152">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="d7068-152">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_samlbase.png)

3. <span data-ttu-id="d7068-154">Na **Cerner centralnej domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="d7068-154">On the **Cerner Central Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_url.png)

    <span data-ttu-id="d7068-156">a.</span><span class="sxs-lookup"><span data-stu-id="d7068-156">a.</span></span> <span data-ttu-id="d7068-157">W **identyfikator** tekstowym, wpisz wartość, przy użyciu następujących wzorców:</span><span class="sxs-lookup"><span data-stu-id="d7068-157">In the **Identifier** textbox, type the value using the following patterns:</span></span>
    
    | |
    |--|
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.sandboxcerner.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.sandboxcernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://sandboxcernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/metadata` |

    <span data-ttu-id="d7068-158">b.</span><span class="sxs-lookup"><span data-stu-id="d7068-158">b.</span></span> <span data-ttu-id="d7068-159">W **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą następujących wzorców:</span><span class="sxs-lookup"><span data-stu-id="d7068-159">In the **Reply URL** textbox, type a URL using the following patterns:</span></span> 
    | |
    |--|
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/sso` |
    | `https://cernercentral.com/<instasncename>` |
    | `https://sandboxcernercentral.com/<instancename>` |
    | `https://sandboxcernercentral.com/<instancename>` |
    | `https://<subdomain>.sandboxcernercentral.com/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="d7068-160">Wartości te nie są rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="d7068-160">These values are not the real.</span></span> <span data-ttu-id="d7068-161">Rzeczywisty identyfikator i adres URL odpowiedzi, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="d7068-161">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="d7068-162">Skontaktuj się z [zespołem pomocy technicznej centralnego Cerner](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="d7068-162">Contact [Cerner Central support team](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations) to get these values.</span></span>
 
4. <span data-ttu-id="d7068-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d7068-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cernercentral-tutorial/tutorial_general_400.png)

5. <span data-ttu-id="d7068-165">Aby wygenerować **metadanych** adres url, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="d7068-165">To generate the **Metadata** url, perform the following steps:</span></span>

    <span data-ttu-id="d7068-166">a.</span><span class="sxs-lookup"><span data-stu-id="d7068-166">a.</span></span> <span data-ttu-id="d7068-167">Kliknij przycisk **rejestracji aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="d7068-167">Click **App registrations**.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_appregistrations.png)
   
    <span data-ttu-id="d7068-169">b.</span><span class="sxs-lookup"><span data-stu-id="d7068-169">b.</span></span> <span data-ttu-id="d7068-170">Kliknij przycisk **punkty końcowe** otworzyć **punkty końcowe** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="d7068-170">Click **Endpoints** to open **Endpoints** dialog box.</span></span>  
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_endpointicon.png)

    <span data-ttu-id="d7068-172">c.</span><span class="sxs-lookup"><span data-stu-id="d7068-172">c.</span></span> <span data-ttu-id="d7068-173">Kliknij przycisk Kopiuj, aby skopiować **dokument METADANYCH usług FEDERACYJNYCH** adresu url i wklej go do Notatnika.</span><span class="sxs-lookup"><span data-stu-id="d7068-173">Click the copy button to copy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_endpoint.png)
     
    <span data-ttu-id="d7068-175">d.</span><span class="sxs-lookup"><span data-stu-id="d7068-175">d.</span></span> <span data-ttu-id="d7068-176">Teraz przejdź do strony właściwości **centralnego Cerner** i skopiuj **identyfikator aplikacji** przy użyciu **kopiowania** przycisk i wklej go do Notatnika.</span><span class="sxs-lookup"><span data-stu-id="d7068-176">Now go to the property page of **Cerner Central** and copy the **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_appid.png)

    <span data-ttu-id="d7068-178">e.</span><span class="sxs-lookup"><span data-stu-id="d7068-178">e.</span></span> <span data-ttu-id="d7068-179">Generowanie **adres URL metadanych** przy użyciu następującego wzorca:`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="d7068-179">Generate the **Metadata URL** using the following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

6. <span data-ttu-id="d7068-180">Skonfigurować logowanie jednokrotne w **centralnego Cerner** stronie, musisz wysłać **adres URL metadanych** do [Obsługa centralnego Cerner](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations).</span><span class="sxs-lookup"><span data-stu-id="d7068-180">To configure single sign-on on **Cerner Central** side, you need to send the **Metadata URL** to [Cerner Central support](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations).</span></span> <span data-ttu-id="d7068-181">Skonfigurowano SSO po stronie aplikacji, aby ukończyć integracji.</span><span class="sxs-lookup"><span data-stu-id="d7068-181">They configure the SSO on application side to complete the integration.</span></span>

> [!TIP]
> <span data-ttu-id="d7068-182">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="d7068-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d7068-183">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="d7068-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d7068-184">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d7068-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d7068-185">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7068-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="d7068-186">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="d7068-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span> 

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="d7068-188">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="d7068-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d7068-189">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="d7068-189">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d7068-191">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="d7068-191">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d7068-193">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="d7068-193">To open the **User** dialog, click **Add**.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d7068-195">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="d7068-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d7068-197">a.</span><span class="sxs-lookup"><span data-stu-id="d7068-197">a.</span></span> <span data-ttu-id="d7068-198">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d7068-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d7068-199">b.</span><span class="sxs-lookup"><span data-stu-id="d7068-199">b.</span></span> <span data-ttu-id="d7068-200">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="d7068-200">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="d7068-201">c.</span><span class="sxs-lookup"><span data-stu-id="d7068-201">c.</span></span> <span data-ttu-id="d7068-202">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="d7068-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d7068-203">d.</span><span class="sxs-lookup"><span data-stu-id="d7068-203">d.</span></span> <span data-ttu-id="d7068-204">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d7068-204">Click **Create**.</span></span>
 
### <a name="creating-a-cerner-central-test-user"></a><span data-ttu-id="d7068-205">Tworzenie użytkownika testowego Cerner środkowe</span><span class="sxs-lookup"><span data-stu-id="d7068-205">Creating a Cerner Central test user</span></span>

<span data-ttu-id="d7068-206">**Środkowe Cerner** aplikacji pozwala na uwierzytelnianie z każdego dostawcy tożsamości federacyjnych.</span><span class="sxs-lookup"><span data-stu-id="d7068-206">**Cerner Central** application allows authentication from any federated identity provider.</span></span> <span data-ttu-id="d7068-207">Jeśli użytkownik będzie mógł logować się do strony głównej aplikacji, są federacyjnych i nie potrzebują ręcznej obsługi.</span><span class="sxs-lookup"><span data-stu-id="d7068-207">If a user is able to log in to the application home page, they are federated and have no need for any manual provisioning.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d7068-208">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7068-208">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d7068-209">W tej sekcji musisz włączyć Simona Britta do użycia usługi Azure logowania jednokrotnego za udzielanie dostępu do centralnego Cerner.</span><span class="sxs-lookup"><span data-stu-id="d7068-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Cerner Central.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="d7068-211">**Aby przypisać centralne Cerner Simona Britta, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="d7068-211">**To assign Britta Simon to Cerner Central, perform the following steps:**</span></span>

1. <span data-ttu-id="d7068-212">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="d7068-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="d7068-214">Na liście aplikacji zaznacz **centralnego Cerner**.</span><span class="sxs-lookup"><span data-stu-id="d7068-214">In the applications list, select **Cerner Central**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_app.png) 

3. <span data-ttu-id="d7068-216">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="d7068-216">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="d7068-218">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d7068-218">Click **Add** button.</span></span> <span data-ttu-id="d7068-219">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d7068-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="d7068-221">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="d7068-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d7068-222">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d7068-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d7068-223">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d7068-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d7068-224">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d7068-224">Testing single sign-on</span></span>

<span data-ttu-id="d7068-225">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="d7068-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d7068-226">Po kliknięciu kafelka Cerner centralnego w panelu dostępu należy należy pobrać automatycznie zalogowane do centralnego Cerner aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d7068-226">When you click the Cerner Central tile in the Access Panel, you should get automatically signed-on to your Cerner Central application.</span></span> <span data-ttu-id="d7068-227">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d7068-227">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d7068-228">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="d7068-228">Additional resources</span></span>

* [<span data-ttu-id="d7068-229">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d7068-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d7068-230">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d7068-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_203.png

