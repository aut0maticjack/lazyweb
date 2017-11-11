I found it hard to get good data on 3D printed part strength, so here's some scratch notes and references.

## Broad Recommendations

### Cosmetic Parts

Things meant to look good but not stand up to mechanical stress beyond everyday human handling.

* Perimeters: 2 to 3
* Bottom Layers: 2 to 4
* Top Layers: 4 to 6
* Infill:
    * If the part can be printed without infill, don't use infill.
    * If the part has overhanging top layers which need infill, use as little as possible. Consider using Simplify3D's multiple processes or Cura's concentric infill to reduce the amount of infill plastic used. You only need enough infill to support the top layers so they look nice.
* Layer Height: Low (0.1mm) looks better but takes a long time, high (0.3mm) prints faster but looks worse

### Mechanical Parts

Or more accurately, 3D printer parts. Pieces meant to hold frames and linear motion systems in place under the stress of torque applied through belts and motors.

* Perimeters: 4, though reduce to 3 or 2 if the part *really* doesn't print well with 4
* Bottom Layers: 8
* Top Layers: 8 to 10
* Infill: 50%. Maybe a printed CNC should have more like 75%?
* Layer Height: 0.25mm as most parts have dimensions in multiples of 0.5mm

## General Notes

* Rectangular/rectilinear infill varies the least under stress, I'd use this for stable mechanical parts.
* Hexagon/honeycomb infill is still fairly okay, it resists stretch less and is faster to print.
* The difference from low infill like 10% or 20% to high infill like 50% is drastic.
* There is diminishing returns from 50% infill to 75% infill.
* I don't think it's worth printing over 80% infill.
* Adding another shell is about as good as another ~15% infill, at least at low infill rates.
* Different blends of the same material vary greatly, so you can't make generalizations like "PETG is this strong" and "PLA is that strong". Some PLAs are stronger than some PETGs and vice versa.
* Different colors can matter too. White pigment changes flow properties. People say black filament is often blends of other failed batches with more pigment added in so is weaker because there's less plastic. "Natural" color with no pigment is the most pure plastic and also seems easiest to print with.
* Temperature matters, it probably results in layers adhering to each other better.
* Orientation matters, the weak point is always the layer lines.
* I couldn't find any conclusive data on whether smaller layers or larger layers are better. Some people say their parts printed at 0.1mm are stronger, some people say their parts printed at 0.3mm are stronger.
* To really be conclusive, you would need to build a test rig and put parts through specific mechanical tests of interest to you, like Tom Sanladerer and CNC Kitchen have done.

## References

* http://my3dmatter.com/influence-infill-layer-height-pattern/
* http://3dprintingforbeginners.com/infill-strength/
* https://www.3dhubs.com/knowledge-base/selecting-optimal-shell-and-infill-parameters-fdm-3d-printing
* [3D Printing Nerd: Stop Wasting Plastic on Infill Percentage](https://www.youtube.com/watch?v=fuGqsZjdPQM)
* [Maker's Muse: Multiple Infills in the same 3D Print using Simplify3D](https://www.youtube.com/watch?v=UTs7Y5VGNm8)
* [3D Printing Nerd: How To Use Multiple Infill Percentages When 3D Printing With Simplify3D](https://www.youtube.com/watch?v=9hw-6KTvZdA)
* https://www.typeamachines.com/3d-printing/infill-patterns-in-the-new-cura-part-6-concentric-infill-a-capping-surfaces-best-friend
* https://www.filaween.com/
* [Tom Sanladerer: Filaween Playlist](https://www.youtube.com/watch?v=sJER9QYnAcw&list=PLDJMid0lOOYl8TZJV9xHznKFq5yA5ZTi2)
* [CNC Kitchen: Strength Tests](https://www.youtube.com/watch?v=mIv507btE08&list=PLEOQTmIWJ_rncRcWmjQIvMKFAeM071CXM)
* http://makerstoolworks.com/all-filament-is-not-created-equal/