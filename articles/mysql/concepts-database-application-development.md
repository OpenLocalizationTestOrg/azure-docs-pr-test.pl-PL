---
title: "Omówienie tworzenia aplikacji bazy danych dla bazy danych Azure dla programu MySQL | Dokumentacja firmy Microsoft"
description: "Wprowadza zagadnienia dotyczące projektowania, które dewelopera należy stosować podczas pisania kodu aplikacji do łączenia z bazą danych Azure dla programu MySQL"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 350dd775e172120d806d1193877a34d94f4d3f6a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="application-development-overview-for-azure-database-for-mysql"></a><span data-ttu-id="654a2-103">Omówienie tworzenia aplikacji dla bazy danych Azure dla programu MySQL</span><span class="sxs-lookup"><span data-stu-id="654a2-103">Application development overview for Azure Database for MySQL</span></span> 
<span data-ttu-id="654a2-104">W tym artykule omówiono zagadnienia dotyczące projektowania, które dewelopera należy stosować podczas pisania kodu aplikacji do łączenia z bazą danych Azure dla programu MySQL</span><span class="sxs-lookup"><span data-stu-id="654a2-104">This article discusses design considerations that a developer should follow when writing application code to connect to Azure Database for MySQL</span></span> 

> [!TIP]
> <span data-ttu-id="654a2-105">Samouczek pokazuje, jak utworzyć serwer, utworzenie zapory na serwerze, wyświetlić właściwości serwera, Utwórz bazę danych, Połącz i zapytań przy użyciu narzędzia workbench i mysql.exe, zobacz [projektowania pierwszą bazę danych MySQL na platformie Azure](tutorial-design-database-using-portal.md)</span><span class="sxs-lookup"><span data-stu-id="654a2-105">For a tutorial showing you how to create a server, create a server-based firewall, view server properties, create database, connect and query using workbench and mysql.exe, see [Design your first Azure MySQL database](tutorial-design-database-using-portal.md)</span></span>

