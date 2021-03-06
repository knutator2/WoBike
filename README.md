# WoBike
Documentation of Bike Sharing APIs

It is userfull to show nearby bikesharing bikes in public transport apps. So i try to list the APIs from different bike sharing platforms. Also it could be interesting for multimodal routing apps.

## Nextbike (Worldwide)

URL: `https://api.nextbike.net/maps/nextbike-live.json` as JSON or `https://api.nextbike.net/maps/nextbike-live.xml` as XML. You also can filter by city, with the GET-Parameter `city`. Eg `https://api.nextbike.net/maps/nextbike-live.json?city=362` for Berlin.

For some citys nextbike has flexzones (free floating in this zones). At the moment these are:
 
 * Köln `https://api.nextbike.net/reservation/geojson/flexzone_kg.json`
 * Berlin `https://api.nextbike.net/reservation/geojson/flexzone_bn.json`
 * Dresden `https://api.nextbike.net/reservation/geojson/flexzone_sz.json`
 * Karlsruhe `https://api.nextbike.net/reservation/geojson/flexzone_fg.json`
 * Nürnberg `https://api.nextbike.net/reservation/geojson/flexzone_nb.json`
 * For all zones: `https://api.nextbike.net/reservation/geojson/flexzone_all.json`

## Call-a-Bike (Germany / Deutsche Bahn)

Call-a-Bike has [historic datasets](http://data.deutschebahn.com/dataset/data-call-a-bike) OpenData on the DeutscheBahn OpenData portal under CC-BY License.

You can use the [Flinkster API](http://data.deutschebahn.com/dataset/flinkster-api) with `providernetwork=2` to access Call-a-Bike live Data. You need to register on [developer.deutschebahn.com](https://developer.deutschebahn.com/store/site/pages/sign-up.jag) to get a free, unlimited API Key (Zugangstoken).

Example Request: `https://api.deutschebahn.com/flinkster-api-ng/v1/bookingproposals?lat=48.15&lon=11.5&radius=5000&limit=100&providernetwork=2` – You also have to set the `Authorization` header to `Bearer <YOUR-API-KEY>`

 * Paramter `limit` max value is `100`, but you can use `offset` to request more
 * Paramter `radius` is the searchradius in meters, max value is `10000`, min value is `100`, default `500`,
 * You can also add parameter `expand` to `rentalobject,price` to get vehicle and price info

There is also a [Documentation PDF](https://developer.deutschebahn.com/store/site/themes/responsive/templates/api/documentation/download.jag?tenant=carbon.super&resourceUrl=/registry/resource/_system/governance/apimgt/applicationdata/provider/DBOpenData/Flinkster_API_NG/v1/documentation/files/Schnittstellenspezifikation_FlinksterApiNG.pdf) (german only), and you can use the [API-console (3rd tab)](https://developer.deutschebahn.com/store/apis/info?name=Flinkster_API_NG&version=v1&provider=DBOpenData)

## oBike (Worldwide)

URL: `https://mobile.o.bike/api/v1/bike/list?latitude=<LAT>&longitude=<LON>` gives you all available bikes in a 1km*1km bounding box around the requested point. Example: `https://mobile.o.bike/api/v1/bike/list?latitude=48.1481&longitude=11.5755`

## ofo bike (China, UK, US, Austria, Thailand, Singapore)

For ofo bike you can only get the bike-locations if you have registered an account with a phone number. 

POST Request: `http://one.ofo.so/nearbyofoCar` with form parameters:

 * `lat`: `52.20`
 * `lng`: `0.134`
 * `source`: `1`
 * `token`: You need to register an account via phone number to get a token

## mobike (China, Italy, UK, Japan)

POST-Request to `https://mwx.mobike.com/mobike-api/rent/nearbyBikesInfo.do` with form parameters:

 * `latitude`: `22.5376`
 * `longitude`: `114.0577`

 Also you need to set the `Referer` header to `https://servicewechat.com/`.
 Maybe you need to set `user-agent` header to `MicroMessenger/6.5.4.1000 NetType/WIFI Language/zh_CN`

 The requested radius looks very small.

## yobike/ohbike

POST-Request to `https://en.api.ohbike.com/v1/vehicle/` with form-paramters:
 
 * `bounds`: `51.319838,-2.735466;51.605178,-2.477974` (boundingbox)
 * `coord_type`: `1`
 * `distance`: `700`
 * `ak`: `WWTaJQrg-NHe_Zl0iwghHyYypYw6g-6GEZHPGBBF6TI7OzZWo9VVLXWRs2ngQJ18` (Application Key)
 * `lat`: `51.462731`
 * `lng`: `-2.606720`
 * `zoom`: `11.000000`
 * `sign`: `58f66c2424cb6d410e9277a8f6cc81b4` md5 sum

The sign parameter is a md5 sum of all paramters. You need to build it, by:
 * get all POST *values* (excl. sign)
 * sort the values
 * concat the sorted values (ignoring empty values) to string
 * add `@ohbile` on the end of the string
 * md5 sum the string and add as sign paramter
 * string of this example would be `-2.606720111.00000051.319838,-2.735466;51.605178,-2.47797451.462731700WWTaJQrg-NHe_Zl0iwghHyYypYw6g-6GEZHPGBBF6TI7OzZWo9VVLXWRs2ngQJ18geonear@ohbile` and the md5: `58f66c2424cb6d410e9277a8f6cc81b4`

## Gobee bike (Hong Kong)

Simple GET-Request example: `http://aws.gobee.bike/GobeeBike/bikes/near_bikes?accuracy=20&lat=22.38&lng=114.198`

## bluegogo (China, US)

tbd

## LimeBike (US)

tbd

## Motivate (US)

[Motivate](https://www.motivateco.com/) builds Bikeshring Systems. They Publish there [Data and APIs](https://www.motivateco.com/use-our-data/). This includes the Following Systems (Cities) in the US:

 * Ford GoBike (Bay Area, CA)
 	* GBFS: `https://gbfs.fordgobike.com/gbfs/gbfs.json`
 * Biketown (Portland, OR)
 * Capital Bikeshare (Washington, DC)
 * Bike Chattanooga (Chattanooga, TN)
 * Citi Bike (New York)
 * CoGo (Columbus, OH)
 * Divvy (Chicago, IL)
 * Hubway (Boston, MA)

All APIs and Data are also listed on `https://www.motivateco.com/use-our-data/`

## BYKE (Germany)

Simple GET-Request example: `https://api-prod.ibyke.io/v1/bikes?latitude=52.55001&longitude=13.40902&order=nearby`

## dropbike (Canada)

* `POST`-Request: `https://dropbikeadminapi.herokuapp.com/v1/bikes_nearby`
* (Header `Content-Type` to `application/json`)
* Requst Payload example: `{"lat":43.659415191015498,"lng":-79.395512826740742}`

* You can also get there Regions with a simple `POST`-Request (without payload) to `https://dropbikeadminapi.herokuapp.com/v1/region_polygons`

## More...

 * Also have a look at [this Project](https://github.com/eskerda/pybikes/tree/master/pybikes)
 * [GBFS (General Bikeshare Feed Specification)](https://github.com/NABSA/gbfs)
 * [Bikesharing World Map](https://www.google.com/maps/d/u/0/viewer?mid=1UxYw9YrwT_R3SGsktJU3D-2GpMU&ll=50.01042750703113%2C35.03132237929685&z=2)
 * [Open Bike Share Data](https://bikeshare-research.org/)
