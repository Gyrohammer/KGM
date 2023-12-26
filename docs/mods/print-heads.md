# Print Heads

## [Hero Me Gen7](https://www.printables.com/model/39322-hero-me-gen-7-platform-release-4){target=_blank}
Pros

* Extreme modularity almost makes it a 'silver bullet' of print heads.
* Cooling potential is extremely high with dual 5015.
* Light bars can be built in to the design. 

Cons

* A complicated build process is daunting for the average user.
* Performing maintenance on the hot end is extremely tedious.
* The printed mounting point for the nozzle is not stable vs carriage mounting. 
* Bed size will be affected by the width of the head and probe placement.
* Default carriage adapter does not trigger x-endstop

??? info "Carriage adapter endstop fix"
    I modified the [carriage adapter](https://www.printables.com/model/616520-anycubic-kobra-go-hero-me-gen-7-endstop-fix){target=_blank} ensuring it triggers the endstop correctly.
 

Although to start this was a good solution, I'm sorry to say that the novelty wore on me. Not only was having
dual 5015 fans overkill, the maintenance and annoyances I had with this setup far exceeded the nice print time I 
had with it. Valiant effort, but not for me.

## [ENDLI Orbiter 2.0](https://cults3d.com/en/3d-model/gadget/orbiter-2-0-5015-fan-mount-for-ender-3){target=_blank}  
Pros

* Small, compact, light design
* Easy maintenance and part accessibility
* Excellent probe placement
* Original mount points used
* Direct drive agnostic
* Simple assembly

Cons

* Not free (But worth every penny)
* Incompatible with the standard kobra go carriage
* Needs modification for heated inserts
* Non-universal mounting
* X-Endstop doesnt trigger correctly

??? warning "X-Endstop Compatibility"
    The ENDLI print head does not properly trigger the x-endstop. To combat this, I designed [my own X-endstop](https://www.printables.com/model/639326-cable-chain-x-motor-mount-orbiter-20){target=_blank} mount which positions the switch such that it should hit the frame of the fan attached. I would recommend sensorless homing as well. It will work for stock setups and needs only minor modification. 

After some debate I ended up replacing the standard Kobra Go carriage plate with one from an Ender 3 ([Link here](https://amzn.to/3RWWkjW){target=_blank}). I 
made this call after getting fed up with the lack of support in the general community. I could have modified
countless files and made adapters, or I could spend a relatively small amount of money and save myself the 
headache. Cheating? Kind of. Worth it? Yes. 