## <a name="language-and-platform"></a><span data-ttu-id="654a2-106">Język i platforma</span><span class="sxs-lookup"><span data-stu-id="654a2-106">Language and platform</span></span>
<span data-ttu-id="654a2-107">Dostępne są przykłady kodu dla różnych języków programowania i platform programistycznych.</span><span class="sxs-lookup"><span data-stu-id="654a2-107">There are code samples available for various programming languages and platforms.</span></span> <span data-ttu-id="654a2-108">Można znaleźć łącza do przykładów kodu w: [bibliotek łączności używane do łączenia z bazą danych Azure dla programu MySQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="654a2-108">You can find links to the code samples at: [Connectivity libraries used to connect to Azure Database for MySQL](concepts-connection-libraries.md)</span></span>

## <a name="tools"></a><span data-ttu-id="654a2-109">Narzędzia</span><span class="sxs-lookup"><span data-stu-id="654a2-109">Tools</span></span>
<span data-ttu-id="654a2-110">Wersja ciągu identyfikacyjnego MySQL, zgodne z MySQL popularnych narzędzi do zarządzania takich jak narzędzia Workbench lub MySQL, takich jak mysql.exe, korzysta z bazy danych platformy Azure dla programu MySQL [phpMyAdmin](https://www.phpmyadmin.net/), [Navicat](https://www.navicat.com/products/navicat-for-mysql)i inne.</span><span class="sxs-lookup"><span data-stu-id="654a2-110">Azure Database for MySQL uses the MySQL community version, compatible with MySQL common management tools such as Workbench or MySQL utilities such as mysql.exe, [phpMyAdmin](https://www.phpmyadmin.net/), [Navicat](https://www.navicat.com/products/navicat-for-mysql), and others.</span></span> <span data-ttu-id="654a2-111">Do interakcji z usługą baza danych, można użyć portalu Azure, interfejsu wiersza polecenia Azure i interfejsów API REST.</span><span class="sxs-lookup"><span data-stu-id="654a2-111">You can also use the Azure portal, Azure CLI, and REST APIs to interact with the database service.</span></span>

## <a name="resource-limitations"></a><span data-ttu-id="654a2-112">Ograniczenia zasobów</span><span class="sxs-lookup"><span data-stu-id="654a2-112">Resource limitations</span></span>
<span data-ttu-id="654a2-113">Baza danych MySQL Azure zarządza zasoby dostępne dla serwera przy użyciu dwóch różnych mechanizmów:</span><span class="sxs-lookup"><span data-stu-id="654a2-113">Azure MySQL Database manages the resources available to a server using two different mechanisms:</span></span> 
- <span data-ttu-id="654a2-114">Zarządzanie zasobami</span><span class="sxs-lookup"><span data-stu-id="654a2-114">Resources Governance</span></span> 
- <span data-ttu-id="654a2-115">Wymuszanie ograniczeń.</span><span class="sxs-lookup"><span data-stu-id="654a2-115">Enforcement of Limits.</span></span>

## <a name="security"></a><span data-ttu-id="654a2-116">Bezpieczeństwo</span><span class="sxs-lookup"><span data-stu-id="654a2-116">Security</span></span>
<span data-ttu-id="654a2-117">Baza danych MySQL Azure zawiera zasoby dotyczące ograniczanie dostępu, ochrona danych Konfigurowanie użytkowników i ról i monitorowanie działań na bazę danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="654a2-117">Azure MySQL Database provides resources for limiting access, protecting data, configuring users and role, and monitoring activities on a MySQL Database.</span></span>

## <a name="authentication"></a><span data-ttu-id="654a2-118">Authentication</span><span class="sxs-lookup"><span data-stu-id="654a2-118">Authentication</span></span>
<span data-ttu-id="654a2-119">Baza danych MySQL Azure obsługuje uwierzytelnianie serwera użytkowników i nazwy logowania.</span><span class="sxs-lookup"><span data-stu-id="654a2-119">Azure MySQL Database supports server authentication of users and logins.</span></span>

## <a name="resiliency"></a><span data-ttu-id="654a2-120">Odporność</span><span class="sxs-lookup"><span data-stu-id="654a2-120">Resiliency</span></span>
<span data-ttu-id="654a2-121">Po wystąpieniu błędu przejściowego podczas łączenia z bazą danych MySQL, ponów wywołanie kodu.</span><span class="sxs-lookup"><span data-stu-id="654a2-121">When a transient error occurs while connecting to MySQL Database, your code should retry the call.</span></span> <span data-ttu-id="654a2-122">Firma Microsoft zaleca, użyj logiki ponawiania wycofania logiki, więc, że nie przeciąży bazy danych SQL z wielu klientów jednocześnie ponawianie próby.</span><span class="sxs-lookup"><span data-stu-id="654a2-122">We recommend the retry logic use back off logic, so that it does not overwhelm the SQL Database with multiple clients retrying simultaneously.</span></span>

- <span data-ttu-id="654a2-123">Przykłady kodu: Logika ponawiania próby przykłady kodu, które ilustrują temacie Przykłady w języku wybranym w: [bibliotek łączności używane do łączenia z bazą danych Azure dla programu MySQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="654a2-123">Code samples: For code samples that illustrate retry logic, see samples for the language of your choice at: [Connectivity libraries used to connect to Azure Database for MySQL](concepts-connection-libraries.md)</span></span>

## <a name="managing-connections"></a><span data-ttu-id="654a2-124">Zarządzanie połączeniami</span><span class="sxs-lookup"><span data-stu-id="654a2-124">Managing Connections</span></span>
<span data-ttu-id="654a2-125">Połączenia bazy danych są ograniczone zasobów, dlatego zalecamy użycie za pośrednictwem połączenia podczas uzyskiwania dostępu do bazy danych MySQL osiągnąć większą wydajność.</span><span class="sxs-lookup"><span data-stu-id="654a2-125">Database connections are a limited resource, so we recommend sensible use of connections when accessing your MySQL Database to achieve better performance.</span></span>
- <span data-ttu-id="654a2-126">Dostęp do bazy danych przy użyciu puli połączeń lub połączeń trwałych.</span><span class="sxs-lookup"><span data-stu-id="654a2-126">Access the database by using connection pooling or persistent connections.</span></span>
- <span data-ttu-id="654a2-127">Dostęp do bazy danych przy użyciu krótkich połączenia życia.</span><span class="sxs-lookup"><span data-stu-id="654a2-127">Access the database by using short connection life span.</span></span> 
- <span data-ttu-id="654a2-128">Użyj logiki ponawiania próby w aplikacji w punkcie próba połączenia, aby wykryć błędy z powodu równoczesnych połączeń osiągnięto maksymalną dozwoloną.</span><span class="sxs-lookup"><span data-stu-id="654a2-128">Use retry logic in your application at the point of the connection attempt, to catch failures due to concurrent connections have reached the maximum allowed.</span></span> <span data-ttu-id="654a2-129">W Logika ponawiania ustawić krótkie opóźnienie i poczekaj losowy czas przed prób dodatkowego połączenia.</span><span class="sxs-lookup"><span data-stu-id="654a2-129">In the retry logic, set a short delay, and then wait for a random time before the additional connection attempts.</span></span>