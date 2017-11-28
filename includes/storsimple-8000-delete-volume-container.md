<!--author=alkohli last changed: 01/13/17-->

<span data-ttu-id="2152f-101">Jeśli kontener woluminów ma skojarzone woluminy, wykonać tych woluminów w trybie offline najpierw.</span><span class="sxs-lookup"><span data-stu-id="2152f-101">If the volume container has associated volumes, take those volumes offline first.</span></span> <span data-ttu-id="2152f-102">Postępuj zgodnie z instrukcjami [Przełącz do trybu offline wolumin](../articles/storsimple/storsimple-manage-volumes.md#take-a-volume-offline).</span><span class="sxs-lookup"><span data-stu-id="2152f-102">Follow the steps in [Take a volume offline](../articles/storsimple/storsimple-manage-volumes.md#take-a-volume-offline).</span></span> <span data-ttu-id="2152f-103">Po woluminy są w trybie offline, można je usunąć.</span><span class="sxs-lookup"><span data-stu-id="2152f-103">After the volumes are offline, you can delete them.</span></span> <span data-ttu-id="2152f-104">Kontener woluminów ma skojarzone woluminów, usunięcie kontenera woluminów.</span><span class="sxs-lookup"><span data-stu-id="2152f-104">When the volume container has no associated volumes, delete the volume container.</span></span> <span data-ttu-id="2152f-105">Wykonaj następującą procedurę, aby usunąć kontener woluminów.</span><span class="sxs-lookup"><span data-stu-id="2152f-105">Perform the following procedure to delete a volume container.</span></span>

#### <a name="to-delete-a-volume-container"></a><span data-ttu-id="2152f-106">Aby usunąć kontener woluminów</span><span class="sxs-lookup"><span data-stu-id="2152f-106">To delete a volume container</span></span>
1. <span data-ttu-id="2152f-107">Przejdź do usługi Menedżer urządzeń StorSimple i kliknij pozycję **Urządzenia**.</span><span class="sxs-lookup"><span data-stu-id="2152f-107">Go to your StorSimple Device Manager service and click **Devices**.</span></span> <span data-ttu-id="2152f-108">Wybierz i kliknij urządzenie, a następnie przejdź do **Ustawienia > Zarządzaj > kontenery woluminów**.</span><span class="sxs-lookup"><span data-stu-id="2152f-108">Select and click the device and then go to **Settings > Manage > Volume containers**.</span></span>

    ![Wolumin kontenerów bloku](./media/storsimple-8000-create-volume-container/createvolumecontainer2.png)

2. <span data-ttu-id="2152f-110">Z listy tabelarycznej kontenery woluminów, wybierz kontener woluminów, które chcesz usunąć, kliknij prawym przyciskiem myszy **...**  , a następnie wybierz **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="2152f-110">From the tabular list of volume containers, select the volume container you want to delete, right click **...** and then select **Delete**.</span></span>

    ![Usunięcie kontenera woluminów](./media/storsimple-8000-delete-volume-container/deletevolumecontainer1.png)

3. <span data-ttu-id="2152f-112">Jeśli kontener woluminów ma skojarzone woluminów, mogą zostać usunięte.</span><span class="sxs-lookup"><span data-stu-id="2152f-112">If a volume container has no associated volumes, then it can be deleted.</span></span> <span data-ttu-id="2152f-113">Po wyświetleniu monitu o potwierdzenie, przejrzyj i zaznacz pole wyboru, podając wpływ usunięcie kontenera woluminów.</span><span class="sxs-lookup"><span data-stu-id="2152f-113">When prompted for confirmation, review and select the checkbox stating the impact of deleting the volume container.</span></span> <span data-ttu-id="2152f-114">Kliknij przycisk **usunąć** aby następnie usunąć kontener woluminów.</span><span class="sxs-lookup"><span data-stu-id="2152f-114">Click **Delete** to then delete the volume container.</span></span>

    ![Potwierdzenie usunięcia](./media/storsimple-8000-delete-volume-container/deletevolumecontainer2.png)

<span data-ttu-id="2152f-116">Lista kontenery woluminów jest aktualizowana do uwzględnienia kontenera usuniętych woluminów.</span><span class="sxs-lookup"><span data-stu-id="2152f-116">The list of volume containers is updated to reflect the deleted volume container.</span></span>

![](./media/storsimple-8000-delete-volume-container/deletevolumecontainer5.png)


