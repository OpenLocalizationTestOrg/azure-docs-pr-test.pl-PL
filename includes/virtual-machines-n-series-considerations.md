## <a name="deployment-considerations"></a>Zagadnienia dotyczące wdrażania

* Dostępność N serii maszyn wirtualnych, zobacz [produkty, które są dostępne w regionie](https://azure.microsoft.com/en-us/regions/services/).

* N-series maszyny wirtualne mogą być wdrażane tylko w modelu wdrażania usługi Resource Manager hello.

* Podczas tworzenia N-series maszynę Wirtualną przy użyciu portalu Azure na powitania hello **podstawy** bloku, wybierz opcję **typu dysku maszyny Wirtualnej** z **HDD**. rozmiar toochoose dostępny N-series, na powitania **rozmiar** bloku, kliknij przycisk **Wyświetl wszystkie**.

* Maszyny wirtualne z serii N nie obsługują dysków maszyny Wirtualnej, które bazują na magazynu Azure Premium.

* Jeśli chcesz toodeploy więcej niż kilka N serii maszyn wirtualnych, należy wziąć pod uwagę z subskrypcji lub inne opcje zakupu. Jeśli używasz [bezpłatnego konta platformy Azure](https://azure.microsoft.com/free/), możesz użyć ograniczonej liczby rdzeni obliczeniowych platformy Azure.

* Może być muszą przydziału rdzeni hello tooincrease (dla regionu) w Twojej subskrypcji platformy Azure, a zwiększyć hello oddzielne przydziału rdzeni NC lub wirtualizacją sieci. Zwiększ limit przydziału toorequest [otwarcia żądania pomocy technicznej online klienta](../articles/azure-supportability/how-to-create-azure-support-request.md) bez dodatkowych opłat. Domyślne limity może się różnić w zależności od kategorii subskrypcji.

* Jeden obraz maszyny Wirtualnej, można wdrożyć na maszynach wirtualnych serii N jest hello [maszyny wirtualnej platformy Azure danych nauki](../articles/machine-learning/machine-learning-data-science-virtual-machine-overview.md). Witaj maszyny wirtualnej nauki danych preinstaluje i konfiguruje wielu popularnych danych nauki i dokładnego narzędzie. On również preinstaluje wersji sterowników procesora GPU tesla — NVIDIA NC wystąpień.





