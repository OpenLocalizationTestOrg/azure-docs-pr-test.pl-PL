## <a name="sample-scenario"></a>Przykładowy scenariusz
toobetter pokazują, jak toomanage grup NSG, w tym artykule używa scenariusz hello poniżej.

![Scenariusz sieci wirtualnych](./media/virtual-networks-create-nsg-scenario-include/figure1.png)

W tym scenariuszu utworzysz grupy NSG dla każdej podsieci w hello **TestVNet** sieci wirtualnej, zgodnie z opisem poniżej: 

* **Grupa NSG frontonu**. Hello frontonu NSG zostaną zastosowane toohello *frontonu* podsieci i zawiera dwie reguły:    
  * **Reguła RDP**. Ta reguła umożliwia toohello ruch RDP *frontonu* podsieci.
  * **Reguła sieci Web**. Ta reguła umożliwia toohello ruch HTTP *frontonu* podsieci.
* **Grupa NSG zaplecza**. Hello wewnętrzna grupa NSG zostaną zastosowane toohello *zaplecza* podsieci i zawiera dwie reguły:    
  * **Reguła SQL**. Ta reguła zezwala na ruch SQL tylko z hello *frontonu* podsieci.
  * **Reguła sieci Web**. Ta reguła nie zezwala na wszystkie internet powiązany ruch z hello *zaplecza* podsieci.

Hello kombinacji tych zasad tworzenia scenariusza przypominającej DMZ, gdzie może odbierać ruchu przychodzącego ruchu SQL z podsieci frontonu hello hello zaplecza podsieci i nie toohello Brak dostępu do Internetu, podsieci frontonu hello może komunikować się z hello Internet i odbierać przychodzące żądania HTTP.

Scenariusz hello toodeploy opisany powyżej, wykonaj [to łącze](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd-NSG), kliknij przycisk **wdrażanie tooAzure**, Zastąp hello domyślne wartości parametrów w razie potrzeby i wykonaj te instrukcje hello hello portalu. W hello przykładowymi instrukcjami poniżej szablonu hello została toodeploy używany zasób nazwy grup **NSG zarządcy zasobów**. 

