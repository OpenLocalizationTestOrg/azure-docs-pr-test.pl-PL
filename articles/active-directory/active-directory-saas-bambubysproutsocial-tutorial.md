---
title: "Samouczek: Integracji Azure Active Directory z Bambu przez Sprout społecznościowych | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Bambu przez Sprout społecznościowych."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2b9ddbc-cab7-40d6-aca1-5b171cab4199
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: jeedes
ms.openlocfilehash: 985966d26f6ed0dcd4db47589abf94260ce62bf0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bambu-by-sprout-social"></a><span data-ttu-id="3bb6b-103">Samouczek: Integracji Azure Active Directory z Bambu przez Sprout społecznościowych</span><span class="sxs-lookup"><span data-stu-id="3bb6b-103">Tutorial: Azure Active Directory integration with Bambu by Sprout Social</span></span>

<span data-ttu-id="3bb6b-104">Z tego samouczka dowiesz się integrowanie Bambu przez Sprout społecznościowych w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3bb6b-104">In this tutorial, you learn how to integrate Bambu by Sprout Social with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3bb6b-105">Integracja z usługą Azure AD Bambu przez Sprout społecznościowych zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="3bb6b-105">Integrating Bambu by Sprout Social with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3bb6b-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Bambu przez Sprout społecznościowych</span><span class="sxs-lookup"><span data-stu-id="3bb6b-106">You can control in Azure AD who has access to Bambu by Sprout Social</span></span>
- <span data-ttu-id="3bb6b-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Bambu przez Sprout społecznościowych (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="3bb6b-107">You can enable your users to automatically get signed-on to Bambu by Sprout Social (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3bb6b-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="3bb6b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3bb6b-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3bb6b-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

To enable single sign-on with Bambu by Sprout Social, it must be configured to use Azure Active Directory as an identity provider. This guide provides information and tips on how to perform this configuration in Bambu by Sprout Social.

