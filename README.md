# openstack-2-

## Glance 映像檔套件
Glance作為OpenStack的Image service，提供使用者可以去尋找、註冊、取得虛擬機的Image。並提供了一個REST API，使你能夠查詢虛擬機Image的metadata與取得實際的Image。你可以透過Image service儲存在不同的地點所提供虛擬機Image，從簡單的檔案系統到像是物件儲存系統的OpenStack Object Storage（Swift）。除了可以讓使用者新增 image 之外，也可以從正在運作的 server 上取得 snapshop 來作為 image 的備份或者是其他虛擬磁碟的 image。

OpenStack的映像檔服務(Image service)包含了以下幾個元件：
- glance-api：接受來至其他服務的API呼叫，諸如Image尋找、取得、儲存。
- glance-registry：儲存、處理以及取得Image的metadata，metadata（包含諸如檔案大小、類型等資訊）。
- Database：存放Images的metadata資訊，使用者可以根據個人喜好選擇資料庫，大多數選擇MySQL或SQLite。
- Image的Storage Repository：支援多種類型的Repository，可以從一般檔案系統、Object Storage（Swift）、RADOS Block device、HTTP、Amazon S3等。但要注意，其中一些Repository只支援讀取。

![openstack](https://kairen.gitbooks.io/openstack-liberty/content/conceptions/glance/images/openstack_kilo_conceptual_arch.png)

從Openstack架構圖，可以看到Glance的定位：
- 可以將 image 存於 Swift 中。
- 提供 image 給 Nova 作為執行 VM 之用。
- 使用者可以透過 Horizon 呼叫 Glance API 來管理 image。
- 在使用 Glance API 之前，都需要通過 Keystone 的認證。

![openstack](https://kairen.gitbooks.io/openstack-liberty/content/conceptions/glance/images/glance_architecture.png)

## OpenStack Nova
OpenStack的Nova套件提供了Compute Service ，在整個 IaaS 的架構中是屬於最主要的部份，同時會向 Identity Service 進行認證授權、向 Image Service 要求 image、將資料提供給 Dashboard …. 等等。

OpenStack 運算互動於OpenStack登入驗證、OpenStack Image service的磁碟與伺服器映像檔、OpenStack儀表板的使用者與管理介面。映像檔的存取是受限制於projects以及users; quotas受限於每個project(好比Instance的數量)。OpenStack 運算能夠水平擴展於基底硬體以及下載映像檔來執行instances。

Nova是一個管理運算資源的套件，因而被稱為一個運算套件。
![openstack](https://kairen.gitbooks.io/openstack-liberty/content/conceptions/nova/images/nova_architecture.svg)


參考資料｜
- https://goo.gl/GBDUT8
