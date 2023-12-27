# The Enclosure

As many 3d printer enthusiasts will tell you, an enclosure is the best of all worlds. You can keep VOC's (mostly) contained, reduce temperature fluctuations, control ambient temp, and much more! It was (and still is) my goal to make an enclosure that is both compatible with the Kobra Go form factor and somewhat nice looking. 

## About the Project
This has been a goal of mine ever since I obtained this printer. To build a 'bespoke' Lack enclosure for the printer. I initially was going to build one of the many existing projects out there, but found that none of them matched exactly what I wanted, nor did they fit the Go. I will be doing my best to fully document the build process, although not many photos were taken.

## Bought Parts List
| Item      | Quantity | Description |
| ----------- | ----------- | ----------- |
|[IKEA Lack Tables](https://amzn.to/3RC7edl){target=_blank}| 3 | These will form the structure of the enclosure. |
|[22AWG Wire](https://amzn.to/3v8cCxc){target=_blank} | 1 | Generic wire for various applications. |
|[Neodynium Magnets](https://amzn.to/3txnx3a){target=_blank} | 1 | These will be what secure the top to the enclosure. |
|[Govee LED Strip](https://amzn.to/3GV1GFW){target=_blank} | 1 | These attach to the ceiling of the upper lid to provide light. |
|[12v Fan PSU](https://amzn.to/3TyUW8g){target=_blank} | 1 | Power for the two 120mm fans that will be used as exhaust and filter. |
|[Arctic BioniX P12](https://amzn.to/47gqR0e){target=_blank} | 2 | Fans for aformentioned filter and exhasut system. |
|[PWM Controller](https://amzn.to/41BJWc6){target=_blank}  | 2-3 | These are needed for fan control for the exhausts and optional internal filter. |
|[PTFE Tubing/Fittings](https://amzn.to/41AaqLh){target=_blank}  | 1 | Plenty of fittings for this project and future ones. |
|[WinSinn 12v 5015 Fans](https://amzn.to/48z9CbA){target=_blank}| 2 | This is a pack of four fans, these are quite useful for 3D printing in general, you only need two for this project though. |
|[Activated Carbon & Filter](https://www.etsy.com/listing/1563529764/carbon-hepa-filter-refill-pack?etsrc=sdt&variation0=3914981833){target=_blank}| 1 | These packs are made specifically for the bento box and are a great starting point if it will be part of your build! |
|[Fan Extensions](https://www.aliexpress.us/item/3256802339021307.html?spm=a2g0o.order_list.order_list_main.41.6f251802NiPLFz&gatewayAdapt=glo2usa){target=_blank} | 7 | Be sure to order the **80cm** versions as they will be needed to power the exhaust fans and filter from the PSU to the control panel. |
|[Plexiglass](https://www.tapplastics.com/product/plastics/cut_to_size_plastic/recycled-acrylic-sheets-clear){target=_blank} | 2 | 609mm x 448mm x 4.5mm   |
|[Plexiglass](https://www.tapplastics.com/product/plastics/cut_to_size_plastic/recycled-acrylic-sheets-clear){target=_blank} | 1 | 606mm x 443mm x 4.5mm   |
|[Metric Screw Set](https://amzn.to/3TFvwpr){target=_blank}| 1 |Always good to have a spread of bolts and such for this project.|
|[Wood Screw Set](https://amzn.to/3RLfl7I){target=_blank}| 1 | Wood screws that will be used to secure the feet into the legs. |

??? tip "Plexiglass vs PVC Foam Board"
    Plexiglass is *not* the end-all-be-all. A cheaper (and probably better) alternative is some kind of PVC [foam board](https://amzn.to/3TFST2e){target=_blank}. The enlcosure is designed for the following rear dimensions of 18in. x 24in. x 0.236in. Yes I realize I switched to imperial, I'm sorry, thats just what the website says. I had to convert it in the design anyway. Other foam board can work as well so long as it is close to 4.5mm thick to fit into the slots in the legs. 


!!! note "Take Note!" 
    More may be added to this list in the future, this is what I can recall in this moment. A lot more than those parts went into this design, the printer itself also had to be modified. 

## Printed Parts
I've compiled all my parts into a zip file divided into sections for easy sorting and printing.

|Item   | Author | Description |
|---    |---    |---    |
|[Enclosure Build Files](../assets/3d-models/enlcosure.zip)| @me | These are the files for the bones of the enclosure, included the exhaust and handles etc. |
|[PTFE Tube Conduit](../assets/3d-models/ptfe-tube-passthru.zip)| [@fuchsr](https://www.printables.com/model/51457-ptfe-filament-conduit-for-lack-enclosure){target=_blank} | Pass through tube for the filament into the enclosure. |
| [Bento Box](../assets/3d-models/bentobox5015_v1.zip)  | [@thrutheframe](https://www.printables.com/model/272525-bentobox-v20-carbon-filter-for-bambu-lab-x1c-enclo/files){target=_blank}  | The bento box is an internal air scrubber that I find to be beneficial for stinkier filaments (ABS, ASA, etc.)  |
| Bento Box 5015 Adaptor | [@SSX556](https://www.printables.com/model/503886-bentobox-v20-5015-pull-configuration-caseshroud){target=_blank} | This adaptor is included with the bento box, this modification moves more air in a quieter manner vs the stock box. |

!!! note "Developmental"
    Do keep in mind this is all in development and is my first time designing something that is as involved as this. I found building this to be a bit annoying as some of my tolerances were too tight. **This may be an issue for you!** 