>[!Note]: 
>This embedded guide is brand new in the new Azure portal, and we’d love to hear your thoughts. Use the Feedback ? button at the top of the portal to provide feedback. The older guide for using the [Azure classic portal](https://manage.windowsazure.com) to configure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="3bb6b-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3bb6b-110">Prerequisites</span></span>

<span data-ttu-id="3bb6b-111">Aby skonfigurować integrację usługi Azure AD z Bambu przez Sprout społecznościowych, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="3bb6b-111">To configure Azure AD integration with Bambu by Sprout Social, you need the following items:</span></span>

- <span data-ttu-id="3bb6b-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="3bb6b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3bb6b-113">Bambu przez Sprout społecznościowych jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="3bb6b-113">A Bambu by Sprout Social single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3bb6b-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3bb6b-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="3bb6b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3bb6b-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="3bb6b-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3bb6b-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3bb6b-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="3bb6b-118">Scenario description</span></span>
<span data-ttu-id="3bb6b-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3bb6b-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="3bb6b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3bb6b-121">Dodawanie Bambu przez Sprout społecznościowych z galerii</span><span class="sxs-lookup"><span data-stu-id="3bb6b-121">Adding Bambu by Sprout Social from the gallery</span></span>
2. <span data-ttu-id="3bb6b-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="3bb6b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bambu-by-sprout-social-from-the-gallery"></a><span data-ttu-id="3bb6b-123">Dodawanie Bambu przez Sprout społecznościowych z galerii</span><span class="sxs-lookup"><span data-stu-id="3bb6b-123">Adding Bambu by Sprout Social from the gallery</span></span>
<span data-ttu-id="3bb6b-124">Aby skonfigurować integrację usługi Azure AD Bambu przez Sprout społecznych, należy dodać Bambu przez Sprout społecznościowych z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-124">To configure the integration of Bambu by Sprout Social into Azure AD, you need to add Bambu by Sprout Social from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3bb6b-125">**Aby dodać Bambu przez Sprout społecznościowych z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="3bb6b-125">**To add Bambu by Sprout Social from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3bb6b-126">W  **[Azure Portal](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-126">In the **[Azure Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="3bb6b-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3bb6b-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="3bb6b-131">Kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego, aby dodać nową aplikację.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-131">Click **New application** button on the top of the dialog to add new application.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="3bb6b-133">W polu wyszukiwania wpisz **Bambu przez Sprout społecznościowych**.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-133">In the search box, type **Bambu by Sprout Social**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_search.png)

5. <span data-ttu-id="3bb6b-135">W panelu wyników wybierz **Bambu przez Sprout społecznościowych**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-135">In the results panel, select **Bambu by Sprout Social**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3bb6b-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="3bb6b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3bb6b-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Bambu przez Sprout społecznościowych w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-138">In this section, you configure and test Azure AD single sign-on with Bambu by Sprout Social based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3bb6b-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Bambu przez Sprout społecznościowych jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Bambu by Sprout Social is to a user in Azure AD.</span></span> <span data-ttu-id="3bb6b-140">Innymi słowy musi można ustanowić łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Bambu przez Sprout społecznościowych.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-140">In other words, a link relationship between an Azure AD user and the related user in Bambu by Sprout Social needs to be established.</span></span>

<span data-ttu-id="3bb6b-141">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w Bambu przez Sprout społecznościowych.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Bambu by Sprout Social.</span></span>

<span data-ttu-id="3bb6b-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Bambu przez Sprout społecznościowych, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="3bb6b-142">To configure and test Azure AD single sign-on with Bambu by Sprout Social, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3bb6b-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3bb6b-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3bb6b-145">**[Tworzenie Bambu przez użytkownika testowego Sprout społecznościowych](#creating-a-bambu-by-sprout-social-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Bambu przez Sprout społecznościowych połączonego z jej reprezentacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-145">**[Creating a Bambu by Sprout Social test user](#creating-a-bambu-by-sprout-social-test-user)** - to have a counterpart of Britta Simon in Bambu by Sprout Social that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="3bb6b-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3bb6b-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3bb6b-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="3bb6b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3bb6b-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i konfigurowanie rejestracji jednokrotnej w sieci Bambu przez aplikację Sprout społecznościowych.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Bambu by Sprout Social application.</span></span>

<span data-ttu-id="3bb6b-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Bambu przez Sprout społecznościowych, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="3bb6b-150">**To configure Azure AD single sign-on with Bambu by Sprout Social, perform the following steps:**</span></span>

1. <span data-ttu-id="3bb6b-151">W portalu Azure na **Bambu przez Sprout społecznościowych** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-151">In the Azure portal, on the **Bambu by Sprout Social** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="3bb6b-153">Na **logowanie jednokrotne** okna dialogowego, jako **tryb** wybierz **na języku SAML logowania jednokrotnego** Włącz funkcji logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_samlbase.png)

3. <span data-ttu-id="3bb6b-155">Na **Bambu Sprout domena społecznościowych i adresy URL** sekcji, użytkownik nie trzeba wykonywać żadnych czynności, jak aplikacja już jest wstępna Integracja z usługą Azure.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-155">On the **Bambu by Sprout Social Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_url.png)

4. <span data-ttu-id="3bb6b-157">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-157">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_certificate.png) 

5. <span data-ttu-id="3bb6b-159">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-159">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="3bb6b-161">Na **Bambu Sprout społecznościowych Konfiguracja** , kliknij przycisk **skonfigurować Bambu przez Sprout społecznościowych** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-161">On the **Bambu by Sprout Social Configuration** section, click **Configure Bambu by Sprout Social** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3bb6b-162">Kopiuj **SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="3bb6b-162">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_configure.png) 

7. <span data-ttu-id="3bb6b-164">Skonfigurować logowanie jednokrotne w **Bambu przez Sprout społecznościowych** stronie, musisz wysłać pobrany **XML metadanych** i **SAML pojedynczy znak na adres URL usługi** do [Bambu Sprout społecznościowych Obsługa](mailto:support@getbambu.com).</span><span class="sxs-lookup"><span data-stu-id="3bb6b-164">To configure single sign-on on **Bambu by Sprout Social** side, you need to send the downloaded **Metadata XML** and **SAML Single Sign-On Service URL** to [Bambu by Sprout Social support](mailto:support@getbambu.com).</span></span> <span data-ttu-id="3bb6b-165">One będzie skonfigurowanie tego numeru w celu połączenia logowania jednokrotnego SAML prawidłowo po obu stronach.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-165">They will set this up in order to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="3bb6b-166">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="3bb6b-166">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3bb6b-167">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** sekcji, po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-167">After adding this app from the **Active Directory > Enterprise Applications** section, simply click on the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3bb6b-168">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3bb6b-168">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

<!--### Next steps

To ensure users can sign-in to Bambu by Sprout Social after it has been configured to use Azure Active Directory, review the following tasks and topics:

- User accounts must be pre-provisioned into Bambu by Sprout Social prior to sign-in. To set this up, see Provisioning.
 
- Users must be assigned access to Bambu by Sprout Social in Azure AD to sign-in. To assign users, see Users.
 
- To configure access polices for Bambu by Sprout Social users, see Access Policies.
 
- For additional information on deploying single sign-on to users, see [this article](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3bb6b-169">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="3bb6b-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="3bb6b-170">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-170">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="3bb6b-172">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="3bb6b-172">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3bb6b-173">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-173">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3bb6b-175">Przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** do wyświetlenia na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-175">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3bb6b-177">W górnej części okna dialogowego kliknij **Dodaj** otworzyć **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-177">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3bb6b-179">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="3bb6b-179">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3bb6b-181">a.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-181">a.</span></span> <span data-ttu-id="3bb6b-182">W **nazwa** pole tekstowe, typ **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-182">In the **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="3bb6b-183">b.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-183">b.</span></span> <span data-ttu-id="3bb6b-184">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-184">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="3bb6b-185">c.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-185">c.</span></span> <span data-ttu-id="3bb6b-186">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-186">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3bb6b-187">d.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-187">d.</span></span> <span data-ttu-id="3bb6b-188">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-188">Click **Create**.</span></span>
 
### <a name="creating-a-bambu-by-sprout-social-test-user"></a><span data-ttu-id="3bb6b-189">Tworzenie Bambu przez Sprout społecznościowych użytkownika testowego</span><span class="sxs-lookup"><span data-stu-id="3bb6b-189">Creating a Bambu by Sprout Social test user</span></span>

<span data-ttu-id="3bb6b-190">Aplikacja obsługuje tylko w czasie Inicjowanie obsługi użytkowników i uwierzytelnianie użytkowników zostaną utworzone w aplikacji automatycznie.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-190">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3bb6b-191">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="3bb6b-191">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3bb6b-192">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu jej Bambu przez Sprout społecznościowych.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-192">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Bambu by Sprout Social.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="3bb6b-194">**Aby przypisać Simona Britta Bambu przez Sprout społecznościowych, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="3bb6b-194">**To assign Britta Simon to Bambu by Sprout Social, perform the following steps:**</span></span>

1. <span data-ttu-id="3bb6b-195">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-195">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="3bb6b-197">Na liście aplikacji zaznacz **Bambu przez Sprout społecznościowych**.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-197">In the applications list, select **Bambu by Sprout Social**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_app.png) 

3. <span data-ttu-id="3bb6b-199">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-199">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="3bb6b-201">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-201">Click **Add** button.</span></span> <span data-ttu-id="3bb6b-202">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-202">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="3bb6b-204">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-204">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3bb6b-205">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-205">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3bb6b-206">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-206">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3bb6b-207">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="3bb6b-207">Testing single sign-on</span></span>

<span data-ttu-id="3bb6b-208">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-208">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3bb6b-209">Kliknięcie Bambu Sprout społecznościowych kafelka w panelu dostępu, możesz należy pobrać automatycznie zalogowane do Twojej Bambu przez aplikację Sprout społecznościowych.</span><span class="sxs-lookup"><span data-stu-id="3bb6b-209">When you click the Bambu by Sprout Social tile in the Access Panel, you should get automatically signed-on to your Bambu by Sprout Social application.</span></span> <span data-ttu-id="3bb6b-210">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="3bb6b-210">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3bb6b-211">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="3bb6b-211">Additional resources</span></span>

* [<span data-ttu-id="3bb6b-212">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3bb6b-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3bb6b-213">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3bb6b-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_203.png

